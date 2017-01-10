+++
categories = [
  "programming",
  "editors"
]
linktitle = ""
featuredalt = ""
date = "2017-01-06T15:17:23-08:00"
description = "A Guide for Those Who Want to Give Spacemacs a Try"
featured = ""
featuredpath = ""
author = "beppu"
title = "Spacemacs Tips"

+++

{{< img-post "title" "spacemacs-logo.svg" "Spacemacs" "center" >}}

[Spacemacs](http://spacemacs.org/) is a radical reconfiguration of Emacs that tries to bring the good parts of
vi and emacs together while also adding some good ideas of its own.  A few months ago
I gave it a try, and the longer I use it, the more impressed I become with how well
this curated Emacs system comes together.

With that said, there are a few things that were not immediately obvious to me that I
wish I had known sooner.

# Basics

**Leave the Editor Running** - If you're new to Emacs, and especially if you previously
used an editor that starts up quickly like Vim, this will probably be one of the hardest
habits to break.  Emacs doesn't start up instantaneously, so the common wisdom among Emacs
users is to start it up and leave it running for a long time while you edit various files.

One thing that may help ease the pain is to create the following alias.

```sh
alias e='emacsclient --no-wait'
```

Spacemacs automatically puts Emacs in `server-mode` which lets `emacsclient` tell `emacs`
to edit files.  If you were in the terminal and came across a file you'd want to edit,
you could type:

```sh
e some-file.txt
```

**Classical Emacs Bindings** - If you've used Emacs before and are used to its traditional
keybindings, don't worry.  They're mostly all there.  However, to get the most out of Spacemacs,
you should gradually learn to do things the Spacemacs way, and that means using the `SPC` menu.

**The Space Menu** - This is one of the most ingenious parts of Spacemacs, and it eliminates
one of the big complaints many people have about Emacs -- the keybindings.  I'm sorry, but
classical Emacs keybindings can be hell on your fingers and wrists, and they can be hard to
memorize too.

Commands in the `SPC` menu, on the other hand, are very easy to type, and the mnemonics that have been
picked are a lot more intuitive.  The way it works is while you're in command mode in a buffer,
hit `SPC` and a menu will appear.  Each character leads to either a submenu or a command.  This
presents you with a hierarchical tree of commands that can be explored and learned as you use
Spacemacs.

The more you use it, the more you may come to appreciate its genius as I have.

**Major Mode vs Minor Mode** - In Emacs terminology, a buffer may have one major mode and many 
minor modes activated.  A mode usually defines keybindings and special behaviors such as automatic
indentation for programming languages.  I don't know what makes a mode major versus minor, but it's
not essential knowledge at this time.

**Packages** - Emacs has a packaging system, and traditionally, you'd install them by
typing `M-x package-install`, but that's **NOT** how you do things in Spacemacs.

1. In Spacemacs, package installation is defined by the ~/.spacemacs
   configuration file which is described in the next section.
2. In Spacemacs, layers should be favored over packages.

**Layers** - A layer takes a package (or a set of packages) and adapts them to
the Spacemacs way which usually means adding entries to the `SPC` menu and
setting a few variables. Layers are usually small, and you can find a list of
them by typing `SPC h SPC`.

A complete list is also available at:

* https://github.com/syl20bnr/spacemacs/tree/master/layers
* http://spacemacs.org/layers/LAYERS.html

# Configuration

To add a layer to your Spacemacs configuration, you edit your `~/.spacemacs` file, and you do that by
typing:

`SPC f e d` - edit ~/.spacemacs file

Although this is a big file, most of your time will be spent with these 3 symbols: 

1. **dotspacemacs-configuration-layers** - This is a list of layers you want to
   use. To install a new layer, add it to the list and restart emacs.
2. **dotspacemacs-additional-packages** - This is a list of extra packages you
   want. If you need a package that hasn't had a layer made for it yet, this is
   where you add it.
3. **dotspacemacs/user-config** - This is a function that is run during
   Spacemacs startup. Any configuration that doesn't already have a spacemacs
   variable as well as any custom code goes here. For example, if you need to
   set some variables (such as indentation settings) this is where you'd do it.

`SPC q R` - This is a handy way to restart emacs after changing the configuration.

# Navigation

**Window Management**

`SPC w /` - Split window vertically.  (`C-w v` in vim)

`SPC w v` - Also split window vertically.

`SPC w V` - Split window vertically and focus new window.

`SPC w -` - Split window horizontally. (`C-w s` in vim) 

`SPC w s` - Also split window horizontally.

`SPC w S` - Split window horizontally and focus new window.

`SPC 1`, `SPC 2`, ... `SPC 9` - Switch to window N.  Notice that each window has a little number in the bottom
left corner.  This lets you switch to windows in O(1) time.

**File Management**

`SPC f t` - Toggle neotree.  This is very similar to vim's NERDTree, and Spacemacs favors neotree over the traditional speedbar for file navigation.

`SPC 0` - Switch to the neotree window.  Window 0 is specially reserved just for neotree.

`SPC p f` - Open file via projectile.  This is nice if you're working on a project, because it lets you complete a filename within the project you're in, and it seems to know what files to ignore.  For example, if you were in a node.js project, it knows to ignore **node_modules/**.

`SPC f f` - Open file.

`SPC b b` - Switch to buffer.

`SPC b d` - Delete buffer.  (`:bd` in vim)

`SPC j i` - Go to imenu location in current buffer.

`SPC j I` - Go to imenu location in all open buffers.  **Imenu** is a game changer.  This lets you jump directly to function definitions by name.

# Documentation

`SPC h d b` - Discover key binding.  This will help you find the functionality you're looking for.

`SPC h d f` - Show docstring for an elisp function.  This is very useful if you start getting into serious elisp hacking.

`SPC h SPC` - Show Spacemacs documentation.

# Miscellaneous

`SPC T s` - Switch themes.  (Add the **[themes-megapack](http://themegallery.robdor.com/)** layer to get a big selection.)

`SPC T T` - Toggle transparency.

`SPC t TAB` - Toggle indent guide.  If you use a language where indentation is significant, this is very useful.  Try it and see for yourself.

`SPC t n` - Toggle line numbers.

`,` - The comma is a shortcut for `SPC m` which is where all the major mode
bindings are. Depending on what major mode you're in, you may get a completely
different set of commands under `SPC m`. A lot of useful functionality is
organized under `SPC m`, so `,` gets you there with one fewer keystroke.

`SPC SPC` - This is a shortcut for `M-x`.  In classic Emacs, `M-x` was your gateway to all kinds of emacs functions, and there
are many functions that are only reachable through this, so it's good to know.

Note that some versions of Spacemacs, this was mapped to `SPC :`. 

`C-g` - Abort!  If you find yourself in a funky state, Control-G can usually get you out of it.

# Enjoy Spacemacs

Play with it.  Try these key combinations out.  Hopefully, you'll come to appreciate how nice Spacemacs can be.
