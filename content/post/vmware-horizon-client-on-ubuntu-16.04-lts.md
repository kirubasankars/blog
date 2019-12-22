---
title: "Vmware Horizon Client on Ubuntu 16.04 LTS."
date: 2017-09-05T21:59:29-04:00
draft: false
tags: ["linux", "shell", "vmware"]
---

## How to install VMware Horizon Client on Ubuntu 16.04. LTS

I had a issue installing VMware Horizon Client. Resolved it with some common tools in Linux. Thought a blog post probably make sense, could save someone's time. Also this knowledge could help to debug any general shared libraries related issues.

following command help you to download bundle file from vmware and assign executable permission to it. 

```$ wget https://download3.vmware.com/software/view/viewclients/CART17Q2/VMware-Horizon-Client-4.5.0-5650368.x64.bundle -o ~/Downloads/VMware-Horizon-Client-4.5.0.x64.bundle & chmod +x ~/Downloads/VMware-Horizon-Client-4.5.0.x64.bundle```

Note: Please don't copy & paste it and go to vmware website and get a latest or particular version you wanted to install. 

To install, run the following command.

```$ sudo ~/Downloads/VMware-Horizon-Client-4.5.0.x64.bundle```

Go through setup wizard and complete the installation. Good Luck for you. my Horizon client failed on start up. 

VMware Horizon Client was missing some shared library on my machine. How do I know what's missing? i did ran following command

```
    $ ldd /usr/lib/vmware/view/bin/vmware-view | grep 'not found'
		 libudev.so.0 => not found
		 libssl.so.1.0.2 => not found
		 libcrypto.so.1.0.2 => not found
```

Unlike other operating systems, Linux uses shared libraries a lot. There are good and bad thing about it. read about it. "**ldd**" command on any executable gives you list of all shared libraries used and weather a shared library exists on your machine. I needed those libs to start my horizon client. 

After spent a hour in google, found a **libglibmm** package has those libraries. 

#### Installing libglibmm

First find a right version to install it with following command.

```$ apt search libglibmm```

```
libglibmm-2.4-1v5/xenial,now 2.46.3-1 amd64 [installed]
  C++ wrapper for the GLib toolkit (shared libraries)

libglibmm-2.4-dbg/xenial 2.46.3-1 amd64
  C++ wrapper for the GLib toolkit (debug symbols)

libglibmm-2.4-dev/xenial,now 2.46.3-1 amd64 [installed]
  C++ wrapper for the GLib toolkit (development files)

libglibmm-2.4-doc/xenial,xenial 2.46.3-1 all
  C++ wrapper for the GLib toolkit (documentation)
```

Install the one tagged with **(shared libraries)**. in my case, the first one.

```$ sudo apt install libglibmm-2.4-1v5```

Now You can make sure with **ldd**, is all libraries are exits. Good Luck.

