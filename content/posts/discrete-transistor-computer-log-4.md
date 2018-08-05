---
title: "Transistor Computer Log #4 - Actual Good Flip-Flops"
date: 2018-08-04T03:31:24+10:00
draft: false
---

<p>I received some constructive criticism about the Flip-Flops I am using the construct the various elements of the RAVEN. I think a lot of the apprehension other hackers have about the R201 DEC Flip-Flop I am using is because it contains a great number of circuit elements -- if these circuit elements were in a large part <em>active</em> during Flip-Flop operation, then obviously the R201 would be very slow.</p>

<p>In this log I'd like to clean up and and explain exactly how the main Flip-Flops in the RAVEN will function. I do not believe these DTL Flip-Flops I have lifted from DEC R-Series Logic are slow, and will result in less than 1 MHz performance.</p>

<h1>The Most Basic Element of R-Series DTL Logic</h1>

<p>The most basic circuit element of any electronic digital logic is the inverter. This is the basic inverter of the DTL logic that the RAVEN uses:</p>

<p><img src="https://bootlicker.party/raven-discrete-computer/log-4/r-series-inverter.png"></p>

<p>A couple of examples can be provided which show the actual way this inverter is implemented in R-Series Flip-Chips:</p>

<h2>The R113 Diode Gate</h2>

<figure><img src="https://bootlicker.party/raven-discrete-computer/log-4/inverter-gate-113.png" width=80%></figure>

<h2>The R121 NAND Gate</h2>

<p><img src="https://bootlicker.party/raven-discrete-computer/log-4/inverter-gate-121.png" width=80%></p>

<p>R-Series digital logic specifies -3V as logical ONE, and 0V/Ground as logical ZERO.</p>

<h1>Inverter Simulation</h1>

[Inverter Simulation YouTube Video](https://www.youtube.com/embed/Dzy130OhlYY)

<p>Conventional current flows up through the emitter of the transistor, and out through the collector. Depending on whether there is 0V/ZERO or -3V/ONE at the INPUT terminal determines whether current will flow out through the base of the transistor and cause it to saturate.</p>

<p>-3V/ONE at the INPUT terminal will reverse bias the INPUT terminal diode, and open up a path for current through the transistor base up through the -15V terminal past the steering diodes. The transistor will then conduct, and the voltage at the output terminal will be 0V/ZERO, effecting an inversion.</p>

<p>0V/ZERO at the input terminal will cause the INPUT terminal diode to become <em>forward biased</em>, making the current path through the transistor base a path of much higher resistance. A small amount of current still leaks through the base through to the -15V terminal near the INPUT, but it is not enough to turn the transistor on. The transistor <em>stops</em> conducting and the voltage at the output terminal is therefore -3V.</p>

<h1>R-Series Logic Flip-Flops</h1>

<p>The simplest Flip-Flop of the RAVEN is two Inverters complementarily connected together like so:</p>

<img src="https://bootlicker.party/raven-discrete-computer/log-4/flip-flop-basic.png" width=80%>

<p>As you can see, this is the heart of the R201 Flip-Chip:</p>

<img src="https://bootlicker.party/raven-discrete-computer/log-4/flip-flop-201.png" width=80%>

<p>What, then, is the rest of the circuitry in this schematic?</p>

<h1>Diode-Capacitor-Diode Gates</h1>

<p>The answer is that the extra circuitry is 'Diode-Capacitor-Diode' gates. This circuit element is a very innovative and useful solution for both (a) edge-triggering; and (b) constructing JK and D Flip-Flops is as little circuitry as possible.</p>

<p>This is the basic DCD gate:</p>

<img src="https://bootlicker.party/raven-discrete-computer/log-4/dcd-gate-basic.png">

<p>The basic principle behind this circuit is that the capacitor charges and remains charged so long as the PULSE INPUT is held at -3V, and the LEVEL INPUT is held at 0V.</p>

<p>When the LEVEL INPUT equals 0V, and the positive edge of a PULSE INPUT signal changes from -3V to 0V, a positive voltage is generated at the output, which serves as a trigger for a Flip-Flop.</p>

<p>When LEVEL INPUT = -3V and PULSE INPUT changes from -3V to 0V, no such positive pulse is produced.</p>

<p>See the following simulation:</p>

[DCD Gate Simulation YouTube Link](https://www.youtube.com/embed/j7gl-JNBt8g)

<h1>Creating D and JK Flip-Flops</h1>

<p>The process of creating complex, clocked, edge-triggered Flip-Flops is as simple as preparing the inputs to Flip-Flops attached to DCD gates. The following two schematics are isomorphic/identical in meaning:</p>

<img src="https://bootlicker.party/raven-discrete-computer/log-4/flip-flop-plus-dcd-gate.png">

<img src="https://bootlicker.party/raven-discrete-computer/log-4/flip-flop-dcd-gate-schematic.png">

<p>A JK Flip-Flop can be constructed by simply sending identical pulse inputs to a DCD-gated Flip-Flop:</p>

<img src="https://bootlicker.party/raven-discrete-computer/log-4/complementing-flip-flop.png">

<p>So long as the LEVEL INPUTS are tied to ground, identical PULSE INPUTS will cause a Flip-Flop to complement.</p>

<p>This simulation demonstrates a JK Flip-Flop constructed from a DCD-gated Flip-Flop:</p>

[DCD-Gated Flip-Flop Simulation YouTube Link](https://www.youtube.com/embed/96dTc_yumO4)

<p>This serves as the basis for this Up-Down Binary Counter Register:</p>

<img src="https://bootlicker.party/raven-discrete-computer/log-4/up-down-counter.png">

<p>Binary counting is therefore achieved with the minimum number of circuit elements, as well as minimum number of transistors!</p>

<p>The exciting thing about DCD gates is that they allow <em>logical isolation</em> - meaning one does not need to resort to using Master-Slave Flip-Flops in order to clock some Flip-Flop element. Logical isolation from input and output is <em>achieved</em> by DCD gates, which allows the component count to be reduced dramatically.</p>
