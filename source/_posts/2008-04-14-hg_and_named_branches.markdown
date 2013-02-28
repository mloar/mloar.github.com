---
layout: post
title: "hg and named branches"
date: 2008-04-14
comments: false
---
A few days ago I read [a comparison of Mercurial and Git][0]. One of the things the author had to say against Mercurial was that it had a really bad model surrounding named branches. At the time I hadn't really used named branches, so I didn't think much of it.




Well tonight I was working on setting up hgweb so that I could deprecate my svn repository, and I ran right into this problem. When I set up my crazy hg stuff to track PuTTY development, I managed to create two named branches in my repository: the upstream branch (putty) and my local branch (PuTTY). Now since I was only exposing my changes by pushing to a svn repo, this didn't really matter much. But now that I was going to expose the repository for public consumption, I wanted more descriptive names.




Unfortunately, this isn't straightforward by any means. In hg, the branch name is an arbitrary string that is intrinsic to the changeset. It is included in the changeset description which is used to generate the changeset hash. So there is no simply no way to change it on committed changesets. You can make a branch inactive by committing on it with a different branch name, but this doesn't hide it from hgweb or the output of `hg branches`. And there is no way to prevent an attempt to reuse that branch name later from generating a branch-shadow warning.




I see this as a rather severe problem. There are some ideas on the [Mercurial Wiki][1] about how to address this, but so far nothing.




So I am currently attempting to do nasty things with `hg transplant` to rebuild the repository history with more meaningful names. It's a huge pain, but I still think I prefer hg to git. I had to use git the other day to check out the [Ceph][2] code, and git still puts me off. For one thing, there's this whole 1.4-vs-cogito-vs-1.5 nonsense I don't really care to understand. The crazy development-all-over-the-place model that git enthusiasts tout as its greatest feature is its greatest downfall from a usability perspective. And the documentation still sucks.



[0]: http://www.rockstarprogrammer.org/post/2008/apr/06/differences-between-mercurial-and-git/
[1]: http://www.selenic.com/mercurial/wiki/index.cgi/BranchPlan
[2]: http://ceph.newdream.net/
