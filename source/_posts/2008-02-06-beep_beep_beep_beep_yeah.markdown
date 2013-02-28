---
layout: post
title: "Beep Beep, Beep Beep, Yeah!"
date: 2008-02-06
comments: false
---
In a previous post, I described setting up a zsh preexec function to change the current window title in screen. However, if you have tried this you may have noticed that if a background window changes its title, screen doesn't always update the caption bar to reflect the new title until you switch between windows. This limits the usefulness of this feature for telling when a long-running command finishes, or for telling when a bell is sounded in a window.




The key to this is forcing screen to refresh the caption bar at a reasonable interval. If you have nothing but window titles in your caption string, it does not appear to be refreshed at all unless you switch windows or the title of the current window changes.




There are a couple format strings which are useful for this. %c displays a clock which will force a refresh every minute; if you use %s you get a seconds display which obviously refreshes every second. %l also appears to refresh once a minute.




But suppose you don't want any of these - you just want the refresh. Fear not, for screen has a very cool feature: the backtick directive. This allows you to execute an external command and substitute its output into the caption. But it also allows you to specify how often to force a refresh of the caption.




The following example .screenrc lines force a redraw every 5 seconds:



    backtick 1 1 5 true
    caption always "%-Lw%{= BW}%50&gt;%n%f* %t%{-}%+w%1`"
    





The first parameter to backtick is a numeric id - use this same id as the length modifier on %\` to specify which backtick command is executed. The second parameter is the valid period, the third is the auto-refresh interval. As I understand it, the command will be executed valid &lt;= x &lt;= auto-refresh seconds after its previous execution.




This caption string places the window flags next to each window. One of these flags tells you when a bell occurs in the window. The other thing I like to do in screen disable visual bell with `vbell off`. I then `set beep_new` in my .muttrc and add the following to my irssi config:



    "fe-common/core" = {
        beep_when_window_active = "yes";
        beep_when_away = "yes";
        beep_msg_level = "msgs notices dccmsgs hilight";
        bell_beeps = "yes";
    };
    





I then configure PuTTY to highlight its taskbar icon when it receives a bell. So I can have PuTTY minimized, and if I get mail or someone says my name in IRC, PuTTY highlights its icon, I open it, and the window with the bell has a ! next to its name. Beautiful.
