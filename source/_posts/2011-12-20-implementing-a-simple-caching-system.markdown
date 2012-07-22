---
comments: true
date: 2011-12-20 10:55:05
layout: post
slug: implementing-a-simple-caching-system
title: Implementing a simple caching system
wordpress_id: 1690
categories:
- Development
- Tutorials
tags:
- cache system
- php
- php cache
---

Hello, 

I'm going to show you a simple way to cache a file. 

To illustrate my example, I will use a script that creates a single image from multiple images. 
I have writen [that script](https://github.com/Dinduks/Lastfm-Top-Albums) a few months ago to generate a patchwork of my top albums in [Last.fm](http://www.lastfm.com/user/Dinduks), due to the lack of working similar scripts. 




[
![Dinduks' Top Albums](http://lastfmtopalbums.dinduks.com/patchwork.php?user=Dinduks&period=3month&rows=2&cols=2&imageSize=200)
](http://lastfmtopalbums.dinduks.com/)




First, let's see how the script works, without the cache _system_: 



As you can see, the image is generated whenever the script is called. This isn't only greedy on the server's resources, but does also take a little time ; between 4 and 6 seconds for a common patchwork.

To avoid this repetitive task, the idea is to save the generated image on a file, and, each time the script is called, check if the image doesn't already exist before creating it again. 



### Create a signature of the source file


Since the image is generated from data that comes from the Last.fm Web Service, it will change according to it's response. Let's then create a MD5 hash of it.

    
    
    $response = file_get_contents($query);
    $responseHash = md5($response);
    





### Name the generated file


It's time now to choose a name format for our file. I chose the following:

    
    
    $fileName = "images/$user.$period.$rows.$cols.$imagesSize.$responseHash";
    



**Note**: Make sure you have the write and read permissions on `images/`.



### Save the file


At the end of the script, just before displaying the image, save it.

    
    
    imagejpeg($patchwork, $fileName);
    


You'll have to use `fwrite()` or a similar function depending on the type of the file you want to save.



### Check if the file exists 


The file is well saved now. 
The final step consists in checking, at the next request, if that file exists. If it's the case, answer with it, if it is not, run the usual code ; which is the image creation. 
The code below should be put right before the image creation process.

    
    
    if (file_exists($fileName)) {
        header("Content-type: image/jpg");
        echo file_get_contents($fileName);
        exit;
    }
    



You are now ready to implement your own little cache system. Have fun. :)
