---
layout: post
title: "More Caveats and Features"
date: 2007-06-19
comments: false
---
I have run across some other interesting things in my testing that I would
like to point out:



    
*   
    
    Using shared repositories with bzr on Windows, I have run into some
    interesting locking issues; namely, bzr locks the repository and then waits on
    its own lock.
    
    
*   
    
    Using bzr-svn, you can only clone the root of a repository. This kind of
    makes sense, but is annoying. **UPDATE: The author of bzr-svn set me straight.
    bzr-svn has this notion of branching schemes that may require you to specify
    additional parameters if the svn repository doesn't use the standard
    trunk/branches/tags layout.**
    
    
*   
    
    Using hgsvn, the working copy that results will be both an hg repository
    and a subversion working copy. Therefore, the following workflow should work:
    
    
    
        
    1.  
        
        Import a subversion repository using `hgimportsvn` and `hgpullsvn`
        
        
    1.  
        
        Make changes and version-control them with `hg`
        
        
    1.  
        
        Submit changes back to subversion repository with `svn`
        
        
    
    
    
    





Continuing my ramblings on the differences between these systems, I must say
that bzr's command set is very close to subversion. hg, on the other hand, has
a decidedly different workflow.




I realized that I didn't comment on git in my last post. While this is yet
another option, it is only supported on Windows under cygwin (yuck!), so I
won't be trying it.
