---
title: "Guerrilla Game Playfield Graphics Purpose"
date: 2018-04-05T11:20:32+10:00
draft: false
---

Out of nowhere, I figured out how to simulate progressing from the beach, to the jungle, to the mountain in the game.
 
I am gonna use randomly generated "speckles" of playfield graphics on top of layered background colours.
 
What I will do is allow colours between certain vertical bands of screens up and down the map. I will just have a forward counting, non-rerversible polynomial counter for the random speckles. The playfield of course will be reflected.
