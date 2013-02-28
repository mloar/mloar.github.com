---
layout: post
title: "A Brave New World of Secure DNS"
date: 2009-01-27
comments: false
---
I was looking at the OpenSSH code the other day and I saw some code related to
retrieving fingerprints from DNS. I had never heard of this, and I wondered how
that could be secure.




Reading [RFC 4255][0], the answer
to that was simple: DNSSEC. This really makes a lot of sense: if you're
trusting DNSSEC to guarantee the integrity of the value of the A record
providing you the IP address to connect to, why not trust it for the encryption
key to expect when you connect? This is actually quite nice, since DNSSEC
protects you against DNS spoofing but doesn't protect you against IP spoofing.




Of course, there's no reason it has to stop with SSH. It turns out that there
is a CERT RR defined in [RFC
2238][1] which is designed for storing X.509 or PGP certificates in DNS. This is
particularly interesting given the way that the trust chain for X.509
certificates for HTTPS currently works. The only guarantee you are connecting
to the real HTTP server for www.amazon.com and not one run by an attacker is
trusting that none of the Certificate Authorities that your browser trusts would
issue a certificate for www.amazon.com to anyone other than Amazon.com, Inc.
And for the vast majority of users, the CAs their browser trusts are the ones
that their browser or operating system vendor saw fit to include, which is
generally a very long list of CAs run by private companies whose rationale for
why you can trust them seems to range from "we charge money" to "we charge
obscene amounts of money."




However, if it were possible to securely publish SSL certificates in DNS, the
need for these shady authorities would be eliminated. And in turn, not needing
to shell out money for SSL certificates would hopefully lead to greater
proliferation of SSL for general web browsing, not simply for things like
order forms and online banking. The true beauty is that this is
backward-compatible - there is no reason why you couldn't obtain a certificate
from a CA and publish it in DNS. CAs might even continue to serve a purpose for
those who want to go to the hassle of getting an Extended Validation
certificate.




Likewise, the CERT record could be used for storing public keys for signing and
encryption of email. It would be much simpler for someone wishing to send you
an encrypted message to find your key if it were published in DNS, as they would
not have to determine which keyserver your key was on and whether it was in fact
your key. Having such a key in DNS would also make verification of signed
messages easier for tools such as SpamAssassin or even MTAs. Greater
proliferation of signed email could help in the neverending battle against spam.




Keys stored in such a manner could also be used to solve the longstanding
problem of having to remember passwords for the myriad websites you visit. Many
websites already use email addresses as usernames. In a future world, this
email address might be used to look up a public key, which could be used for a
challenge-response authentication. Though there's no reason sites couldn't ask
for a PGP public key instead of a password when creating an account today - the
main problem is that there is no protocol I know of for doing web authentication
using PGP keys - instead browsers support SSL client authentication, which
appears to me to be very unwieldy and I have never personally seen it used.




And I think that about sums it up - there are several separate public-key
cryptography systems that serve overlapping purposes: X.509 certificates, PGP
keys, and SSH keys. Each has a different trust model. But imagine if hosts
and users on the internet were able to authenticate themselves to each other
based on a single trust apex at the DNS root. Maybe this is all
pie-in-the-sky, but I have to hope that the future will bring resolution of the
awful mess we have now.



[0]: http://www.rfc-editor.org/rfc/rfc4255.txt
[1]: http://www.rfc-editor.org/rfc/rfc2538.txt
