---
layout: post
title: "Self-Righteous Stupidity"
date: 2008-02-23
comments: false
---
So I was reading a [strategy guide][0], and I noticed the following text:



> 
> Some of the information in this guide are spoilers, so I have greyed them out like this: Vyse is really a woman! This requires basic CSS1 support in your browsers (Netscape 6+ , Internet Explorer 4+, any KHTML or Gecko browers). Note: I never code with IE support in mind and I don't care if it works in it or not, I'm the one following web standards, not them.
> 





Of course the supposedly grey text was not grey in IE7, so I looked at the markup:



    <span class="spoiler">Vyse is really a woman!</span>





Okay so far, but where is class "spoiler" defined?



    <div id="faqBody">
    <style type="text/css">
    legend  {color: black; text-decoration: none; font-size: larger}
    .top  {font-size: smaller; text-align: right;}
    .spoiler{color: grey; background-color: grey;}
    





Of course, what does the [HTML 4.01 specification][1] have to say about this?



> 
> HTML permits any number of STYLE elements in the HEAD section of a document.
> 





Oops.



[0]: http://faqs.ign.com/articles/430/430440p1.html
[1]: http://www.w3.org/TR/html401/present/styles.html#h-14.2.3
