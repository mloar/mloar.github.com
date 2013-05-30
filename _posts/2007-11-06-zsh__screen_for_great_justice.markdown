---
layout: post
title: "zsh + screen for great justice"
date: 2007-11-06
comments: false
categories: software
---
So I was reading screen(1) last night, and I came across something in the section on screen titles
which interested me:



    Finally, screen has a shell-specific heuristic that is enabled by setting the window's
    name to "search|name" and arranging to have a null title escape-sequence output
    as a part of your prompt.  The search portion specifies an end-of-prompt search string,
    while the name portion specifies the default shell name for the window.  If  the name
    ends in a ':' screen will add what it believes to be the current command running in
    the window to the end of the window's shell name (e.g. "name:cmd").  Otherwise
    the current command name supersedes the shell name while it is running.
    





If found this very interesting. I start mutt and irssi using the screen command, so their window
titles are useful, but I usually end up with 3-4 windows all named 'zsh'. This would be an easy way
to remedy that.




I use zsh's new fancy prompt theme system, so what I ended up doing was copying the stock theme file
to my home directory and changing its name. But here's the guts of what I had to do:



    screen_hack="%{^[k^[%}"
    PS1="$screen_hack$base_prompt$path_prompt %# $post_prompt"
    





The ^\[ are literal escape characters. Apparently the %{ %} are important - if you exclude them, zsh will
get very confused when you use tab completion. Try it and you'll see what I mean.

Once you have done this, all that's left is setting the shelltitle in .screenrc:



    shelltitle '% |zsh'
    






And voila! Magic auto window-titling.

After that, I was reading the part of screen(1) that talks about what escape sequences screen
recognizes, and I found something interesting:



    ESC ] 83 ; cmd ^G     (A)  Execute  screen command.  This  only  works if multi-user support
                          is compiled into screen. The pseudo-user ":window:" is used to check the
                          access control list.  Use "addacl :window: -rwx #?" to create a user with
                          no rights and allow only the needed commands.
    






Hmm! It struck me that this could be used for a lot of cool things, including an alternate way to do the titling. Since zsh has the very cool duo of precmd and preexec, it was relatively simple to set this up. .zshrc:



    function precmd {
      prompt_adam1_precmd
      echo -ne "\033]83;title zsh\007"
    }
    
    function preexec {
      local foo="$2 "
      local bar=${${=foo}[1]}
      echo -ne "\033]83;title $bar\007"
    }
    






My precmd calls the function that my themed prompt, adam1, requires, as well as resets the title to
zsh. The one sticking point was parsing out the part of the command I wanted. $2 contains the full
command after alias expansion. However, by default zsh does not break variables into words, so
$2\[1\] will be the first character of the command, not the first word. the ${=2} tells zsh to break
foo into words on spaces. However, there's yet another trick: it won't do anything if $2 does not
contain spaces. So that's why I add a space to $2 and call it $foo.

And here's the .screenrc:



    aclchg :window: -rwx  #?
    aclchg :window: +x title
    






And there you are. This approach strikes me as a little cleaner, so I think it's what I'm going to
go with. Plus, you can use this special escape for lots of cool other things. Right now I'm
working on setting it up so that urlview will open lynx in a separate window, so that I can open
links and then go right back to mutt.

**UPDATE:** I just solved that last part for someone in comp.mail.mutt.
It's as simple as putting the following in a .urlview:



    COMMAND /bin/echo -e "\033]83;screen lynx -accept_all_cookies -vikeys %s\007"
    






**UPDATE:** Someone in comp.mail.mutt posted a much simpler solution to the later problem.
You can accomplish the same thing with screen's -X option, like so:



    COMMAND /usr/bin/screen -X screen lynx -accept_all_cookies -vikeys %s
    






This has the advantage of not requiring you to grant the :window: user access to the screen command.
Since this allows any process that can write to your terminal to start processes under screen, it could
be a potential security risk. So I would recommend using the latter solution.
