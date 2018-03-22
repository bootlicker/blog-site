---
title: Command Line Interface Phone
author: bootlicker
type: post
date: 2018-02-20T04:48:34+00:00
url: /2018/02/20/command-line-interface-phone/
tags:
  - Uncategorised

---
Here is a project I want to work on. I recently got some birthday money, so I think this is possible!

# **Motivation**

Here&#8217;s my idea:

A Command Line Interface phone. After graduating from Ubuntu Linux to Gentoo and Arch, I have really come to enjoy the greater control and transparency a &#8220;proper&#8221; linux distribution allows you. Self-enabling services, writing your own configuration files, understanding exactly what daemons on your system do what &#8212; it&#8217;s a much more comforting feeling to actually understand how your OS works and exactly what it is doing.

So far I suppose I have discussed desktop computers, but the situation is worse with mobile phones. You have to root your phone now in order to get full control over it &#8212; and that voids the warranty, so you can no longer get it repaired by the vendor.

Furthermore the language that describes how you are using your phone is terrible. Everything is an &#8220;app&#8221;.

I want to design and build a completely software transparent mobile phone. The user will have full software control over the phone.

# Project Details

Some details of this project are fairly straight forward &#8211;

  * I will use a cheap TFT display, probably from a car reversing camera screen. I may use a digital signal, but I feel like a composite video signal will do until i settle on the actual hardware I will be using
  * I will use a second hand Xbox 360 chat pad for the keyboard interface because it is reasonably small, and some other hackers have made it possible to [reprogram it to output serial terminal data][1].

The main problem I am having is finding a suitable processor platform around which to structure the entire project. **If you are reading this and you have any suggestions, I would love to hear them**.

What I want this CLI Phone to be able to do is:

  * Send SMS
  * Browse and interact on the Web

I feel that using 3G Mobile Data would be sufficient to achieve this. So I need a Cell Data breakout board or chip to interface with a microprocessor or microcontroller.

## I     The Quick and Dirty Solution

A very simple hardware solution to this project would be:

  * A Raspberry Pi Nano
  * A cheap 3G USB Cell Data dongle

I could set up Raspian Linux to boot up to a command line, and if I selected the Cell Data Dongle correctly, I could get a good kernel module to enable it to work with the linux install. Browsing the web would be as simple as using w3m or elinks or lynx. You could even use a CLI mail client like mutt. Mouse support could even be implemented using a hacked analogue stick or the like.

## II     Something More Elegant?

I feel like the Raspberry Pi Nano solution is too quick and dirty. Using a full-blown small Single Board Computer seems like overkill, even though it is very cheap. These projects came to my attention, and I feel like they illustrate a more parsimonious and less wasteful solution to the goal of the project:

  * Ben Heck&#8217;s Mobile PIC-based 80s BASIC Computer ([Link][2])
  * The PIP Arduino Web Browser ([Link][3])
  * The Contiki Operating System, TCP/IP Stack and Web Browser ([Link][4]) 
      * I thought this OS only ran on the 6502! Apparently it runs on a whole host of microcontrollers! This might be the way to go!
  * A few web browsers for the Commodore 64 
      * HyperLink 2.5e ([Link][5])

  * Hardware such as the Lantronix USD1100 which converts ethernet to RS232 etc serial communication ([Link][6])
  * uClinux, linux for microcontrollers ([Link][7])
  * Porting uClinux to an m68k ([Link][7])
  * m68 Katy &#8211; an implementation of uClinux on a Motorola 68k ([Link][8])

The main issue with selecting a lower power (both in terms of computing power and electrical power) processor is getting enough RAM in order to run a web browser. Sending SMS is not difficult at all, because a GSM/Cell Data chip can be addressed to send SMS via serial terminal AT commands.

My current issue is &#8211; can I find a microcontroller, or an embedded microprocessor with enough RAM to run a web browser than can SUBMIT as well as RECEIVE data. A software solution that can actually run linux would be ideal because it would allow greater portability and extensibility. We could port or modify GNU software tools to run on an embedded linux distribution like uClinux.

 [1]: https://forum.arduino.cc/index.php?topic=58463.0
 [2]: https://www.youtube.com/watch?v=Hjdj14C_jAI
 [3]: https://hackaday.io/project/3116-pip-arduino-web-browser
 [4]: http://contiki-os.org/
 [5]: http://www.armory.com/~spectre/cwi/hl/
 [6]: https://www.lantronix.com/products/uds1100-uds1100-poe/
 [7]: http://www.uclinux.org/
 [8]: https://www.bigmessowires.com/2014/11/17/68-katy-68000-linux-on-a-solderless-breadboard/
