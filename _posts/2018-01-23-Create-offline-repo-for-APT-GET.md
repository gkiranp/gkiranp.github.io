---
layout: post
title: "Create your own OFFLINE repository for apt-get"
date: 2018-01-23
tags: Ubuntu Linux apt-get
---

It's a nightmare, if you do not have connected to internet for your *Debian or Ubuntu* machine. I use to struggle to install dependent packages after first installation of my Debian. Untill I connect to internet I cannot install packages and untill I install relevant packages I am no way on internet.
I have found an alternative, where I get offline debian package collection in one of my directory and I will do #apt-get install from there. Let me list how to do that in 3 steps. <!--more-->

**Step 1: Collect all available DEB files:**
+ Your Debian/Ubuntu distribution DVD might have come with deb installer distribution. Check your cdrom, for `.../pool/main/` directory, and if it has deb files, then 'hola', copy them into your local directory.
+ You will definitely get download deb packages from cyber cafe and get them in thumb-drive and copy them to your local machine.
+ Check `/var/cache/apt/archives` in a Debian/Ubuntu machine, (may be your friend's), which has all the packages pre-installed. If it is not cleared/deleted, you will get them all in one place.

So, by now I have deb files copied in my local machine and I kept them in `/opt/deb-packages/` location.

**Step 2: Create a list:**
Goto `/opt/deb-packages/` directory and run below command,
```
#dpkg-scanpackages .  /dev/null  |  gzip -9c > Packages.gz
```

This shall take some time, give yourself a break.

**Step 3: Now, add sources list:**
Open `sources.list` file from `/etc/apt`
```
#gedit  /etc/apt/sources.list
```
and, add below line at the bottom of file,
`deb  file:/opt/deb-packages/  ./ `

That's it. You are ready to install your offline packages.

Run, `#apt-get  update `
and let it update all list.

Enjoy running `#apt-get install <your-package-name> `
and see your package getting installed..