# Laterna brand

The mark, wordmark and colours for Laterna. The full board with construction drawings, lockups and usage rules is the [Laterna Identity artifact](https://claude.ai/artifact/SiBDZfgymRGSvVaSMdR4ug). This file is the source of truth for the numbers.

![Laterna lockup](laterna-lockup-dark.svg)

## Idea

*Laterna* is a Latin form of "lantern". The magic lantern (*laterna magica*) was a 17th-century projector that showed an image through a glass lens ([Wikipedia](https://en.wikipedia.org/wiki/Magic_lantern)). Laterna shows a render through a glass orb. The mark squares off one corner of that orb with an amber L.

## Files

| File | Use |
|---|---|
| `laterna-mark-dark.svg` | Mark on dark backgrounds (paper arc, amber L) |
| `laterna-mark-light.svg` | Mark on light backgrounds (black arc, dark amber L) |
| `laterna-mark-mono.svg` | One colour, follows the surrounding text colour (`currentColor`) |
| `laterna-lockup-{dark,light,mono}.svg` | Mark plus wordmark, side by side |
| `laterna-wordmark-{dark,light,mono}.svg` | "laterna." on its own |
| `laterna-app-icon.svg`, `laterna-app-icon-512.png` | Rounded black tile with the mark |
| `favicon-16.png`, `favicon-32.png` | Browser tab icon (the app icon tile, small) |

The wordmark files are outlines, not live text, so they look the same without the font installed. Always use these files; never type the wordmark (see Wordmark below).

## Mark

Drawn on a 64-unit grid.

| Part | Value |
|---|---|
| Circle | centre 32/32, radius 24 |
| Stroke | 5 units, flat ends, square corner on the L |
| L | from (8, 32) down to (8, 56) and across to (32, 56): both legs 24, along the bottom-left of the circle's 48 × 48 square |
| Arc | the rest of the circle, trimmed so 6 units of clear space separate it from the L at both ends |
| Ink box | 5.5 to 58.5 (53 × 53); the SVGs are cropped to it |

The mark holds at 16 px. Below that, use the app icon.

## Wordmark

"laterna." in **IBM Plex Mono Light (300)**, lower case, the full stop in amber.

Plex Mono gives every letter the same width, so typed text spaces letters unevenly. Measured from the font outlines (units are thousandths of the font size), the gaps between letter shapes are:

| | l–a | a–t | t–e | e–r | r–n | n–a | a–. |
|---|---|---|---|---|---|---|---|
| Typed | 155 | 95 | 153 | 154 | 151 | 173 | 299 |
| Drawn | 155 | 95 | 153 | 154 | 151 | 153 | 153 |

The drawn wordmark moves the last a 20 units left and the full stop a further 146, so both match the 153 between most other letters. The a–t gap stays narrow because the t's crossbar reaches out; its upright is far enough away.

## Lockups

- **Horizontal:** mark height = height of the l (740 units); mark bottom on the baseline; gap between mark and word = half the mark.
- **Stacked:** mark twice the height of the l, centred over the word, gap = half the mark.
- **Clear space:** half the mark on every side. Minimum lockup width: 96 px.

## Colour

| Name | Hex | Use |
|---|---|---|
| Black | `#000000` | Ground |
| Paper | `#ECE7DF` | Text, the arc |
| Stone | `#9A948B` | Secondary text |
| Amber | `#FFB000` | The L, live state |
| Dark amber | `#B86E00` | The L on light backgrounds |
| Fault | `#E8664A` | Errors only |

## Type

IBM Plex Mono for the wordmark, numbers and labels; IBM Plex Sans for running text. Both are free under the SIL Open Font License, which allows using the font in logos and leaves the artwork's licence to us ([OFL FAQ 1.1](https://tug.ctan.org/fonts/gentium/OFL-FAQ.txt)).

## Don't

- Rotate or mirror the mark.
- Close the gaps between the L and the arc.
- Swap the colours of the L and the arc.
- Add glows, shadows or gradients.
