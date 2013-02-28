---
layout: post
title: "The Elusive Perfect VCS"
date: 2007-06-18
comments: false
---
This is the first in what I hope to be a series of posts about my search for a
VCS that fits my needs. I'm sure yet another discussion on this topic is the
last thing the web needs, but hey, you're reading it.




I have been using [Subversion][0] for both personal and group projects for
quite a while now. It is very nice, especially compared to the archaic CVS,
but it has one feature that is glaringly absent: merge management. It also
does not allow for disconnected operation, which is annoying when you like to
work on the go.




There is an [svnmerge.py][1] that is in the subversion repository, but is not
officially part of subversion. It also only allows you to merge changes within
the same subversion respository, so its usefulness to me is limited.




What I need in a VCS, and what gave rise to this adventure, is the ability to
maintain what is often called a "vendor branch." Specifically, I want the
ability to:



    
*   
    
    Create a branch of an open-source project
    
    
*   
    
    Version-control my changes
    
    
*   
    
    Merge upstream changes into my branch
    
    
*   
    
    Ideally, I would like to be able to push my changes back upstream (in
    those cases where I actually have commit access)
    
    
    





This is what got me looking at the so-called third-generation VCSs. The three
most popular are:



    
*   
    
    [Bazaar][2]
    
    
*   
    
    [Mercurial][3]
    
    
*   
    
    [Darcs][4]
    
    
    





Bazaar and Mercurial are both written in [Python][5], whereas Darcs is written
in everyone's favorite language, [Haskell][6]. Darcs is also based on an
"theory of patches," whereas Bazaar and Mercurial are more like subversion in
how they track changes.




At this point it should be clear that interoperability is key for these new
VCS. Especially important is interoperability with subversion, as it has
become almost a gold-standard in the open-source world.




Both Bazaar and Mercurial, like all good Python apps, support plugins. Darcs,
as far as I can tell does not. Bazaar has a number of interop plugins,
including [bzr-svn][7], which supports two-way merging. There is a set of
scripts available for Mercurial called [hgsvn][8] which supports pulling from
subversion repositories. Darcs does not have anything built-in, but the people
behind Darcs have put together this nifty script called [Tailor][9] which can
convert between almost anything and almost anything else.




In my case, I have for the moment chosen to go with bzr-svn. I hit one small
snag, however. bzr-svn requires patches to the Python bindings for Subversion
that are not included in any released version of Subversion. I use Windows,
and I attempted and was shamefully unsuccessful in recompiling with these
patches. However, someone else [had better luck][10]. After installing his
bindings, I was able to check a subversion repository out using bzr. I have
not yet thoroughly tested it, however.




I think that does it for this installment. I may have more to say on this
topic in the future.



[0]: http://subversion.tigris.org
[1]: http://www.orcaware.com/svn/wiki/Svnmerge.py
[2]: http://bazaar-vcs.org
[3]: http://www.selenic.com/mercurial
[4]: http://www.darcs.net
[5]: http://www.python.org
[6]: http://www.haskell.org
[7]: http://bazaar-vcs.org/BzrForeignBranches/Subversion
[8]: http://cheeseshop.python.org/pypi/hgsvn
[9]: http://wiki.darcs.net/index.html/Tailor
[10]: https://answers.launchpad.net/bzr-svn/+question/7801
