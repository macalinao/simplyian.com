---
layout: post
title: "How to Change the Theme of the XFCE Terminal"
date: 2014-03-29 05:20:52 -0500
comments: true
categories: XFCE
---

I use [XFCE](http://xfce.org) as my primary desktop environment. It's a fast, lightweight operating system that when combined with [Synapse](https://launchpad.net/synapse-project) provides a great, lag-free computing experience.

As a typical developer and Linux user, I use the terminal quite a bit. XFCE's terminal emulator has a pretty bland default theme. There is an awesome repository called [Base16](https://github.com/chriskempson/base16-xfce4-terminal) that provides a wide selection of themes for the terminal.

To install one of these themes, you need to create a directory at `~/.config/Terminal/`. Then, run the following command:

```
curl -L https://raw.githubusercontent.com/chriskempson/base16-xfce4-terminal/master/base16-default.dark.terminalrc >> ~/.config/Terminal/terminalrc
```

Replace the URL with the raw of whatever theme you want to use. Check out the [Base16](http://chriskempson.github.io/base16/) website to preview all available themes. The changes should take effect next time you run a command; if not, just restart the terminal.

These themes are a huge step up compared to the default. Personally, I use the "Bright" theme. Have fun with a nice looking terminal!
