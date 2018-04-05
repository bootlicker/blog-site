---
title: "Guerrilla Game: I Decided To Go With The Blank Frame Method"
date: 2018-04-03T18:12:35+10:00
draft: false
---

Okay!

Remember the git repository is here:

[https://github.com/bootlicker/guerrilla-game](https://github.com/bootlicker/guerrilla-game)

After looking through the different options for finding enough time to calculate a 16-bit LFSR on the Atari 2600, I decided to go with Thomas Jentzsch's suggestion of a _synchronised_ blank frame every screen transition. This affords me 192 * 76 ~= 15 000 cycles extra on top of Vertical Blank and Overscan.

I have now:

1. Walking off the side of one screen and entering in on another
2. Updating the map coordinates (I may make a mini-map)
3. Created the structure for the code to swap out the kernel and draw the blank frame
4. Updated the placeholder graphics to include 2 digits - the kernel will draw $00 to $40, as there are 64 unique objects in the overworld

I still have to:

- Create the logic to switch out the kernel and draw a blank frame on screen-change
- Link the random number generator to the Environment Graphics pointers

Then the scaffolding of the randomly generated overworld will be finished, really. A demo should be available after these things have been achieved.
