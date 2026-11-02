# Joust

A browser-playable, Joust-inspired arcade prototype built with a single HTML file and a pixel-art sprite sheet. It uses the browser's Canvas API and has no build step or external runtime dependencies.

## Play

Keep `index.html` and `joust-spritesheet.png` in the same directory. You can open `index.html` directly in a browser, or serve the directory locally:

```sh
python3 -m http.server 8000
```

Then visit <http://localhost:8000/>.

## Controls

- **Left / Right arrows**: steer
- **Up arrow or Space**: flap

## How it plays

- The player and up to five enemy riders fly around a multi-level arena. Enemies enter from either side, at varied heights, and use one of two sprite types.
- Birds wrap around the left and right edges of the arena. Platforms have solid sides and undersides; the middle platform can be crossed while walking.
- In a rider collision, the higher bird wins. Equal-height enemy collisions are resolved at random.
- The game continues after the player is defeated. The player loses 1 point per death, down to a minimum score of 0.
- Defeated enemy riders drop an egg that falls toward a nearby platform. Catching an egg is worth 5 points. If left alone, it hatches after a short delay into a rider on foot.
- A riderless enemy bird seeks hatched riders to pick them up. The player can stomp a hatchling for 7 points before it is rescued.
- Defeating an enemy rider is worth 1 point.

## Files

- `index.html` — game, rendering, controls, and gameplay logic
- `joust-spritesheet.png` — arena background and sprite atlas
