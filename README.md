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

- One enemy rider enters at the start. A replacement arrives 1 second after an enemy rider is defeated. If no enemy is defeated, another enemy appears every 50 seconds. Enemies enter from a randomly chosen side at a varied height; about two-thirds are green birds with red riders. At most 10 active or dying enemy riders are kept at once, with one slot reserved for a rescued hatchling; spawns wait when the limit is reached.
- Birds wrap around the left and right edges of the arena. Platforms have solid sides and undersides; the middle platform can be crossed while walking.
- In a player/enemy collision, the higher bird wins and an equal-height tie favors the player. Equal-height enemy collisions are resolved at random.
- The game continues after the player is defeated. Each death costs 50 points, down to a minimum score of 0.
- Defeating a Bounder (red rider) is worth 500 points. Defeating a Hunter (gray/silver rider) is worth 750 points. The 1,500-point Shadow Lord reward is reserved for a future blue-rider enemy type. Stomping a hatched rider awards the points for that rider's enemy type.
- Eggs caught by the player are worth 250, 500, 750, then 1,000 points for the fourth and every later egg. Catching one before it lands adds a 500-point bonus. Egg order continues through the endless run and resets when the page is reloaded. If left alone, an egg hatches after a short delay into a rider on foot. An egg that falls into the bottom void is destroyed and queues another enemy spawn.
- A riderless enemy bird seeks hatched riders to pick them up. The player can stomp a hatchling for the points awarded to that rider's enemy type before it is rescued.
- A rescued hatchling can return to play as an enemy rider.

## Files

- `index.html` — game, rendering, controls, and gameplay logic
- `joust-spritesheet.png` — arena background and sprite atlas
