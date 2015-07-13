---
layout: post
title: How to automatically connect to Windows Share
tags:
- Mac
---

My current HTPC setup includes a [Mac
Mini](http://www.apple.com/macmini/ "Mac Mini") sitting under a 40" LCD
flatscreen running [Boxee](http://www.boxee.tv/).  All my media is
sitting on a Windows 7 machine, with standard windows shares setup.  My
MacMini doesn't have any mouse or keyboard, so everything needs to be
done via the apple remote.  When not in use the MacMini sleeps so things
to come up correctly when waking.

Before coming up with a solution that worked, I tried a few other
options;

**Q.** Doesn't Boxee have a built-in Windows Share (Samba) client?\
\
 **A.** Well, yes technically it does.  However in practice I found it
to be pretty unreliable.  Some shares would connect fine while some
wouldn't, then the next day those that worked yesterday wouldn't
connect.  I wasn't able to find any log file to say what the problem
was.  Also another problem is that when you started Boxee it would
connect, but it would take a while (\~30 secs) before the media would
show up as available.  Not a big issue but annoying when I want to watch
something now!\
\
 *Cateat: This was with the Boxee Alpha, I am currently using the beta
which is much improved so these issues* ***may*** *be addressed.  Let me
know in the comments, I would like to hear!<span
style="font-style:normal;"> </span>*

*<span style="font-style:normal;">**Q.** Why don't you use the standard
Windows share mounting in Finder?\
\
 **A.** The problem with this is that this only works for as long as you
are logged in.  I can do a 'Reconnect at Login' by [adding the mounted
Volume to Login
Items](http://www.brightrev.com/how-to/apple/27-automatically-mount-a-windows-share-in-mac-os-x-tiger.html),
but this has issues as well.  When the machine wakes from sleep, the
volume says it's connected by there are no items in the volume.  Funny I
know....\
\
 *Cateat: This was with Mac OSX 10.5 Leopard so these issues* ***may***
*be addressed in 10.6 Snow Leopard.  Let me know in the comments, I
would like to hear!* </span>*

**Q.** OK smartie-pants, how did you make this work then?\
\
 **A.** I'm glad you asked!  I used the power of
[autofs](http://www.autofs.org/).  Autofs is a way of mounting local and
remote filesystems, and is used by OSX already.  The setup is quite
simple, but will require sudo/root access and simple use of command line
tools.

1.  Create and edit a new file: sudo nano /etc/auto\_smb
2.  Add an entry (one per line) to this file in the format

        -fstype=smbfs ://:@/

    Replace the with the your details, for example my line is

        Photos -fstype=smbfs ://dave:secretPassword@windows/Photos

3.  Save & quit (Ctrl+x) and run `chmod 700 /etc/auto_smb` to keep your
    password safe
4.  Now edit the master autofs configuration file:

        sudo nano /etc/auto_master

5.  Add a line that says:

        /Volumes auto_smb

    (You can set the first word to be whereever you want to volume
    mounted, but `/Volumes` is the default place in OSX)

6.  To force refresh run: `sudo automount -vc`
7.  Done!

This solution fulfils all my requirements and has been working great for
6+ months.  It doesn't matter what order I turn on my machines, the
autofs daemon will see if the network is up and then mount the shares as
soon as it can.  It doesn't seem to sit there trying non-stop to mount
the share if unavailable either, so it seems quite lightweight.

Occasionally I do get the annoying 'Shares are unavailable' window, but
not usually.  If anyone has a solution for hiding this window I would
love to hear it!  It floats above all other windows including Boxee.  I
am ok with writing my password in the file as it just my local home
network, I assume there are ways around this but I haven't bothered to
investigate it.

If you have similar setup or need help setting this up on your machine,
let me know in the comments ;)

Happy Sharing
