---
layout: post
title: "liquidsoap"
date: 2008-08-09
comments: false
---
I recently upgraded my development box to lenny, and while it went very smoothly, it caused my Neztu setup to stop working. Turns out it was because the way apache would switch users changed somehow. While it used to get www-data's full group list, now it just changes uids without adding supplemental groups. Since my setup needed apache to run as a member of the audio group, I was no longer able to start the daemon from the web interface.




However, this turned out to be a blessing in disguise, as it caused me to go looking for alternate ways for the daemon to work besides simply shelling out to mplayer. This caused me to discover [liquidsoap][0]. It's a project, written in OCaml, which provides a simple functional scripting language for building and mixing audio streams. It supports several different audio formats, and it allows you to do all kinds of cool things - mixing, preemption, cross-fading, random or scheduled selection. You can send the resulting streams to an icecast server or output them to a soundcard. It even has an icecast 'harbor' so that you can use icecast clients as sources.




I have already rigged up a way to connect it to Neztu using the request.dynamic facility. However, this approach has some drawbacks. Namely, liquidsoap "prepares" two tracks in advance (it is built on the premise that the audio should never stop) and so it causes the queue as seen from Neztu to differ from the liquidsoap output. To resolve this, I think that I will probably implement a full-fledged source for liquidsoap that connects to Neztu.




How to do so is a bit of a quandary. My intention during Neztu development has been to support extensibility with respect to queue management and random song selection. The mechanism by which I achieve this is by having IScheduler and IRandomSelector interfaces. The theory is that these interfaces can be implemented by any class. This class then queries the votes as recorded in the database and puts together a schedule. By making sure that the same class type is used by both the web interface and the daemon, the view of the queue is consistent.




So a source for Neztu couldn't conceivably replace the entire daemon, since even with the advent of F\#, there doesn't seem to be any sane way to interop between OCaml and .NET. My thoughts right now are that I will have the source communicate with a modified Neztu daemon using some kind of IPC mechanism.




But I just wanted to post about this liquidsoap thing. I haven't been so excited about a software project in a long time.



[0]: http://savonet.sourceforge.net/
