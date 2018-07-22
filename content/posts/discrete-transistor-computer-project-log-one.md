---
title: "Discrete Transistor Computer Project Log #1"
date: 2018-07-22T14:28:28+10:00
draft: false
---

<p>This is the first attempt at a data flow diagram of the RAVEN. I spent a lot of time researching and analysing the <a href="https://hackaday.io/project/4237-mental-1-a-brainfuck-cpu/" target="_blank">MENTAL-1 computer</a> built by Trey Keown here on <a target="_blank" rel="noopener noreferrer" href="http://Hackaday.io">Hackaday.io</a>. That computer was built with TTL logic. It implemented a simple but slow 'SCAN' control signal which decremented the Program Counter to a corresponding [ instruction after executing a ] instruction.</p>

<p>After reading the discussion that Trey <a href="https://www.reddit.com/r/electronics/comments/730r7c/i_built_a_cpu_that_natively_runs_brainfuck_code/" target="_blank">conducted on reddit</a>, and seeing that he suggested implementing a stack pointer register in order to speed up the [ and ] looping process in <em>brainfuck</em> code, I decided to come up with a CPU architecture based on the PDP-8/S and Malvino SAP-2 that implemented a stack pointer.</p>

<p>This is the rough idea I have for the CPU architecture data flow for the RAVEN, after looking at the PDP-8/S and SAP-2:</p>

<img class="lazy" src="/raven-discrete-computer/Data_Flow_Diagram.png" width=75%>

<p>
The CPU does not require an accumulator, or temporary buffer registers, because the only data manipulation that the brainfuck instruction set implements is incrementing and decrementing memory cells ("memory locations", "memory words").</p>

<p>So in order to implement the instructions +, -, and &lt; and &gt;, all that is required is control signals from the control sequencer that increment and decrement the MAR and MDR.</p>

<h1>The MAR</h1>

<p>The MAR is not a bidirectional/three state register. After it receives a memory location from the PC, or is cleared to $0000, or increments or decrements itself, it always holds the address locations to which it points in the core memory HIGH.</p>

<p>Currently I do not want to implement ROM memory, I will implement a tape reader like Yann Guidon's <a href="https://hackaday.io/project/8921-low-resolution-scanner-for-cheap-data-input">optical-based reader</a>. I haven't checked out how the PDP-8 loaded in programs. I envisage loading programs will be a lot like bootstrapping and running something like an Altair 8800.</p>

<h1>The Stack Pointer; [ and ] instructions</h1>

<p>The SP will be able to be initialised anywhere in memory, but from my time with 6502 Assembly, I would recommend somethere like $XXFF. Instead of a [ instruction incrementing a SCAN counter register like in MENTAL-1, [ will:</p>

<ol><li>test to see if the current stack location is non-zero</li><li>if non-zero, increment the stack pointer</li><li>then push the next Program Counter (PC) state onto the stack (the memory cell after a [ command is the loop counter), </li><li>and then continue execution.</li></ol>

<p>When a ] instruction is executed, </p>

<ol><li>the stack pointer is incremented, </li>
<li>and the PC state after the ] instruction is pushed onto the stack. </li><li>Then, the stack pointer is decremented </li>
<li>and the PC state of the loop counter cell is popped off the stack and loaded into the PC. </li>
<li>The MAR is then loaded with the memory cell location, </li><li>and the data is loaded into the MDR. </li>
<li>If the cell is data equals zero (<em>I need to implement a flags register linked to the MDR</em>), the stack pointer is incremented </li>
<li>and the state after the ] instruction is popped from the stack and loaded into the PC, </li><li>the stack pointer is then decremented to cause the old [ location to be overwritten, and execution continues.</li>
<li>I think it would probably be wise implement a 'stack clear' operation to write $0000 to the old [ location. This would just require loading the MDR with ZERO, and then writing that to the SP memory address.</li></ol>

<p>BUT</p>

<ol><li>If the loop counter cell is non-zero, the old ] location is written with ZERO, </li>
<li>and the stack pointer decremented and execution continues.</li></ol>

<p>The organisation of the stack will look like this, as [ and ] are executed:</p>

<img src="/raven-discrete-computer/Stack_Operation.png" width=75%>
