---
layout: post
title: "Comparing buffers on vim"
categories: vimtips note_to_self
date:   2015-04-05 21:49:15
---

In my opinion comparing a set of files has to be one of the most tedious, boring
and error prone tasks one can do without adequate software. When I first
discovered KDE's comparing tool kompare, I thought it was the single most useful
and coolest tool I had run into for a while. Kompare is an awesome tool that I can't
recommend enough, but as I moved away form the X environment and embraced the
`tmux + vim` environment I started relying on `vimdiff` to do my comparing.

`vimdiff` has its own set of features that I have learned to love, and as my personal
preference is a more adequate tool for the job than compare. Now I have heard good
things of [meld](http://meldmerge.org), but haven't tried it mainly because the
same reasons I no longer use kompare.

One of the things that took me longer that it should to realize, is that vim's
diff mode could be activated from an existing vim instance.

The way to set it up this requires two steps
1- Arrange the desired buffers on windows 
With the help of `:sp [filename]` and `:vsp [filename]` respectively to create 
horizontal or vertical window/splits; the filename being optional, but if omitted,
one will have to move into each window and place the desired buffer into it.

2- Step into the diff mode for the visible windows
```VimL
:windo diffthis
```

And thats is, you should have a view similar to [this] ({{site.url}}/assets/comparing_buffers_on_vim_expample_1_comparing_3_buffers.png)

Exit the diff mode with the command
```VimL
:windo diffoff
```

