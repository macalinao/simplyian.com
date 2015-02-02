title: The real reason why Caps Lock and Escape are in terrible positions
date: 2015-01-08 13:41:08
tags: vim
---

It is a truth universally acknowledged that **the Caps Lock key is completely useless.** I use it about once or twice a year, and that definitely does not warrant it a spot right next to my pinky finger on the home row. It's in a place that is just as convenient as the Enter key, despite being completely useless.

Conversely, the Escape key is extremely useful. I use it when watching full screen videos on YouTube, closing chats on Facebook, and using commands in Vim. However, it often is in the worst spot possible to be used extremely frequently: the top left of the keyboard. And on many laptops, it's tiny.

![Chromebook Keyboard][chromebook-keyboard]
![Mac Keyboard][escape-mac]

For heavy escape users, this is an incredible boon to productivity.

## How Caps Lock got its prominent position

Back in the days of the typewriter, the Shift key basically shifted some mechanisms in the typewriter to allow you to type another set of characters, usually uppercase. "Shift Lock" was a toggle that basically kept the keyboard in shifted position, and it was located in the same position that Caps Lock is located on most keyboards today.

![typewriter][typewriter]

When the days of computing came around, Caps Lock was moved to where the Control key now is, and the Control key was placed in the location of Caps Lock. However, the Control key was inconvenient to former typewriter users and mainframe users, and the Caps Lock key was moved pack to its original position on the 101 Enhanced Keyboard by IBM.

![101-Key IBM][101key-ibm]

This 101 Enhanced Keyboard soon became the de-facto standard for keyboard layouts, which is why our keyboards have this Caps Lock positioning. [More info on the 101 Enhanced Keyboard can be found here.][101key-info]

## How the Escape key was placed in the worst possible position

Meanwhile, the Escape key was placed on the very far top left on the keyboard, meant to be used as much as much as the function keys. It was created in the 1960's to allow programmers to switch from one type of code to another.

However, once this made no sense for the general user, Windows began using the key to close dialogs, mostly to mean "Stop". Other operating systems followed, and Escape became the key to exit or suspend the program in some sort of way.

## Why Vi uses the Escape key to switch modes

If you're a Vi/Vim user, you probably use the Escape key quite a bit. It's necessary to be able to any of the features of the program, and you'll probably find yourself hitting it at least twice per minute. The positioning doesn't make sense however, as it's in such an awkward spot. Why not the Control key? Or the Alt key?

Vi was built for a keyboard where Escape was in the position of Tab and Control was in the position of Caps Lock: **the ADM-3A.**

![ADM-3A Keyboard][adm-3a]

This is an incredibly convenient position. You don't have to move your hand in order to hit the key, and the key is big, unlike the tiny squares on a current laptop keyboard. It's too bad that keyboards aren't built like that today.

## Solutions?

On Chromebooks, you can change your keyboard settings to map the "Search" button to the Escape key.

The easiest and cheapest solution is to swap Caps Lock and Escape. On systems running the X Window System, you can put the following into `~/.Xmodmap`.

```
! Swap caps lock and escape
remove Lock = Caps_Lock
keysym Escape = Caps_Lock
keysym Caps_Lock = Escape
add Lock = Caps_Lock
```

There are many other solutions on how to do this, but the above is the one I currently use as a Linux user.

However, you still have the issue of mislabeled keys. Additionally, this fix does not work on Windows.

There are several keyboards out there that you can purchase that have the keys in a nice spot, e.g. the [Happy Hacking Keyboard][happy-hacking-keyboard]. However, they're usually a bit expensive as they're produced in very limited quantities due to the low demand.

Caps Lock and Escape were designed in a time where we didn't have many of the tools we have today. They're relics of the past that have carried on throughout computing history.

[101key-info]: http://www.pcguide.com/ref/kb/layout/stdEnh101-c.html
[happy-hacking-keyboard]: http://www.amazon.com/gp/product/B000EXZ0VC/ref=as_li_tl?ie=UTF8&camp=1789&creative=390957&creativeASIN=B000EXZ0VC&linkCode=as2&tag=colleged07a-20&linkId=NZT5S47X3O26UYYH

[chromebook-keyboard]: /img/chromebook-keyboard.png
[escape-mac]: /img/escape-mac.png
[typewriter]: /img/typewriter.png
[101key-ibm]: /img/101key-ibm.png
[adm-3a]: /img/adm-3a.png
