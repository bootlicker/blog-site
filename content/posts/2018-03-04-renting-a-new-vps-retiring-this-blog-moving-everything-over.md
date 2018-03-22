---
title: Renting a new VPS, Retiring this blog, Moving Everything Over
author: bootlicker
type: post
date: 2018-03-04T11:31:04+00:00
url: /2018/03/04/renting-a-new-vps-retiring-this-blog-moving-everything-over/
tags:
  - Uncategorised

---
Well, I suppose I finally acted on one of my day dreams that I wrote about on this blog.

I am not happy that this blog uses non-free scripts, so I thought I would backup everything here on Bootlicker and set up a new site. A comrade of mine recommended _Hugo_ go to me, a static site generation platform written in Golang. They also recommended that I rent a Virtual Private Server and manually configure it to host HTTP.

So I did all that. I rented the VPS, and I configured it so that it is very secure &#8212; it only uses 4096 SSH keys, and it has a very strong firewall now. There is much more information and support for configuring and taking control of a VPS than there is in fixing a WordPress installation.

I have also been having terrible perfomance on this web server. the .htaccess file (Apache&#8230; :/) for this site has become corrupted several times over the last week. It has completely disabled my ability to use and maintain this blog, so I guess the terrible performance of this server finally pushed me over the edge to setting up my own VPS.

The great this about this new VPS is that I will now be able to unify all my old blogs:

  * The Mondegreen (theamazingfruitsalad.wordpress.com)
  * Come See the Duck (burninghotelsdown.tumblr.com)
  * JumpnShoot 9000 (jumpnshoot9000.wordpress.com)
  * This one, Bootlicker (bootlicker.doubledashgames.com)

I think I even have a LiveJournal&#8230; but that one got backed up and published onto the Mondegreen.

Anyway, exciting times. Finally I will have bootlicker.party actually parked onto a server, and not just a simple web redirect.
