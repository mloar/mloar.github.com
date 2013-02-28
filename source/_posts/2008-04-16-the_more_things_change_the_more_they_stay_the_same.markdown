---
layout: post
title: "The more things change, the more they stay the same"
date: 2008-04-16
comments: false
---
So as I said I would in last night's post, I read more of the Git documentation and various blog posts surrounding the topic. Now that I understand more about Git, I do find its model interesting. As I understand it, Git basically stores changesets as floating objects, and you have heads (which they call branches) which point to changesets, which then point to their parent changesets. You can pull random changes into a Git repository - it doesn't care. So you could have the Linux kernel sources in your repo, and pull in Samba, and then nuke all of the heads that point at the Linux kernel sources, prune your repository, and hey! You just switched your repository from Linux to Samba! What fun!




But as cool as that sounds, I've decided to stick with Mercurial. Here's why:



    
*   
    
    _Append-only storage model._ With Git, you have it creating new files all over. You're supposed to periodically run `git gc` if you want your disk usage to be reasonable. This also comes into play when serving Git repos over HTTP, as mentioned in the next item.
    
    
*   
    
    _HTTP as a first-class transport mechanism._ The [Git documentation][0] says that the preferred method of serving Git repos is running a daemon that listens on port 9418\. HTTP is supported, but the documentation warns that its less performant, since it works the same way that the static-http transport in Mercurial. You also need to run some command to give your repository extra magic or something for serving in this way. Mercurial has a handy-dandy CGI script that is both a smart server for hg clients and displays a pretty interface for web browsers, which I greatly prefer, since I need another daemon running like I need another hole in my head.
    
    
*   
    
    _More consistent commands._ The Git documentation may be getting better, but there is still a dizzying array of different commands with different options.
    
    
    





I have been working with hg for a while now and really the only problem I have had is this thing surrounding named branches which ultimately is little more than an annoyance. So I'm going to stick with it and hopefully they'll come up with a good solution for it in a future version. Or I'll get bored some night and come up with something myself. You never know.




I also gave [bzr][1] another look. Apparently back in February it became an official GNU project. So from the perspective of avoiding projects backed by either Linus Torvalds or Richard Stallman, Mercurial is a winner. They recently released version 1.3\. Thoughts:



    
*   
    
    Their interoperability is still lacking. The bzr-hg read-only support had an OMGINCOMPLETE warning on it. I tried to try out bzr-svn again, but apparently Jelmer's idea of "stable" isn't what you think - it bailed and told me I needed bzr 1.4\. But the version they released all of a week ago is 1.3\. I didn't see any other branch in his directory that was obviously meant for 1.3, so I gave up.
    
    
*   
    
    The bzr project is backed by Canonical, the same folks behind Ubuntu, and they have given bzr the slogan _Version Control for Human Beings_. That's just too funny.
    
    
*   
    
    Still no inline branch support. They have this lightweight branch thing that [didn't work so well when I tried it last][2]. Now, hg's inline branch support is what got me into this whole mess of looking at VCS again, so I don't hold this one against them too much.
    
    
*   
    
    Other than the branches on launchpad.net, there doesn't seem to be a pretty web interface commonly used. Some of the branches linked to from the plugins page give you the wonderful empty directory listing of a bare bzr branch.
    
    
    





And I guess I shouldn't neglect to mention [Darcs][3] while I'm at it. But it's late and I really should be in bed, so I'll be laconic about it:



    
*   
    
    Haskell
    
    
*   
    
    Tailor
    
    
    





'Nuff said.




P.S. To be fair, you could do the Linux-\>Samba thing with hg if you wanted to. But it would at least require a `--force` to `hg pull`.



[0]: http://www.kernel.org/pub/software/scm/git/docs/user-manual.html#exporting-via-git
[1]: http://bazaar-vcs.org
[2]: /blog/archives/2007/06/19/more_caveats_and_features/
[3]: http://wiki.darcs.net/
