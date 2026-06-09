# Jale Bonk

A tiny browser timing game built from a night-time clip of Jale. His head loops
from neutral into a big grin and back, over and over. Click at the exact moment
his grin is fullest — the closer you nail the peak, the flashier the rank
(GOOD → GREAT → EPIC → LEGENDARY) and the bigger the score. Miss it badly and you
lose a life. It keeps getting faster.

## Play

Open `index.html` in a browser, or play the hosted version on GitHub Pages:
https://tomekmaleni.github.io/jale-game/

- **Mouse / touch:** click or tap at the peak of the grin
- **Keyboard:** Space (or Enter) at the peak

## How it's made

The animation frames are pulled straight from
`assets/WhatsApp Video 2026-06-05 at 22.36.47.mp4`:

- `img/jale_01.jpg … jale_21.jpg` — Jale going from a neutral pose into a grin
  (the clip from ~t=4s to ~t=8.8s), brightened and centered.

The game eases a sine "ping-pong" through those frames so the grin builds and
relaxes; your click is scored on how close the grin was to its fullest frame.
Everything is a single self-contained `index.html` (HTML canvas + vanilla JS,
no dependencies, no build step). Sounds are synthesized with the Web Audio API.

### Re-extracting frames

With `ffmpeg` installed:

```bash
ffmpeg -ss 4.0 -i "assets/WhatsApp Video 2026-06-05 at 22.36.47.mp4" -t 4.8 \
  -vf "fps=4.4,eq=brightness=0.20:contrast=1.32:saturation=1.1,scale=432:-1" \
  img/jale_%02d.jpg
```
