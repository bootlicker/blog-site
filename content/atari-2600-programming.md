---
title: Atari 2600 Programming
author: bootlicker
type: page
date: 2017-07-20T02:43:41+00:00

---
I am currently learning how to program video games for the Atari 2600 in machine code. There is a large amount of resources for amateurs and beginners online, but they are frequently not collected in one place. For example, there is an enormous wealth of information for learning how to program the Atari 2600 on the Atariage forums, but there is only a small amount of centralised organisation of the total amount of information you can read on the forums. Another example of the difficulty of finding information for programming the Atari 2600 is Random Terrain&#8217;s [website][1]. Random Terrain collects a lot of incredibly useful resources for Atari 2600 programming, but almost all of the information is only relevant for learning batari BASIC, the high-level programming language for the 2600. It is very difficult to find information about machine language on Random Terrain&#8217;s website. I also disagree with the formatting and delivery of the information on the website. Much of the information on batari BASIC is located on one very big web page. The page is also somewhat out of date. For example, if you didn&#8217;t pay attention to _completely all_ of the text on the page, you would be fooled into thinking that the 2007 version 1.0 of batari BASIC was the latest version, when in fact there is a much more current version which was released in 2013. Even this version of batari BASIC may be old.

The purpose of this page on my blog is to collect as much information about learning how to program the Atari 2600 as possible. The first section deals with machine language. The second section deals with batari BASIC.

<p style="text-align: center; font-variant: small-caps;">
  I     Machine Language
</p>

asdf.

<p style="text-align: center;">
  A     <em>The Basics of Machine Language</em>
</p>

1     _Complete Tutorials From the AtariAge Forums_

  * <span style="text-decoration: underline;">Atari 2600 Programming for Newbies by Andrew Davie</span>: Random Terrain&#8217;s reformatting [here][2]. The index thread on the AtariAge forums [here][3] and [here][4]. They&#8217;re both the same. I don&#8217;t know why there are two.
  * <span style="text-decoration: underline;">Robert M&#8217;s Introduction to Assembly</span>: Random Terrain [here][5]. AtariAge [at the bottom][4] of the first post on the thread.
  * <span style="text-decoration: underline;">SpiceWare&#8217;s Collect Tutorial</span>: Random Terrain [here][6]. AtariAge [here][7]. Just in case something changes about the tutorial, the entire category for the Collect Tutorial is [here][8].

2     _The Atari Archives_

The website&#8217;s index can be found [here][9]. There are many good books for beginners on 6502 machine language on this website. They really break the issue down into simple elements.

3     _Random Terrain&#8217;s Assembly Language Links_

  * The &#8220;Useful Links&#8221; section can be found [at the bottom of the index page][10] of the reformatted SpiceWare tutorial.
  * Nick Bensema&#8217;s _How to Draw a Playfield_ guide is [here][11].
  * Nick Bensema&#8217;s _Guide to Counting Cycles_ can be found [here][12].

4     _Easy 6502_

The GitHub webpage for the interactive tutorial for learning 6502 machine language can be found [here][13].

5     _Nick Bensema&#8217;s Atari 2600 Programming Page_

The archived version of the website from 1997-2006 is [here][14].

<p style="text-align: center;">
  B     <em>Advanced Machine Language Techniques</em>
</p>

1     _The Stella Mailing List_

The Stella Mailing List was (or is?) a mailing list set up by the people who programmed and maintained the Stella Atari emulator. Many people who worked on the emulator conducted many important technical discussions on this mailing list. Spending a lot of time reading this mailing list will teach you many important lessons about how the Atari 2600 works, and how to get the most out of the system. You can browse or search the mailing list [here][15].

2     _The MiniDig_

This webpage contains an incomplete list of all the commented/annotated decompilations of Atari 2600 ROMs conducted through the Stella Mailing List. You can find the MiniDig [here][16].

3     _AtariAge Links_

_(a)     Discussion About Various Ways of Using the Kernel to Draw to the Screen_

  * Entire Thread [here][17].
  * Useful post from thread describing each of the various methods [here][18]: SwitchDraw, SkipDraw, FlipDraw, DoDraw.
  * The links in the thread to the Stella Mailing List discussion of each of the methods are broken. Find repaired links to the discussion on the topic here: 
      * SwitchDraw [here][19]. (Read the whole thread).
      * SkipDraw: Kirk Israel&#8217;s thread [here][20]. Dennis Debro&#8217;s thread [here][21].
      * FlipDraw [here][22].
      * DoDraw does not occur in the Stella Mailing List.

4     _6502.org_

This is an entire website dedicated to documenting and teaching machine language for the MOS 6502 processor. The 6502 is the CPU of the Atari 2600.

  * Please find the index of the website [here][23].
  * If you need to examine some examples of source code in order to learn a technique, the website provides a [long list][24].
  * This probably doesn&#8217;t belong under this subheading, but the website also contains a list of [tutorials][25].

<p style="text-align: center; font-variant: small-caps;">
  II     Batari BASIC
</p>

asdf

 [1]: http://www.randomterrain.com/atari-2600-memories.html
 [2]: http://www.randomterrain.com/atari-2600-memories-tutorial-andrew-davie-01.html
 [3]: https://atariage.com/forums/topic/33233-sorted-table-of-contents/
 [4]: https://atariage.com/forums/topic/47479-atari-programming-workshop-chapter-links/
 [5]: http://www.randomterrain.com/atari-2600-memories-tutorial-robert-m-01.html
 [6]: http://www.randomterrain.com/atari-2600-lets-make-a-game-spiceware-00.html
 [7]: https://atariage.com/forums/blog/148/entry-13884-collect-tutorial-index/
 [8]: https://atariage.com/forums/blog/blog-148/cat-188-collect
 [9]: http://atariarchives.org/
 [10]: http://www.randomterrain.com/atari-2600-lets-make-a-game-spiceware-00.html#useful_links
 [11]: http://www.randomterrain.com/atari-2600-memories-how-to-draw-a-playfield.html
 [12]: http://www.randomterrain.com/atari-2600-memories-guide-to-cycle-counting.html
 [13]: https://skilldrick.github.io/easy6502/
 [14]: https://web.archive.org/web/20130208050106/http://www.prismnet.com:80/~nickb/atari/index.html
 [15]: http://www.biglist.com/lists/stella/archives/
 [16]: http://www.qotile.net/minidig/
 [17]: https://atariage.com/forums/topic/75982-skipdraw-and-graphics/
 [18]: http://atariage.com/forums/topic/75982-skipdraw-and-graphics/?p=928232
 [19]: http://www.biglist.com/lists/stella/archives/200502/msg00058.html
 [20]: http://www.biglist.com/lists/stella/archives/200309/msg00117.html
 [21]: http://www.biglist.com/lists/stella/archives/200309/msg00056.html
 [22]: http://www.biglist.com/lists/stella/archives/200508/msg00049.html
 [23]: http://www.6502.org/
 [24]: http://www.6502.org/source/
 [25]: http://www.6502.org/tutorials/