---
title: "Guerrilla Game Season 2"
date: 2018-04-29T19:10:01+10:00
draft: false
---

OKAY. I AM RETURNING TO THIS PROJECT.

It has only been 39-40 days anyway. A lot of my friends and party members are always asking me about this game, and their positive encouragement recently has made me want to return to development. If I keep making games people are interested in, I think I'll never want to stop working on them!

I still have a lot of time left in the kernel for drawing the screen, so I think I can return at some time and include playfield graphics or missiles. But I will do that later.

I will call this next phase "Phase Three" - and I will dedicate it to creating a multi-screen world in which for you to move Che around in. "Phase One" was me learning how to draw the screen and a moving multi-colour character AT ALL, "Phase Two" was creating a multi-band kernel.

What I want to achieve in Phase Three is a randomly generated multi-screen world. I think I will achieve this with a polynomial counter. Anguna has a 13x13 screen world. I think I'll aim for that size.

I was thinking "how would it be possible to create a two-dimensional world using a polynomial counter?" I thought maybe I would have 13 individual different polynomial counters for each row/column of the square world, but after some daydreaming I thought perhaps a single polynomial counter that snaked down the world like this would probably work best:

```|-1-|-2-|-3-|-4-|-5-|-6-|-7-|-8-|-8-|-10|-11|-12|-13|
|-14|-15|-16|-17|...|---|---|---|---|---|---|---|---|```

What would happen is that if you moved up one cell, the polynomial counter could decrement by 13 positions, and if you moved down a cell, it would increment 13 positions.

The benefits of randomly generating a world are:

- I would not have to store a complete isomorphic representation of the world in ROM
- Players could still have the option of playing the same world again by entering a seed number
- Players would be able to share interesting worlds by sharing seed numbers
- Players would have the choice of randomly generating a world through a title screen menu
- Random generation would add replay value

I don't fully understand polynomial counters yet, but I anticipate that a big disadvantage of using them would be that they would use up more RAM. However as I am writing this, I don't see how this would really be so, as the polynomial counter would really just be counting up and down for a single screen. The counter just moves up and down its one-dimensional pathway, and it gives the illusion that there is a permanent world cast out into two-dimensional space. Really there is just one screen, being loaded with different elements depending on what position the counter is at along its pathway.

I will reduce the number of bands in the multi-screen kernel from 5 to 4. I want to give the moving enemies and friendly NPCs more room to randomly move around on the screen. As it stands, I am not happy with the amount of vertical room that NPCs have to move.

So the polynomial counter will have 13 screens x 4 screen bands through which to step.

I want there to be a sense of progression to the game, so I will add in a finite number of bosses. I am hoping that the polynomial counter will generate, say, the locations for 5 bosses randomly throughout the world without needing a separate subroutine, but what I may do is have the polynomial counter for the total world to distribute trees and NPCs, and, eventually, playfield graphics, and then a separate routine to nicely position the five boss garrisons throughout the world.

I want the boss locations to be kind of like "castles" -- they'll be a barracks or a big building into which you enter.

---

# Work timeline:

I think I will be able to actually put some effort into coding on tuesday next week, because it's a holiday here in Australia, and my girlfriend has time off work and some family members are flying 4000km to come stay in my city for the holiday.

***

# Social encouragement:

Finally, I want to say that if you're like me, and you've been finding this year really hard emotionally, I'm always here to talk. It has been very difficult finding steady work, and I am not sure I actually want to continue in the career of academic philosophy after my PhD, so I am naturally feeling worried about my scholarship running out in 3 months.

If you feel ashamed about yourself, and if you feel pathetic - I'm always here to listen. Depression is an artificial mental state. It is also temporary. The reason why you (and I) might feel depressed is not because of YOU (or in my case, ME). Everyone well-intentioned person in this Atari community is a wonderful person, and deserves to pursue a life and career that is fulfilling and satisfying.

I have JUST gotten over a spell of deep, deep depression - AND paranoid delusions after testing to see if I actually do have schizophrenia, so I am very very relieved. I hope I can be the person to believe in someone else while they can't believe in themselves. I want this because I have so many people in my life who have believed in me while I couldn't.

FIGHT IT. YOU CAN DO IT. FIGHT AND WIN. YOU ARE A GOOD AND WORTHWHILE PERSON.
