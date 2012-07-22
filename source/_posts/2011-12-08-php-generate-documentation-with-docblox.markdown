---
comments: true
date: 2011-12-08 00:00:17
layout: post
slug: php-generate-documentation-with-docblox
title: 'PHP: Generate documentation with DocBlox'
wordpress_id: 1608
categories:
- Development
tags:
- docblox
- documentation
- php
- phpdocumentor
---

I recently have had to generate a PHP project's documentation and I've chosen the popular [PhpDocumentor](http://phpdoc.org/) for this purpose. 
This tool is unfortunately outdated, hasn't been updated since 2007, and thus throws a lot of PHP warnings and cannot do what I was asking it. 

My friend [Ludo](http://testonsteroid.tumblr.com/) has suggested using [DocBlox](http://www.docblox-project.org/) which is, compared to PhpDocumentor, more modern - supports PHP 5.3, faster, and consumes less memory. 

After trying it, I can say that it's indeed a great tool, inasmuch as I could generate documentation for my project 5 seconds after installing it. 



### How to use it: 




#### Installation


Make PEAR know about DocBlox's channel

    
    
    pear channel-discover pear.docblox-project.org
    


Then install DocBlox(-beta)

    
    
    pear install docblox/DocBlox-beta
    



The command line _docblox_ should be available for use now.



#### Use




    
    
    docblox -d /path/folder1,/path/folder1/folder2 -t /path/to/target/directory
    


Easy, ha? :)

Make sure you separate the source directories by commas only, no spaces. 
You can also use some of the basic PhpDocumentor commands.  
