---
layout: post
title: JavaOne Day 1
tags:
- JavaOne
---
The first full day at JavaOne was fullon, I left the hotel at 7.30am and
have just got home now at 10.45pm![]()! First call of the day was the
free breakfast and then the first General Session of the conference. The
queue was huge, with basically everyone attending queuing to be in the
same room all at the same time. It filled up three walls of the massive
food hall. We got in really quickly though (the whole conference has
been really efficient really, it has to be with 15,000+ people
attending). As we got closer I could hear Hey Ya by Outkast playing and
when I walked in the door to the literally the largest room I have ever
seen there was a bunch of people dancing on the stage. As we crowded for
a closer look, we found out that it was actually Outkast (not what sure
what they have to with Java but anyway) and they basically rattled off
all their hits as the room was filled. I will take some photos of the
main hall, words cannot describe how large it is!

The keynote then started with some big wigs from Sun and it was really
interesting. They invited guests in Amazon (to show the Kindle), the CEO
of Sony Erricsson and then finally Neil Young. Neil was showing off his
latest discography collection on Blu Ray that makes use of Java for the
interactive menu system, pretty sweet really. It was announced that 100%
of all Blu ray players run Java too, so it definitely gives us a foot up
in the market. They also threw out some numbers, NetBeans has been
growing at 44% for 3 years in a row now, and MySQL now has **65,000
downloads per day** (up from 50,000 before the takeover by Sun).

For some really flashy stuff, there was an awesome demo of JavaFX. It
allows Java to run on the web, desktop and mobile devices with no change
to the source. The demo was called ConnectedLife which was a mashup of
Flickr, Twitter and Facebook. The next JavaFX demo showed off how it
could use the specific hardware for graphics acceleration and stuff. It
was an app running on a mac that played about 100 different HD movie
trailers simultaneously, while swirling around in a globe, very cool.
Hard to believe that is Java![]()! The big announcements were that Java
6 update 10 was being shipped today and that OpenJDK had made it into
the latest releases of Ubuntu, Red Hat and Fedora (to much rapturous
applause).

That set up for a really good and full on day, with my first session
taking an in-depth look at Java 6 update 10. the new features are:

-   A new Java Plugin to replace the aging WebStart browser plugin. It
    is now modular, so just downloads what parts of the JRE it needs
-   A new Deployment Toolkit
-   A new modular Java Kernel
-   No more cold starts, jre running in background process
-   Better AA fonts on windows
-   Nimbus Swing look and feel to replace Metal
-   JavaFX updates

Then a quick session on the next Eclipse release (Ganymede) due for
June:

-   A new Update Manager (finally)
-   Subversive SVN client
-   RAP and RCP improvements. These allow rich swing based clients built
    within eclipse to also be deployed on the web with Ajax with some
    changes to config files… very cool

Then a session aptly named " JavaScript™ Programming Language: The
Language Everybody Loves to Hate". This was a really good session if you
had an indepth knowledge of the intricacies and anomalies within
javascript. Most of which went way over the top of my head, especially
when he talked about Higher Order Functions (thats 2 or more nested
functions….) …. ahhhh wow

After that was a totally packed session called “Defective Java™ Code:
Turning WTF Code into a Learning Experience” which was taken by a
lecturer and lead developer on FindBugs. I highly suggest you take a
look at [his
slides](http://daveharris.files.wordpress.com/2008/05/turning-wtf-code-into-a-learning-experience.pdf).
He showed some common traps for young developers such as:

-   When writing multi-threaded apps, they use the field that they are
    synchronising as the lock/mutex which fails miserably
-   Using the same simple class name as a class in another package and
    not realising
-   DateFormat should be called DateFormatter and is not thread-safe
-   The intricacies of overriding .equals because it can mean different
    things in different circumstances

The last 2 sessions were how to develop desktop games with the
jMonkeyEngine engine. This is very very cool… and so easy to make
something with water effects and 3D effects and stuff. Nice and fast
too. The other session was to do with the new field-based annotations
(such as `NotNull and `Immutable) to be included in jdk7 as part of
JSR308.

After that (yes there is more) I managed to squeeze into a full
hands-on-lab session using OpenPortal and GWT to create a simple Ajax
application that uses WebServices to display stock price updates. There
seems to be a huge focus on Ajax and Rich Internet Applications (RIA) so
it was nice to get hands on with some of this.

I have another very full day tomorrow but [here are today’s
photos](https://www.flickr.com/photos/daveharris/sets/72157623731805218)

I see the iPhone is going to be released in NZ…. hmmmmm lol

Seeya all tomorrow night ;)

Dave
