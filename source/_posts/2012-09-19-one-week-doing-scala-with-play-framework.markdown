---
layout: post
title: "One week doing Scala with Play framework"
date: 2012-09-19 21:24
comments: true
categories:
---

I have recently joined the company behind the
<a href="http://playframework.org/">Play framework</a>,
<a href="http://zenexity.com/">Zenexity</a>, in which I'll be working along with my
computer science studies, and spent my first week learning Scala and the framework
mentioned above.  


Besides the benefits of having (almost) free coffee, a free MacBook Pro (I'm not
materialistic, just glad to save 1500€), working with skilled developers and getting
a discount for doing sport (although I'm not going to do it #FatAssForLife),
this job will be the opportunity for me to learn a language completely different
than what I've been used to, new programming techniques (asynchronous and
non-blocking stuff) which Play is all about, all of that while pursuing my studies.

During that week, I managed to build a small application which doesn't do much,
it just displays the contributors of a specific GitHub projet, but helped me
learning Scala, getting familiar with its syntax, learning some of its subtleties,
and getting familiar with the Scala/SBT/Play ecosystem.

This first week has been exciting and interesting so far, I have enjoyed using Scala
and been surprised many times by what it can do.

Below are random thoughts about this experience.

### It's compiled!
As an ex-PHP guy and rubyist, my experience with compiled languages came down to
writing code in an IDE, pressing F6 and waiting for stuff to compile and getting
executed.  
It was quite different this time, using VIM and and the console allowed me to be
closer to the code I write, and aware of what's happening behind the scene.  

An awesome feature of SBT (Scala Build Tool) that is worth mentionning is the
ability of compiling, running tests, or doing any other task every time the
source code changes. An editor in full screen and a little (say 5 lines) console
at the bottom of the screen makes coding faster since the compilation errors are
shown as the code is being updated.  

Beside the nifty *cool* features, having a compiler that warns of shit that
might happen is a big plus. You know when your app is broken, and that might save
writing few extra functional tests.

### Explicit parameters and return types
No more duck typing for me, in Scala, as in many *serious* languages, you **have**
to explicitely tell the type of the arguments a function or method may take.  
Example: `def add(a: Int, b: Int) = a + b`.

On the other hand, the return type isn't mandatory, it is implicitily detected.  
The same function as above with the return type specified:
`def add(a: Int, b: Int): Int = a + b`.  
I personally specify it for all my methods, I believe it's a good practice and helps
readability (you know what a function returns just by reading its signature).

These constraints may be annoying at some point, for example when wanting to
return some dumb result, or using a `println` in the last line of a function:
`println` returns a Unit type (you can see it as Java's `void`) while your function
expects an `Int` result for instance.  
The annoyance is just temporary anyway, and it's only a matter of time before
one gets used to it; I actually did by the end of the week.

### I can use VIM
I love VIM, and just the thought of switching to some IDE to do *real* made me sad,
but my sadness vanished quickly when I noticed that most of the guys at Zenexity use
text editors (TextMate, Sublime Text).  
[VIM's Scala plugin](https://github.com/derekwyatt/vim-scala) works pretty well,
but may need some polishing. In fact, I'm planning to learn some VimL so I can
improve it a bit.

### Tuples
I have never used a language that has tuples before, and I have to admit that
they're really awesome. A tuple is basically a collection with a constraint on the
number of elements, their type, and their order.  
One of its  most useful use case is the ability of returning more than one value
from a function. Example:

    def nameAndAge: (String, Int) = ("Samy", 20)
    val (name, age) = nameAndAge

In this case, a method that returns a tuple (notice the parenthesis, they're tuples
delimiters) is defined. Below, we define **two values**, not a tuple, that contain
the first and second tuple elements respectively.
