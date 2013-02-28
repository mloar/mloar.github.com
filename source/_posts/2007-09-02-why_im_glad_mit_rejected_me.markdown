---
layout: post
title: "Why I'm glad MIT rejected me"
date: 2007-09-02
comments: false
---
MIT Kerberos is a steaming pile of shit.




"What critical functionality can we break in this release?"




"I know! Let's make it so you can't initialize a kadmin interface out of a
credential cache!"




"Brilliant!"




**UPDATE 9-27-2007:** While this remains an issue, it turns out that what I'm
trying to do is an uncommon scenario. By default, the kadmin/admin principal
has the attribute DISALLOW_TGT_BASED, which specifically prohibits
instantiating a kadmin interface using a TGT (a credential cache containing a
ticket for kadmin/admin will work, and that is not affected by this bug).
However, at ACM, we have for a long time created user accounts using a script
which initializes the interface using a TGT out of a credential cache, so that
it can perform AFS operations without having to reprompt for a password, and
as a result removed the DISALLOW_TGT_BASED attribute from the kadmin/admin
principal. This works fine with the MIT Kerberos 1.3 client, but fails with
newer clients.




At any rate, we will likely be switching to [kadmin-remctl][0].



[0]: http://www.eyrie.org/~eagle/software/kadmin-remctl
