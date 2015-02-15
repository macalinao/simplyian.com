title: How to skip all Yaourt prompts on Arch Linux
date: 2015-02-15 16:39:31
tags:
- arch
- linux
---

[Yaourt][yaourt] is probably the best tool to automatically download and install packages from the [Arch User Repository][aur], also known as AUR. It's really powerful; however, by default, it prompts you a **LOT** for confirmations of different things, such as checking if you want to install something, if you want to edit the `PKGBUILD`, etc. As a result, Yaourt is pretty annoying if you're used to the hands-free nature of most other package managers.

As it turns out, there is a file you can create called `~/.yaourtrc` that can change the behavior of Yaourt.

To turn off all of the prompts, type the following into a new file called `~/.yaourtrc`:

```
NOCONFIRM=1
BUILD_NOCONFIRM=1
EDITFILES=0
```

The first line will skip the messages confirming if you really want to install the package.

The second line will skip the messages asking you if you want to continue the build.

The third and last line will skip the messages asking if you want to edit the `PKGBUILD` files.

When you're done doing this, Yaourt should now stop being a pain to use. Have fun with your hands-free installs!

[yaourt]: https://wiki.archlinux.org/index.php/yaourt
[aur]: https://aur.archlinux.org/

