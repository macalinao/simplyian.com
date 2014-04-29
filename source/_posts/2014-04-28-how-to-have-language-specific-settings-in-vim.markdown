---
layout: post
title: "How to Have Language-Specific Settings in Vim"
date: 2014-04-28 20:50:27 -0500
comments: true
categories: [Vim]
---

I wanted to set up Vim so that [Coffeescript](http://coffeescript.org/) files would use 2 spaces for indentation. This was very simple:

1. Create a file at `~/.vim/ftplugin/<language>.vim` where `<language>` is the language you want to modify. For Coffeescript, this is `coffee`. The language name you should use is just the file extension.
2. In this file, add your settings. In my `coffee.vim`, I have `setlocal tabstop=2` and `setlocal shiftwidth=2` to make my tabs 2 spaces.
3. Open up a file in that language and enjoy your language specific settings!
