---
layout: post
title:  "Laptop config management with Ansible"
date:   2019-04-12 18:30:00 +0100
categories: ansible config-management archlinux
---

Recently I got a new laptop and, at the same time, I was excited (more computing power, more battery, less noise) but also despaired: "Now I have to install and configure everything again".

I use [Arch Linux](https://archlinux.org) and I love it but you need to configure lots of options.

Good thing, though, is that there are official packages and AUR packages available for almost everything.

Anyway, I considered doing a dump of the packages in the old laptop, install them in the new one and copy their config files. But still, that was too much manual work, prone to error, etc.

Also, I wanted to try something different. Configure my laptop to use [Wayland](https://wayland.freedesktop.org) and [Sway](https://swaywm.org).

Lastly, I didn't want to repeat these actions manually again in the future.

In a conversation with my friend [Abel](https://twitter.com/amart1nr) he suggested that I could configure everything with [Ansible](https://ansible.com).
I told him "no way, too much work". But then I thought about and... "what the hell, why not? Can't be that complex".

So I created a [new repo](https://github.com/chmeee/arch-laptop-ansible) in Github and started working in it.

At the moment, I'm already using the laptop and making config changes directly from the Ansible roles. Although it is a work in progress as I intend to use Ansible for all configuration purposes.
That way, my configuration is going to be documented and I can reproduce it in any other Arch Linux.

I'll summarize a bit what I did. Even if you do not use Arch Linux, you can find some information that may be useful to you in case you want to go in this kind of journey.

For each group of packages and configuration, I created a role:

    ansible-galaxy init <whatever>

For instance: home-config, window-manager, editors, containers, virtualization, etc.

Then in each of them I install the packages, copy config files and launch services (if needed).

I created a new Ansible module for the AUR packages helper [`yay`](https://github.com/Jguer/yay) which is basically a copy of the `pacman` module substituting `pacman` for `yay` and modifying some options.

And also I had to do some logic to install vagrant plugins and visual studio code extensions.

There are some things still missing that I'm working but overall, it has everything I need.

Of course, there are some missing parts (like the `$HOME/.ssh` directory, API keys for cloud services, etc.) that obviously are not going to the github repo (me being paranoid I feel uneasy about having it public with the current data).

In the end, it's been an interesting exercise, I have learned more ansible and now I know exactly what's installed in my laptop and I can reproduce it painlessly in the future.

Please, feel free to fork, PR or contact me for comments.
