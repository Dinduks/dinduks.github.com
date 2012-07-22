---
comments: true
date: 2012-01-05 17:57:21
layout: post
slug: rails-cannot-load-such-file-openssl
title: 'Rails: cannot load such file -- openssl'
wordpress_id: 1831
categories:
- Development
- Rails
- Tutorials
tags:
- openssl
- rails
- ruby
---

While setting up my **Rails** development environment on my fresh Kubuntu VM, I've encountered many errors. 
This one was occurring when trying to launch a WEBrick server: 

    
    
    /home/dinduks/.rvm/gems/ruby-1.9.3-p0/gems/activesupport-3.1.3/lib/active_support/dependencies.rb:240:in `require': cannot load such file -- openssl (LoadError)
    



This error means that your Ruby isn't compiled with **openssl**. 

Assuming that you use RVM, these are the steps to follow to fix this issue.

Install the _openssl_ package

    
    
    rvm pkg install openssl
    


Remove the Ruby installation you're using

    
    
    rvm remove 1.9.3
    


And finally recompile Ruby with _openssl_

    
    
    rvm install 1.9.3 --with-openssl-dir=$HOME/.rvm/usr
    



Everything should be working now. Don't forget to: 

    
    
    rvm use 1.9.3 --default
    



I hope my first Rails related tutorial was helpful, happy coding! :)
