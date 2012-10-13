---
layout: post
title: "Review your code with Git"
date: 2012-10-13 14:47
comments: true
categories:
---

Whether you want to commit a part of your changes only or simply check your work
before you commit it, one of the Git commands you probably use the most, `add`, can
help you doing it throught its option `-p` (*patch*).

This option allows to choose the changes you want to stage.  
Or word for word, from Git's man:

> Interactively choose hunks of patch between the index and
  the work tree and add them to the index. This gives the
  user a chance to review the difference before adding
  modified contents to the index.

This is how it works, or rather how I use it:

After executing `git add -p .`, git enters an interactive mode, from where many
actions can be taken. Below are the ones I use the most.

* If the diff is too long, you can try splitting it with `s`. That will split it into
the smallest possible parts.
* If you want to stage the diff, simply choose `y`es.
* Otherwise, say `n`o.
* When the whole diff has been viewed, the interactive mode will quit automatically.
You can do it yourself tough, through the classic `^C`, or by selecting `q`.  
Note that this will simply quit the interactive mode and won't undo your actions.

Feel free to ask `?` about the other commands meaning, they might be useful in some
cases.

`git add -p` your best friend to review your code and not to commit stuff like
`console.log()`.  
Make the most of it!

