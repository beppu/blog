+++
date = "2019-03-15T09:00:00-07:00"
author = "beppu"
categories = ["shopify"]
title = "Shopify App Installation Was Harder Than We Thought"
description = "It's been difficult."
linktitle = ""
featured = ""
featuredpath = ""
featuredalt = ""
draft = false
+++

Who would have thought installing a Shopify app would be so hard. It's something
a developer does repeatedly during the course of development for debugging
purposes, but when you want to get your app into the [Shopify App Store](https://apps.shopify.com/), there
are more constraints put upon you, and they're not all obvious.  (I swear I did not see some of these things
in their documentation.)

Installation problems can prevent your Shopify app from being accepted into the
Shopify app store, and the turnaround between the time you submit and the time
you get a response can take many days. Furthermore, if you go through more than 3
iterations with them, they make you wait a month before you can submit the app
again. It's frustrating and time consuming, and you don't want to go through
that.

Learn from our mistakes, and save yourself a lot of time.

# Using the correct Shopify App URL

When you configure your app, there's an input field that asks for your app's URL.  If you have built a public landing
page for your app, you might be tempted to put the URL for that there.  Unfortunately, that would be wrong.

What's not immediately obvious is that this has to be the URL that accepts the POST request that initiates the installation sequence.
If you use 
[@shopify/koa-shopify-auth](https://github.com/Shopify/quilt/tree/master/packages/koa-shopify-auth), 
the URL typically ends with `/shopify/auth`.

TODO: Add screenshot

# Working around a bug in koa-shopify-auth

Even if you get that right, you might be thwarted by something more insidious if you happen to be using @shopify/koa-shopify-auth.  It has a bug that
makes it fail on the first installation attempt, but it'll be fine on every subsequent attempt thereafter.  The QA people will only try once, though,
and that failure is an automatic rejection.

We have submitted a
[pull request](https://github.com/Shopify/quilt/pull/469) to get this fixed, but in the meanwhile,
you can use our forked version to get a version that has this bug fixed.

https://www.npmjs.com/package/@dimensionsoftware/koa-shopify-auth

For the curious, koa-shopify-auth has a route that tests to see if your browser supports cookies.  If it does, it redirects to `window.shopOrigin + "/admin/apps/" + window.apiKey`
which is your app's URL within the Shopify admin.  Unfortunately, before the first install, that URL is invalid.  Instead, our fork redirects to `https://${host}/${inlineOAuthPath}?${queryString}`
which goes back to your app's koa-shopify-auth routes and continues the OAuth sequence as intended.

This was really hard to find, because we couldn't even replicate the error until we cleared our cookies and tried an app installation.  It also felt
unjust to be penalized for a bug in Shopify's own software, but life is like that sometimes.  We fixed it and resubmitted.

# Automating Setup

After their QA team was able to install the app on the first try, they had a long list of complaints about our app.
One of those complaints was related to installation.

> 4. The primary method of installation needs to be automated and cannot require manual processes. Manual instructions should be included as a backup but the primary method needs to be automated. With proper documentation, merchants should be able to install and set up apps on their own.

We were faced with a tough dilemna. In the interest of not making destructive
and potentially fragile changes to a theme, we intentionally chose to not modify
a shop's theme during app installation.  What now?

Our app, [Passwordless Social Login](https://login.dimensionsoftware.com/install) was intended to provide a dialog box for logging in to a store.
To set it up, we wanted store owners to add one CSS class to their theme.  It's seriously a one-line change, but there's no safe way to programmatically
make that change in a way that would work for all themes out there. Therefore, we still refuse to make theme edits, because we refuse to break a store's theme.

What we chose to do instead was hijack some content on the `/account/login` page via JavaScript and replace the stock login dialog with our own dialog.
This will also not work for every store, but it will work for a lot of stores, and it won't break a store's theme by doing fragile and error-prone text editing.
It's not ideal, but it seemed like the best course of action under the circumstances.

TODO: Add screenshot

---

Going through this approval process has taken months, and we're still not done.  Honestly, it sucks, but you don't have to go through this pain if you 
learn from our mistakes.
