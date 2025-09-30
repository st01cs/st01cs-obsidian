---
title: "Flexoki"
source: "https://stephango.com/flexoki"
author:
  - "[[Steph Ango]]"
published:
created: 2025-09-30
description: "An inky color scheme for prose and code."
tags:
  - "clippings"
---
Flexoki is an inky color scheme for prose and code. Flexoki is designed for reading and writing on digital screens. It is inspired by analog inks and warm shades of paper.

Flexoki is minimalistic and high-contrast. The colors are calibrated for legibility and perceptual balance across devices and when switching between light and dark modes.

Flexoki is [open-source](https://github.com/kepano/flexoki) under the MIT license. Flexoki is available for dozens of popular apps, including [Obsidian](https://stephango.com/obsidian) using my theme [Minimal](https://stephango.com/minimal).

## Palette

Flexoki is the color palette used on this site. To switch between light and dark mode press the D key or use the toggle at the top of the page. Click any swatch to copy a color to your clipboard.

bg

bg-2

ui

ui-2

ui-3

tx-3

tx-2

tx

re

or

ye

gr

cy

bl

pu

ma

## Syntax highlighting

![](https://stephango.com/assets/flexoki-code-dark.png "Flexoki highlighting") ![](https://stephango.com/assets/flexoki-code-light.png "Flexoki highlighting")

## Why?

I created Flexoki for my personal site, [stephango.com](https://stephango.com/). You’re reading it now. I wanted the colors to feel distinctive yet familiar. Like ink on paper.

The name Flexoki comes from *[flexography](https://en.wikipedia.org/wiki/Flexography)* — a common printing process for paper and cardboard [^1]. I spent many years working with dyes and inks particularly for my companies [Inkodye](https://stephango.com/inkodye) and [Lumi](https://stephango.com/lumi). I also have a fascination with [digital paper](https://stephango.com/the-elusiveness-of-digital-paper). I wanted to bring the comfort of analog color to emissive digital screens.

One challenge is that ink on paper is a subtractive process whereas LCD and OLED screens use additive color. Replicating the effect of mixing pigments digitally is difficult. The following video illustrates the problem:

![](https://www.youtube.com/watch?v=6JVjHqas60Q)

See the [full SIGGRAPH 2021 talk](https://www.youtube.com/watch?v=_qa5iWdfNKg)

Mixing blue and yellow paint creates green, whereas digital color mixing results in a brownish hue. Watercolors retain their saturation when you dilute them, whereas reducing the opacity of digital colors makes them look desaturated.

Another challenge with digital color is [human perception](https://en.wikipedia.org/wiki/List_of_color_spaces_and_their_uses) across color spaces. For example, yellow appears much brighter than blue. Ethan Schoonover’s color scheme [Solarized](https://ethanschoonover.com/solarized/) (2011) was an important inspiration for Flexoki. His emphasis on lightness relationships in the [CIELAB](https://en.wikipedia.org/wiki/CIELAB_color_space) color space helped me understand how to find colors that appear cohesive. Flexoki derives colors from the more recent [Oklab](https://en.wikipedia.org/wiki/Oklab_color_space) color space to maintain those perceptual relationships at the light and dark ends of the spectrum — ramping up color intensity exponentially to emulate the vibrancy that pigments exhibit even when diluted.

I found that choosing colors with perfect perceptual consistency can be at odds with the distinctiveness of colors in practical applications like syntax highlighting. If you adhere too closely to evenness in perceptual lightness you can end up with a palette that looks washed out and difficult to parse.

This project has been a battle between my competing desires in science and art. One part of my brain searches for reliability and precision, while another part searches for those elusive [imperfections](https://stephango.com/scars) that remind us what feels *real*. Solving for all these problems is how I arrived at Flexoki. I hope you find it useful.

## Base color

Flexoki uses warm monochromatic base values that blend the black value with the paper value. 8 values are used in light and dark mode:

- **3 text values:** normal, muted, faint
- **3 interface values:** normal, hover, active
- **2 background values:** primary, secondary

Incremental values can be derived using opacity. For example, you can use a 60% opacity black value on top of the paper value to create the 600 value.

| Color | Hex | Light theme | Dark theme |
| --- | --- | --- | --- |
| `black` | `#100F0F` | `tx` | `bg` |
| `base-950` | `#1C1B1A` |  | `bg-2` |
| `base-900` | `#282726` |  | `ui` |
| `base-850` | `#343331` |  | `ui-2` |
| `base-800` | `#403E3C` |  | `ui-3` |
| `base-700` | `#575653` |  | `tx-3` |
| `base-600` | `#6F6E69` | `tx-2` |  |
| `base-500` | `#878580` |  | `tx-2` |
| `base-300` | `#B7B5AC` | `tx-3` |  |
| `base-200` | `#CECDC3` | `ui-3` | `tx` |
| `base-150` | `#DAD8CE` | `ui-2` |  |
| `base-100` | `#E6E4D9` | `ui` |  |
| `base-50` | `#F2F0E5` | `bg-2` |  |
| `paper` | `#FFFCF0` | `bg` |  |

## Accent colors

8 accent colors are available for accents and syntax highlighting. Unlike the base values, accent values cannot be derived using opacity because this desaturates the pigment effect. Use the [extended palette](https://stephango.com/#extended-palette) for the full range of values.

The following 16 values are the main accent values used for syntax highlighting and interface elements like buttons and links. Light themes should use **600** for syntax highlighted text, dark themes should use **400**.

| Color | Hex | Light theme | Dark theme |
| --- | --- | --- | --- |
| `red-600` | `#AF3029` | `re` | `re-2` |
| `orange-600` | `#BC5215` | `or` | `or-2` |
| `yellow-600` | `#AD8301` | `ye` | `ye-2` |
| `green-600` | `#66800B` | `gr` | `gr-2` |
| `cyan-600` | `#24837B` | `cy` | `cy-2` |
| `blue-600` | `#205EA6` | `bl` | `bl-2` |
| `purple-600` | `#5E409D` | `pu` | `pu-2` |
| `magenta-600` | `#A02F6F` | `ma` | `ma-2` |

| Color | Hex | Light theme | Dark theme |
| --- | --- | --- | --- |
| `red-400` | `#D14D41` | `re-2` | `re` |
| `orange-400` | `#DA702C` | `or-2` | `or` |
| `yellow-400` | `#D0A215` | `ye-2` | `ye` |
| `green-400` | `#879A39` | `gr-2` | `gr` |
| `cyan-400` | `#3AA99F` | `cy-2` | `cy` |
| `blue-400` | `#4385BE` | `bl-2` | `bl` |
| `purple-400` | `#8B7EC8` | `pu-2` | `pu` |
| `magenta-400` | `#CE5D97` | `ma-2` | `ma` |

## Extended palette

If you wish to use Flexoki for more complex applications beyond syntax highlighting and basic color schemes, the extended palette includes a complete set of values for every accent color from **50** to **950**.

Note that **paper** and **black** are special values that represent the lightest and darkest colors in the palette, equivalent to **0** and **1000**.

Flexoki emulates the feeling of pigment on paper by exponentially increasing intensity as colors get lighter or darker. This makes the colors feel vibrant and warm, like watercolor inks.

Base

50

100

150

200

300

400

500

600

700

800

850

900

950

Red

50

100

150

200

300

400

500

600

700

800

850

900

950

Orange

50

100

150

200

300

400

500

600

700

800

850

900

950

Yellow

50

100

150

200

300

400

500

600

700

800

850

900

950

Green

50

100

150

200

300

400

500

600

700

800

850

900

950

Cyan

50

100

150

200

300

400

500

600

700

800

850

900

950

Blue

50

100

150

200

300

400

500

600

700

800

850

900

950

Purple

50

100

150

200

300

400

500

600

700

800

850

900

950

Magenta

50

100

150

200

300

400

500

600

700

800

850

900

950

## Mappings

This table describes how to use each variable in the context of user interfaces and syntax highlighting.

| Color | Variable | UI | Syntax highlighting |  |
| --- | --- | --- | --- | --- |
|  | `bg` | Main background |  |  |
|  | `bg-2` | Secondary background |  |  |
|  | `ui` | Borders |  |  |
|  | `ui-2` | Hovered borders |  |  |
|  | `ui-3` | Active borders |  |  |
|  | `tx-3` | Faint text | Comments |  |
|  | `tx-2` | Muted text | Punctuation, operators |  |
|  | `tx` | Primary text |  |  |
|  | `re` | Error text | Invalid, imports |  |
|  | `or` | Warning text | Functions |  |
|  | `ye` |  | Constants |  |
|  | `gr` | Success text | Keywords |  |
|  | `cy` | Links, active states | Strings |  |
|  | `bl` |  | Variables, attributes |  |
|  | `pu` |  | Numbers |  |
|  | `ma` |  | Language features |  |

## Ports

Flexoki is available for the following apps and tools. [See the full list](https://github.com/kepano/flexoki).

### Apps

- [Alacritty](https://github.com/kepano/flexoki/tree/main/alacritty)
- [Drafts](https://github.com/kepano/flexoki/tree/main/drafts)
- [Emacs](https://github.com/crmsnbleyd/flexoki-emacs-theme)
- Ghostty (built-in)
- [IntelliJ](https://github.com/kepano/flexoki/tree/main/intellij)
- [iTerm2](https://github.com/kepano/flexoki/tree/main/iterm2)
- [Kitty](https://github.com/kepano/flexoki/tree/main/kitty)
- [Lite XL](https://github.com/kepano/flexoki/tree/main/lite_xl)
- [macOS Terminal](https://github.com/kepano/flexoki/tree/main/terminal)
- [Neovim](https://github.com/kepano/flexoki-neovim)
- [Obsidian](https://github.com/kepano/flexoki-obsidian) and included with [Minimal](https://stephango.com/minimal)
- [Omarchy](https://github.com/euandeas/omarchy-flexoki-dark-theme)
- [Slack](https://github.com/kepano/flexoki/blob/main/slack/slack.md)
- [Standard Notes](https://github.com/myreli/sn-flexoki)
- [Sublime Text](https://github.com/kepano/flexoki-sublime)
- [tmux](https://github.com/kepano/flexoki/tree/main/tmux)
- [Ulysses](https://github.com/kepano/flexoki/tree/main/ulysses)
- [VS Code](https://github.com/kepano/flexoki/tree/main/vscode)
- [Warp](https://github.com/kepano/flexoki/tree/main/warp-terminal)
- [WezTerm](https://github.com/kepano/flexoki/tree/main/wezterm)
- [Windows Terminal](https://github.com/kepano/flexoki/tree/main/windows-terminal)
- [Xresources](https://github.com/kepano/flexoki/tree/main/resources)
- [Zed](https://github.com/kepano/flexoki/tree/main/zed)
- [Zellij](https://github.com/kepano/flexoki/tree/main/zellij)

### Frameworks

- [Shadcn](https://gist.github.com/phenomen/affd8c346538378548febd20dccdbfcc)
- [Tailwind](https://gist.github.com/martin-mael/4b50fa8e55da846f3f73399d84fa1848)
- [theme.sh](https://github.com/kepano/flexoki/tree/main/theme.sh)

### Other

- [Figma](https://www.figma.com/community/file/1293274371462921490/flexoki)
- [GIMP](https://github.com/kepano/flexoki/tree/main/gimp)

## Contributing

Flexoki is MIT licensed. You are free to port Flexoki to any app. Please include attribution and a link to [stephango.com/flexoki](https://www.stephango.com/flexoki). You can submit your port to the list via pull request on the [Flexoki repo](https://github.com/kepano/flexoki).

## Changelog

| Date |  |  |
| --- | --- | --- |
| **2025‑01‑07** | `2.0` | Add 88 new values from 50 to 950 for accent colors. |
| **2023‑10‑07** | `1.0` | Initial release. |

[^1]: [![](https://stephango.com/assets/flexo.jpg)](https://stephango.com/flexo) I also have a [dog named Flexo](https://stephango.com/flexo) whose greatness deserved to be immortalized.