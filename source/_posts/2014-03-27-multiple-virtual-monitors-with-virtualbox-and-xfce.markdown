---
layout: post
title: "Multiple Virtual Monitors with Virtualbox and XFCE"
date: 2014-03-27 19:31:52 -0500
comments: true
categories: [VirtualBox, XFCE]
---

I love VirtualBox. I need Windows in order to run some programs (read: games) so VirtualBox lets me run Linux when I need it. Sometimes, I need to use more screen space -- I want a terminal on one window and my web browser/IDE on the other.

First of all, you want to go to your VM's settings and increase the monitor account. You can only do this when the VM is shut down.

![Set the settings](http://i.imgur.com/Zf7U04J.png)

Once that's done, fire up your VM and log in. Notice that there are now multiple VirtualBox windows running your VM. To double check this, go to `Start > Settings > Settings Manager` and choose `Display`. Make sure the `Use this output` box is checked.

Next, open a terminal and run the following command:

`xrandr`

You should see a list of your virtual monitors, labeled `VBOX0` and `VBOX1`. If you don't see them, try changing your display settigns again. Next, type the following command to extend your desktop to both monitors:

`xrandr --output VBOX0 --left-of VBOX1`

Now you have your multi-monitor desktop. However, this will not persist after rebooting. Go to `Start > Settings > Settings Manager > Session and Startup`, click on `Application Autostart`, click `Add`, then add the command in the dialog box. Now when you reboot, you should have your awesome dual monitors!

I did not figure this out on my own. I found the answer on the following Ask Ubuntu post: [http://askubuntu.com/questions/62681/how-do-i-setup-dual-monitors-in-xfce]
