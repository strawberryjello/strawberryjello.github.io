---
layout: post
title: "Resetting keymaps using setxkbmap"
author: "Cristina Elep"
tags: [xmodmap, setxkbmap, emacs]
---

As a long-time emacs user, I've gotten used to swapping the locations of the Ctrl keys on whatever laptop or computer I'm using to make daily typing easier on my pinky fingers. I learned how to create a custom keymap (a .Xmodmap file) using [xmodmap][xmodmap] and kept a backup just in case. However, since I started using [Spacemacs][spacemacs] a few years ago I haven't relied on my .Xmodmap as much. I'd even forgotten that I had one until I started using an external keyboard and couldn't find a working Alt key.

The easiest thing to do would have been to delete or rename the .Xmodmap and reboot; I renamed my .Xmodmap but didn't want to reboot just yet, so I looked up how to reset the xmodmap settings. I wound up at [an xmodmap question on AskUbuntu][askubuntu], which pointed me towards setxkbmap. I checked the current keyboard layout using `setxkbmap -query`, then reset it to the default (US) using `setxkbmap -layout us`.

Notes

- The Arch Linux wiki has a [page about keyboard configuration][archwiki]; it says that setxkbmap only sets the keyboard layout for the current X session.

- The LinuxQuestions.org wiki [has a similar page][lqwiki] that also provides examples using setxkbmap.

[archwiki]: https://wiki.archlinux.org/index.php/Xorg/Keyboard_configuration
[askubuntu]: https://askubuntu.com/questions/29603/how-do-i-clear-xmodmap-settings
[lqwiki]: http://wiki.linuxquestions.org/wiki/Configuring_keyboards
[spacemacs]: https://github.com/syl20bnr/spacemacs
[xmodmap]: https://wiki.archlinux.org/index.php/Xmodmap
