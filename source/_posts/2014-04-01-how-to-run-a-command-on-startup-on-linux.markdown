---
layout: post
title: "How to Run a Command on Startup on Linux"
date: 2014-04-01 23:43:26 -0500
comments: true
categories: [Linux]
---

I recently purchased a VPS to run my IRC client in. I wanted to start my IRC client in tmux on startup. The answer is simple: crontabs.

Run the following command on the user you want to run the command on:

```
crontab -e
```

This will open up the crontab of your current user. A crontab is basically a file stating a bunch of tasks that you want to run on some sort of schedule.

Next, add the following text to the file:

```
@reboot <command>
```

where `<command>` is, of course, the command you want to run. For example, on boot, I run a shell script that starts up my tmux stuff, so I have `@reboot /usr/ian/tmux_start.sh`.

Pretty simple, right? Crontabs have a lot more uses that you can probably find on Google.

Source: `man cron` and `man crontab`.
