+++
featuredpath = ""
description = ""
linktitle = ""
date = "2016-10-18T14:50:07-07:00"
title = "On Choosing Frameworks"
featured = ""
featuredalt = ""
author = "beppu"
categories = [
  "frameworks", "libraries"
]

+++

A friend of mine who is an experienced systems programmer was working on familiarizing himself with web development, and he was overwhelmed by all the choices he had to make.  This was my advice to him:

> The explosion of frameworks is a headache for everyone, but you don't have to know all of them, because no one does.  You're just going to have to pick a couple and go with them for a while.

> On the server side, there are many adequate frameworks these days.  What you should pick is largely determined by what server side language you're comfortable with.  This filter reduces the size of the list considerably.  Then, from what's left, pick a framework that is actively being maintained and has good documentation.  As long as they give you good control over HTTP requests and responses, you're good to go.  It's hard to go wrong here, because almost anything can be made to work adequately -- HTTP servers are well understood today.

> On the client side, there were two major eras of library wars so far.  In the mid to late 2000s, there was a battle between Prototype, jQuery, and a bunch of other Javascript utility libraries.  jQuery was the winner of that era, and it would be good to have basic familiarity with jQuery even though it's gone out of fashion now.

> The second major library war on the client side was waged between Backbone, Angular, React, and many others -- too many to name.  This war started in the early 2010s, and it is ongoing, but I believe the winner is React.js.  It has many good qualities going for it, but it is also very different from anything that came before it.

> This blog post on React.js was probably the turning point that made a lot of people start taking it seriously.  http://swannodette.github.io/2013/12/17/the-future-of-javascript-mvcs

> It showed that React.js could be extremely performant while also promoting a style of programming that made client-side UI behavior a lot more predictable than it had been in the past.  (Believe me, it was (and sometimes still is) a mess.)

> Another big plus for React.js is that it can be used to develop native Android and iOS applications which few other libraries can claim.  Perhaps no other library can do this, because the main idea behind React.js is to represent your UI as a pure function, and this is a broad idea that isn't confined to just HTML.  This makes it special among the client side libraries.

> It's downside (if you could call it that) is that the Facebook engineers who made it are fond of source code transformers, so you're development setup will need to have tools like WebPack, Babel, sometimes Flow, etc...  configured.  That's a god damned headache, but such is life in the web development world.  Hopefully, you only have to set it up once in the beginning and not worry about it later, but I find it annoying to need all these tools.
