---
layout: post
title: "Comparing buffers on vim"
categories: vimtips note_to_self
date:   2015-04-08 19:28:57
comments: true
---

In my opinion comparing a set of files has to be one of the most tedious, boring
and error prone tasks one can do without adequate software. When I first
discovered KDE's comparing tool kompare, I thought it was the single most useful
and coolest tool I had run into for a while. Kompare is an awesome tool that I can't
recommend enough, but as I moved away form the X environment and embraced the
`tmux + vim` environment I started relying on `vimdiff` to do my comparing.

`vimdiff` has its own set of features that I have learned to love, and as to my personal
preference is a more adequate tool for the job than kompare. Now I have heard good
things of [meld](http://meldmerge.org), but haven't tried it mainly because the
same reasons I no longer use kompare and that I mainly used qt based applications.

One of the things that took me longer that it should to realize, is that vim's
diff mode can be activated from an existing vim instance.

So, way you want is to follow this two steps.

* **Step 1:** Arrange the desired buffers on windows

With the help of `:sp [filename]` and `:vsp [filename]` respectively to create
horizontal or vertical window/splits; the filename being optional, but if omitted,
one will have to change focus  into each window and place the desired buffer into it.

* **Step 2:** Step into the diff mode for the visible windows

```
:windo diffthis
```

And thats is, you should have a view similar to ![Comparing buffers on vim]({{ site.url }}assets/comparing_buffers_on_vim_expample_1_comparing_3_buffers.png)

To exit the diff mode use the command

```
:windo diffoff
```

Amongst the advantages of accessing the diff mode this way are:

Selecting buffers with ease, either with the help of auto completion and/or
the use of one of the many plug ins out there, such as
[ctrlp](https://github.com/kien/ctrlp.vim) or
[unite.vim ](https://github.com/Shougo/unite.vim)


Mixing vertical and horizontal splits, which at the time, this feels a little bit silly, I
am sure some one can find a perfectly valid case where mixing mixing splits orientation can
make a lot of sense.


And while I am aware all those things could have be accomplished by running vim without
composing an incredibly long list of parameters, There is one use case that I consider not
only the most useful of them all, but it is what makes it a killer feater for me. One of
the key differences between files and buffers is that files need to be with a name and
inside a directory of our choosing, buffers don't.

Is because this difference that allow you to compare things that are not necessary on your
file system like clipboards or command outputs, buffers not yet saved, or even websites or
remote files.
