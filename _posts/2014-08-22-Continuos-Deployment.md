---
layout: default
title: Ensuring stability through Continuous Deployment
author: Barry Rhodes
bodyclass: blog continuous-deployment
excerpt: Continuous Deployment is a system whereby any changes to your application can be rolled out to your live servers simply, safely and quickly. Moving toward this methodology is significantly more than a trivial efficiency improvement. The benefits can be surprising.
description: Continuous Deployment is a system whereby any changes to your application can be rolled out to your live servers simply, safely and quickly. Moving toward this methodology is significantly more than a trivial efficiency improvement. The benefits can be surprising.
---
## What is Continuous deployemnt?

Continuous Deployment is a system whereby any changes to your application can be rolled out to your live servers simply,
safely and quickly. Moving toward this methodology is significantly more than a trivial efficiency improvement. The
benefits can be surprising.

## Why should I care?

### Efficiency

Lets get the obvious out of the way. Push-button deployments as required for continuous deployment promote a very
efficient release workflow. On projects without continuous deployment, we find a release takes at least an afternoon to
perform. There are backups, versioning and testing to be done, as well as managing and mitigating any human error.

Automating this task means less hands-on time for your development team, so more time doing what they do best. Crafting
your product.

### Agility

Being able to get solid, beneficial features written in a timely fashion is a challenge in and of itself. If you then
need to fight with a live server environment to get that code in front of the userbase, chances are fetures will be
batched and releases will be large. These larger releases then bring issues of their own through the sheer amount of
changes to the system and the tests required.

Continuous Deployment neatly bypasses these issues and allows you to get your new features and improvements to where
they matter, in front of your userbase.

### Stability

At the core of any successful continuous deployment strategy you'll find **testing**. Fully automated tests, run on every
release, no matter how minor the change. The release process demands that your development team constantly and
consistently consider how the application may break and write test-suites to prove that it will not. Should they
overlook something, the bugfix release should add tests cover that exact problem, meaning regressions cannot get back
into your live environment. Without every test passing successfully, your product will not ship.

The stability this brings to your product can have a huge impact on user satisfaction, brand perception and prodcut
trust. A fully test-covered codebase also gives your development team the confidence to move quickly on new features,
knowing that the tests will fail if they break anything. This often overlooked benefit can dramatically improve time to
market for new features.

## I'm sold. how do I get there?

There is no hard-and-fast solution, every product is different and offers slightly different challenges, but a wealth of
tools exist to make the process a smooth one. I recommend starting with finding the easy gains in your release flow.
Instead of FTP'ing files over the top of your live code, upload to a new folder and deploy with a release script. this
can be as simple as a bash script that sets file permissions on your new folders and then renames into your live path. A
similar rollback script can get you out of trouble fast. At the same time, start adding tests to your codebase and
running them before deployment.

Even these small pieces of automation will start leading you toward where you want to be and highlighting the steps an
automated process should take. Removing yourself as much as possible is the goal.
