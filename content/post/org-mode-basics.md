+++
description = "The bare minimum you need to be effective"
featured = ""
featuredpath = ""
featuredalt = ""
categories = [
  "editors"
]
date = "2017-01-30T11:12:37-08:00"
linktitle = ""
author = "beppu"
title = "org-mode Basics"

+++

**[Org-mode](http://orgmode.org/)** is an Emacs mode for authoring hierarchical documents.  It's most commonly used for note
taking and managing TODO lists. The basics are quite simple, and the default
keybindings are quite ergonomic and intuitive.

# Basic Keybindings

Let's get started by opening a new file named `index.org`.  Any file that ends in `.org` will be opened in org-mode by default.

Try using these keybindngs as I describe them.

`M-RET` - Meta-Return creates a new list item.  You can type text on this line, and you can add additional content underneath the item as well.

`M-RIGHT` - Indent an item.

`M-LEFT` - Dedent an item.  With these 3 commands, you can construct a hierarchical list.

`M-UP` - Move an item up.

`M-DOWN` - Move an item down.

`TAB` - Cycle the visibility of an item.  If an item has sub-items, `TAB` will collapse and expand them.

`C-c .` - Add a timestamp.  This is handy for when you're keeping a journal.

`S-RIGHT` - Cycle TODO state.

`S-LEFT` - Cycle TODO state in reverse.  The default TODO states are `TODO`, `DONE` and nothing.

----

These are the most important keybindings, and they will take you far.

# Linking to Other Files

The reason I like to start with a file called `index.org` is because I use that as entry point for other `.org` files.  This
can make org-mode feel like a personal wiki.  I link to other files using the `file:$path` notation.  Here is what my `index.org`
looks like:

``` org
#+TITLE Index
* file:log.org - personal log
* file:clojure.org - notes on Clojure
* file:people.org - a list of people I find interesting
* Projects
** file:timer.org - timer implemented in Clojure
** file:konfederation.org - generalized authentication
** file:blog.org - my personal blog
** file:archiver.org - self-hosted archive.is alternative
```

If you were to put that in an org document, those `file:` links would be clickable.  You can also hit `RET` while your cursor
is on the link to open that file.  Regular URLs are clickable too.  Emacs will open the link in your web browser in that case.

# Embedding Source Code

If you're a programmer, you'll love org-mode's ability to embed source code.  If nothing else, it makes programming notes
look really good, because it's syntax highlighted correctly inside your org document.

``` org
#+BEGIN_SRC clojurescript
(-> (fn-that-returns-a-promise)
    (.then (fn [r] (return-another-promise)))
    (.then (fn [r] (return-another-promise)))
    (.catch (fn [e] (handle-your-exceptions))))
#+END
```

There are advanced org-mode users who use this to do a form of literate
programming, but I have note tried doing that yet.

There are many things I haven't tried yet in org-mode. For the curious, there is
a very thorough manual that you can read at:

# http://orgmode.org/
