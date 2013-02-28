---
layout: post
title: "Yay for Microsoft!"
date: 2005-06-17
comments: false
---
OK, so here's what happened:



    
*   
    
    I'm working on an application that uses the CredUI. To do so, I need to
    include WinCred.h. No problem, right? Except that WinCred.h didn't ship with
    VS.NET 2003\. In order to get it, I need to download the Platform SDK.
    
    
*   
    
    So I do just that. I download and install the Platform SDK, then try to
    start Visual Studio.
    
    
*   
    
    Except VS doesn't start. Instead it gives an error: "MS Development
    Environment has not been installed for the current user. Please run setup." I
    search all over the net, looking for a solution.
    
    
*   
    
    I spend all day trying different things: uninstall the .NET Framework
    manually, uninstall, reinstall, slaughter a goat and soak the computer in its
    blood - nothing works.
    
    
*   
    
    I notice that it only gives this error for my user account. Not for any of
    the other user accounts that I have set up. So I move my profile to a
    different folder, creating a default profile for my user account. I figure
    removing any filesystem documents unique to me **and** changing out my
    registry hive would do it, right?
    
    
*   
    
    But it doesn't. Finally I give up and delete and recreate my account to
    get a different SID, and that worked.
    
    
    





But that's a whole day down the drain, and I never found out what the problem
was. If anyone happens to find out, do let me know!
