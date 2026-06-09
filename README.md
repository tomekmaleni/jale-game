# Jale Bonk

A tiny browser game built from a night-time clip of Jale. Move his head up and
down to line up with the incoming balls, **hold** to charge his smile, then
**release** to tilt his head and bonk them with his nose. A bigger smile reaches
further. Miss three and it's over.

## Play

Open `index.html` in a browser, or play the hosted version on GitHub Pages.

- **Mouse:** move to aim, hold left button to charge, release to tilt
- **Touch:** drag to aim, hold to charge, release to tilt
- **Keyboard:** Up/Down to aim, hold Space to charge, release to tilt

## How it's made

The character and background are real frames pulled from
`assets/WhatsApp Video 2026-06-05 at 22.36.47.mp4`:

- `img/head_01.jpg … head_18.jpg` — Jale's head across the smile-and-tilt motion,
  cropped, brightened, and feathered at runtime so it blends into the scene.
- `img/bg.jpg` — a darkened, blurred frame used as the backdrop.

Everything else is a single self-contained `index.html` (HTML canvas + vanilla JS,
no dependencies, no build step).

### Re-extracting frames

With `ffmpeg` installed:

```bash
# head sprite sequence (18 frames)
ffmpeg -i "assets/WhatsApp Video 2026-06-05 at 22.36.47.mp4" \
  -vf "fps=1.74,crop=360:360:90:330,eq=brightness=0.20:contrast=1.32:saturation=1.1,scale=320:320" \
  -frames:v 18 img/head_%02d.jpg

# background
ffmpeg -ss 0.5 -i "assets/WhatsApp Video 2026-06-05 at 22.36.47.mp4" -vframes 1 \
  -vf "eq=brightness=0.06:contrast=1.1,gblur=sigma=8,eq=brightness=-0.12,scale=540:-1" img/bg.jpg
```
