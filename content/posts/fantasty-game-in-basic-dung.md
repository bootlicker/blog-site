+++
date = "2018-12-14T13:50:59Z"
title = "A Fantasty Game in Commodore 64 BASIC: Dungeon Generator"
+++

This is the first in a three-part series where I give the listing of a game in BASIC for the Commodore 64. This listing comes from the Usborne Publishers book _Write Your Own Fantasy Games_. The listing on that book uses replaceable keywords so that many different 80s microcomputers can each run the game.

I have taken the liberty of doing all the necessary replacements for the game listing so that it can be completely copied over to the Commodore 64 without thinking.

Here is the listing:

# Preparation

Before typing in or loading this program, type in the following:

POKE 44,28: POKE 642,28: SYS(64824)<br>

# The Dungeon Generator

---5 GOSUB 5000<br>
--10 GOSUB 610<br>
--20 PRINT CHR$(147): POKE 53280,0: POKE 53281,0<br>
--30 LET BG=2: LET FG=1: LET T=0: LET L=3: LET LW=W-3: GOSUB 280<br>
--40 PRINT BG$(2);<br>
--50 PRINT HM$;LEFT$(CU$, 1); SPC(1); "LEVEL GENERATOR";<br>
--60 PRINT HM$;LEFT$(CU$, 2); SPC(1); "THIS IS LEVEL:"; LE;<br>
--70 PRINT HM$;LEFT$(CU$, 3); SPC(1); "PRESS H FOR HELP"<br>
--80 LET BG=3: LET FG=2: LET T=5: LET L=15: LET LW=15: GOSUB 280<br>
--90 LET X=1: LET Y=1<br>
-100 GET I$<br>
-110 IF I$="H" THEN GOSUB 360<br>
-120 IF I$="A" AND Y>1 THEN LET Y=Y-1<br>
-130 IF I$="Z" AND Y<15 THEN LET Y=Y+1<br>
-140 IF I$="N" AND X>1 THEN LET X=X-1<br>
-150 IF I$="M" AND X<15 THEN LET X=X+1<br>
-160 IF I$>"/" AND I$<":" THEN GOSUB 230<br>
-170 PRINT BG$(3);<br>
-180 PRINT HM$;LEFT$(CU$, Y+5); SPC(X); CHR$(OS);<br>
-190 PRINT HM$;LEFT$(CU$, Y+5); SPC(X); CHR$(R(X,Y));<br>
-200 IF I$="S" AND IX>0 THEN GOSUB 450:GOTO 20<br>
-210 IF I$<>"F" THEN GOTO 100<br>
-220 STOP<br>

-230 LET I=VAL(I$)<br>
-240 IF I=9 THEN LET I=8+INT(RND(1)*3+1)<br>
-250 IF I=5 THEN LET IX=X:LET IY=Y<br>
-260 LET R(X,Y)=C0+I<br>
-270 RETURN<br>

-280 PRINT HM$;LEFT$(CU$, T); SPC(0);<br>
-290 PRINT BG$(FG);: PRINT LEFT$(B$,LW+2)<br>
-300 PRINT BG$(BG);<br>
-310 FOR I=1 TO L<br>
-320    PRINT BG$(FG); " "; BG$(BG); LEFT$(B$,LW); BG$(FG); " "<br>
-330 NEXT I<br>
-340 PRINT BG$(FG);: PRINT LEFT$(B$,LW+2);<br>
-350 RETURN<br>
-360 PRINT BG$(1);<br>
-370 FOR H=1 TO 10<br>
-380    PRINT HM$;LEFT$(CU$,4); SPC(1); H$(H); : GOSUB 430<br>
-390    HM$;LEFT$(CU$, 4); SPC(1); LEFT$(B$,W-2);<br>
-400 NEXT H<br>
-420 RETURN<br>

## Loop if no key pressed

-430 GET G$: IF G$="" THEN GOTO 430<br>
-440 RETURN<br>

-450 PRINT HM$;LEFT$(1,4); "ONE MOMENT PLEASE";<br>
-460 LET S$=""<br>
-470 FOR J=1 TO 15<br>
-480    FOR K=1 TO 15<br>
-490        LET S$=S$+CHR$(R(K,J))<br>
-500    NEXT K<br>
-510 NEXT J<br>
-520 LET S$=S$+CHR$(IX+OS): LET S$=S$"CHR$(IY+OS)<br>
-530 LET S$=S$+CHR$(LE+OS)<br>
-540 PRINT HM$;LEFT$(1,4); "ANY KEY TO SAVE  "; : GOSUB 430<br>
-550 OPEN 1,1,1,"LEVEL"<br>
-555 FOR I=0 TO 2<br>
-560    PRINT#1, MID$(S$,I*76+1,76)<br>
-565 NEXT I<br>
-570 CLOSE 1<br>
-580 PRINT HM$;LEFT$(1,4); LEFT$(B$,W)<br>
-590 LET LE=LE+1: GOSUB 700<br>
-600 RETURN<br>

## The dungeon generator is initialised in this subroutine

-610 DIM R(15,15), H$(10)<br>
-620 GOSUB 790<br>
-630 DATA "PRESS ANY KEY", "TO MOVE A Z N M", "1 WALL   2 VASE"<br>
-640 DATA "3 CHEST 4 * IDOL *", "5 WAY IN  6 EXIT", "7 TRAP", "8 SAFE PLACE"<br>
-650 DATA "9 GUARD", "0 TO ERASE", "S TO SAVE"<br>
-660 LET LE=1<br>
-670 FOR I=1 TO 10<br>
-680    READ H$(I)<br>
-690 NEXT I: GOSUB 810<br>
-700 FOR J=1 TO 15<br>
-710    FOR K=1 TO 15<br>
-720        LET R(J,K)=C0<br>
-730    NEXT K<br>
-740 NEXT J<br>
-750 LET IX=0: LET IY=0<br>
-760 LET B$="": FOR I=1 TO W: LET B$=B$+" ": NEXT I<br>
-770 RETURN<br>

-790 OS=96: C0=OS+6: W=40: GOSUB 4000<br>
-800 RETURN<br>

## This subroutine copies the graphics data into memory using POKEs

-810 REM READ THE CHARACTERS<br>
-820 FOR I=0 TO 7: READ A: POKE 36532+I,255-A: NEXT I<br>
-830 FOR I=0 TO 95: READ A: POKE 36400+I,255-A: NEXT I<br>
-840 RETURN<br>

1000 DATA 255,255,255,255,255,255,255,255<br>

```
XXXXXXXX
XXXXXXXX
XXXXXXXX
XXXXXXXX
XXXXXXXX
XXXXXXXX
XXXXXXXX
XXXXXXXX
```

1010 DATA 0,0,0,0,0,0,0,0<br>
1020 DATA 85,170,85,170,85,170,85,170<br>

``` 
 X X X X
X X X X 
 X X X X
X X X X 
 X X X X
X X X X 
 X X X X
X X X X
```

1030 DATA 0,60,24,60,126,126,126,60


```

  XXXX  
   XX   
  XXXX
 XXXXXX
 XXXXXX
 XXXXXX
  XXXX
```

1040 DATA 0,56,100,114,95,73,41,31

```

  XXX   
 XX  X
 XXX  X
 X XXXXX 
 X  X  X
  X X  X
   XXXXX
```

1050 DATA 20,42,20,20,93,93,62,99

```
   X X
  X X X
   X X
   X X
 X XXX X
 X XXX X
  XXXXX
 XX   XX
```

1060 DATA 60,126,255,255,255,253,255,255

```
  XXXX
 XXXXXX
XXXXXXXX
XXXXXXXX
XXXXXXXX
XXXXXX X
XXXXXXXX
XXXXXXXX

```

1070 DATA 60,102,195,129,129,129,153,129

```
  XXXX
 XX  XX
XX    XX
X      X
X      X
X      X
X  XX  X
X      X
```

1080 DATA 129,66,36,0,0,36,66,129

```
X      X
 X    X
  X  X

  
  X  X
 X    X
X      X
```

1090 DATA 0,60,66,66,66,66,60,0


```

  XXXX
 X    X
 X    X
 X    X
 X    X
  XXXX
  
 
```

1100 DATA 76,158,170,190,84,30,37,88


```
 X  XX
X  XXXX
X X X X
X XXXXX
 X X X
   XXXX
  X  X X
 X XX   
  
```

1110 DATA 0,56,84,124,56,44,68,102


```
  XXX 
 X X X
 XXXXX
  XXX
  X XX
 X   X
 XX  XX
```

1120 DATA 0,8,28,42,127,85,65,34


```

    X
   XXX
  X X X
 XXXXXXX 
 X X X X
 X     X
  X   X
```

## These three lines needs to be added to all three component programs to the adventure game

4000 BG$(0)=CHR$(146): BG$(1)=CHR$(18)+CHR$(28)<br>
4010 BG$(2)=CHR$(18)+CHR$(158): BG$(3)=CHR$(18)+CHR$(5)<br>
4020 HM$=CHR$(19): CU$="": FOR I=1 TO W: LET CU$=CU$+CHR$(17): NEXT I<br>
4030 POKE 650,255: RETURN<br>

5000 POKE 52,128: POKE 56, 128<br>
5010 POKE 56334, PEEK (56334) AND 254: POKE 1, PEEK(1) AND 251<br>
5020 FOR I=0 TO 2047: POKE 34816+I, PEEK (53248+I): NEXT I<br>
5030 POKE 1, PEEK (1) OR 4<br>
5040 POKE 56334, PEEK (56334) OR 1<br>
5050 POKE 56578, PEEK (56578) OR 3<br>
5060 POKE 56576, PEEK (56576 AND 252) OR 1<br>
5070 POKE 53272, 2: POKE 648, 128<br>
5080 RETURN<br>
