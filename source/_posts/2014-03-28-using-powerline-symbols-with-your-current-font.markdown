---
layout: post
title: "Using Powerline Symbols With ZSH"
date: 2014-03-28 22:26:13 -0500
comments: true
categories: [zsh]
---

Recently, I tried to install the [agnoster](https://gist.github.com/agnoster/3712874) theme with zsh. However, a bunch of symbols appeared instead of the powerline font. I installed one of the provided patched powerline fonts to fix it, but it still didn't work.

I did a bit of Googling and found that I needed to install the PowerlineSymbols font, which is basically a font that just adds on to your current font. Here's the steps I took to get things working.

1. Download `PowerlineSymbols.otf` to your `~/.fonts/` directory using `curl https://github.com/Lokaltog/powerline/raw/develop/font/PowerlineSymbols.otf -L >> ~/.fonts/PowerlineSymbols.otf`.

2. Run `fc-cache -vf ~/.fonts` to refresh the font cache and thus install the font.

3. Download `10-powerline-symbols.conf` to your `~/.config/fontconfig/conf.d/` using `curl https://github.com/Lokaltog/powerline/raw/develop/font/10-powerline-symbols.conf -L >> ~/config/fontconfig/conf.d/10-powerline-symbols.conf`.

Once you've done things, this should work. If not, you may need to restart your terminal or even your entire computer. You can also change your theme to the `agnoster` theme by changing your theme in your `~/.zshrc`.
