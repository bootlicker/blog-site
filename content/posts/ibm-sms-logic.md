---
title: "The Electronics of IBM Standard Modular System Logic"
date: 2018-03-27T15:21:58+11:00
draft: false
---
# Introduction

Okay! We've had a look at the Diode-Transistor Logic of the DEC R-Series Logic, but that isn't the only electronic logic system that was employed in building discrete discrete component computers. As I explained in the post on R-Series logic, back in 2013 it was [some IBM computer](https://bootlicker.party/posts/r-series-logic/) which implemented an exotic electronic logic system which lead me to go down the "popular" DTL path. I will continue my investigation into different logic systems in this post with the IBM Standard Modular System (SMS) logic. IBM SMS logic doesn't just implement specific _systems_ of logic families, but also _whole different logic families!_ The IBM SMS uses what is now known as Emitter-Coupled Logic (ECL), as well at Resistor-Transistor (RTL) logic and DTL. ECL is a very difficult logic family, and RTL is unpopular in hacker circles, so we will look at the IBM SMS DTL logic implementation first, and then just look at their ECL circuits. The Don Lancaster _RTL Cookbook_ is sufficient really for people who wish to build discrete component RTL computers.

# IBM Standard Modular System Diode-Transistor Logic

I have obtained the electronic description of the different IBM logic implementations from the IBM _Transistor Component Circuits_ volume of the *Customer Engineering Manual of Instruction*. You can find this manual easily by searching the above words on the internet. There are also manuals describing the exact electronic schematics of the flip-chip cards used in IBM mainframes such as the 7070 and the 7090. They're worth a look if you want some inspiration for solving a particular concrete problem.

## Logic Levels

The SMS DTL system uses *four* different logic levels. They are divided into two fundamental kinds, "T" line levels and "U" line levels.

![The IBM SMS DTL Logic Levels](/IBM_SMS_images/001_SMS_DTL_Logic_Levels.png)

As you can see, positive T levels swing from -0.7V to 6.0V, whereas negative T levels swing from 1.4V to -6.0V. Positive U levels go from 0V to -7.4V, and negative U levels move from -5.3V to -12V. There are schematics in the _Transistor Component Circuits_ manual for how to convert T and U lines to each other. They're not worth mentioning here because we don't need to get into that much detail.

## The Fundamental Gates

Below you can find the schematic for the fundamental positive-logic NAND gate, or negative-logic NOR gate. IBM doesn't use the standard terminology for these gates, probably because the manuals for this system were written in the late-50s early-60s, before the terminology settled to what we know today. You'll also notice that the symbols for transistors here are also non-standard by contemporary wisdom. The same reason should apply here. We won't concern ourselves here with the physical electronic characteristics of the transistors and the diodes. I'll put some work into that later.

![The IBM SMS DTL Basic Gates](/IBM_SMS_images/002_SMS_DTL_Pos_NAND_Neg_OR.png)

There are three gates specified here. As you can see:

1. It is possible to interface the output of a DTL gate into ECL gates.
2. The first gate (at the top) takes a +U logic level and outputs a -T logic level.
3. The second gate (Gate "A") takes a +U input and outputs a +T logic level.
4. The third gate (Gate "B") is similar to the first one: it recieves a +U level, and outputs a -T level, as well as being able to interface with ECL gates.

It is possible to take T-line inputs and output U-line logic:

![The IBM SMS DTL U-line Output](/IBM_SMS_images/003_SMS_DTL_Neg_NAND_Pos_NOR.png)

These gates can drive ECL gates as well! Note well that the T-line inputs for the above gates are NEGATIVE T line levels (-T levels).

There are other inverters specified in this manual, such as "Power Inverters", which drive bigger loads and have bigger gate fan-outs. You can peruse the manual to look at those at your leisure.

There are also emitter-follower gates, which amplify the current of signals. There are also circuits for driving indicators connected to T and U line signals.

## Basic Flip-Flops

Below you can find the schematic for a basic IBM SMS flip-flop:

![IBM SMS Flip-Flop](/IBM_SMS_images/004_SMS_DTL_Basic_Flip_Flop.png)

This complex flip-flop can be set with what IBM describe as "AC signals" and "DC signals". I assume they mean changing digital signals for "AC" and static current signals for "DC".

It also outputs U and T level signals. The emitter-follower outputs at the bottom are T-level, and the inverter outputs at the top are U level. If I am right, there are both the POSITIVE versions of these signals.

## Miscellaneous

There are a great deal of other gates specified in this manual which may interest the reader. They are debouncers, oscillators, more logic level converters, and so on. Check out the manual for a better look.

# IBM Standard Modular System Emitter-Coupled Logic

## Logic Levels

Below you can find the definition of the four different forms of logic levels that IBM's SMS ECL uses:

![IBM SMS ECL Logic Levels](/IBM_SMS_images/005_SMS_ECL_Logic_Levels.png)

The Positive and Negative P and N levels are fairly reminiscent of the T and U lines of IBM SMS DTL. As you will see as we look at the basic gates of SMS ECL, the actual voltages that the gates use will be much much closer together than in SMS DTL. This is because _electrical current_ is the bearer of logic meaning in ECL. The whole point of ECL gates is to very quickly switch electrical current with transistors that are NOT saturated or cut off. This makes ECL a much faster logic family to use, but it also means ECL uses a great deal more power, because ECL systems typically have large amounts of current flowing through them. The greater the current, the higher the amount of power the system ends up using.

## Fundamental Gates

Below please find two schematics for the fundamental Positive AND and Negative OR gate:

![Positive AND, Negative OR, ECL](/IBM_SMS_images/006_SMS_ECL_Pos_AND_Neg_OR.png)

and Negative AND and Positive gate:

![Neg AND, Pos OR, ECL](/IBM_SMS_images/007_SMS_ECL_Neg_AND_Pos_OR.png)

They respectively take N and P inputs, and output both in-phase and out-of-phase opposite fundamental logic level outputs. That is, if you feed the first gate, the Positive AND gate, an N level signal, it will output a P level signal of both phases: +P and -P. The opposite goes for the Negative AND: a P input and an N output.

There are other circuits specified in the manual - Emitter followers, for driving large numbers of gates, and Power Inverters, which convert ECL logic into DTL logic.

I am actually amazed about how it is possible to combine different logic families together into one computer. It just goes to show that if you have a lot of time, energy and resources, you can construct incredibly eclectic systems.

Here is the schematic for an N-level ECL to U-level DTL converter, for instance:

![ECL to DTL converter](/IBM_SMS_images/008_SMS_ECL_to_DTL_Converter.png)

There are also line drivers, transmission drivers, indicator drivers, and more in this manual.

## Basic Flip-Flops

IBM SMS ECL flip-flops are incredibly complex. In fact I think they may be of absolutely no use whatsoever to the ordinary hacker - they require many capacitors and inductors. See below:

![ECL Flip-Flop](/IBM_SMS_images/009_SMS_ECL_Flip_Flop.png)

The flip-flop does also not receive or output DC signals. It is a purely AC operated gate. I now revise what I took "AC signal" to mean - it is an entirely analogue current signal. Perhaps this is incorrect, but as you can see below, basic flip-flops made from AND and OR gates are called "DC triggers":

![Basic ECL Flip-Flop](/IBM_SMS_images/010_SMS_ECL_Basic_Flip_Flop.png)

As the schematic shows, you need to delay input signals to make sure you don't create racing conditions, which would cause the flip-flop to enter a state of feedback.

# Conclusion

Hopefully someone finds this useful!
