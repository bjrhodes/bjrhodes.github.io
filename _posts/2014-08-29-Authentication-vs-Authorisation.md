---
layout: default
title: Authentication and Authorisation.
author: Barry Rhodes
bodyclass: blog authentication-authorisation
excerpt: By far the most common flaw we see in large applications is the assumption that an authenticated user is an authorised user. When building an application with a login area knowing the difference is very important.
description: By far the most common flaw we see in large applications is the assumption that an authenticated user is an authorised user. When building an application with a login area knowing the difference is very important.
---
For the large-scale projects we get involved in, security is often a major consideration. When taking over an existing
concern, one of the first areas we audit is application security. More often than not there are holes. Usually these
are simple oversights, and sometimes the exploits are only available to technically savvy people with a lot of time to
spend on an attack. However the most common flaws we see in large applications are caused by mistaken assumptions. The
most dangerous and most common of these is the assumption that an **authenticated** user is an **authorised** user.

## What's the difference?

In simple terms, authentication is the process of identifying yourself and proving it. Online, this is usually
achieved with a combination of a username and password. This can be considered equivalent to entering a building with a
keycard. Assuming your identification doesn't get stolen, you can securely verify who you are. This is
**authentication**.

Lets assume the building you've just let yourself into is a large, shared office block. You now have free roam of the
circulation spaces in the building, but you wouldn't expect your keycard to get you into other peoples offices. Why not?
The keycard is still doing the same job, it **authenticates** that you are you. It doesn't and shouldn't **authorise**
you to do things you shouldn't. This is authorisation, and where a lot of web developers have a large and dangerous
blind spot.

Online, authentication is often handled at the application level. When you request a page or try to make a change, the
application authenticates you and passes you through to the requested functionality. From there it is the developers
job to ensure you are **authorised** to perform the requested action. There are many different patterns and paradigms
around authorisation, but by far the most common we see is... none. Even with paid-for user accounts, it may be worthwhile
for a hacker to sign-up to an exploitable system in order to mine user data or attack the service. In this age of Free
trials, free tiers and social integration, it is critical to ensure your application developer has carefully considered
authorisation and fully understands the ramifications of a missing authorisation layer.

## A simple example

So what's at stake? Here's an easy example. A user has a profile, and an edit-profile page. That page submits a modify
request to your application. Inside the request is a user-id to identify which user the change is for. Without a
suitable authentication layer, a malicious user can change the user-id in the form and submit changes to another users
profile. One module of the application checks they are a valid user and authenticates them. A second module is then
invoked which updates the profile. Without reliable confirmation that the profile being updated belongs to the user who
submitted it, any user can change any other users details. Simple attacks like this are incredibly easy, and can be just
as easily stopped by a solid authorisation system.
