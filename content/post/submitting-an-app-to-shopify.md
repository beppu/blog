+++
date = "2019-03-15T09:00:00-07:00"
author = "beppu"
categories = ["shopify"]
title = "Submitting an App to the Shopify App Store"
description = "It's been difficult."
linktitle = ""
featured = ""
featuredpath = ""
featuredalt = ""
draft = false
+++

Installation problems can prevent your Shopify app from being accepted into the Shopify app store.  Also, days can pass between
the time you submit an app and the time their QA people respond to you with a list of things to fix.  Furthermore, if you go through
more than 3 iterations with them, they make you wait a month before you can submit the app again.  It's frustrating and time consuming,
and you don't want to go through that.

Learn from our mistakes, and save yourself a lot of time.

# Using the correct Shopify App URL

When you configure your app, there's an input field that asks for your app's URL.  If you have built a public landing
page for your app, you might be tempted to put the URL for that there.  Unfortunately, that would be wrong.

What's not immediately obvious is that this has to be the URL that accepts a POST request that initiates the installation sequence.
If you use koa-shopify-auth, the URL will be `/shopify/auth`.

# Working around a bug in koa-shopify-auth

Even if you get that right, you might be thwarted by something more insidious if you're using koa-shopify-auth.  It has a bug that
makes it fail on the first installation attempt, but it'll be fine on every subsequent attempt thereafter.  We have submitted a
pull request to get this fixed, but in the meanwhile, you can use our forked version to get a version that has this bug fixed.

# Automating Setup

In the interest of not making destructive and potentially fragile changes to a theme, we intentionally chose to not modify a shop's
theme during app installation.
