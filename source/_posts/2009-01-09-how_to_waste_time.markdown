---
layout: post
title: "How to Waste Time"
date: 2009-01-09
comments: false
---
My method of choice? Rewriting managed code projects in C++.




I've been doing that for a couple of things, namely [Neztu][0] and most recently [bloog][1]. The former actually makes sense, since I have blogged before about my issues with Mono. My most significant qualm about it is its lack of support for fully precompiled sites, which means your clients get wonderful 5-10 second delays when it decides it needs to recompile something. I had been under the impression that writing a web application in C++ would be an exercise in pain and suffering, but it turns out that when you combine [cgicc][2] with the absolutely excellent [pqxx][3], you get a (relatively) rapid development platform, and combined with the magic of FastCGI you get the performance and stability that is sorely lacking on so many sites these days. I have my new C++ Neztu in a very functional state, but I wanted to implement all of the features of my 0.1 release before I make a formal release. In the meantime, you can look at the [hg repo][4], under the neztu-cxx branch. I have also decided to drop the liquidsoap support. It seemed cool at the time, but forcing two tracks into a "not queued but not playing" state is kind of a dealbreaker, and the methods of interacting with the rest of Neztu were kludgey at best.




My other project was pretty stupid, as other than being managed code, there wasn't anything terribly wrong with bloog. But my philosophy is that if I enjoy it, it's not really wasting time. Which is good, because thanks to [wmwork][5] I can tell you that I spent 15 hours rewriting it in C++. The two main benefits were that I discovered the original bloog had some bugs in date parsing that meant it didn't handle timezones correctly (all my latest entries are timestamped in UTC, but older ones need adjustment). Also, even my get-it-done sloppy unperformant C++ is 22% faster than the Boo version. Like the original Boo version, I don't intend to make any formal release of this code, both because it's hardly production quality and because I seriously doubt its usefulness to anyone else, but it is in [Mercurial][6].



[0]: /software/neztu
[1]: /blog/2008/09/04/me_and_you_and_a_blog_in_boo/
[2]: http://www.gnu.org/software/cgicc/
[3]: http://pqxx.org
[4]: /hg/neztu
[5]: http://www.godisch.de/debian/wmwork/
[6]: /hg/bloog
