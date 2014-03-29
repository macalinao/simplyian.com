---
layout: post
title: "Making Powerline Work With Tmux And ZSH"
date: 2014-03-29 02:45:17 -0500
comments: true
categories: [zsh, Powerline]
---

After hearing good things about Powerline for a while, today I finally decided to install Powerline on tmux. However, it didn't work when I followed the directions. Apparently, this is a [common error](https://github.com/Lokaltog/powerline/issues/150).

To get it working, I placed the following in my `~/.tmux.conf`, in addition to `source`ing the `powerline.conf`:


```
set -g status-right '#(.local/bin/powerline tmux right)'
```

Basically, tmux does not load the `PATH` variable in your `.zshrc`. Therefore, you have to specify the path that powerline is installed at in your `~/.tmux.conf`.

If this does not work, you can also try this:

```
tmux set -g status-right '#(/usr/local/share/python/powerline tmux right)'
```

This uses powerline as if you installed it as root.

Source: [an issue on the Github Powerline repository](https://github.com/Lokaltog/powerline/issues/150)
