---
layout: post
title: "The Internet is Broken"
date: 2005-05-02
comments: false
---
Well, it seems I've finally found the reason why I have intermittent
connection problems to this site and the other sites I host. It seems that the
GTLD servers, which are authoritative for all .COM domains, are having some
trouble with .COM nameservers. Namely, they don't think they're authoritative
for them, when in fact they are THE authority for them. Since the SamAMac
nameservers are .COMs, this causes problems. So now I have registered them as
.NET nameservers as well. Hopefully this should solve everything.




It's kind of annoying, though, that nothing has been done about this problem.
Very infuriating.
