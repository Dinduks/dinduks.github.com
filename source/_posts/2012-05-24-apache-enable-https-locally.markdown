---
comments: true
date: 2012-05-24 13:37:11
layout: post
slug: apache-enable-https-locally
title: 'Apache: Enable HTTPS locally'
wordpress_id: 2003
categories:
- Tutorials
tags:
- apache
- apache2
- linux
- ssl
---

Sometime you'd like to use SSL on a local website, for development purposes. This is possible to do in few minutes. 



#### Enable Apache's SSL mod


If you're on some Debian based distro, and installed Apache with _aptitude_ or _apt-get_, executing the `a2enmod ssl` command will do the trick. 
This means _Apache2 Enable MOD_, and will simply create a symbolic link to _/etc/apache2/mods-available/ssl.*_ in _/etc/apache2/mods-enabled/_. 



If you installed Apache in some other way, enable the SSL mod manually. 





#### Ask Apache to listen on the port 443


443 is the default SSL port. Ask Apache to listen on it by adding `Listen 443` in your config file (_httpd.conf_ for example). 
You don't need to do that if you installed Apache with _aptitude_ or _apt-get_. Apache automatically listens on this port when the _SSL mod_ in enabled. 



#### Create an SSL certificate

#### 

    
    
    mkdir /etc/apache2/ssl/
    make-ssl-cert /usr/share/ssl-cert/ssleay.cnf /etc/apache2/ssl/apache.pem
    


This will generate a SSL certificate, based on the _ssleay.cnf_ template.



#### Setup your application's virtual host



Setting up SSL is over. Now it's time to create a virtual host for our application. 


    
    
    <VirtualHost *:443> # listen on the 443 port
      ServerName myawesomeapp.dev
    
      SSLEngine On # enabled SSL
      SSLCertificateFile /etc/apache2/ssl/apache.pem # specify the certificate file
    
      DocumentRoot /var/www/dev/myawesomeapp/
    </VirtualHost>
    



We're done, happy coding!
