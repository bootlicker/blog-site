---
title: Tamagotchi Hacking
author: admin
type: post
date: 2013-10-27T09:11:36+00:00
url: /random-updates/tamagotchi-hacking/
publicize_facebook_url:
  - https://facebook.com/552216077_10151679305456078
  - https://facebook.com/
publicize_twitter_user:
  - hotelsdown
publicize_twitter_url:
  - http://t.co/nbCHdDDVUz
categories:
  - Random Updates
tags:
  - hacking
  - Tamagotchi

---
[youtube http://www.youtube.com/watch?v=WOJfUcCOhJ0?feature=player_embedded]

&nbsp;

So it turns out that the age-old Tamagotchi uses the architecture from the 6502! What is even more startling is the discovery about how Tamagotchi toys actually _work_. The programming of Tamagotchis revolve _entirely_ around one-bit logic: all of the interaction between a Tamagotchi and the player is controlled through switches, checking to see if a player has pressed a button at the right time. Further, all of the data associated with games on the Tamagotchi toy is _bound up with the frames of animation_.

It\&#8217;s all so simple, despite the need for more reverse engineering due to the use of mask ROM within Tamagotchis: since the toy manifests its programming in discrete transistor logic, it notoriously difficult to &#8216;dump&#8217; its data. The author of the presentation hypothesises that if she can get a hold of the test program associated with the industrial mask ROM burning process, a program used by the chip company to prove that hardware errors are not their fault, she might be able to finally shed light completely on how Tamagotchis work.