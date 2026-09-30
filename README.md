# Fourier 1

**A seed-based generative system for layered parametric curve compositions.**

A catalogue of computational textile compositions for fashion, textile and surface design — algorithmically drawn, seed-documented, and ready for production.

---

## Overview

Fourier 1 is a generative design system rather than a single artwork. Each composition is layered in three passes: a tree of filled circles clipped inside a circle, a tree of branch lines clipped outside the same circle, and a luminous parametric curve drawn over both. The result is a dense, layered field that reads as both astronomy and botany.

The system is designed for:

- **Fashion houses** adapting parametric ornament for apparel and accessories
- **Textile studios** developing repeat patterns and yardage
- **Surface designers** working across print, wallpaper, and interior applications

Every composition can be licensed, adapted, or commissioned to a brief.

---

## Concept

A curve, when it is *summed from sines*, becomes a harmony — periodic, precise, quietly yours.

The parametric curve — summed from layered sines and cosines — has always carried the structure of ornament. From the Fourier series that decomposes any periodic motion into pure tones, to the geometric curves of a Persian garden plan, harmony is one of the oldest systems of mathematical beauty we have. Fourier 1 translates that harmony into code. Each composition begins with a palette and a set of harmonic frequencies, and unfolds through recursion, clipping, and summation, until the frame fills with a luminous field.

The palette, the tree structures, the curve frequencies, and the harmonic terms are all derived from a single numeric seed.

Like the other still volumes in this series (Girih, Arachne, Celestial Grove, ChaotiColor, Citrus Mosaic, Crazy Knight Curve, Crazy Knight Line, Crazy Letter, cyPollock, Digital Pollen, Draconic Fractals, Dreamscape Watercolors, Elliott Waves, Ellipses, Enigma Sudoku, Ephemeral Whirls, Eyes), **Fourier 1 is a static composition.** The plate, the framed plate, the surfaces, and the archive are all static frames. A harmony is something you read; its character is stillness, not motion.

---

## Features

- **Seed-based generation** — every composition is defined by a numeric seed and can be regenerated exactly
- **Deterministic output** — the same seed always produces the same composition
- **Three layered passes** — a circle tree, a branch tree, and a parametric curve
- **Ring-clipped circle tree** — filled circles drawn inside a central ring clip
- **Inverse-clipped branch tree** — branch lines drawn outside the same ring clip
- **Parametric curve** — a luminous closed curve traced from four sines and four cosines
- **Harmonic period** — the curve's total period is the LCM of all eight frequencies, so the curve closes exactly
- **Sixteen-colour palette** — four colour arrays (dark backgrounds, light backgrounds, hot foregrounds, cool foregrounds)
- **Glow effect** — the parametric curve carries a soft shadow, giving it a luminous quality
- **Adaptive surfaces** — one seed applied across print, scarf, textile, and wall formats
- **Archive** — eight curated seeds available for immediate loading
- **Download** — export the composition as a high-resolution PNG
- **Keyboard shortcuts** — `R` for new seed, `S` to save

---

## Project Structure

```
.
├── index.html          # Main catalogue page
├── images/
│   ├── fav.svg         # Favicon
│   ├── tote.png        # Mockup: tote bag
│   ├── tee.png         # Mockup: t-shirt
│   └── cushion.png     # Mockup: cushion
└── README.md
```

---

## How It Works

### The Seed

A numeric seed (a large integer) initializes a deterministic pseudo-random generator. From this seed, the system derives:

- Four colours from the dark background palette
- Two colours from the light background palette
- Two colours from the hot foreground palette
- One colour from the cool foreground palette
- Eight harmonic frequencies for the parametric curve (A1[0..3] and A2[0..3], each 1–7)
- Four amplitude coefficients (B1[0..2] and B2[0..2])
- Six weighting constants (C1[0..2] and C2[0..2])

Because the generator is deterministic, the same seed always produces the same composition — on any device, at any time.

### The Circle Tree (Layer 1)

The first layer is a recursive tree of filled circles, drawn from the centre of the frame:

1. Starting at the centre, a circle is drawn at the current position with a random radius derived from a base `radius` value.
2. The tree branches: between 1 and 4 sub-branches, each rotated by a random angle, each starting at the endpoint of the parent.
3. The recursion stops at a fixed depth (8 levels).

This entire layer is **clipped inside a ring** — a circle of `w / 3` radius centred on the frame. So the tree of circles only appears in the centre of the composition, not spilling to the edges.

### The Branch Tree (Layer 2)

The second layer is a recursive tree of branch lines, drawn from the same centre:

1. Starting at the centre, a straight line is drawn from the current position to an endpoint.
2. The tree branches: between 1 and 5 sub-branches, each rotated by a random angle.
3. The recursion stops at a fixed depth (12 levels).

This entire layer is **clipped outside the same ring** — a rectangle of the full frame minus the central circle. So the branch tree appears only in the outer band of the composition, wrapping around the circle tree.

### The Parametric Curve (Layer 3)

The third layer is a single luminous closed curve, traced from summed sines and cosines:

```
x(T) = cx + R/B1[0] · sin(T/A1[0]) + C1[0]·R/B1[1] · sin(T/A1[1]) + C1[1]·R/B1[2] · sin(T/A1[2]) + C1[2]·R/6 · cos(T/A1[3])
y(T) = cy + R/B2[0] · cos(T/A2[0]) + C2[0]·R/B2[1] · cos(T/A2[1]) + C2[1]·R/B2[2] · cos(T/A2[2]) + C2[2]·R/6 · sin(T/A2[3])
```

where `T` is the parameter, `R` is the curve radius, and the `A`, `B`, `C` values are drawn from the seed.

The curve is sampled from `T = 0` to `T = 2·LCM(A1 ∪ A2)·π`, so the curve closes exactly. The result is a dense, flower-like parametric figure that overlaps both the circle tree and the branch tree.

### The Colours

Four palettes meet in every composition:

| Palette                 | Role                       |
|-------------------------|----------------------------|
| Dark backgrounds        | Circle-tree inner colour, branch-tree inner colour |
| Light backgrounds       | Circle-tree outer colour, branch-tree outer colour |
| Hot foregrounds         | Parametric curve stroke    |
| Cool foregrounds        | Parametric curve glow      |

The result is a layered composition: dark branches on the outside, light circles on the inside, and a luminous curve running through both.

### The Surfaces

The same seed is rendered across four surface formats. These are static frames — they represent the print-ready composition.

| Surface  | Aspect | Material          |
|----------|--------|-------------------|
| Print    | 1 : 1  | Cotton rag        |
| Scarf    | 3 : 1  | Twill silk        |
| Textile  | 4 : 3  | Fabric yardage    |
| Wall     | 2 : 3  | Wallpaper         |

Each surface uses the same underlying seed and structural logic — only the repeat, orientation, and scale change.

### Stillness

Like the rest of the still volumes, Fourier 1 does not animate. The plate is a single frozen frame — the composition is complete the moment it is generated.

This is a deliberate design choice. A harmony is not a swarm. It is not a rotation. It is a summed curve, drawn once and left. Its stillness is what makes it print-ready in the strictest sense: what you see is what you get.

---

## Usage

### In the browser

1. Open `index.html` in any modern browser.
2. Click **New Seed** to generate a new composition.
3. Click **Download** to save the composition as a PNG.
4. Scroll to the **Archive** section and click any plate to load it into Plate 001.

### Keyboard shortcuts

| Key | Action          |
|-----|-----------------|
| `R` | New seed        |
| `S` | Save as PNG     |

### Reproducing a composition

Each composition is identified by an 8-digit seed label displayed in the metadata panel. To reproduce a specific composition, note the seed and regenerate it programmatically:

```js
const rng = new RandomGenerator(seed);
const features = buildFeatures(rng);
renderComposition(canvas, features, rng);
```

Because the generator is deterministic, this will produce the identical composition on any device.

---

## Technical Notes

- **No build step.** The system is a single HTML file with inline CSS and JavaScript.
- **No dependencies.** All drawing is done with the native Canvas 2D API.
- **Deterministic.** The `RandomGenerator` class uses a xorshift-based PRNG seeded by an integer, so identical seeds produce identical outputs.
- **Static rendering.** Every canvas renders a single frame. There is no animation loop.
- **Feature isolation.** Cover, framed plate, surfaces, and archive thumbnails each derive their own feature set from their own local RNG, without disturbing the main plate's state.
- **LCM-bounded curve.** The parametric curve runs from `T = 0` to `T = 2·LCM(A1 ∪ A2)·π`, so it always closes exactly — no mismatched endpoints.
- **Ring clipping.** The circle tree and branch tree are drawn inside complementary regions of the same ring clip, so their boundaries meet cleanly on the ring of `w/3` radius.
- **Bounded recursion.** The tree recursions have fixed depth limits (8 and 12), so no recursion overflows.
- **Clean shadow exit.** Every `renderComposition` resets `shadowBlur` and `shadowColor` at the end, so the glow from the parametric curve never bleeds into subsequent drawing.
- **Responsive.** The layout adapts from large desktop down to very small mobile devices (tested at 360px viewport width).
- **Accessible.** Supports `prefers-reduced-motion`. Pinch-zoom is enabled.

### Browser support

Tested in current versions of:

- Chrome / Edge
- Firefox
- Safari (desktop and iOS)

---

## Licensing

All Fourier 1 compositions are **seed-documented** and available for licensing across textile, surface, and print applications.

- **Standard licenses** cover single-product production runs.
- **Commercial use, custom editions, or exclusive rights** are available on request.

Each license is issued against a specific seed ID. Regeneration of the same seed produces the identical composition — ensuring reproducibility between artist, studio, and manufacturer.

For licensing enquiries: [reyhanehdaneshdoost@gmail.com](mailto:reyhanehdaneshdoost@gmail.com)

---

## Commission

Fourier 1 is a generative design system, not a fixed artwork. It can be adapted for specific briefs:

| Service     | Description                                                       |
|-------------|-------------------------------------------------------------------|
| Licensing   | Existing seeds from the archive, licensed for production use      |
| Commission  | New compositions designed to your palette, repeat, and product    |
| Systems     | A private generative tool built for your studio's ongoing use     |

To begin a conversation: [reyhanehdaneshdoost@gmail.com](mailto:reyhanehdaneshdoost@gmail.com)

---

## Series

Fourier 1 is part of a computational textile series. Each volume approaches ornament from a different structural angle:

| Volume                     | Structure                    | Motion                     |
|----------------------------|------------------------------|----------------------------|
| Girih 1                    | Islamic geometric            | Static                     |
| Arachne                    | Rotating rings               | Static                     |
| Baroque Me Baby            | Baroque frames               | Static                     |
| Bezier 1                   | Concentric curves            | Static                     |
| Bezier 2                   | Single rotating curve        | Animated (plate)           |
| Brownian Graphe            | Graph networks               | Animated + interactive     |
| Celestial Grove            | Recursive branch trees       | Static                     |
| ChaotiColor                | Cellular automata            | Static                     |
| Citrus Mosaic              | Arc-and-triangle tiles       | Static                     |
| Crazy Knight Curve         | Knight's-tour smooth path    | Static                     |
| Crazy Knight Line          | Knight's-tour gradient       | Static                     |
| Crazy Letter               | Framed wavy lines            | Static                     |
| cyPollock                  | Scattered branch field       | Static                     |
| Digital Pollen             | Noise-driven texture         | Static                     |
| Draconic Fractals          | Tiled dragon curve           | Static                     |
| Dreamscape Watercolors     | Layered watercolor blooms    | Static                     |
| Elliott Waves              | Financial chart              | Static                     |
| Ellipses                   | Concentric elliptical rings  | Static                     |
| Enigma Sudoku              | Playable 9×9 puzzle          | Interactive (plate)        |
| Ephemeral Whirls           | Wandering looper field       | Static                     |
| Eyes                       | Layered iris portrait        | Static                     |
| Fibonacci Fourier          | Harmonic line field          | Animated (plate)           |
| Fixed Wave                 | Wave-equation field          | Animated (plate)           |
| **Fourier 1**              | **Layered parametric curve** | **Static**                 |

The series is designed as a coherent whole — same page structure, same seed logic, same licensing and commission terms — so that each volume can be presented individually or as part of a larger body of work.

---

## Credits

- **Design & Generative System** — Reyhaneh Daneshdoost
- **Typefaces** — Cormorant Garamond · DM Mono
- **Platform** — Reyrove Studio
- **Edition** — Fourier 1, Autumn 2026

### On AI tools

Where technical obstacles were encountered, AI tools were used for debugging and code optimization. Every structural, aesthetic, and conceptual decision remained the artist's own.

---

## Links

- Website — [reyrove.github.io](https://reyrove.github.io/)
- Instagram — [@rey._.rove](https://www.instagram.com/rey._.rove/)
- LinkedIn — [Reyhaneh Daneshdoost](https://www.linkedin.com/in/reyhaneh-daneshdoost-730481160/)
- X — [@reyrove](https://x.com/reyrove)

---

© Fourier 1 · All compositions reproducible by seed · Computational Textile Design