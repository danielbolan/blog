---
title: "Your Dutch Flag is Probably Wrong"
date: 2022-03-16
category: art
tags:
 - art
---

_This is a rewrite of an older post, edited down since the original rambled a bit. You can read the original [here](/archived/red-waiss-blauw)._

## First, A Few Fun Flag Facts

The Luxembourgish and Dutch flags are nearly identical, save for their slightly different shades of blue used for their bottom stripes.[^1] One day I was curious to see how different they were, and whether the reds are actually the same.[^2] This sent me down a much deeper rabbit hole than even the usual questions about colors tend to be.

[^1]: Their proportions are also a bit different. Interestingly, the Luxembourgish flag has two officially accepted proportions --- 1:2 and 3:5 are both considered fine. I don’t know of any other countries that do this, though I’m sure someone better versed in vexillology could come up with an example.

[^2]: They aren't. The Netherlands uses {{< inlineColor ad1d25 >}} and Luxembourg uses the decidedly brighter {{< inlineColor EF3340 >}}.

Because Luxembourg didn't bother to standardize the colors of its flag until 1993, they were able to use Pantone to make a [precise definition.](https://legilux.public.lu/eli/etat/leg/rgd/1993/07/27/n2/jo) The Dutch flag is a big trickier --- it was formally defined back in 1949, predating Pantone. Here's a (rough) translation of its [official definition](https://puc.overheid.nl/mp-bundels/doc/PUC_41859_10/1/#8c824c38-7a1e-4b09-a6db-2f10b19ad950):

> When illuminated by standard illuminant C with an incident angle 45 degrees to the surface, the values ​​of the trichromatic coordinates and the trichromatic coefficients when observed in a direction perpendicular to the surface are as follows:
>
>
> |      | X | Y | Z |
> |------|:-:|:-:|:-:|
> | __Red__ |18.3|10.0|3.0|
> | __Blue__ |7.5|6.6|25.3|
>
> The coordinate system is chosen in such a way that the following applies for an idealized white surface: Y=100.

As the column names might suggest, this is the [CIE 1931 XYZ color space](https://en.wikipedia.org/wiki/CIE_1931_color_space). Using any online conversion tool you can easily find the sRGB equivalent {{< inlineColor 21468B >}}. Except...

## Oops, Wrong White

Converting between color spaces depends heavily upon what exactly you mean when you say something is "white." This in turn depends upon what kind of light you're using. For nearly all modern applications, this refers to a color known as D65, which is meant to approximate the color of sunlight on a clear day in central Europe. Due to its ubiquity, just about any color converter you'll find online uses D65 implicitly. The issue, though, is that D65 wasn't a standard until 1967, long after the Dutch flag was standardized! Standard Illuminant C, as used in the flag specification, was defined by the CIE in 1931 by using an incandescent lightbulb at a specific temperature and a liquid filter. This was also meant to mimic that spectrum of sunlight, but it turned out that this wasn't a very good approximation and has been deprecated since the D series was formalized.

[^3]: If you're working with printing processes, you might be using an illuminant called D50.

So, what happens when we use the correct illuminant? Drumroll please...

{{< colorSwatch 1e4785 "Illum. C" >}} {{< colorSwatch 21468b "Illum. D65" >}}

{{< colorSwatch ad1d25 "Illum. C" >}} {{< colorSwatch AE1C28 "Illum. D65" >}}

Hm. Not much, apparently. dE00, an equation used for perceptual distance, spits out a ΔE of 0.86 and 1.73, respectively --- below the human capacity to tell the difference without close scrutiny.[^5]

[^5]: For replication's sake, [Here's](https://gist.github.com/danielbolan/7a68a8623383464b4456e67de65f84c0) the code I used for color conversion, thanks to version 3.0.0 of the [colormath python module](https://github.com/gtaylor/python-colormath/releases/tag/3.0.0).

## In the wild

The incorrect colors were listed on the English Wikipedia page in early 2009, and have since proliferated into many, many instances of people using this value in their code as found on GitHub. It's fixed now (at least in the English entry), but the incorrect color is likely to live on far into the future.

The [Rijkshuisstijl](https://www.rijkshuisstijl.nl/english/colours), the graphic design authority for the Dutch central government, doesn't have much to say about the flag. It specifies that the blue used in the central government's logo is {{< inlineColor 154273 >}}, which is similar but noticeably different from the color we got by converting from XYZ. If this is meant to be a direct conversion from the flag's blue then I'm not sure how they calculated it. If someone has an official source on the digitized colors of the flag, I'd love to see it.

{{< colorSwatch 1e4785 "Illum. C" >}} {{< colorSwatch 154273 "Logoblauw" >}}

All this said, our lives are made much easier by the fact that the Dutch flag has at least been quite consistent in its definition of reds and blues. This is in contrast to France which has never formally defined their colors and has a history of [changing them occasionally.](https://drapeaux-sfv.org/vexillologie/actualites/article/a-propos-du-bleu-du-drapeau-tricolore) This is a whole other rabbit hole I am trying to steer well clear of --- I've already spent far too much time thinking about these things as it stands.