---
layout: post
title: "Use Java 7 for IntelliJ's SBT plugin"
date: 2013-03-23 18:51
comments: true
categories: 
---

IntelliJ IDEA runs on JRE 6, and so does its SBT plugin. 
 
If you need to use a more recent version of Java (and you should): 

* Open the *Preferences* panel
* Go to the SBT section
* Tick the *Use alternative JRE* option
* Click the arrow on the right of the field to check if the IDE suggests the desired JRE
  * If so, choose it.
  * Otherwise, look for the path by yourself.  
It's `/Library/Java/JavaVirtualMachines/jdk1.7.0_09.jdk/Contents/Home` on my Mac.
