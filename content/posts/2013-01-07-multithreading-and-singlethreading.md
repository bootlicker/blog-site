---
title: Multithreading and Singlethreading
author: admin
type: post
date: 2013-01-07T15:01:59+00:00
url: /pc/multithreading-and-singlethreading/
original_post_id:
  - 308
categories:
  - PC

---
Because I&#8217;ve been toying with the idea of starting up a YouTube channel (to further inflate my own ego), I&#8217;ve been investigating the possibility of putting together a budget video-editing computer. What I&#8217;ve discovered is that not only is it possible to put together a computer for video-editing for fairly cheap (around $AUD400, excluding certain things), but one need not throw away lots of money on constructing a computer for playing video games, either.

The websites I&#8217;ve been collecting data from include the Perth-based computer component suppliers [VTech][1], [Netplus][2] and (the much maligned) [Austin Computers][3]; and the benchmarking website [Passmark][4]. I&#8217;m sure there are plenty more other such websites, but I haven&#8217;t had the time to look further.

One of the important tasks in building a video-editing PC was to choose a CPU that was well suited for such a job. The difference between a gaming PC and the one I wanted to make was that the CPU, in video-editing, would primarily be used to crunch rendering data, and not used for displaying graphics on the fly. This is what lead me to multithreading.

[This article][5] lead me to the concept of multithreading, and was the motivation behind this post. It provides an insightful analysis of the new AMD CPUs that I had, before reading, become convinced were suitable for my purpose. The important piece of information that it highlighted (with a single sentence) was that PC gaming is dominated by singlethreaded CPU processes. For the reader&#8217;s information, &#8216;threads&#8217; are the smallest unit of computer instruction that an operating system can manipulate, and are the chief building block of the computer science concept of &#8216;multitasking&#8217;. The article plainly demonstrates that the new AMD processors are fantastic at multithreading computer instructions (highly suited to video-editing), but are lacklustre in comparison to the new Intel Ivy Bridge technology in terms of their ability to process singlethreaded (linear sets of instructions) information.

What also interested me was the fact that the article alluded to the ways in which the different political-economic factors that underlie the production of either of the two companies&#8217; CPU ranges impact on the products that they end up making. AMD is tied to another company with respect to some of its research and development, and this hampers its ability to reduce the size of the circuitry in its processors, amongst other things.

The outcome of all of this research is that if you&#8217;ve got your heart set on gaming and you want to spend modestly, I recommend buying an Intel i5 3470, 3570 or 3570K. Pursuant to the excel spreadsheet that I compiled below, you can purchase any one of these CPUs online, in Perth, for about $AUD200 each. _However_, if you are strapped for cash, or you have very little interest in the whizz-bang-pop-shazam-look-at-me-I&#8217;m-Bethezda-I&#8217;ve-been-making-the-same-game-for-decades-and-my-logo-sucks and you just want to edit videos and/or render 3D models, any of the well-performing AMD CPUs are more than capable of the job. It&#8217;s worth reiterating that the sheer pricetag of these AMD chips does much to commend themselves to the impecunious gamer.

&#8212;

This <a href="http://jumpnshoot9000.com/?attachment_id=311" rel="attachment wp-att-311">data</a> about the different CPUs under $200 (inclusive) available in Perth might also interest the reader. On Sheet 2 can be found graphical representations of the relationship between the processors&#8217; price, and aggregated processing power.

 [1]: http://www.vtechindustries.com.au/
 [2]: http://www.netplus.com.au/
 [3]: http://www.austin.net.au/
 [4]: http://www.cpubenchmark.net/index.php
 [5]: http://www.anandtech.com/show/6396/the-vishera-review-amd-fx8350-fx8320-fx6300-and-fx4300-tested