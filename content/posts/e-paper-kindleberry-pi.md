---
title: "An e-Paper Screen Portable Terminal: The Kindleberry Pi"
date: 2018-05-16T09:32:18Z
draft: false
---
I have been putting some effort into 
developing a portable device that I can 
use to replace my phone. My smart phone 
has many poor features:

1. Poor battery life.
2. Awful touch screen 'soft' keyboard
3. Full of 'Google Services' CPU 
processes that the operating 
system requires to function.
4. Poor cell data reception.
5. Weak construction that is difficult to 
repair: I dropped it, and the glass 
screen smashed. The audio jack has also 
now failed, making it useless for 
listening to music.
6. Illogical file system structure.

The phone does have some benefits - 

1. Its ability to act as a USB gateway 
makes it useful for internet in remote locations.
2. It does possess a terminal emulator, 
making it great for interfacing with my 
VPS.
3. The GPS module is very convenient for 
getting around new places.
4. The front-facing camera is great for 
making vlogs because you get a live 
preview of the footage being filmed.

Overall, the issues of poor text input 
and lack of ability to hack the device 
push me towards finding a solution for 
portable computing. I also want to 
start using less HTTP and more of other 
protocols for my communication.

I believe there is a command line 
mastodon client, NNTP is a convenient 
text based communication protocol, and 
email has long used the command line.

# The Kindleberry Pi

The Kindleberry Pi presents itself as an 
excellent candidate for replacing my 
phone. It is the combination of a 
Raspberry Pi ssh'ed into a jailbroken 
Amazon kindle. The combination of two low 
power computers and an e-paper screen 
makes for a device which is excellent on 
power performance.

The Raspberry Pi is also compatible with 
GPS modules, and one can combine the 
Kindleberry with a cell data router in 
order to allow you to use the net in 
public. As you can see below, the cell 
data router can be used to connect the 
Raspberry Pi and the Kindle together for 
the SSH session as well.

## The Three Previous Kindleberry Builds

Here are the three previous separate 
attempts at the Kindleberry:

The [First version](http://ponnuki.net/2012/09/kindleberry-pi/)

<img src="/kindleberry/kindle_berry_pi.jpg" width=25%>

[Second version, a wireless version](https://maxogden.com/kindleberry-wireless.html)

<img src="/kindleberry/kindle-table.png" width=25%>

[Third version, using the Zero W Raspberry Pi model](http://blog.yarm.is/kindleberry-pi-zero-w.html)

<img src="/kindleberry/KindleberryPiZeroW.jpg" width=25%>

## The Cigar Box and the Mechanical Keyboard

I will build the Kindleberry with a 40% 
mechanical keyboard. 40% sized keyboards 
are roughly 3 inches long, and this suits 
the combined length of the cigar box I 
will be fitting the entire project into. 

The cigar box I have is 292mm wide, and 
189mm long, across the lid. Any longer 
and wider out, and the components would 
be cutting into the housing of the box.

I will use a Kindle 3, AKA a Kindle 
Keyboard, because it is easy to 
jailbreak, and it has a 6 inch screen. 
That makes for a 120mm wide screen. The 
length, however, is 96mm. A 3 inch long 
mechanical keyboard is approximately 
76.2mm long, so these two major 
components will definitely fit into this 
housing.

I want to have passthrough charging for 
this device, so I will find a board from 
Adafruit or somewhere which will allow 
this.
