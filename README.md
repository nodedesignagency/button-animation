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
| Outer frame | 1244 × 335, gradient top `#D84C38` → bottom `#E7983B` |
| Inner frame | 1200 × 327, solid `#371F0F` |
| Fires | 243 × 243, bottom-left and bottom-right corners, in front of the button |

## States

| State | What happens |
| --- | --- |
| Idle | Flame silhouettes slowly morph — a wave travels up each fire (SMIL path morphing), a few embers rise |
| Hover / focus | Fires grow gently, glow and text shadow intensify, sheen sweeps the face, arrow slides right, button lifts, all embers release |
| Click | One-shot flare: fires swell briefly, the face flashes warm |

Keyboard focus (`Tab`) gets the same treatment as hover, plus a visible focus ring.

## Customizing

Colors live in `:root`; size is one value on `.fire-btn`:

```css
:root {
  --ring-top: #d84c38;     /* outer frame gradient, 0%   */
  --ring-bottom: #e7983b;  /* outer frame gradient, 100% */
  --face: #371f0f;         /* inner frame                */
}

.fire-btn { font-size: min(calc(780px / 12.44), calc((100vw - 44px) / 12.44)); }
```

Change `780px` to render the button larger or smaller — padding, radius, ring,
fires and ember travel all follow. Label text lives in `.label`; flame morph speed is
the `dur` on the two `<animate>` elements inside each fire. Ember
count and spread are set in the script at the bottom of the file.

## Notes

- `prefers-reduced-motion: reduce` keeps the visual design but stops every loop.
- Font: [Silkscreen](https://fonts.google.com/specimen/Silkscreen) by Jason Kottke, SIL Open Font License 1.1, embedded as base64 woff2.
