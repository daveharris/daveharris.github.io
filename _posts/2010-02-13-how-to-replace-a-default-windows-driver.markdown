---
layout: post
title: How To Replace a Default Windows Driver
tags:
- Windows
---

I had a problem where the network card driver in Windows 7 was faulty. 
It is a [known
issue](http://windowsfixup.com/2009/08/windows-7-freezes-during-network-file-copying/)
with the Asus on-board ethernet card.  The fix was to install the Vista
driver, but doing that is easier said than done.

I first tried to just install the driver over the top of the old one
which looks like it worked but didn’t replace it.  I then tried to
un-install the driver via the Device Manager.  You then have to reboot
for it to take effect, but on boot Windows detects the hardware and
installs the same driver again!!!

To get around this you need to turn off hardware detection.  You may
also need to allow unsigned drivers (a new requirement in Windows 7, not
Vista).  Both of these are set via Group Policy.

Click Start -&gt; Run -&gt; gpedit.msc (and push Shift + Enter to run as
admin) Navigate to Computer Configuration -&gt; Administrative Templates
-&gt; System -&gt; Device Installation -&gt; Device Installation
Restrictions Set ‘Prevent installation of devices not described by other
policy settings’ to ‘Enabled’ Set ‘Allow administrators to override
Device Installation Restriction policies’ to ‘Enabled’

Then go to the Device Manager (&lt;Right Click&gt; Computer -&gt; Manage
-&gt; System Tools -&gt; Device Manager) and un-install the driver. 
Then reboot.  The driver should not be installed by Windows.  Go to the
Device Manager again and it will be listed under unrecognised device or
something.  Now right click on the device and then ‘Install Driver’ and
give it the proper device driver.
