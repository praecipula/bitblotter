---
layout: tech
title: What's in a Name - Bitwise Block Transfer
categories: [tech meta pre-cursor]
---


Bitwise Block Transfer
====

Or, why Windows used to do that weird thing when you dragged crashed apps
----

On a trip to the Computer History Museum in Mountain View a few years back I noticed a small (well, small for a historical computer) machine in a corner of a room. This was an odd device compared to both older and newer machines: it sat on a small cabinet and had a distinctly photocopier-like boxiness typical of office electronics "back then", whenever then was. So far, fairly normal - but it had some 5-key periperhal thing, a chunky 3 button mouse, and a rounded, portrait-orientation CRT that looked like a love child between M-O (the "foreign contaminant" scrubber bot from Wall-E) and an old bowling alley scorekeeping screen.

This was, in fact, a completely revolutionary device: the [Xerox Alto](https://en.wikipedia.org/wiki/Xerox_Alto), developed in the Xerox PARC research facility in the early 1970's. This was the first machine to feature:

1. A mouse
1. A removable disk drive
1. A network adapter
1. A Graphical User Interface (GUI)
1. A rasterized, bitmapped screen (Individually addresable pixels, rather than those vector screens like [early video games](https://upload.wikimedia.org/wikipedia/en/1/13/Asteroi1.png) or [character displays](https://en.wikipedia.org/wiki/Computer_terminal#/media/File:DEC_VT100_terminal_transparent.png)
1. Graphics editing software
1. WYSIWYG document editor
1. E-mail
1. A "chording" keyboard (one that detects multiple keypresses at once)
1. A networked [multiplayer game](https://en.wikipedia.org/wiki/Alto_Trek)

Yowza! Other computers and technology demonstrators for these types of features already existed, but this was the first real demonstration of the future of computing - so much so that when Steve Jobs saw it, he immediately ~appropriated~ was inspired to adopt many of these features into Apple's Macintosh computer.

One of the technologies in particular--the rasterized, bitmapped screen--contained a software / hardware innovation that was so creative that it blew the minds of everyone who saw it: BiTBLT.

The way this algorithm worked makes the most sense when working from the hardware up. The Alto had a 606x808 pixel screen with only 2 colors: on (white) and off (black). These 2 color pixels can be represented with a single bit in memory, adding up to just under 62kB. This was a significant chunk of memory for the times; the Alto was offered in configurations from 96kB to 512 kB, so the majority of the low-end computer's memory went simply to storing the pixels that were being displayed!

The alto would repeatedly paint the screen with whatever is in this chunk of memory, but the rest of the software has to set up this memory correctly. The method by which this is done is the _painter's algorithm_. This algorithm is based on how painters layer features on a canvas from back to front: sky, say, then mountains, then clouds, then happy trees, then a river, all layered by a friendly ex-drill-sergeant with a 'fro.
