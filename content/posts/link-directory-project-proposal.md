---
title: "A Proposal For a Web Without Search Engines"
date: 2019-12-27T05:57:20+08:00
draft: false
---

i am very close to beginning yet another project, which will be constantly maintained.

it will be a directory of hyperlinks (not just HTTP links, either - i want to include dat:// and gopher:// and other hypertext resources as well), human-maintained at first, initially just by myself.

virtually all of the search engines that i trust to enter keywords into have been non-functional lately, and it's time for me to stop wasting time being displayed captchas and being told i am making too many requests.

this directory of hyperlinks will be public, and i may even use a simple content management system for them, but more than likely i will use 'hugo' or 'jekyll' etc because that way the list of links can be more machine-processable and transportable

one key feature i'd like to implement is the generation or creation of link blurbs that allows one to complete the purpose of one's search without ever having to access the hypertext resource beyond the list. so many blurbs on searx.me, google, duckduckgo, and qwant are completely useless - search engine requests should look like this:

] 'how to kill buffer emacs'
> C-x k kills one buffer...

and not:

>Killing a buffer makes its name unknown to Emacs and makes the memory space it occupied available for other use. The buffer object for the buffer that has ...

which is the third actual google search result on the first page of results. pathetic. waste of time. bad. in order to answer my question, i would have to load the GNU.org web page resource, and begin interpreting it. this had nothing to do with my original reason for using the search engine.

because this directory of links will be a list, it will, obviously, require LISP list processing if it ever becomes more complex than just a really long set of bookmarks >:3
