---
layout: post
title: "Using Tmux Remotely Within a Local Tmux Session"
date: 2014-03-29 05:40:53 -0500
comments: true
categories: [tmux]
---

I often SSH to remote servers, and those servers usually have tmux installed. (tmux is better than Screen in every way) However, conflicts arise when you want to manipulate a remote tmux session within a local one. `Ctrl-B` refers to the local tmux session, not the remote one, and you have to press `Ctrl-B` twice to manipulate the remote one. This is pretty annoying. Fortunately, there is a solution to this.

{% img http://i.imgur.com/HQBdV1J.jpg %}

There is one line you need to add to your `~/.tmux.conf` (if this file doesn't exist, create it):

```
bind-key -n C-a send-prefix
```

This binds the command `send-prefix` to `Ctrl-A`. Basically, you are sending a `Ctrl-B` (assuming you've left tmux at its defaults) directly to the server when you press `Ctrl-A`. This will let you manipulate the remote session with `Ctrl-A` and still use your local session with `Ctrl-B`. Pretty nice, eh?

Source: [StackOverflow](http://stackoverflow.com/questions/8518815/how-to-send-commands-when-opening-a-tmux-session-inside-another-tmux-session)

