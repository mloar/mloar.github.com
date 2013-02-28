---
layout: post
title: "PuTTY and GSSAPI"
date: 2008-11-03
comments: false
---
So apparently when I wasn't looking, the PuTTY authors added support for GSSAPI, which is great. Unfortunately, they only support SSPI on Windows. Granted, this is the cleanest way, but depending on which version of Windows you are running, SSPI may or may not work for you. If the client and server are in the same realm or AD domain it should work, but cross-realm is dicey since support for client-side host-to-realm mappings wasn't added until Vista. Some people on the Kerberos list expressed disappointment that the PuTTY authors went this route.




So I intend to add this support back in. The PuTTY GSSAPI support has a radically different code layout from my current patch, so the first thing I have done is merge in the PuTTY upstream and streamline my diff against it. The PuTTY code delayloads SSPI, so I'm hoping it will be straightforward to delayload MIT GSSAPI instead.




At the same time, I got a feature request a few months ago for gssapi-keyex support. I haven't made much progress there, but I am determined to fully exploit my current enthusiasm for working on PuTTY - it's always nice to work on projects that are actually useful to other people :).
