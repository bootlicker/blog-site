---
title: "Guerrilla Game: Random Number Translator"
date: 2018-04-05T13:13:57+10:00
draft: false
---

Okay I have written the code for transforming the output of the 16 bit random number generator into (what I think are) unique indexes for the four zones to be drawn on the screen.

This is the code:

```

;=================================
; Forming the input of the Random Number Generator
;=================================

; Bit 5 of Map_Coords, the Up bit, is in the carry bit.
; The status register should look like this now:
;
; C76543210
; UXXXX0RLD

;==================================
;Is the UP flag set in Map_Coords?
;==================================

    bcc CheckRNG_Down   ; If UP flag not set, check DOWN flag
    ldx #0
    jmp ShiftBackwards
    
.CheckRNG_Down

    ror                 ; Put D in carry bit
    bcc CheckRNG_Left   ; If DOWN flag not set, check LEFT flag
    ldx #0
    jmp ShiftForwards
    
.CheckRNG_Left

    ror                 ; Put L in carry bit
    bcc CheckRNG_Right  ; If LEFT flag not set, check RIGHT flag
    ldx #255
    jmp ShiftBackwards
    
.CheckRNG_Right

    ror           ; Put R in carry bit
    bcc No_RNG    ; If RIGHT flag not set, then no flags set, then exit
    ldx #255
    
;=================================
; Wait for Vertical Blank to End
;=================================

; What we're going to do is use up a blank frame of kernel time
; in order to have enough time to calculate a full row of screens:
; 256 positions on the RNG counter.

	lda #$00        ; 2 13
	sta COLUBK      ; 3 16

RNGStartWait:
	
    sta WSYNC
;---------------------------------
	lda INTIM		    ; 4  4
	bne RNGStartWait    ; 2  6
	sta VBLANK		    ; 3  9 - Accumulator D1=0

;=================================
; Set timer for blank frame
;
; (192 * 76) / 64 = 228
;=================================

RNG_Timer:
	ldx #228
	stx TIM64T

;=================================
; Random Number Generator Routine
;=================================

; SHIFT FORWARDS 

ShiftForwards:
    lda Rand8   ; 3  3
    lsr         ; 2  5
    rol Rand16  ; 5 10
    bcc noeor   ; 2 12
    eor #$D4    ; 2 14 - $D4 is the only number I know the inverse to 

.noeor          ;
    sta Rand8   ; 3 17
    eor Rand16  ; 3 20
    
    inx
    clc
    bne ShiftForwards
    beq Pointer_Calc
    
; SHIFT BACKWARDS

ShiftBackwards:

    lda Rand8
    lsr
    rol Rand16
    bcc noeorleft
    eor #$A9    ; $D4 is the only number I know the inverse to 

.noeorleft 
    sta Rand8
    eor Rand16
        
    inx
    clc
    bne ShiftForwards
    beq Pointer_Calc

;================================================
; Translation of the output of the random number
; generator into a useful index for selecting
; a random object in ROM.
; 
; Here we:
; - Buffer the output of the RNG into RAM
; - Enter into a 4 cycle loop, which masks off
;   different portions of the 16 bit random number
;   so that a number between 0-63 is produced.
;
; This translates the random number output into
; an index that is 64 positions long, and allows
; us to randomly select 4 different objects from
; that 64 bit number.
;
; A second level of randomness could be introduced
; by generating an 8 bit random number, and masking
; THOSE bits off. But that would make the game
; impossible to seed the same way every time.
;
;================================================
    
Pointer_Calc:
    
    ldy #3
    
.Pointer_Calc_Loop

    ldx Rand8
    stx Rand_Pointer_Calc8
    
    ldx Rand16
    stx Rand_Pointer_Calc16
    
    cpy #3
    beq Band_3_Calc
    cpy #2
    beq Band_2_Calc
    cpy #1
    beq Band_1_Calc
    cpy #0
    beq Band_0_Calc
    
.Band_3_Calc

    lda Rand_Pointer_Calc16
    and #%11111100
    lsr
    lsr
    sta Band_3_Index

    jmp Done_Calc
    
.Band_0_Calc

    lda Rand_Pointer_Calc8
    and #%00111111
    sta Band_0_Index
    jmp Done_Calc
    
.Band_2_Calc

    lda Rand_Pointer_Calc16
    and #%00000111
    asl
    asl
    asl
    sta Rand_Pointer_Calc16
    
    lda Rand_Pointer_Calc8
    and #%11100000
    rol
    rol
    rol
    rol
    clc
    and Rand_Pointer_Calc16
    sta Band_2_Index
    
    
    jmp Done_Calc

.Band_1_Calc

    lda Rand_Pointer_Calc16
    and #%0011100
    asl
    asl
    sta Rand_Pointer_Calc16
    
    lda Rand_Pointer_Calc8
    and #%0011100
    rol
    rol
    clc
    and Rand_Pointer_Calc16
    sta Band_1_Index

.Done_Calc

    dey
    bpl Pointer_Calc_Loop

```

My main concern is that masking off 6 bits from the random number generator output is actually reducing the number of random numbers from the generator.

I don't quite know the maths, but I am hoping that masking off 6 bits from the 16 bits is not actually making the output of the random number generator less random.

If it is reducing the randomness of the generator -- how else would one produce a random number between 0 and 2^6 four different times over 2^16 different screens?

My thinking was that 64 CHOOSE 4 combinations of objects is a larger number than 2^16, and that way there would always be a unique combination of 4 objects across the 2^16 screens.

The problem is, I don't quite know what mathematical function is being performed by masking off 6 bits from 16 bits.

Any ideas?

---

EDIT:

Is what is happening with my masking 16 CHOOSE 6 = 8008? Of which I am choosing 4 combinations?

Is the randomness of that choice then 6! or 6 CHOOSE 4? or is it 64! ?

There's an answer to this, but I have never been good at combinatorial logic and statistics...
