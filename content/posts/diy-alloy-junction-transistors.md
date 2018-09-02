---
title: "DIY Alloy Junction Transistors"
date: 2018-09-03T03:05:18+10:00
draft: false
---

# Part 0 - The Rationale for Early 1950s Transistors

Before you ask, "Why make your own transistors at home??" -- read my [Manfiesto for Why](https://bootlicker.party/posts/manifesto-for-communist-technology-use/).

## Not Just MOSFETs!

Most of the homebrew community has been focused on fabricating Field Effect Transistors (FETs) at home. Sam Zeloof and Jeri Ellsworth are probably wiser to try and 'etch FETs' because they are much better suited to fabricating Integrated Circuits (ICs). ICs were a real revolution in electronics because they miniaturised sometimes enormous circuits into small, convenient packages. Discrete circuits also do not last as long as integrated circuits, because it is expensive to render them mechanically inert. ICs can be completely encased in plastic, shielding their components from dust, and heat, and other kinds of physical mechanical interference.

_But_, from studying the work of Ellsworth and Zeloof, and following up on their references, it seems that manufacturing the kind of transistors they have, in the ways they have, may still be too expensive and difficult for hackers. So in this article I am going to argue that _one option_ for hackers is to fabricate not _silicon, planar process FETs_, but _germanium, alloy-junction, Bipolar Junction Transistors_.

Alloy-junction BJTs are a much older and more primitive type of transistor to fabricate than the planar process transistors that Ellsworth and Zeloof talk about, but I will argue that alloy-junction transistors present themselves as an attractive option for hackers who cannot afford expensive equipment and materials, and who have to push most of the cost of hacking onto using their own labour in order to get things done.

## Why Choose Alloy-Junction Transistors

Alloy-junction transistors are not _the earliest_ and most primitive kinds of transistors, but they are one of the earliest and most primitive. These kinds of transistors are **necessarily discrete** transistors. I argue they present themselves as an attractive kind of transistor to fabricate at home in a DIY, homebrew setting because:

- Their die-size is much larger than your average planar transistor, which means they are far better suited to making in small batches, by hand, one-at-a-time. [This Wikipedia Reference](http://www.thevalvepage.com/trans/manufac/manufac1.htm) explains that the 600mW Mullard OC81 transistor wafer size is 2.4mm x 2.44mm. OC44 and OC45 transistors have a circular wafer size of 1.45mm diameter. The actual transistor die is created by melting pellets of indium or antimony into the very thin germanium wafer. The pellets are relatively simple to make, conceptually. The pellets are also quite large -- they are visible individually to the naked eye. See the following image below:

<img src="/alloy-junction-transistors/indium-pellets.jpg">

- The temperatures of furnaces required for fabrication are much, much lower, in the order of hundreds of degrees Celsius, and not thousands.
- The techniques of transistor fabrication are much more primitive, and are therefore much more suited to beginners, and require the knowledge of far less complex chemistry.
- Most of their materials seem inexpensive to gather (germanium, indium, antimony).
- Most of the materials for the fabrication of these transistors seem relatively safe to be exposed to in reasonable amounts, with some notable exceptions, like indium. But even indium is a lot safer than the etching fluid Sam Zeloof recommends-- Hydrofluoric acid, HF.
- The process of their fabrication does not require photo-lithography. So, making these transistors does not require expensive projection equipment to be fabricated at ''small'' sizes, and does not require **complex proprietary materials** in order to etch.

# Part 1 - The Actual Manufacture of Alloy-Junction Transistors

Now, I will describe the rough process of how to fabricate this primitive type of transistor.

## The Creation of Monocrystalline Wafers

First, a wafer of germanium make of a single crystal is formed. This can be done yourself with great amounts of heat, or more conveniently, and be obtained online. This is not the most important process to consider when making these transistors.

## Dicing

Dice your germanium wafers into wafers required to manufacture the base of the transistors.

The wafer of germanium forms the alloy-junction in this way. It is sandwiched between two melted pellets of semiconductor alloy:

<img src="/alloy-junction-transistors/diagram-of-transistor.gif">

The [Wikipedia reference](http://www.thevalvepage.com/trans/manufac/manufac1.htm) mentioned above suggests that an ''ultrasonic drill'' can satisfactorily dice germanium wafers into the right size.

## Etching

The wafers of germanium then need to be ''etched'' into the correct thickness in order to satisfy the operating conditions of the transistor. This is not photo-lithographic ''etching'', it is the chemical erosion of the diced germanium wafer into a much smaller thickness than previous.

## Pellets

Pellets of indium or antinomy need to be fabricated in order to dope the ''etched'' germanium wafer which is intended to be the base of the transistor. These pellets of semiconductive precious metals form the collector and emitters of the transistor.

The [Wikipedia reference](http://www.thevalvepage.com/trans/manufac/manufac1.htm) above describes the process of forming the small pellets of metal:

> Indium wire or strip is cut into portions containing the amount of material required for the pellets. The pellet which forms the Collector is three to five times the size of the one used for the emitter, according to the type of transistor.

> The process for shaping or 'balling up' the pellets bears some resemblance to that used for making lead shot. The pieces of indium are dropped down a glass tube about three feet high and filled with liquid. At the top the liquid is sufficiently hot to melt the pieces of indium into droplets. Further down the liquid is cooler and the drops of indium solidify into spherical pellets.

## Alloying

Using a jig, you then alloy to the wafer of germanium first the emitter of the transistor, and then the collector. This is the part of the fabrication that requires a furnace that can reach a high temperature.

The temperature of the furnace is much lower than that required for the fabrication of planar process FETs, and the actual stages of heating are also much simpler. The _chemistry_ of the alloying process is also less mission-critical than the chemical process of FET construction.

The furnace temperature is _below_ the melting point of germanium, but _above_ the melting point of the semiconductor alloy -- so below 650 degrees Celsius.

# Part 2 - Conclusion

I will not discuss the soldering of lead connections to the finished germanium transistor, because they're not different from any other transistor fabrication process -- either Zeloof's or Ellsworth's. _But_, these transistors are much larger and easier to solder than the ICs of Zeloof etc.

Anyway that's it!
