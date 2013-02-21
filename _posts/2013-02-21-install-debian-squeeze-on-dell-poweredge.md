---
layout: blog
title: Installing Debian Squeeze on Dell PowerEdge R420
summary: Debian Squeeze is a stable (but really OLD) distribution, here is how to install it on newer hardware
---

# {{ page.title }}

__21 Feb 2013 - Chandigarh, India__

I am a big fan of Debian. Debian is not bleeding edge (though there is "unstable" and "experimental"), Debian does not have a time-based release cycle. The thing I like the most about Debian is that they are so damn stable. I love apt-get. I use Debian on all the production machines I run.

Recently, we bought these new Dell PowerEdge R420 machines. Debian installation was a breeze except that the Ethernet controller (Broadcom) would not show up. Accompanying Dell manuals suggested I go in for Redhat/SuSE, which are supported out of the box, as these Dell servers came with some management CD-ROM, which would load some drivers etc. Since, the network interface would not come up and I had only the first installation CD, I could not download get anything with apt-get.

Solution is to do a basic install and download a newer kernel from (squeeze-backports)[http://packages.debian.org/search?suite=squeeze-backports&section=all&arch=any&searchon=names&keywords=linux-image-3.2], which support these newer hardware. All, I had to do was download the following packages:

    linux-image-3.2.0-0.bpo.4-amd64
    firmware-linux-free
    initramfs-tools
    linux-base

Copy these packages to a USB drive and then to the Dell machine. A quick reboot, and I could see the Ethernet controllers:

    02:00.0 Ethernet controller: Broadcom Corporation Device 165f
    02:00.1 Ethernet controller: Broadcom Corporation Device 165f
