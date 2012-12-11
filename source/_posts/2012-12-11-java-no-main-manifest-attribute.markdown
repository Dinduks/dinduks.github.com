---
layout: post
title: "Java: no main manifest attribute"
date: 2012-12-11 11:42
comments: true
categories:
---

I won't go though explaining how to create a *build.xml* file, the
[official manual](http://ant.apache.org/manual/using.html), which is really good,
does it better than I would.

The error in question occurs because the *java* executable, after reading the
[Manifest](http://en.wikipedia.org/wiki/Manifest_file) file from the inside of the
JAR, doesn't know what is the entry point of the program; i.e. the class that
contains the ugly `public static void main(String[] args)` method.

To fix the error, that class' full name needs to be specified in the *build.xml* file.  
For example:

    <jar destfile="${jar}" basedir="${build}">
        <manifest>
          <attribute name="Main-Class" value="my.awesome.package.Main" />
        </manifest>
    </jar>
