---
layout: post
title: "Computer Science Programs - Joel Spolsky Saves Me Some Effort"
date: 2009-10-27
comments: false
---
Ever since my friend Elton made a
[post][0]
about what he wished he had learned in college, I have been meaning to make my
own post about my experiences at [UIUC][1], er, I mean,
[ILLINOIS][2]. I don't disagree with the things he
wishes CS programs would teach, though I do disagree with the value of the
education I received in college. While Elton seems to have enjoyed his time at
UT and done well, the three years I spent at UIUC were the most miserable of my
life so far. As I often find myself explaining to people today, there is
surprisingly little overlap between the skills required to be a good software
engineer and the things they teach you as an undergrad in what is supposedly one
of the top 5 computer science programs in the country. My classes there were
far more about obtaining a pretty piece of paper to hang on my wall than
preparing to enter the workforce. This was exemplified by the CS grad student I
met who appeared to be incapable of writing "Hello World" in C if his life
depended on it.




Anyway, today I was going through my RSS feeds and found Joel Spolsky's
[post][3] on the subject,
and he hits it on the head. Let's teach our students Scheme! It's so
functional and elegant! Nobody in industry uses it, but that's because they're
all unsophisticated heathens! One of my colleagues once remarked on my zeal for
producing a quality product by saying that "If you ignore a bug long enough,
Matt will fix it." Apparently if I delay a blog post long enough, Joel Spolsky
will write it.




While I'm on the subject of Joel Spolsky, however, I need to take exception to
something he said in his
[post][4] on "Duct Tape
Programmers":



> 
> Duct tape programmers have to have a lot of talent to pull off this
> shtick. They have to be good enough programmers to ship code, and we'll forgive
> them if they never write a unit test, or if they xor the "next" and "prev"
> pointers of their linked list into a single DWORD to save 32 bits, because
> they're pretty enough, and smart enough, to pull it off.
> 





As a member of the team which recently became the not-so-proud owner of GDI and
GDI+, I will say that if you do a crazy what-the-eff-is-he-doing "optimization"
like munging bits in a pointer and then fail to supply any unit tests for the
poor bastard who has to maintain your code after you run off to work on the Next
Big Thing, then you deserve to be fired. Or shot. Maybe both.



[0]: http://eptiger.blogspot.com/search?updated-max=2009-08-27T00%3A32%3A00-07%3A00
[1]: http://www.uiuc.edu
[2]: http://www.illinois.edu
[3]: http://www.joelonsoftware.com/items/2009/10/26.html
[4]: http://www.joelonsoftware.com/items/2009/09/23.html
