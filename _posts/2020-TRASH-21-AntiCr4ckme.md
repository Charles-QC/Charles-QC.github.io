---
layout: post
title: Anti_Cr4ckme writeup
feature-img: "assets/img/thumbnails/aCrackme.jpg"
thumbnail: "assets/img/thumbnails/aCrackme.jpg"
tags: []
---

<h4>CTF: Reversing [Medium] | <a href="https://crackmes.one/crackme/600098f733c5d42c3d0166c8">LINK_TO_CHALL</a> </h4>

<hr>

### Overview

This crackme is harder then the last one i did, its .text section is packed. I will try my best to reverse the encrption and find/patch the anti-debugging techniques it utilizes. All links to subjects i wrote about in this write-up will be at the bottom of the page in the <a href="#Resource">Resource</a> section. Also it's my second write-up and i'm trying to improve myself :)

![ENTROPY]({{ site.baseurl }}/assets/img/aCrackme/entropy.PNG)
`I figured that its .text section is packed by looking at the entropy with DIE (Detect It Easy)`

![OV1]({{ site.baseurl }}/assets/img/aCrackme/overview1.PNG)

The crackme is a console program which asks for a username & password when the inputs are incorrect it just loops back to start.

<hr>

### Write-up

#### AntiDebug Mesures

![AD1]({{ site.baseurl }}/assets/img/aCrackme/stringScan.PNG)

Would you look at this. All these strings have something in common, they are all popular debugers so if we use our logic the only reason a program would have this is if it would look for them in the memory. Following this theory it would mean that there is a function that does some kind of snapshot of all running processes and check if one of them has the name of one of these strings. We can comfirm this theory just by running the crackme while a "knowned" debuger is also running (Not attached).

![STOP]({{ site.baseurl }}/assets/img/aCrackme/exit.gif)

And as you can see it crashed when i openned x32dbg. But now that we know all of this why not trying to find this function ? And i did no long after looking into some functions with IDA.

![AD2]({{ site.baseurl }}/assets/img/aCrackme/snapshot.PNG)

I align some of the graphs this way you can clearly see the strings. So i was right, the function constantly loop in a separate thread while doing a snapshot of all the running processes then going trought a big condition tree checking if current process in snapshot has the name of a "knowed" debugger.

![EXPLAIN1]({{ site.baseurl }}/assets/img/aCrackme/explain1.PNG)

But i also saw that it was creating another thread, let's see where its 'lpStartAdress' gets us.

![EXPLAIN1]({{ site.baseurl }}/assets/img/aCrackme/explain2.PNG)

Oh boy so it also constantly checks IsDebuggerPresent. I will add some comments and try to look for more anti debugging mesures.

Coming soon...

### Resources

- <a href="http://www.ntinfo.biz/index.html">DIE (Detect It Easy)</a>
- <a href="https://en.wikipedia.org/wiki/Entropy_(computing)">Entropy</a>