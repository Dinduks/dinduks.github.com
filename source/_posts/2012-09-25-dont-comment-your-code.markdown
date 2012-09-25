---
layout: post
title: "Don't comment your code, write good one"
date: 2012-09-25 22:33
comments: true
categories: 
---

Whether you've learned programming alone or had classes about the subject, you've
probably been taught to *use comments*.  
The more I write code and read about good practices, the more I realize this
*advice* is exactly the one you shouldn't give. It only encourages laziness,
writing dirty code, and filling the holes by commenting every piece of code.

I believe that, unless exception, you should not use comments, but instead think
every time before you write one: why are you doing this? Is your method or function
name not explicit enough? Fix it. Is it complex? Refactor it and move its main parts
to new methods or functions. Is it non-understandable? You're writing bad code.

When I say *exception*, I mean specific cases where you really need to explain
what you are doing: you're hacking to get the shit done, writing some complex
algorithm, etc.  
Also, if one needs to specify where he did copy some code from, comments might be a
good place.

    /**
    * Source: http://stackoverflow.com/a/9261887/604041
    */
    function getPopoverPlacement(popover, element) {
    }

The reason why I'm writing this post (rant?) is that I've seen this piece of code

    // The logo's copyright checksum
    const CHECKSUM = "herpderp";

used to justify the use of comments.

Wrong. I haven't had to think twice before recommending to name that constant
`LOGO_COPYRIGHT_CHECKSUM`.

That's quite an easy example to wreck, but one could improve almost any code outta
here the same way.

Let's see some examples of what how we can avoid comments:

#### From Jeff Atwood's [Coding without comments](http://www.codinghorror.com/blog/2008/07/coding-without-comments.html) blog post
A simple but efficient example:

    // square root of n with Newton-Raphson approximation
    r = n / 2;
    while ( abs( r - (n/r) ) > t ) {
        r = 0.5 * ( r + (n/r) );
    }

    System.out.println( "r = " + r );

Could be refactored to:

    private double SquareRootApproximation(n) {
        r = n / 2;
        while ( abs( r - (n/r) ) > t ) {
            r = 0.5 * ( r + (n/r) );
        }

        return r;
    }

    System.out.println( "r = " + SquareRootApproximation(r) );

I recommend reading his article where he too, calls to avoid comments.  
After all, Jeff Atwood word' more valuable than mine, right? ;)

#### Another example from the awesome [Objects Calisthenics]() manifesto
Here, it isn't about comments, but a complex code that a lazy-ass would have used
comments to explain:

    String board() {
        StringBuffer buf = new StringBuffer();
        for (int i = 0; i < 10; i++) {
            for (int j = 0; j < 10; j++)
            buf.append(data[i][j]);
            buf.append(“\n”);
        }

        return buf.toString();
    }

Well written, it looks like:

    String board() {
        StringBuffer buf = new StringBuffer();
        collectRows(buf);
        return buf.toString();
    }

    void collectRows(StringBuffer buf) {
        for (int i = 0; i < 10; i++)
          collectRow(buf, i);
    }

    void collectRow(StringBuffer buf, int row) {
        for (int i = 0; i < 10; i++)
            Buf.append(data[row][i]);
        buf.append(“\n”);
    }

Is that a lot of code? Oh, sorry. :( I didn't know you pay a fee for each LoC you write.

Objects Calisthenics is a wonderful manifesto to follow to improve the quality of
object oriented thinking and coding. If you can't follow all the rules, start with
some and improve.

