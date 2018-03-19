---
title: 'PS4 Architecture: More ‘Open’?'
author: admin
type: post
date: 2013-02-23T06:16:32+00:00
url: /ps4/ps4-architecture-more-open/
al2fb_facebook_link_id:
  - 552216077_10151276415666078
al2fb_facebook_link_time:
  - 2013-02-23T06:16:37+00:00
al2fb_facebook_link_picture:
  - featured=http://jumpnshoot9000.com/wp-content/uploads/2013/02/38_sony_computer_entertainment-prev-150x150.png
original_post_id:
  - 497
categories:
  - PS4
tags:
  - 16-bit
  - 8-bit
  - Genesis
  - Hardware
  - Mega Drive
  - n64
  - NES
  - PS1
  - PS3
  - SNES
  - Theory

---
[<img class="alignleft size-medium wp-image-500" alt="ps4 controller" src="http://jumpnshoot9000.com/wp-content/uploads/2013/02/ps4-controller-300x182.jpg" width="300" height="182" />][1]Recent comments that game console software distribution is quickly becoming a media channel that is too archaic for reaching today&#8217;s gamers are somewhat misguided. Many high-profile websites like Eurogamer and Kotaku seem to be [lauding][2] the rough specifications of the new PS4 console as a sort of dramatic shift in the way console gaming has traditionally been conceived. They allege that by adopting a hardware architecture more in line with that of the PC, the PS4 will exhibit an openness as yet unseen in console gaming. Is this really true? [This article][3] from Gamasutra applies some healthy scepticism to Sony and Eurogamer&#8217;s optimism&#8211;what does an &#8216;open console&#8217; mean, and, perhaps importantly, what isn&#8217;t an open console?

## Confucius Say, Look To The Past

Wise old Confucius tells us to look to the past if we want to divine answers about the future, and by looking back at the console architectures of ages gone by, one can tell that he&#8217;s not far off the mark. It&#8217;s a commonly known fact that the most popular at successful game platforms of the last 40 years have usually always featured relatively open and accessible hardware architecture:

  1. <span style="line-height:16px;">Atari 2600: It may have only possessed 128 bytes of RAM, and lacked any kind of frame-buffer&#8211;not to mention Video RAM&#8211;but its CPU was a stripped down the MOS Technology 6502.</span>
  2. NES: While its PPU featured bit-mapped sprite indices (limited sprites per TV scan-line, limited sprite sizes, colours and transformation rules), which caused developers endless frustration late in its life-cycle, it&#8217;s CPU was, again, based on the MOS 6502&#8211;it was modified to incorporate a sound generator, and more O/I addresses.
  3. Commodore 64: Famously employed the MOS 6502 in its modified form, the 6510, which incorporated a general 8-bit O/I port into its design.
  4. TurboGrafx-16: Possessed a very intelligent three-chip architecture, which featured a CPU based on a modified 6502 design. Its CPU had an additional memory management unit, allowing it to address many times more memory than the original 6502, a parallel I/O port and a programmable sound generator. The brilliant thing about the TurboGrafx/PC Engine&#8217;s architecture was that its 16-bit Video Processor and accompanying Colour Encoder chip allowed the processing ability of its CPU to be maximised, allowing what was really a much cheaper console architecture to convincingly compete with its more modern rivals. 
    Starting to see a pattern emerging?</li> 
    
      * Super NES: Utilised a 16-bit CPU that was based on the architecture of the MOS 6502. Its instruction set (the list of digital input data required to make the processor do something) was a _superset_ of that of the 6502, meaning that it could emulate its operation more or less flawlessly. In designing one of the most famous and fondly-remembered game consoles of all time, Nintendo made the decision to base its architecture on a platform already well-understood.
      * Sega Mega Drive: Had its CPU based on the Motorola 68000, which was, for a time, very popular for its power and inexpensiveness. It was used in many famous computers such as the Apple II, the first Macintoshes and the Commodore Amiga. One of the stand-out features about the 68000 family of processors is that their design philosophy focused on _orthogonality_. This meant that its instruction set was as divided into two types of instructions as strictly as possible: operations and address modes. Ideally, all operations and address modes should be available and compatible with one another. Very simply, operations specified how to process/manipulate information, and address modes more or less specified where that information was. For a time during the 80s, it was uncertain whether the design architecture of the 68000 or the x86 (8086, 80286 &c) Intel IBM PC architecture would come to dominate the future design of computers. In comparison to the 68000 design philosophy, the x86 architecture was (and is) incredibly ugly and unintuitive.
      * TRS80, Sinclair ZX80/Spectrum, Sega Master System: These gaming platforms used the Zilog 80 CPU, which, along with the MOS 6502, dominated home computing in the 80s. The Commodore 128 used famously the Z80 alongside its 6502-derivative CPU so that it could attain CP/M (a widespread Operating System) compatibility. 
        Compare the CPUs used in the following post-fourth generation era consoles with those of the above.</li> 
        
          * Playstation 1: Used a MIPS Computer System&#8217;s R3000-family CPU, then a high-end graphics workstation processor. It was fairly well understood and documented in elite graphics-production circles, but did not have anywhere near as widely-spread commercial use as the above processors.
          * N64: Made of use of another member of a MIPS CPU family, the VR4300. Again, a very specialised processor.
          * PS2: The _Emotion Engine_; custom processor designed _for the PS2 alone_ by Sony and Toshiba. While it features a MIPS-compatible instruction set, the processor is actually eight separate processors that were designed to work in parallel. This design architecture was notoriously difficult to harness without special effort, in comparison to the Intel Pentium 3-based Xbox and IBM PowerPC-based GameCube.
          * PS3: Another highly customised CPU developed in conjunction by Sony with Toshiba, and this time IBM, the _Cell Broadband Engine_. It was another parallel-processing chip. As many commentators have said before, its potential has not been realised due to the increasing prevalence of multi-platform</ol> 
        
        While there are exceptions (barring the original Xbox, both Nintendo consoles and the latter Xbox being based on slightly more common, but still commercially obscure IBM PowerPC architecture) to the pattern constructed above, the decision by Sony to base the PS4 on x86 architecture actually presents a _return_ to basing a gaming console on a widely understood and utilised hardware architecture. In this vein, the comments that some media outlets have been making about the purportedly archaic console-concept of game content delivery is misguided because, as history shows, consoles originally echoed the design concepts of personal computing.
        
        Gaming in the 1980s was more-or-less exclusively powered by the MOS 6502, and to only a slightly smaller extent the Zilog 80. In the fifth generation we see something of a deviation from the use of common processor architecture in the form of MIPS CPUs. A qualification here is important&#8211;_both_ Nintendo and Sony used MIPS technology, so, in a sense, the CPU instruction sets that they were asking programmers to deal with was very similar between their two competing systems. However, if the fifth generation was to follow the trend of the first four generations of console gaming, they should have implemented x86-compatible architecture _then_!
        
        The release of the fifth generation of gaming consoles also coincides with the commercial rise of _Reduced Instruction Set Computing_ (RISC): the design philosophy that smaller CPU instructions lead to more efficient and powerful computer processing capabilities. If we use the implementation of RISC CPUs as our independent variable for the analysis of how gaming console processors have diverged from those most commonly used everywhere else (x86 architecture) we can conclude fairly decisively that game consoles have done nothing but very significantly specialised their hardware since the mid-to-late nineties, since the PowerPC architecture is indeed RISC.
        
        ## Yes, Indeed More Open
        
        Ignoring content delivery systems (Blu-ray discs, Steam-like online content delivery &c), based on a mere cursory glance at the Central Processing Units used in game consoles since the late seventies, the PS4 architecture, if indeed based on the Intel x86 design concept, actually does present a more open platform for development. Much like the jump from the more-or-less exclusive use of assembly language to the use of higher level programming (like C) from the fourth to the fifth generation of consoles, the use of an architecture more familiar to that of the PC will allow developers to access more resources (both in terms of capital and labour) at much cheaper costs, _ideally_ causing games to be more plentiful, and of better quality due to the ability of everyone being able to &#8216;talk the same language&#8217;. However this increased openness doesn&#8217;t actually present a challenge to console gaming as a tradition or a concept, because the dichotomy between console-versus-PC is actually only a relatively new event. It&#8217;s only really subsisted since the mid-to-late nineties.
        
        ## __Shovelware: Plato&#8217;s _Republic_
        
        This might present itself as a fairly obscure and convoluted way of making what is really a very simple argument, but in _The Republic_, Socrates outlines to his listeners that justice manifests itself in three different compartments in people&#8217;s &#8216;souls&#8217; (their personhood or psychology &c): a rational part, that pursues and lusts after truth, a &#8216;spirited&#8217; part that desires nothing but honour, and an appetitive soul-section that lusts after everything else: carnal desires, food and money. Socrates argues that in order for someone to be just, these three parts of someone&#8217;s personhood need to be in the correct proportion. The same could be argued to apply to the design of console hardware.
        
        If this strikes the reader as a fairly bizarre connection, I point them towards Egoraptor&#8217;s famous and influential (not in an academic sense, obviously) &#8216;Sequilitis&#8217; video about the [first and second NES Castlevania titles][4]. His argument is actually just a derivative of Plato&#8217;s argument in _The Republic_! The point trying to be made here is that by basing their console on x86 hardware, Sony risks exacerbating what their _Playstation_ _1_ and _2_ console libraries suffered from worst of all: poorly and cheaply developed games. While the cause of the production of all the terrible money-grubbing titles that flooded store shelves in the 90s and 2000s for the _Playstations_ was not due to the hardware design of those consoles, but due to their branding good will, Sony are actually risking the creation of a particularly efficient cause for the development of PS4 _shovelware_.
        
        While Plato&#8217;s argument about justice (in the mouth of Socrates) has fairly undemocratic consequences about politics, and correspondingly fairly elitist suggestions with respect to the artistic value of games (let alone anything: see the sections where Socrates discusses the &#8216;noble lie&#8217; on which his republic would be founded (n.b. Nintendo fanboyism), and his justification for state censorship), one should at least be partly persuaded by it when the plethora of mindless first-person shooter franchises that dominate our current gaming culture are brought to mind. More than that, if we construe Plato&#8217;s 3-part soul argument more favourably, we can acknowledge that too much appetite (shovelware, mindless sequels &c) is the antithesis of good artistic values, but also see that too much lusting after truth produces illusion, and the excessive pursuit of honour is oppressive and unnecessarily violent.
        
        While quite often success is based on something external to a planner&#8217;s purposive intention, let&#8217;s hope that this return to hardware convergence that the PS4 (and the new Xbox) seems to be making escapes excessive appetite in terms of aesthetics. Who knows, the PS4 might fail due to excessive honour, instead of appetite, like its predeccessor, and many other consoles before it (the _Saturn_, with its rushed redesign due to Sega&#8217;s ignorance of the rise of 3D graphics, and, in part, the _N64_&#8211;with Nintendo&#8217;s spate with Sony leading to their rejection of CD-ROMs as a game medium).

 [1]: http://jumpnshoot9000.com/wp-content/uploads/2013/02/ps4-controller.jpg
 [2]: http://www.eurogamer.net/articles/2013-02-22-ps4-pc-like-architecture-8gb-ram-delight-developers
 [3]: http://www.gamasutra.com/view/news/187093/QA_What_does_Sonys_most_open_console_promise_mean.php#.USgmzKVmiSo
 [4]: http://www.youtube.com/watch?v=Aip2aIt0ROM