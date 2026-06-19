# Text Blur — Gooey Type Studio

A tiny, dependency-free tool for making the "gooey" blurred-wordmark effect:
white type that melts and morphs over a soft colour blob, with **dials** to
control everything live.

![reference vibe](https://img.shields.io/badge/effect-gooey%20blur-e2580f)

## Use it

Just open `index.html` in any modern browser. There is no build step.

## Controls

| Control | What it does |
| --- | --- |
| **Text** | The word to render |
| **Text colour** | Fill colour of the wordmark |
| **Background** | **None** (transparent, the default) · **Colour** (solid fill) · **Image** (upload your own) |
| **Position X / Y** | Figma-style number fields to place the wordmark |
| **Amount** | Gaussian blur strength — higher melts letters together |
| **Feather** | Softens the gooey threshold; low = crisp blob edges, high = soft glow |
| **Play** | Animates the effect: hover the canvas and the blur drifts toward your cursor, then breathes when still (like the reference clip) |

Plus a **Surprise me** randomiser and **Download PNG** (exports at 1600 × 2000;
transparency is preserved when the background is *None*).

## How it works

The morphing look is the classic SVG *gooey* filter:

1. `feGaussianBlur` spreads the glyphs (the **Amount** dial).
2. `feColorMatrix` sharpens the alpha channel back into a hard edge — the
   contrast of that step is the **Feather** dial (full contrast = crisp
   gooey blob, no contrast = soft feathered glow).
3. `feComposite … atop` lays the original crisp text over the goo so the
   centres stay readable while the edges merge.

The blob is a blurred radial gradient and the paper grain is `feTurbulence`,
so the whole thing is a single self-contained SVG that rasterises cleanly on
export.
