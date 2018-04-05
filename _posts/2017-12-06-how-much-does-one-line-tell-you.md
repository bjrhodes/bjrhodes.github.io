---
layout: default
title: How much does one line of code reveal?
author: Barry Rhodes
bodyclass: blog audit security software-design
excerpt: Most software buyers lack the knowledge or skills to fully assess what they've bought. We offer professional auditing of code to find any issues that may need addressing and give you a general indicator of code health. Sometimes these audits turn out to be shockingly easy to complete. Here's a quick exaple of some cowboy code that is a dead giveaway your developers are *not* experienced profesionals.
---

Software is complex, so when auditing it's easy to kneejerk a reaction without fully understanding the decisions, compromises and problems that led to a particular area of code. However, there are some cases where the quality and health of the code is very straightforward to assess. If you're lucky, your code has great test coverage, obvious and predictable code paths and consistent, appropriate architecture. If you're unlucky, your code might contain lines like this gem, which I found in a live PHP website:

{% highlight php %}
$result = mysql_query("UPDATE agente set zona='".$_POST['zona_f']."', nombre='".$_POST['nombre_f']."', direccion='".$_POST['direccion_f']."', direccion2='".$_POST['direccion2_f']." where idAgente=".$_POST['idAgente_f'], $BD) or die("A MySQL error has occurred.<br />Your Query: " . $query . "<br /> Error: (" . mysql_errno() . ") " . mysql_error());
{% endhighlight %}

There is so much wrong with this one line that it's worth seeing what we can learn from it. Let's reformat this line so we can read it, and then break down some issues.

{% highlight php %}
$result = mysql_query(
    "UPDATE agente set
        zona='".$_POST['zona_f']."',
        nombre='".$_POST['nombre_f']."',
        direccion='".$_POST['direccion_f']."',
        direccion2='".$_POST['direccion2_f']."'
    where idAgente=".$_POST['idAgente_f'],
    $BD
) or die (
    "A MySQL error has occurred.<br />
    Your Query: " . $query . "<br />
    Error: (" . mysql_errno() . ") " . mysql_error()
);
{% endhighlight %}

## Problems with this code

### Design & control flow

There's a line in that code that reads `) or die (`. This is a big red flag regarding the UI design and software architecture. What it means is that should a database error be encountered, the program will stop execution immediately and write the following statement to the screen.

If this is in user-facing code, there will be no user interface, no branding, and no sensible actionable error message. The user will just see black text on a white screen with a debug error. If this is an API then the situation is, if anything, worse. You've broken out of whatever standard protocol you were using, to dump nonsense into another program. We'd better hope the caller is better written code, and expects nonsense to come back!

Regarding control flow, this immediate exit from the program means that nothing else can take appropriate reporting or notification actions. In testing, you can't run a simple test for this broken case without stopping the test runner. Both major issues with the architecture.

At best, this is debug code left in, and a break in deploy procedure, at worst it tells us that the developers either don't know, or don't care about these issues. (A quick search of the codebase in this case revealed the latter. This is not an isolated incident.)

### Code maintenance

The first line contains a call to the function `mysql_query`. This function was offically deprecated in PHP back in v5.5.0 and removed completely in PHP v7.0. This means that this has been strongly advised against for over five years now and removed from the language completely for two. To even run this code, you need to install an old and unmaintained version of PHP, missing out on critical security patches and performance gains that newer code provides.

This strongly indicates that code maintenance has been put in the backseat in favour of the sticking-with-what-we-know approach. The longer this continues, the more costly and risky it becomes to address.

### Data design

These two lines:

{% highlight php %}
direccion='".$_POST['direccion_f']."',
direccion2='".$_POST['direccion2_f']."'
{% endhighlight %}

give us an interesting insight into the data layer. In general terms, seeing 'thing' and 'thing2' in a data design suggests a major failure of normalisation, or at best very little consideration given to informative naming of the data columns. Strong indications that we should audit the data layer for design performance.

Additionally, there is no update of who performed the action, and no subsequent or prior queries that do this, so traceability on this update is zero. In the use case of this app, that is a major failing.

### Security problems. So. Many. Security. Problems...

The best has been saved for last. This is riddled with security holes. First up, the `or die` again. Hackers look for any attack surface they can find, and this `or die` causes a lot of internal details to be output to anyone who is interested. This may reveal critical weaknesses in your server or application that you wouldn't want attackers to know.

The query updates based on an agent ID passed in from the user. It is terrifyingly trivial to make this say anything you like, including a wildcard (`%`). This will trigger this statement to effectively wipe your entire database table and write these values to all rows. Even if the attacker "only" vandalises one row, there is no prior checking in the script to ensure the user is an admin, or owns this data. This means *any* user who can access this can update *any* row. Ouch.

In a similar vein, there is no validation of _any_ of the data. Bad data here would crash the query or perhaps just spam garbage into the database.

As an extension of the lack of validation, it's not just bad data that can be put into this query. The biggest flaw here, that I saved until last, is an SQL injection vulnerability. By crafting a specific control sequence and passing it in as one of these variables, you can run *any arbitrary query you would like*.

For experienced hackers, this would be a surprisingly easy 2 minute attack. For novices though, this is a very convenient learning tool, as failures to take control of the app will be returned to you in great detail (via that `die` again) for you to try again!

### Summary

This line indicates code which is terrifyingly ripe for exploitation. A more in depth analysis of the code base revealed much more of the same, alongside bot-injected code from attackers who have already found some of these weaknesses and critical performance bottlenecks. The clean up was long and painful, but the client is in a much better place because of it.
