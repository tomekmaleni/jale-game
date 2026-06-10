# Jale Goblin Climb

A tiny browser platformer where Jale is a little goblin (the night-clip footage is
his head + body; pixel legs are added). Climb a procedurally generated **closed
maze** of dirt corridors to the portal at the top of each level. **Bonk** enemies
with your head to splat them; touch one without bonking and you lose a life.
Collect every gem to open the portal. Score for kills and cleared levels — and it
gets taller and busier each level.

## Play

https://tomekmaleni.github.io/jale-game/ — or open `index.html`.

- **Desktop:** ◀ ▶ move · **Space** jump · **Right Ctrl** bonk (remappable in *Controls*; WASD/J also work)
- **Mobile:** on-screen D-pad (left) + BONK button (right)

## Levels & progression

Four levels. 1–3 are procedurally generated mazes that get taller and busier; **level 4 is the final boss** — a floating one-eyed tentacled kraken with tentacle, laser, and minion-spawn attacks.

Enemies (each worth different points on a bonk kill):

- **Patrol** — walks its floor segment; the basic enemy, all levels.
- **Red cyclops (shooter)** — turret that fires aimed shots on sight. Appears on **levels 3+**.
- **Blue ghost** — wakes when you come near, then flies through walls to chase. Appears on **levels 2+**.

After each cleared level you pick **one** free upgrade in the shop. Always available: more speed, more bonk range, faster attacks (and heart restore if hurt). Conditional:

- **Drop-through** (press Down to fall through a platform) — offered after clearing **levels 2 and 3**.
- **Projectile weapon** (bonking also fires a shot) — offered after clearing **level 3**.

Upgrades and the enemy/ability collection persist between games (localStorage).

## How it's made

- `img/jale_01..32.jpg` — frames from `assets/WhatsApp Video 2026-06-05 at 22.36.47.mp4`.
  1–16 are the neutral→smile idle loop; 17–32 are the smile→tilt the head plays when
  you bonk.
- The **video is drawn smoothly**; everything else (dirt floors/walls, enemies,
  gems, legs) is rendered into a low-res buffer and upscaled for a **pixel-art** look.
- Levels are solid floors (one staggered gap each) with thick jumpable dirt walls,
  generated and **verified solvable** before play. Single self-contained `index.html`
  (canvas + vanilla JS, no dependencies). Sounds are synthesized with Web Audio.

### Re-extracting frames

```bash
ffmpeg -ss 0.6 -i "assets/WhatsApp Video 2026-06-05 at 22.36.47.mp4" -t 6.2 \
  -vf "fps=2.58,crop=340:655:10:355,eq=brightness=0.24:contrast=1.4:saturation=1.15,scale=150:-1" \
  -frames:v 16 img/jale_%02d.jpg
ffmpeg -ss 6.9 -i "assets/WhatsApp Video 2026-06-05 at 22.36.47.mp4" -t 1.8 \
  -vf "fps=8.9,crop=340:655:10:355,eq=brightness=0.24:contrast=1.4:saturation=1.15,scale=150:-1" \
  -frames:v 16 img/tilt_%02d.jpg   # then renamed jale_17..32
```
