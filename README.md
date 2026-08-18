# Fire Button

An animated "GET IN TOUCH" button on a white page — dark pill in a red-to-amber
gradient frame, with two fires burning at the bottom corners. Single
self-contained `index.html`: no build, no dependencies, no network calls
(the pixel font is inlined).

Open `index.html` in a browser.

## Design spec

Built from the Figma frames, with 1em = 100 design px so the whole button
scales as one unit:

| Piece | Spec |
| --- | --- |
| Page | `#f5f5f5` (`--page`) |
| Outer frame | 1244 × 335, gradient top `#D84C38` → bottom `#E7983B` |
| Inner frame | 1200 × 327, solid `#371F0F` |
| Fires | ~260 × 260 box, bottom-left and bottom-right corners, in front of the button |

## States

| State | What happens |
| --- | --- |
| Idle | Real animated-emoji fire — seven layers licking, the two sides out of phase. Detaching tongues fade out just above the flame; a few embers drift up |
| Hover / focus | Button lifts with a springy overshoot, the grounding shadow grows, fires and glow intensify, sheen sweeps the face, arrow slides right, all embers release |
| Press | Button depresses under the pointer and the shadow tightens beneath it; releasing springs it back past its resting point |
| Click | The arrow launches off to the right and returns from the left, fires turn fierce — the flame timeline runs ~3x for a beat, both fires swell, the face flashes, and burning bits spill out and fall away to the left and right |

Keyboard focus (`Tab`) gets the same treatment as hover, plus a visible focus ring.

## Customizing

Colors live in `:root`; size is one value on `.fire-btn`:

```css
:root {
  --ring-top: #d84c38;     /* outer frame gradient, 0%   */
  --ring-bottom: #e7983b;  /* outer frame gradient, 100% */
  --face: #371f0f;         /* inner frame                */
}

.fire-btn { font-size: min(calc(780px / 12.44), calc((100vw - 16px) / 15.34)); }
```

Change `780px` to render the button larger or smaller — padding, radius, ring,
fires and ember travel all follow. Label text lives in `.label`; flame speed is the `dur` on the `<animate>`
elements inside each fire (2.6s per loop). Ember drift, and the click spill's
size, spread and fall, are set in the script at the bottom of the file.

## Notes

- `prefers-reduced-motion: reduce` keeps the visual design but stops every loop.
- Fire: keyframes baked from Google's [Noto animated emoji](https://googlefonts.github.io/noto-emoji-animation/) (CC BY 4.0), resolved to flat SVG paths — no runtime library. `fire-emoji-frames.svg` is the standalone flame.
- Font: [Silkscreen](https://fonts.google.com/specimen/Silkscreen) by Jason Kottke, SIL Open Font License 1.1, embedded as base64 woff2.
