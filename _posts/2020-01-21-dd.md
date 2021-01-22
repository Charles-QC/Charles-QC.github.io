---
layout: post
title: EscapeTheDungeon writeup
feature-img: "assets/img/thumbnails/dd.jpg"
thumbnail: "assets/img/thumbnails/dd.jpg"
tags: []
---

<h4>CTF: Reversing [very easy]</h4>
<h4>Link: <a href="https://crackmes.one/crackme/5f99d7bd33c5d424269a168c">https://crackmes.one/crackme/5f99d7bd33c5d424269a168c</a></h4> <br>

### Overview

This crackme is a D&D game and there is a README file in it.

![README]({{ site.baseurl }}/assets/img/d&d/README.jpg)

As you can see the README tells us to: Remove NAG (MessageBox in the program that says 'NAG'), Finish the game and find a secret key.

![OV-1]({{ site.baseurl }}/assets/img/d&d/ov-1.PNG)

![OV-2]({{ site.baseurl }}/assets/img/d&d/ov-2.PNG)

I will skip the two first parts of this crackme because they are boring and useless, there are paths in the game randomly chose which kills you or complete the game.

![OV-3]({{ site.baseurl }}/assets/img/d&d/ov-3.PNG)

So now that we know what this crackme look like let's start reversing it!

### Write-up

![KEY]({{ site.baseurl }}/assets/img/d&d/Key.PNG)

So we are looking for a secret key that the game/crackme asks us to give it when we complete it. I'll jump in ida to the part where it asks for it...