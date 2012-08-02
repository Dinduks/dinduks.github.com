---
layout: post
title: "Yet another blog that migrates to Octopress"
date: 2012-07-25 19:45
comments: true
categories:
---

Hi,

I recently migrated this from Wordpress to [Octopress](http://octopress.org/).

> Octopress is a framework for Jekyll, the blog aware static site generator
powering Github Pages. To start blogging with Jekyll, you have to write your own
HTML templates, CSS, Javascripts and set up your configuration. But with Octopress
All of that is already taken care of. Simply clone or fork Octopress,
install dependencies and the theme, and you’re set.

### Here are some reasons behind this choice:

#### Markdown
I'm become a fluent Markdown speaker after spending a decent amount of time at
GitHub and Stack Overflow. Not only it's a pleasure to write using it, but it also
let focusing on the most important thing — writing, and not to worry about pointless
things such as HTML formatting for example.

#### Speed
The blog posts being written in Markdown, there's a HTML version of them generated
before deploying the blog. Add `/index.html` at the end of this page's URL to
understand what I'm talking about.  
That basically means that the blog is a simple bunch of HTML files, doesn't have a
database, which make it extremly fast to lead and to be indexed by search engines.

I don't care *much* about SEO and fast loading time, which makes this point just a
simple detail.

#### Portabiliy
Many points here:

* Posts are born in Markdown: I can easily version them.
* Posts reborn as HTML: I can server them from any place, and that'll just work.
* Since the blog is static, the comments are hosted elsewhere, Disqus in my case,
thus making them protable from a blog platform to another.

#### Other random details
Octopress ships with a nice theme, which is perfect in my eyes: it's basic,
responsive and its font size is big enough to not fuck the reader's eyes.

### The migration
Now I'll show you how you can migrate your own blog to Octopress.

#### Migrate your blogs comment to Disqus
As I mentioned above, you need to use an external comments *provider* for your
Octopress blog.  
I personnaly went for Disqus because it's pretty popular and well integrated
with Octopress.

What you need to do is:

* Creating a [Disqus](http://octopress.org/docs/deploying/) account
* Install the Disqus Wordpress plugin
* Import your Wordpress blog comments to Disqus (this feature is available in your
user panel)

#### Create an Octopress blog
You don't say?!  

Start reading the [Octopress Setup](http://octopress.org/docs/setup/) chapter from
Octopress' documentation. It'll help you creating your blog.

#### Migrate Wordpress' posts
For this, use the [exitwp](https://github.com/thomasf/exitwp) tool.  
It's pretty easy to install and use:

* Clone it
* Export your blog
* Run the tool on it

And you're done. You'll now have a *\_post/* directory that you'll just need to move
to your fresh created blog *source/* directory.

More in depth use explanations can be found in *exitwp*'s README.

#### Fix the generated posts syntax
Heh, you really believed it would be that easy?! ;)

Although *exitwp* help *a lot* in the migration process, it sometimes doesn't
convert stuff as it should do. That's especially true if you have some fucked up
HTML formatting, some specific tags, such as Syntax Highlighter plugin ones.

What you need to do now is going throught all the posts one by one, and fix what
should be fixed.  
Good luck.

#### Deploy it!
Now that the migration is complete, you gotta put the results on the internets.

You can either host it on your own, as you would do for a classic Wordpress blog,
host if for free on Heroku, or, if you're as cool as me, host it in GitHub pages.

Whatever the way you choose, the [Deploying](http://octopress.org/docs/deploying/)
chapter on Octopress' doc can help you achieving it.

#### Keeping the blog on the same domain name
This party was straightforward for me, it is well explained in the
[docs](http://octopress.org/docs/deploying/github/#custom_domains).  

There was little problem though, with Disqus: my blog was hosted at *www.dinduks.com*,
the comments were correctly imported as coming from the *www* subdomain, except that
new comments, on the new blog, were detected as coming from the TLD *dinduks.com*
and not the subdomain *www.dinduks.com*.  
I made sure *www* was mentioned everywhere, but it didn't fix the problem.

My solution was to *migrate* the old comments from the correct domain
(*www.dinduks.com*), to the one Disqus was detecting (*dinduks.com*).  
It's not logical, but it's better than having no comments at all.

The [Migrate Threads](disqus.com/admin/tools/migrate/) feature can be found in the
the *Tools* section of your admin panel.
