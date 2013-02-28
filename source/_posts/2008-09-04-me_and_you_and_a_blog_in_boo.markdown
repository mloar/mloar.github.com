---
layout: post
title: "Me and You and A Blog in Boo"
date: 2008-09-04
comments: false
---
You may have noticed that I have changed my blog yet again. I had switched to [NanoBlogger][0] a while back, but I wasn't quite satisfied with it. For one, it was still separate from the rest of my site. Also, while the concept of blogging software written entirely in bash is novel, it is also quite slow. A thousand invocations of sed can't be the most efficient way to do anything.




So I set about coming up with a way to migrate my blog to use spin like the rest of my site. About this time I was also exploring new languages as part of my "maybe C++ isn't so wonderful after all" epiphany. I had dabbled with Python before and found it kind of nice, so I started working in Python.




However, I soon found something about Python that irritated me. Python has automatic memory management, but for other resources, you still have to do C-style cleanup, which is ridiculous. So it uses refcounting/garbage collection to automatically free memory. Great. I still need deterministic cleanup for file handles, database connections, etc. Not only do you have to explicitly call close() on the object when you are done with it, but you need to build for exception safety through the use of try-finally\*. This makes C++ with its RAII designs actually look good.




I had been using [Mono][1] and C\# for other projects. At least the .NET Framework got this right - objects owning unmanaged resources implement the IDisposable interface. C\# contains a `using` statement which not only automatically calls Dispose on the object no matter how the block is exited, but when used correctly also scopes the variable to the block.




However, I've worked with C\# before, and I wanted to try a new language. That's when I discovered [Boo][2]. It's a language inspired by Python, but built as a .NET language (IronPython reimplements the Python class libraries on top of the .NET Framework with the goal of compatibility with code written for CPython; Boo doesn't aim for Python compatibility and uses the .NET class libraries). Boo is also statically typed with type inference (and has optional duck typing).




And thus I wrote Bloog. It is designed to take a NanoBlogger database and build a thread-based blog that can be converted by [spin][3]. While I could have simply used `verbatim` blocks and kept the HTML as is, I didn't want to. Luckily, I found [html2text][4], a Python thing that takes raw HTML and converts it to [Markdown][5], which was the syntax I had been using for my most recent entries anyway. After wiring Bloog up to [Markdown.NET][6], I discovered something disturbing. Not only is it not possible to parse the Markdown syntax in a streaming fashion (it supports grouping link URLs at the end of the content), but all the parser implementations I have seen rely on generating a bunch of MD5 sums for the purposes of escaping certain characters. Not surprisingly, the Markdown conversion was very slow. So I hacked up the Markdown converter to output thread instead, and just converted all of my old blog entries to that. On top of that, I do all the timestamp-based optimizations to only generate what I need to, and the result was a compose-preview cycle that is orders of magnitude faster than NanoBlogger. My hope that got me through this project is that this will persuade me to post more often.




I would be extremely surprised if anyone else has the need to convert a NanoBlogger blog to thread, but I've made my [Mercurial repository][7] public, just in case.




So, this is my new and hopefully more permanent blog. Please let me know if you see anything out of order.




\*Apparently Python 2.5 adds the `with` statement which works like `using`, but you still have to import it from `__future__`.



[0]: http://nanoblogger.sourceforge.net
[1]: http://www.mono-project.com
[2]: http://boo.codehaus.org
[3]: http://www.eyrie.org/~eagle/software/web/
[4]: http://www.aaronsw.com/2002/html2text/
[5]: http://daringfireball.net/projects/markdown
[6]: http://www.aspnetresources.com/blog/markdown_announced.aspx
[7]: /hg/bloog/
