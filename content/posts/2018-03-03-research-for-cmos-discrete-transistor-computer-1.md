---
title: 'Research for CMOS Discrete Transistor Computer #1'
author: bootlicker
type: post
date: 2018-03-03T01:56:11+00:00
url: /2018/03/03/research-for-cmos-discrete-transistor-computer-1/
tags:
  - Uncategorised

---
So CMOS stands for circuits with Complementary Metal Oxide Silicon construction. This contrasts with NMOS and PMOS circuits. CMOS circuits use both PMOS and NMOS MOSFET transistors.

CMOS circuits are able to have quite a large portion of their circuits non-conducting, due to their use of both NMOS and PMOS transistors.

I have chosen to build this discrete transistor computer using a CMOS design. This is because there is much more documentation of CMOS logic than Diode-Transistor logic. My last two attempts at building a discrete transistor computer used DTL, and it was frustrating to find information on how best to construct DTL designs.

It may be that DTL is cheaper. In which case I will ditch CMOS and go back to DTL. I will look at the plans of the PDP-8 and PDP-11 to understand their DTL design.

Anyway, the first issue you have with making a CMOS computer is to make sure you can actually turn on your transistors. I have chosen 5V as my logic level, which means we have to make sure the Drain Current [_I(d)_] is quite large when the Gate-to-Source voltage is HIGH.

We need to make sure the MOSFET is as close to saturation (full conduction between Source and Drain) as possible.

Transistors can be in three modes. Cutoff, Linear Region, and Saturation. If you want to use a transistor as an amplifier, you will use it in the LINEAR region, the region best for analogue circuits &#8211; the Drain current I(d) will vary linearly with the voltage of the gate.

The equations for this are:
  
<span style="color: rgb(34,34,34); font-family:" typoninesansregular18="typoninesansregular18" \_="text-align:\_" \_14.6994px="\_14.6994px" normal="normal" \_400="\_400" \_0px="\_0px" none="none" \_2="\_2" rgb245245245="rgb245245245" initial="initial" inlineimportant="inlineimportant" left="left">V(gs) > V(th); and</span>

V(ds) < (Vgs-Vth).

So the Gate voltage must be higher than the threshold voltage, and the amount of volts the Gate is above the Threshold must be higher than the Drain-to-Source voltage.

This tells us how to turn a transistor ON, how to get it out of the cutoff region.

What it doesn&#8217;t tell us is how to completely _saturate_ a transistor. We want to either turn off (cutoff) or turn on (saturate) the transistor. This will correspond to the binary logic states of 0 and 1.

The fastest way to find out how to saturate a MOSFET is to look at its _transfer function_ in its datasheet. The property to look for is to see _how much more current the MOSFET will conduct through the Drain as the Gate voltage increases._

If the graph of the Drain current looks flat in the region of 5V, it is no longer in the linear mode of operation at that Gate voltage.

Here is a list of the cheapest and most suitable logic level MOSFETS I can find:

<img class="alignnone wp-image-387 size-medium" src="/wordpress-uploads/2018/03/Screenshot_20180303-002532.jpg" width="522" height="522"  />

At V(gs) = 5V, this MOSFET is just at the end of the linear region. _May_ be suitable.

<img class="alignnone wp-image-383 size-medium" src="/wordpress-uploads/2018/03/Screenshot_20180303-000413.jpg" width="539" height="539"  />

5V V(gs) will see this transistor conducting more than 100A &#8211; it may even be harmful to the transistor &#8211; check the Max V(gs).

Just checked the datasheet. The max V(gs) ia 15V. This transistor is probably very suitable.

<img class="alignnone wp-image-385 size-medium" src="/wordpress-uploads/2018/03/Screenshot_20180302-181535.jpg" width="540" height="540" />

This is actually the HUFA76429D3. Same as above. The max V(gs) is 16V. This may be a very suitable component.

<img class="wp-image-384 alignnone size-medium" src="/wordpress-uploads/2018/03/Screenshot_20180302-173617.jpg" width="540" height="540" />

This transistor will have a drain current of more than 10A at V(gs) 5V, even though it won&#8217;t be fully saturated. This component may be suitable.

<img class="alignnone wp-image-388 size-medium" src="/wordpress-uploads/2018/03/Screenshot_20180302-174523.jpg" width="540" height="540" />

The 640N still has 5V V(gs) in the end of the linear region, but it will still be conducting more than an ampere at this stage, so it _may_ be suitable.

<img class="alignnone wp-image-390 size-medium" src="/wordpress-uploads/2018/03/Screenshot_20180303-003725-1.jpg" width="540" height="540"  />

5V is well and truly in the satutation region of this MOSFET, the 3710. The Drain current will not be increasing much more with any more Gate voltage. Bear in mind the logarithmic scale.
