+++
featuredpath = ""
date = "2016-10-19T09:20:15-07:00"
title = "Why I Chose Hugo"
featuredalt = ""
author = "beppu"
categories = [
  "hugo"
]
description = "where I answer from questions from Albert"
linktitle = ""
featured = ""

+++

### Why did you pick hugo (and Go) instead of github's jekyll?

I was initially going to use Jekyll, but when I tried to do a `bundle install`, one of the dependencies failed to install.  I didn't feel like fighting that battle, so I decided to try Hugo instead since I had looked at it in the past.

What I liked about Hugo was that:

* it was fast,
* it had a nice selection of **[themes](http://themes.gohugo.io/)**,
* its blogging functionality was adequate.

As for Go, it wasn't a major factor in choosing a static site generator for me.

### How proficient you need to be in Go to use Hugo?

You don't need to know Go at all, and I haven't even looked at a line of Hugo's Go code yet.

However, what you do need is some proficiency with the Unix shell so that you can run the various `hugo` commands and navigate the directory structure it generates for you.

It's also helpful for when things go wrong and you need to debug.  For example, this **[theme](http://themes.gohugo.io/future-imperfect/)** that I'm using was slightly buggy out of the box, and I had to move some files around to make it work.

### Did you try other static site generators?

I did go over to https://www.staticgen.com/ and look over the list.  I remembered that Hugo was one of the ones you liked, so I gave that a try first, and I liked it.  Thus, the search ended rather quickly.

### Your thoughts on storing comments on your own 

> (it'd probably require a dynamic site, though I saw some weird IMAP tricks with Pelican a while ago) vs using something like Disqus.

On blogs where the topic matter makes censorship unlikely, I don't mind delegating comments to a system like Disqus.  If I were running a blog with political commentary, I would definitely want to handle comments locally, though.

To be honest, I was actually surprised when I saw the Disqus comment widget when I published it to GitHub, because they didn't show up at all while I was developing the site locally.  It's using someone else's generic Disqus forum and not one that I set up myself.

~~I should probably fix that.~~

I fixed it -- I have my own disqus forum now.
