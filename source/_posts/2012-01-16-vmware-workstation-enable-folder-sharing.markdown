---
comments: true
date: 2012-01-16 20:57:48
layout: post
slug: vmware-workstation-enable-folder-sharing
title: 'VMware Workstation: Enable folder sharing'
tags:
- open-vm-tools
- vmware
---

Hello,

I daily use VMware Workstation to code on Linux.  
Yesterday my dear Debian's Gnome broke because of a bad manipulation, so I just took it as a call to move on and try some other distro.  
I first installed Linux Mint Debian, and removed it because folder sharing didn't work, despite my effort to fix the problem. Then I tried with Kubuntu: the same issue.

The problem there was that my shared folders didn't show in `/mnt/hgfs/`.  
After reading many documentations, forums, and mailing lists, and trying to mount the shared folder manually, I reached a point where I got a **FATAL: Module vmhgfs not found** error.  
This error, as far as I understood, was occurring because of a bad installation of *VMware Tools*. Re-installing the latter didn't work.

The *vmhgfs* module, like some others, isn't sometimes built because it is not included in the *VMware tools*.
To build the required modules, you just have to install *open-vm-dkms*:

    apt-get install open-vm-dkms

Now restart *VMware Tools*:

    /etc/init.d/vmware-tools restart

And finally, mount the your shared folder!

    mkdir /mnt/hgfs/my_shared_folder
    mount -t vmhgfs .host:/my_shared_folder /mnt/hgfs/my_shared_folder

If that doesn't work, just log out and on your session.

I hope this tutorial has been helpful.

*Note*: The last post of this thread http://communities.vmware.com/thread/332887 was useful to me.
