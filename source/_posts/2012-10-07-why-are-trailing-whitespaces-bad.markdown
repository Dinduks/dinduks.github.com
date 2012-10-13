---
layout: post
title: "Why are trailing whitespaces bad"
date: 2012-10-07 13:12
comments: true
categories:
---

Whenever I see a trailing whitespace, my teeth gnash and I realize that *some
people just want to see the world burn*.

Trailing whitespaces suck, please, don't use them and ask your code editor to
highlight them. Below are some reasons why.

## Revision control systems and diff tools
This is the most important point.  
For a diff tool, basically the *thing* used by CVS to detect code changes, this
code:

    function updateRepositoriesList($scope, Repository) {

Is not the same as:

    function updateRepositoriesList($scope, Repository) {..

This, along with wrong indentation or using tabs instead of spaces, leads to
unnecessary conflicts and is annoying when merging commits.

## Moving inside the code
When I tell my editor to go to the end of the line, I obviously mean the end of
the meaningful code, not some spaces after it.

## Code display inside editors
On editors that wrap long lines, such as VIM, few spaces at the end of the line may
lead to a useless line wrap.

    function updateRepositoriesList($scope, Repository) {..|
    ...                                                    |
        loadingAnimation('show');                          |

## Other reasons
### Additional spaces increase the file size
That's a very important point... If you store your code on floppy disks.
### The parser will have to skip an extra character when compiling
Yet another important point. When coding on a
[Intel 8086 processor](http://en.wikipedia.org/wiki/Intel_8086).

# How to fight trailing whitespaces
## By correctly configuring your editor
### Highlighting them
If you don't use VIM, skip this part.

If you do, add `set list` to your *.vimrc*, this will display unprintable characters
such as our lovely trailing whitespaces and non-breaking spaces.  
You can customise the characters used for that purpose thanks to the `listchars`
command:

    set listchars=trail:◃,nbsp:•

### Wiping them
By searching and replacing them: `%s/\s\+$//g`.  

I personally created a function that does the dirty work for me:

    function! FutureShock()
      silent! %retab        " Replace tabs by spaces
      silent! %s/\%u00a0/ / " Replace nbsp by spaces
      silent! %s/\s\+$//    " Replace twsp by spaces
    endfunction

And mapped it to *\<LEADER\>f*:

    map <LEADER>f :call FutureShock()<CR>

*[Future Shock](http://youtu.be/aDEX1XO9uW0) is a Stratovarius song.*


Check [my VIM configuration](https://github.com/Dinduks/dotfiles/blob/master/.vimrc)
for more awesome commands.

## By looking for them before you commit
You review your code before committing it, don't you? ;)  
Thanks to the Git diff tool, you can clearly see trailing whitespaces highlighted in red when using `git diff`; `git show`, or `git add -p` (among others).

You now have no excuse for having these abominations in your code.

