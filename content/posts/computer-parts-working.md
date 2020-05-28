---
title: "Applied Method of Calculating Marginal Cost of Desktop PC Parts Sourcing"
date: 2019-12-16T05:55:45+08:00
draft: false
---

# Introduction

I have decided to build a new computer. I wish to use a lot of the
same tools that Alan Kay created for the Smalltalk-like language
Squeak. A lot of these tools are able to be run natively in _Pharo_,
which is the default open source Smalltalk development environment.

I cannot remember the specific names of the packages or development
environments of which I am speaking, but they concern making virtual
3D environments -- I find a lot of them really attractive for making
walking simulators, or 3D sandbox games.

ANYWAY - that's not the purpose of this blog post. This post is my
process for constructing a desktop computer that is supposed to meet
certain requirements. For instance, several years ago, I constructed a
computer around a CPU that was good for processing video files. It was
built to a budget, and the computer was still functioning right up
until I had to throw it away. That's a long story.

Anyway this is how I designed this computer, which is essentially for
both video game development, and for a desire to have the computer
last a good long while.

# Step One: Find Good Base Specifications

The game I am designing is a 3D, open world, sandbox game. The one I
like the best is _Fallout 4_, so I decided to look up the
developer/publisher recommended specifications for that game, which
happened to be:

>Recommended:
>CPU: AMD FX-9590 
>Video card: R9 290X (4GB RAM)
>
>(when I saw this CPU specification my eyes boggled a little,
>this is a beast of a chip, the 9590)
>
>Minimum Specifications:
>CPU: AMD Phenom II X4 945
>Video card: Radeon HD 7870 (2GB RAM)

# Step Two: Transform These Specifications Into Benchmarks

Using the Passmark website for CPU and video card processing power
benchmarks is fairly straight forward. I believe there are also other
websites one can use to work out the relative processing power of
computer components, but I have used this website for years, so I
suppose I am a creative of habit.

Anyway these are the processing power figures extracted from the
Passmark website:

| CPU Name         | Benchmark score |
|:----------------:|:---------------:|
| AMD FX-9590      | 10 193          |
| Phenom II X4 945 | 3 652           |

| Video card name | Benchmark score |
|:---------------:|:---------------:|
| R9 290X         | 7152            |
| HD 7870         | 4384            |

# Step Three: Compare Current Available Components to These Figures

The rough figures we have to work with in order to create a PC capable
of processing the graphics needed for a fairly intensive sandbox 3d
game are obviously:

CPU -> 4 000 to 10 000 on the Passmark score system

and

Video card -> a score of 4 000 to 7 000 

## The Components Available to Me

### CPUs

| CPU Name         | Passmark score | Price  (AUD) |
|:----------------:|:--------------:|:------------:|
| A4-5300          | 2019           | 40           |
| A6-9500          | 3030           | 40           |
| AMD 200GE        | 4952           | 80           |
| AMD Athlon 3000G | 5410           | 80           |
| Ryzen 3 2200G    | 7333           | 119          |
| Ryzen 3 2300X    | 8309           | 145          |
| Ryzen 3 3200G    | 7901           | 125          |
| Ryzen 5 2400G    | 9326           | 179          |
| Ryzen 5 2600     | 13511          | 185          |

### Video cards

| Card Name | Score | Price        |
|:---------:|:-----:|:------------:|
| R5 230    | 247   | 45           |
| R7 240    | 976   | 55           |
| Vega 11   | 2272  | CPU internal |
| RX 550    | 3428  | 105          |
| RX 570    | 6896  | 185          |
| RX 580    | 8564  | 259          |
| Vega 56   | 12039 | 258          |

# Step Four: Tabulating The Performance Relationship

## Best Video Cards Against Worst CPUs

Here we sacrifice CPU performance against video card performance. We
are here using the mathemathical formulat that Passmark uses to
combine the scores obtained from video cards and CPUs on their own, to
give an overall score of the combination of the two.

In this comparison, I have held constant: (a) the RAM score;
and (b) the Hard Disk score.

| Overall System Score | Vega 56 | RX 580 | RX 570 |
|:--------------------:|:-------:|:------:|:------:|
| A4-5300 APU          | 2600    | 2600   |        |
| A6-9500 APU          | 2000    | 2000   |        |
| Athlon 200GE         |         |        | 2000   |

## Worst Video Cards Against Best CPUs

|        | Ryzen 5 2600 | Ryzen 5 3400G | Ryzen 5 3600 |
|:------:|:------------:|:-------------:|:------------:|
| RX 550 | 3800         | 3700          | 4000         |
| R7 240 | 2800         | 2800          | 2900         |

## Median Video Cards Against Median CPUs

|               | RX 570 |
|:-------------:|:------:|
| Ryzen 3 2200G | 3500   |
| Ryzen 3 3200G | 3500   |

# Step Five: Tabulating the Optimum Value

## Table One

|              | Vega 56          | RX 580           | RX 570           |
|:------------:|:----------------:|:----------------:|:----------------:|
| A4-5300 APU  | 2600 / 300 = 8.7 | 2600 / 300 = 8.7 |                  |
| A6-9500 APU  | 2600 / 300 = 6.7 | 2600 / 300 = 6.7 |                  |
| Athlon 200GE |                  |                  | 2000 / 265 = 7.5 |
|              |                  |                  |                  |

## Table Two

|        | Ryzen 5 2600      | Ryzen 5 3400G ($215) | Ryzen 5 3600 ($305) |
|:------:|:-----------------:|:--------------------:|:-------------------:|
| RX 550 | 3800 / 290 = 13.1 | 3700 / 320 = 11.6    | 4000 / 410 = 9.8    |
| R7 240 | 2800 / 240 = 11.7 | 2800 / 234 = 11.9    | 2900 / 360 = 8.1    |

## Table Three

|               | RX 570            |
|:-------------:|:-----------------:|
| Ryzen 3 2200G | 3500 / 304 = 11.5 |
| Ryzen 3 3200G | 3500 / 310 = 11.3 |

# Conclusion

So there you have it! It turns out the combination of Ryzen 5 2600
CPU, and Radeon RX 550 is the most cost effective.

The best CPU combined with the best video card only really yields an
overall system score of around 4000, and at a combined price of $443,
this turns out to be incredibly cost ineffective (around 0.9 score
units per dollar) - and this is to be expected - the best CPU and the
best video cards are usually horribly cost effective and inefficient
at delivering good performance. They are a horrible rush to the bottom
in terms of diminishing marginal returns of unit of computing power
per unit of currency. 

The Fallout 4 Minimum system requirement Passmark system score: 2600
The recommended specifications score: ~4000
