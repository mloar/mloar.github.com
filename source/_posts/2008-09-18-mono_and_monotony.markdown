---
layout: post
title: "Mono and Monotony"
date: 2008-09-18
comments: false
---
Work has been pretty slow lately - not too many bugs to work on. But I have
been keeping busy at night trying to figure out Mono issues. I upgraded the
test webserver at [ACM][0] to lenny and set up Mono
FastCGI, but they still managed to get it to randomly encounter compilation
errors due to missing files.




Several nights of tedious debugging later, I believe I have discovered the
problem - when a new ApplicationHost is instantiated, it deletes all of the
files in the DynamicBase of the AppDomain. Once I discovered this, I remembered
that the Mono people do say to only run one FastCGI server at a time. However,
I'm not sure I like this approach, and so I'm planning to write a wrapper script
that will ensure that different servers use different directories to avoid
interference.




Also, I have made some edits to my previous post on Mono FastCGI. My Deny rule
was ill-conceived, and so I have changed it to simply send all ASP.NET filetypes
to the FastCGI server. And while I realize that the Mono folks
[recommend][1] using
paths instead of extensions, as far as I can tell this is not possible using
mod\_fcgid and FCGIWrapper.




This brings me to another question - what is the best way to make an edit to a
published post? Should I try to preserve the original content, appending edits
to the end or using strikeout? Or simply replace? I'm leaning toward the
latter, though I would like some kind of audit trail. Since I have this all in
a Mercurial repo anyway, I'm thinking I need to get the changelog wired into my
system somehow. I tried this once before, but I couldn't tease the log out of
hg in a format that cl2xhtml would take.




I suppose I should end this post before I really start to ramble.



[0]: http://www.acm.uiuc.edu
[1]: http://www.mono-project.com/FastCGI#Paths_vs._Extensions
