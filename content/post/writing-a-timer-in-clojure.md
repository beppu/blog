+++
categories = [
  "clojure",
  "programming",
  "libraries"
]
description = "What I learned from this experience."
linktitle = ""
title = "Writing A Timer In Clojure"
featuredpath = ""
featuredalt = ""
author = "beppu"
featured = ""
date = "2017-01-29T07:52:08-08:00"

+++

{{< img-post "title" "Timers_003.png" "Clojure" "center" >}}

#### https://github.com/beppu/timer

Recently, I've been working on a desktop application that let's you manage
multiple timers.  It's at the point where it's ugly but it works, so I'm
going to share what I've learned so far.

# Using core.async For Timing And Control

In this application, I have two kinds of entities:

* **Timer** - This holds a duration and an amount of time that has elapsed.
* **Alarm** - This is responsible for providing some kind of effect (like making a sound) when a Timer has finished.  A Timer has an Alarm.

The following code comes from the `play!` function of the timer, and this gives each running timer its own `go-loop`.
It multiplexes between a control channel and a timeout channel, and while it counts down ever 100ms, if a control message
like `:pause` or `:stop` comes in, then the loop ends (because we don't `recur` anymore).

```clojure
    (go-loop []
      (let [[c channel] (alts! [(:control @at) (timeout 100)])]
        (if c
          (case c
            :pause (do (debug "Pause Timer" c))
            :stop (do (debug "Stop Timer" c)
                      (timer.alarm/stop! (:alarm @at))))
          (do
            (elapse! at)
            (recur)))))
```

# Fixing clj-audio

Playing audio with Clojure was a bit harder than I expected. At first, I was
going to use Overtone, but it tended to crash when I suspended my laptop, so I
looked around some more, and I came across
**[clj-audio](https://github.com/budu/clj-audio)**.  It was lightweight, and did
exactly what I needed, but it had suffered some bitrot and no longer worked with
contemporary versions of Clojure.

There was a [pull request](https://github.com/budu/clj-audio/pull/1) by
**[wmealing](https://github.com/wmealing)** that fixed this, but it was never merged
back in by upstream.

I ended up forking the official clj-audio, merging in wmealing's work, resolving the
conflicts in that merge, and then uploading my fork to clojars.org.

https://clojars.org/org.clojars.beppu/clj-audio

# seesaw Is A Great Wrapper For Swing

For the UI, I ended up using **[seesaw](https://github.com/daveray/seesaw)** by
**[daveray](https://github.com/daveray)**. It's a really nice wrapper around
Swing that significantly reduces the pain of creating UIs with Swing.  He has a good
understanding of both Clojure and Swing, and API he created is declarative
and pleasant to use.  It's also documented fairly well, and there are a lot of examples
in the github repo to learn from.

# MigLayout Is Also Amazing

Something else I came to appreciate was MigLayout which is a 3rd party layout
library for Swing. Seesaw provides wrappers around this too, but it's barely
mentioned in the seesaw documentation. However, I noticed `mig-panel` was used a
lot in the example code and there's a good reason why.  It works great.

MigLayout provides an expressive textual DSL for describing widget layouts.  It also
provides the freedom to not care about the layout so much.  I was paralyzed for a few
days, because I kept thinking about how I should organize the widget for each individual
Timer, and my greatest fear was, **"What if I changed my mind?"**

With MigLayout, I can change my mind all day long, because the layout can be changed
relatively easily without massive code changes.  If any of you out there end up using
seesaw in a project, definitely look in to MigLayout.  Although Swing has fallen out of
fashion, MigLayout provided a great solution to a difficult problem, and I want to
give credit where it is due.

https://github.com/mikaelgrev/miglayout

http://miglayout.com/

# Using add-watch To Update The UI

[`add-watch`](https://clojuredocs.org/clojure.core/add-watch) is a function that lets you
observe a Clojure reference (like an atom) and run a function when the reference's state
is updated.  I wrapped all my Timers in atoms and I used `add-watch` to attach a function
to update the UI whenever a Timer changed.  It was convenient.

```clojure
(add-watch timer :refresh (fn [k r o n] (refresh-timer! tw n)))
```

# Using future To Prevent The UI From Blocking

One minor problem that I faced was the UI becoming unresponsive while audio was
playing due to `clj-audio.core/play!` being a synchronous function. To make the
Alarm more responsive to stop signals sent to it, I ended up
using [`future`](https://clojuredocs.org/clojure.core/future) to play the audio
in a separate thread. This allowed the `go-loop` used by each Alarm to stay
responsive.

```clojure
(defn play-with-future
  "Play audio only if another audio is not already playing."
  ([file]
   (future (audio/play (audio/->stream file))))

  ([file ft]
   (if (future? ft)
     (if (future-done? ft)
       (play-with-future file)
       ft)
     (play-with-future file))
   ))
```

# Things I'm Unsure About

I would like to get the advice of more experienced Clojure programmers on the following topics.

**Naming** - I have 3 entities: Timer, Alarm, and App.  I gave each of them their own namespace,
and in that namespace there is a record of the same name.

* timer.timer/Timer
* timer.alarm/Alarm
* timer.app/App

The one that bothered me the most was `timer.timer/Timer`.  Could I have organized my namespaces
differently to avoid that unfortunately repetitive name?

Another naming question I had was about passing atoms around.  At first, I was tempted to prefix
variable names with `a` to signify that I intended for that variable to contain an atom.  Later,
as that got to be annoying, I stopped doing that, but I felt things could become ambiguous at
times.  Does the variable contain an atom or the raw record?

When working with atoms and other reference types, is it recommended to name them differently to
signify that they are references and not plain values?

**Mutation** - Before I started, I wondered how I could organize the timer loop such that I didn't
have to mutate things, but that just seemed awkward.  Am I `swap!`ing too much in this code or
is it a reasonable amount?

Any insight is appreciated.
