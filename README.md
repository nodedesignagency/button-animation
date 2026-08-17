# Fire Button

An animated "GET IN TOUCH" button — dark pill, gradient ember ring, and custom
SVG flames licking up both sides. Single self-contained `index.html`: no build,
no dependencies, no network calls (the pixel font is inlined).

Open `index.html` in a browser.

## States

| State | What happens |
| --- | --- |
| Idle | Flames flicker on four desynced clocks, ring gradient drifts, a few embers rise |
| Hover / focus | Fire flares and speeds up, glow and text shadow intensify, sheen sweeps the face, arrow slides right, button lifts, all embers release |
| Click | One-shot flare: flames burst outward, the face flashes hot |

Keyboard focus (`Tab`) gets the same treatment as hover, plus a visible focus ring.

## Customizing

Everything is driven by tokens in `:root` and one font size on `.fire-btn`:

```css
:root {
  --bg: #f2f2f2;          /* page background        */
  --btn-top: #4d2415;     /* face gradient, top     */
  --btn-bottom: #2a1007;  /* face gradient, bottom  */
  --ember-red / --ember-orange / --ember-amber / --ember-gold / --ember-core;
}

.fire-btn { font-size: clamp(15px, 3.6vw, 40px); }
```

The button's padding, corner radius, ring width, flame size and ember travel are
all expressed in `em`, so changing that one `font-size` rescales the whole thing
as a unit. Label text lives in `.label`; flame speed is the `animation-duration`
on `.lick-outer` / `.lick-mid` / `.lick-inner` / `.lick-core`.

Ember count and spread are set in the script at the bottom of the file.

## Notes

- `prefers-reduced-motion: reduce` keeps the visual design but stops every loop.
- Font: [Silkscreen](https://fonts.google.com/specimen/Silkscreen) by Jason Kottke, SIL Open Font License 1.1, embedded as base64 woff2.
