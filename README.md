# Text Blur — Gooey Type Studio

A tiny, dependency-free tool for making a fluid "gooey" wordmark: type that
liquefies and flows under your cursor like merging droplets, with live dials
to control it.

![effect](https://img.shields.io/badge/effect-liquid%20metaball-e2580f)

## Use it

Just open `index.html` in any modern browser. There is no build step.

## Controls

| Control | What it does |
| --- | --- |
| **Text** | The word to render |
| **Font** | A built-in list of common fonts, plus **Use my computer's fonts** (lists every font installed locally — Chrome/Edge only, asks permission once) and **Upload…** (load a `.ttf`/`.otf`/`.woff` file, works in any browser). Heavy/bold fonts melt best |
| **Text colour** | Fill colour of the wordmark |
| **Background** | **None** (transparent, the default) · **Colour** (solid fill) · **Image** (upload your own) |
| **Position X / Y** | Figma-style number fields to place the wordmark |
| **Amount** | How far the liquid spreads — higher merges more letters into one mark |
| **Feather** | How soft the liquid edge is (low = crisp solid blobs, high = softer) |
| **Play** | With Play **off** the whole word melts by *Amount*. With Play **on** the word is crisp until you move your cursor over it — the letters near the cursor liquefy and flow, merging and pulling apart, then settle back as you move away |

Plus a **Surprise me** randomiser and **Download PNG** (exports at 1600 × 2000;
transparency is preserved when the background is *None*).

## How it works

The effect is a **metaball** rendered on a `<canvas>` (no SVG masks), which is
what makes it read as one continuous liquid surface instead of a layer:

1. The glyphs are rasterised to a coverage field, and a blurred copy of that
   field is computed (the spread is the **Amount** dial).
2. Per pixel, the crisp and blurred coverage are **blended** by a smooth
   weight, then **thresholded**. Because the threshold runs *after* the blend,
   the visible edges follow the ink (forming merged blobs) rather than any
   blend boundary — so there is no mask/spotlight look.
3. In Play mode the blend weight is a soft falloff that follows the cursor,
   plus animated value-noise so the liquid edges wobble and flow. The
   influence fades in and out with the cursor ("comes and goes").

Everything is one self-contained file with no dependencies or build step.
