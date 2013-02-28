---
layout: post
title: "Mono FastCGI and Apache"
date: 2008-09-05
comments: false
---
[ACM][0] has been using Apache with mod\_mono for a while (my fault) and while it works relatively well, there are some issues. Namely, every once in a while the mono server will crash and requires manual restarting. So when I heard that Mono now had FastCGI support, I was intrigued, hoping that it might alleviate these problems.




I couldn't find any instructions on setting it up with Apache (using mod\_fcgid), so I figured it out on my own. Here's how I configured it to run my development copy of Neztu on Debian lenny:



    
    # apt-get install mono-fastcgi-server2
    # mkdir /tmp/mono-fastcgi
    # chown www-data.www-data /tmp/mono-fastcgi
    # echo DefaultInitEnv MONO_SHARED_DIR /tmp/mono-fastcgi > /etc/apache2/conf.d/mono-fastcgi
    





I then put the following in my vhost configuration:



    
    Alias /neztu/ /home/matt/devel/neztu/www/
    <Directory "/home/matt/devel/neztu/www">
      DirectoryIndex index.aspx
      Options ExecCGI FollowSymLinks
      AddHandler fcgid-script .asax .ashx .asmx .aspx .axd .config .cs .dll .rem .soap
    
      FCGIWrapper "/usr/bin/fastcgi-mono-server2 /applications=/neztu:/home/matt/devel/neztu/www" .asax
      FCGIWrapper "/usr/bin/fastcgi-mono-server2 /applications=/neztu:/home/matt/devel/neztu/www" .ashx
      FCGIWrapper "/usr/bin/fastcgi-mono-server2 /applications=/neztu:/home/matt/devel/neztu/www" .asmx
      FCGIWrapper "/usr/bin/fastcgi-mono-server2 /applications=/neztu:/home/matt/devel/neztu/www" .aspx
      FCGIWrapper "/usr/bin/fastcgi-mono-server2 /applications=/neztu:/home/matt/devel/neztu/www" .ascx
      FCGIWrapper "/usr/bin/fastcgi-mono-server2 /applications=/neztu:/home/matt/devel/neztu/www" .axd
      FCGIWrapper "/usr/bin/fastcgi-mono-server2 /applications=/neztu:/home/matt/devel/neztu/www" .config
      FCGIWrapper "/usr/bin/fastcgi-mono-server2 /applications=/neztu:/home/matt/devel/neztu/www" .cs
      FCGIWrapper "/usr/bin/fastcgi-mono-server2 /applications=/neztu:/home/matt/devel/neztu/www" .dll
      FCGIWrapper "/usr/bin/fastcgi-mono-server2 /applications=/neztu:/home/matt/devel/neztu/www" .rem
      FCGIWrapper "/usr/bin/fastcgi-mono-server2 /applications=/neztu:/home/matt/devel/neztu/www" .soap
    </Directory>
    





And that's all there is to it. I will have to test it further to see if it is able to recover from its hiccups with this method.



[0]: http://www.acm.uiuc.edu
