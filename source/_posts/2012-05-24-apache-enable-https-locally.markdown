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


If you're on some Debian based distro, and installed Apache with *aptitude* or *apt-get*, executing the `a2enmod ssl` command will do the trick.
This means *Apache2 Enable MOD*, and will simply create a symbolic link to */etc/apache2/mods-available/ssl.** in */etc/apache2/mods-enabled/*.

If you installed Apache in some other way, enable the SSL mod manually.

#### Ask Apache to listen on the port 443

443 is the default SSL port. Ask Apache to listen on it by adding `Listen 443` in your config file (*httpd.conf* for example).
You don't need to do that if you installed Apache with *aptitude* or *apt-get*. Apache automatically listens on this port when the *SSL mod* in enabled.

#### Create an SSL certificate

    mkdir /etc/apache2/ssl/
    make-ssl-cert /usr/share/ssl-cert/ssleay.cnf /etc/apache2/ssl/apache.pem

This will generate a SSL certificate, based on the *ssleay.cnf* template.

#### Setup your application's virtual host

Setting up SSL is over. Now it's time to create a virtual host for our application.

    <VirtualHost *:443> # listen on the 443 port
      ServerName myawesomeapp.dev

      SSLEngine On # enabled SSL
      SSLCertificateFile /etc/apache2/ssl/apache.pem # specify the certificate file

      DocumentRoot /var/www/dev/myawesomeapp/
    </VirtualHost>

We're done, happy coding!
