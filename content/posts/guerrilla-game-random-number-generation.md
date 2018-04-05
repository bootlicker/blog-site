---
title: "Guerrilla Game Random Number Generation"
date: 2018-04-01T15:18:27+10:00
draft: false
---

OKAY.

First of all, in between finishing Phase Two of the game development and starting this new phase, I learned how to use git properly, so you can find the repository of the source code for this game here:

[https://github.com/bootlicker/guerrilla-game](https://github.com/bootlicker/guerrilla-game)
 
I was able to begin the work on the randomly generated overworld map today, instead of Tuesday. I think tomorrow will be busy, and I will be able to return to work on this on Tuesday.
 
# 16-bit Linear Feedback Shift Registers
 
This person's blog series contains a useful rundown of exactly how a polynomial counter (a Linear Feedback Shift Register) works to create a one-dimensional sequence of pseudo-random numbers.

I opted for a 16-bit LFSR because I thought I had the RAM left over to do so. I was initially very excited to try and build a large world based on the two bytes of RAM, which would afford 65000+ screens of randomly generated content. I imagined I could generate a 256 screen x 256 screen square world.

I figured out that masking off 6 bits of the 16 bit number output of the LFSR would allow me to create 64 Choose 4 Combinations of unique screens across 65k+ screens. This would guarantee that virtually every screen on a 256x256 world would be a unique screen. A combination is the measure of the number of possible sets of some finite number of different objects that can be made from a smaller selection of that superset. A combination is different from a permutation because it doesn't care about the order of the smaller set of unique items. The fact that one of the superset's items appear at all makes a unique combination. If some other ordering of the same set of objects appears, combinatorial counting does not count that set again.

The main problem is, 256 horizontal screens is too large a number of screens to calculate in order one at a time.

This standard/famous code from batari takes at most 20 cycles to execute:

```
        lda Rand8   ; 3  3
        lsr         ; 2  5
        rol Rand16  ; 5 10
        bcc noeor   ; 2 12
        eor #$D4    ; 2 14
.noeor              ;
        sta Rand8   ; 3 17
        eor Rand16  ; 3 20
```

There are 37 x 76 cycles in Vertical Blank, and there are 30 x 76 cycles in Overscan, which means if I dedicated ALL the cycles in Overscan, which is currently empty for me right now, I would only be able to calculate at most 114 loops of the above.

So there is clearly a computational limit to calculating new rows of content in this pseduo-two-dimesional method.

I have done some brief research on two-dimensional LFSRs. This is the structure of the usual 2D LFSR:

![2 Dimensional Linear Feedback Register](/guerrilla-game-figures/2D-LFSR.png)

The CN network on the left are registers of identical length with different XOR taps. These different registers are then selected to output into a small array of registers of identical length. The control unit then chooses which output register to mux with which input register. N is the bit length of the registers, and M is the number of parallel registers. One register at a time is looped back around into the CN network, and one register at a time is outputted from the CN network.

This confirms my suspicion - I think in order to reduce the amount of cycles required to compute some non-single iteration of the LFSR, a large amount of RAM would be needed.

As I am writing this, I'm wondering if it isn't possible somehow to "buffer" the surrounding screens of the current screen the player might be inhabiting. Calculating the left and right screen only requires one iteration of the feedback register. I wonder if there's a mathematical trick to reduce the amount of cycles required to go through in order to calculate a new Y-index of the overworld, instead of a new X-index. Perhaps a lookup table? A lookup table could perhaps be used to do multiple loops through the feedback register, just a row up and a row down. It might be possible to do some algebra and find out what XOR $D4 to XOR $D4 to XOR $D4 to an unknown number is...

Otherwise every movement up or down a Y-index is a full-row's worth of screens' calculations...

There has got to be a faster way... Feel free to jump in and give your two cents!

---

On the other hand, one could remove the STA and LDA functions and speed the routine up quite a bit... You know, just have EOR $D4
