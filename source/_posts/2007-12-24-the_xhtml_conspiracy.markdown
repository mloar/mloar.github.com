---
layout: post
title: "The XHTML Conspiracy"
date: 2007-12-24
comments: false
---
So I had always had the impression that XHTML was the replacement for HTML, and that anything new really ought to be in XHTML. However, I have recently become enlightened:



    
*   
    
    XHTML is only really useful when parsed as XML, which only occurs when it is served with its proper MIME type of `application/xhtml+xml`. IE still does not support this, as it does not yet truly support XHTML. When served as `text/html`, all major browsers will basically parse it as HTML.
    
    
*   
    
    When parsed as XML, standards-compliant browsers will not attempt to render the document at all if it does not validate.
    
    
*   
    
    XHTML is not forward-compatible - XHTML 1.1 pages will need to be rewritten to validate as XHTML 2.0\.
    
    
*   
    
    The W3C is now continuing development of HTML 5 parallel to XHTML development.
    
    
    





As a result, I have been converting my site, including this blog, back to HTML 4.01 Strict.




References:
[Beware of XHTML][0]



[0]: http://www.webdevout.net/articles/beware-of-xhtml
