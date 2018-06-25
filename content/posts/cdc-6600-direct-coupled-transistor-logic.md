---
title: "The CDC 6600's Direct Coupled Transistor Logic"
date: 2018-06-22T12:18:14+10:00
draft: false
---

## Introduction

Yann Guidon from [Hackday.oi](hackaday.io) asked me to do a write-up of the Direct Coupled Transistor Logic (DCTL) of the famous CDC 6600 computer. When it was released, and for some years, the CDC 6600 was one of the fastest and most powerful computers in the world. When we take a look at the logic family that it used, it will be obvious to see why:

+ It uses very few components, primarily transistors, with _no_ diodes
+ The transistors which perform the logic are driven _very hard_, to the point where the quality of the transistor fabrication actually matters a great deal
+ The logic levels are _dangerously_ close together (in the 6600's case "0" = 0.2V, and "1" = 1.2V).
+ The cacading and interlinked circuits must be carefully "tuned" input and output impedances MUST agree precisely, or the logic will not function due to noise or otherwise.

## The Basic Unit: The Inverter 

There are primarily two main articles available online which deal with the electronic description of DCTL logic. The first is the following:

J. E. Thornton, _Design of a Computer: The Control Data 6600_ (Scott, Foresman and Company, 1970), Illinois.

and 

James B. Angell, "Direct-Coupled Logic Circuitry" (1958) _Proceedings of the Western Joint Computer Conference: Contrasts in Computers_, 22-27.

This is not a great deal. On Bitsavers, there is no folder for the engineering documents of the 6600, as opposed to the 1406, and 3600-series CDC logic, which I also aim to cover because it is a very interesting high-speed DTL.

So bear in mind that the information I am presenting here is limited, and if you want to build your own DCTL circuits you are most likely going to have to design your own, because there are no complete design documents online for the 6600 which you would have been able to copy and modify.

Anyway here is the basic building block of DCTL:

The CDC 6600's inverter:

<img src="/6600_DCTL/DCTL_NPN_Inverter.jpg" width=50% >

The 1950s DCTL inverter:

<img src="/6600_DCTL/PNP_Inverters.jpg" width=50% >

By the time the 6600 was built, transistor fabrication had developed and improved markedly. In fact the first few pages of the chapter of the CDC-published book on the digital electronics of the 6600's DCTL go on about how the new silicon transistors they used in '69/'70 made the 6600 possible. So this explains why the 6600 uses NPNs, as opposed to the older implementation using PNPs.

As you can see, you would be forgiven for mistaking DCTL with Resistor-Transistor Logic (RTL) if you had only an inverter to look at. I agree with the speculation on the (tiny) Wikipedia article on DCTL that it evolved from RTL.

Obviously the thought process that lead to developing this logic family was "what if we had RTL but got rid of all the resistors?" The point of having resistors in RTL is to allow you to increase the voltage margins of the logic levels. It also allows you to better control the flow of current throughout the circuitry and match the impedances of the inputs and outputs.

The first problem you have with DCTL is -- how do you make sure you can switch transistors without driving them too far into saturation? The solution is to use transistors with special impedances and gain ratios.

Take a look at the special transistor characteristics that the conference proceeding document outlines:

<img src="/6600_DCTL/Tran_Characteristics.jpg" width=50% >

This is obviously based on an old understanding of exactly how well-designed transistors are, but you can see we're only switching very small amounts of current, and the V(BE) of the operation of the transistors when in saturation/conduction is far lower than your standard BC548/9 or 2N3904/6.

I haven't checked yet, but I believe transistors with these kinds of characteristics should be able to be obtained cheaply. The maximum switching time required in this specification from the 1950s is easily obtained with modern discrete transistors.

## DCTL Logic Levels

The logic levels of DCTL circuitry in the 6600 are very very close together. As you can see the V(BE) of the 6600 transistors closer resembles the operation of modern transistors.

<img src="/6600_DCTL/CDC6600_Logic_Levels.jpg" width=50% >

At this stage, I became very interested about how noise is dealt with in DCTL circuits, because the logic levels are nowhere near as far apart as 0-5V as in TTL.

Angell in the conference proceeding explains how it is possible to minimise noise in DCTL:

>Some kinds of noise are comparatively unimportant in DCTL whereas others are potentially severe. Because of the very low impedance level of "on" circuits, capacitive pickup is generally negligible. Power-supply fluctuations are usually unimportant, because voltage translation circuits are not required and the majority of a complete logical system can, if desired, be run from a single supply. On the other hand, because of the small voltage swings which are experienced in DCTL, inductive coupling in either multiconductor cable or via ground leads may be troublesome.

>It is generally felt that with germanium transistors a maximum induced noise or the order of 25 millivolts can be tolerated; this figure amounts to 10% of the normally encountered voltage swings.

The article then goes on to detail how it is possible to reduce noise. Please see the article for more.

## Matching Impedances

The whole gambit of designing DCTL circuits depends on making sure different logic elements have impedances which agree. Because of the low conducting collector-to-emitter voltages in DCTL,  the transistors involved in this logic family will have quite low gain. The game you play with you tangle with DCTL is attempting to have as much gain as possible to increase fan-out.

Generally speaking, fan-in will be much higher than fan-out in this logic family.

To take a look at the limits you come up against when designing DCTL circuits, consider the following interchange:

<img src="/6600_DCTL/DCTL_interchange.jpeg" width=50%>

This interchange is _n_ paralleled **OR** gates driving _m_ paralleled loads.

Angell explains that two conditions are necessary in order to make this interchange work:

1. When all the input gates are off (V( C)=0.2V), all the output loads must be on (V( C)=1.2V).
2. The conduction in any one of the **OR** gates must turn off all the output loads.

The first condition is fulfilled by the following inequality:

<img src="/6600_DCTL/DCTL_Fan_Eq1.jpg" width=50% >

The term on the left is the smallest possible load current. The term on the right is the leakage current in all of the gates in the interchange _plus_ the minimum required load. 

The second condition is satisfied by the following inequality:

<img src="/6600_DCTL/DCTL_Fan_Eq2.jpg" width=50% >

It means that the collector current of one conducting gate must be greater than the maximum possible current in the load resistor. Here, the node voltage is equal to the specific limit voltage required to maintain the load transistors in the nonconducting state.

So this gives you the limits within which you can match the impedance of the inputs and outputs of the interchange. This will help you determine the fan-in and fan-out, and set the load resistor value.

The important factors in this particular example, therefore, are:

1. The input impedance of a conducting transistor must not be too low. This problem can be solved by setting a maximum limit on the the **ON** base current for a particular base voltage. This way, no one output transistor will take too much of the available driving current.

2. The output impedance of the **OR** transistor network must not be too high. One method of solving _this_ problem is to make sure that the V(CE) of the input transistors is LESS than a certain limit for a given I( C) and V(BE). _Another_ method would be to limit the I( C) with respect to given V(BE) and V(CE). The absolute minimum limit for either of these conditions, the lowest V(CE) or lowest I( C) is determined by the minimum transistor gain. This minimum individual transistor gain will be much greater than the overall circuit gain. However, this individual transistor gain will be much _smaller_ than if the transistor were in the active or non-saturated region. So it is a careful balancing act of switching current from the collectors of input **OR** network into the bases of the output network.

3. The "off" collecor current of a non-conducting transistor must not be too large. This means the "off" I( C) must have a maximum limit compared to its "off", non-conducting base voltage (V(BE)).

All of this boils down to the following: In order to have compatible connections between DCTL logical elements, V(CE) "on" [Logical "0"] =< V(BE) "off" [Logical "1"] for any particular logical element. Angell explains that it is permissible to sacrifice gain in some instances in order to reduce the V(CE) of a given logic element.

Combining the two inequalities above when considering the above interchange, you can solve for the gain of an individual transistor in conduction. This produces the following inequality:

<img src="/6600_DCTL/DCTL_Fan_Eq3.jpg" width=50% >

As Angell explains, the result shows that the input transistor gain must be greater than the (a) circuit gain; multiplied by (b) _m_, the number of output loads; and ( c) factors accounting for the tolerances of the components.

You can derive a rule of thumb to follow if the networks of logic elements is too great:

I( C) "on" / I(B) "on" [Logical "0"] > 2_m_

So the gain of a saturated transistor must be greater than twice the number of output loads.

### CDC 6600 Rules of Thumb

The general rules CDC outlines for 6600 DCTL is:

+ One transistor collector can drive five bases _within a module_
+ One collector can drive two _local_ bases within a module and two bases _by back-panel twisted par on one other module_
+ Six collectors can be connected _within a module_

## Selected Common Logic Elements

There is therefore a lot of work required to match logic element input and output impedances. **But**, the advantage to all this work is that DCTL logic elements are actually very simple.

Consider the following 6600 NPN and 1950s PNP basic logic elements:

<img src="/6600_DCTL/CDC6600_AND_OR.jpg" width=50% >

<img src="/6600_DCTL/CDC660_Flip_Flop.jpg" width=50% >

<img src="/6600_DCTL/PNP_OR_AND_FlipFlop.jpg" width=50% >

After matching all of the impedances of logic elements, you are rewarded with _very_ simple circuitry.

<img src="/6600_DCTL/PNP_HalfAdder.jpg" width=50% >

<img src="/6600_DCTL/PNP_OneShot.jpg" width=50% >

## Switching Times

One can assume that this circuitry switches and propagates faster than the famous and standard hobbyist DTL. I do not have exact measurements, however the CDC documentation assumes the propagation delay of an inverter is 5 nanoseconds.

## Conclusion

Although fairly fiddly, this seems like an interesting logic family.

I will cover CDC's 1604 and 3600 DTL logic in the next write-up.
