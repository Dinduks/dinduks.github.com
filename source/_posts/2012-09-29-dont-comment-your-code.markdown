---
layout: post
title: "Don't comment your code, write good one"
date: 2012-09-29 17:42
comments: true
categories: 
---

*Dislaimer: I'm not a pro and I'm open to your feedback and critics.*

Whether you've learned programming alone or had classes about the subject, you've
probably been taught to *use comments*.  
The more I write code and read about good practices, the more I realize that
*advice* is exactly the one you shouldn't give. It only encourages laziness,
writing dirty code, and filling the cracks in by commenting every piece of code.

I believe that most of the time you should not use comments, but instead think
every time before you write one: why are you doing this? Is your method or function
name not explicit enough? Fix it. Is it complex? Refactor it and move its main parts
to new methods or functions. Is it hard to understand? You're writing bad code.

When I say *exception*, I mean specific cases where you really need to explain
what you are doing: you're hacking to get the shit done, writing some complex
algorithm, etc.  
Also, if one needs to specify where you did copy some code from, comments might be a
good place for this purpose.

    /**
    * Source: http://stackoverflow.com/a/9261887/604041
    */
    function getPopoverPlacement(popover, element) {
    }

The reason why I'm writing this post is that I've seen this piece of code

    // The logo's copyright checksum
    const CHECKSUM = "herpderp";

used to justify the use of comments.

Wrong. I didn't need to think twice before recommending to name that constant
`LOGO_COPYRIGHT_CHECKSUM`.  
That's quite an easy example to counter, but one could improve almost any code out
there as effortlessly as shown above.

Another downside of using comments, as mentionned by my friend
[Nicolas](http://www.badmood.eu/), is that comments need to be maintained, just like
the code.  
Not only this means more things to take care of and more work to do, but in real
life the code gets updated while comments don't.

Let's see some examples of how we can avoid comments by writing better code:

### From Jeff Atwood's [Coding without comments](http://www.codinghorror.com/blog/2008/07/coding-without-comments.html) blog post
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
After all, Jeff Atwood's word's more valuable than mine, right? ;)

### From the awesome [Objects Calisthenics](http://www.bennadel.com/resources/uploads/2012/ObjectCalisthenics.pdf) manifesto
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

Is that a lot of code? Oh, sorry. :( I didn't know you pay a fee for each single LoC
you write.

Objects Calisthenics is a wonderful book about improving the object oriented
thinking and coding. **Read it**, and if you can't follow all the rules, start with
some and improve accordingly.

### Some code of mine
Take a look at this code:

    def find_user_repos(username)
      resp = @http_client.call("/users/#{username}/repos")
      raise UserNotFound.new(username) if resp['message'].to_s == 'Not Found' if resp.is_a? Hash

      repositories_array = Array.new
      resp.each do |repository_hash|
        repo = RepositoryConverter.fill_object_from_hash repository_hash
        repositories_array.push(repo)
      end
      repositories_array
    end

Starting from line 5, you have to carefully read the code to understand it. One
might think *let's just add a comment!*. No.  
Let's clean that mess.

    def find_user_repos(username)
      resp = @http_client.call("/users/#{username}/repos")
      raise UserNotFound.new(username) if resp['message'].to_s == 'Not Found' if resp.is_a? Hash

      create_repos_array(resp) do |hash|
        RepositoryConverter.fill_object_from_hash hash
      end
    end

    private
    def create_repos_array(repositories)
      repositories_array = Array.new
      repositories.each do |repository_hash|
        repo = yield repository_hash
        repositories_array.push(repo)
      end
      repositories_array
    end

Here, I simply moved the code that creates a repositories array in another method,
this has many advantages:

* One can read the code and understand what's happening, without caring about the
implementation.
* This method can be used elsewhere.
* It can be tested... If it wasn't private.

### Where to explain how the big parts of my app fit together?
Probably not in the code itself.  
I'd suggest doing this in a separate or in the *README* file.

