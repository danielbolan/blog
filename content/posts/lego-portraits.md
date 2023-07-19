---
title: "LEGO Portraits"
date: 2023-07-19
category: art
tags:
 - art
---

This is just a quick write-up of a portrait I did of my son about a year ago using LEGO bricks. Between the [portrait of my wife]({{< ref "topographic-halftone-patterns" >}}) and the little watercolor of our pets I commissioned, we've almost got the whole family covered -- I'm the only one missing at this point, though I've got plans to fix that as well.

I was originally combing through [BrickLink](https://www.bricklink.com/v2/catalog/catalogitem.page?P=3070b#T=C) to find 1x1 tiles I could use as pixels for a dithered image, and picking the cheapest colors I could that would still give a halfway decent palette. This proved to be quite challenging and eventually I decided to buy the [Elvis art set](https://www.lego.com/en-us/service/buildinginstructions/31204) since it didn't require ordering from several different suppliers and had a few reasonable colors for my kid's skin tone. The 48x48 pip size was a bit big for my taste, so I decided to use only half the plates for a 32x32 pip portrait. Cutting the pixel count in half also gave a lot of margin since some of the colors were quite limited in quantity.

After that I wrote up a quick implementation of [Floyd-Steinberg dithering](https://en.wikipedia.org/wiki/Floyd%E2%80%93Steinberg_dithering). The normal algorithm tended to produce too many checkerboard patterns that made an image this small a bit hard to parse visually. To fix this I added a slider to multiply the residuals by some value between 0 and 1. A value of 0 outputs a plain nearest-color, and 1 produces the typical Floyd-Steinberg dithering. Setting it somewhere in between produces an image that maintains large spaces of single colors while adequately smoothing the transitions between these spaces. I ended up going for a very low value (0.2, I believe) for this error diffusion modifier, but other images I tried seemed to benefit from higher ones.

![An illustration how different error diffusion rates affect the image](/img/lego-portraits/error-gradient.jpg)

A few other bits worth mentioning about the image processing:
- For the palette I removed the two gray shades included with the set as they would turn up far too often and give the output image a very washed-out look.
- Even with removing the grays, I needed to turn up the contrast on most photos I tried in order to get decent results.
- If you use the Elvis art set, you may want to paint the subject's shirt blue, as there tends to be a surplus of those colors, depending on what you want for a background.

After getting something I liked, I pulled it into [aseprite](https://www.aseprite.org) for final touch-ups and then used [Pillow](https://pypi.org/project/Pillow/) to generate instructions in the same style as the original booklet. The instructions weren't strictly necessary, but I made a second one of a friend's kid as a gift and it was a nice touch for that.

All in all I'm quite satisfied with how it turned out! Here's the final result next to the last portrait I did:

![A photo of the LEGO portrait alongside my old topographic portrait I did of my wife](/img/lego-portraits/result.jpg)

### Future Work

It still feels like taking the easy way out to use 1x1 bricks directly as pixels! There are two options I've been considering in order to be able to use arbitrary lego pieces. One is a genetic algorithm that tries to get closer to a target image through trial and error. There are loads of [implementations like this](https://github.com/peterbraden/genetic-lisa/) for approximating images with simple svg paths, and should be very easy to implement. The other is to extend Floyd-Steinberg dithering to work on graphs rather than grids -- I quite like this idea but it'll take a bit more careful thought to create.