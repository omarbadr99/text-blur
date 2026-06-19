# Text Blur — Gooey Type Studio

A tiny, dependency-free tool for making the "gooey" blurred-wordmark effect:
white type that melts and morphs over a soft colour blob, with **dials** to
control everything live.

![reference vibe](https://img.shields.io/badge/effect-gooey%20blur-e2580f)

## Use it

Just open `index.html` in any modern browser. There is no build step.

## Controls

The effect is driven by four rotary **dials** (drag up/down, scroll to
fine-tune, double-click to reset):

| Dial | What it does |
| --- | --- |
| **Position X / Y** | Nudge the wordmark around inside the blob |
| **Amount** | Gaussian blur strength — higher melts letters together |
| **Feather** | Softens the gooey threshold; low = crisp blob edges, high = soft glow |

Plus a **text** field, six **background** palettes (recolours the blob and
paper), a **Surprise me** randomiser, and **Download PNG** (exports at
1600 × 2000, filters baked in).

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
