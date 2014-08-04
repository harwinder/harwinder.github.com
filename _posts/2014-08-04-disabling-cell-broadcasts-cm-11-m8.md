---
layout: blog
title: Disabling cell broadcasts in Cyanogenmod 11.0 M8 (i9300)
summary: Cyanogenmod has a really annoying Cell Broadcasts bug in Release 11 M8. Here's how to disable it
---

Yesterday was the day which comes after every 3-4 months, when I indulge into the flashing ritual. It was time for Cyanogemod 11 Release M8. (Cyanogenmod doesn't do stable releases etc. Since version 11, they now have monthly milestone releases, dubbed M releases). And my phone feel so snappier, again.

Cyanogenmod 11 M8 is based on Android 4.4.4, which bring some nice visual updates, especially for those updating from Cyanogenmod 10.2. It also fixed the wrong aspect ratio bug from Cyanogenmod 10.2 on my i9300, which crops up when one records videos (recorded videos are fine, btw).

However, M8 has a really annoying bug for my device. The device would continuously show "Cell Broadcasts" in the Messages application and this would keep on beeping my device throughout the day. Trying to disable this from the Settings app does not work either. Apparently, there is a (defect)[https://jira.cyanogenmod.org/browse/CYAN-2103] filed for this as well.

Here are the steps to disable it (copied from comments of the above defect):

{% highlight bash linenos %}

    su
    mount -orw,remount /system
    rm /system/app/CellBroadcastReceiver.apk

{% endhighlight %}