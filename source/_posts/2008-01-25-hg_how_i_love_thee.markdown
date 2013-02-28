---
layout: post
title: "hg, how I love thee"
date: 2008-01-25
comments: false
---
So a few months ago I was looking at a bunch of the 3rd-generation VCSs out there, and found all lacking in one way or another. Well, I recently started looking into it again, since I have been struggling with the problem of maintaining patched local versions of various projects, and the inability to do so in any sane manner using Subversion.




This time around Windows support was less of an issue for me. I have a Linux box running Samba that I use as my main home server, and so in the worst case I could use the VCS tools on the Linux box and compile the project from my Windows VM.




I tried the new bzr 1.1 and found it still to be severely lacking stability. It seemed to spit out a traceback if I so much as looked at it funny. I used bzr-svn to import both the PuTTY upstream Subversion repository and my local svn repo, and then attempted to merge them. I got tracebacks the first few ways I tried, and then I somehow managed to get it to do a merge - kinda. Apparently bzr has this way of representing every file in every repo using a unique identifier. The result of this was the my merge resulted in renames of every file to itself. Like x11fwd.c =\> x11fwd.c. That's not what I wanted at all! So I gave up on bzr.




hg, on the other hand, turned out to be just what I needed. I don't know if [hgpushsvn.py][0] existed the last time I looked at this stuff, but it does the logical thing that I mentioned in a previous post. You have an hg repo and an svn checkout in the same directory. You use hg to update the working tree to the way it existed at a certain revision, and then commit it using svn. Simple.




Here's the process I used to set up my checkouts:



    
1.  
    
    Use hgimportsvn/hgpullsvn to import the upstream repository into directory `upstream`.
    
    
1.  
    
    Use hgimportsvn/hgpullsvn to import my local copy into directory `local`. You could just import an empty directory in your svn repo if you're starting from scratch.
    
    
1.  
    
    Use `hg pull --force /path/to/upstream` from `local` to pull the changesets.
    
    
1.  
    
    `hg merge` to merge the changes.
    
    
    





The crazy thing was that hg somehow managed to do step 4 perfectly without any intervention on my part, even though the two branches had no shared history as far as it knew. I think it worked because it looked at the changesets on a purely chronological basis, but I'm not sure.




After that, it was very easy to use hgpushsvn to push my changes to my svn repo. I plan to migrate all of my svn checkouts of projects I don't own to hg in this fashion.



[0]: http://dev.pitrou.net:8000/hgsvn/devel/file/1212f4b09456/hgpushsvn.py
