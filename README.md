# Joust

A browser-playable, Joust-inspired arcade game built with the Canvas API and a pixel-art sprite sheet. It runs directly from `index.html` without a build step or external runtime dependencies.

## Play

Keep `index.html` and `joust-spritesheet.png` in the same directory. Open `index.html` directly in a browser, or run a local server:

```sh
python3 -m http.server 8000
```

Then visit <http://localhost:8000/>.

## Controls

- **Left / Right arrows**: steer and build horizontal momentum
- **Up arrow**: flap upward

The arena wraps horizontally. Gravity pulls birds down when they are not flapping. Enemy combat is decided by height; an exact-height tie makes both birds bounce away.

## Waves and enemies

- Enemy mounts materialize at four glowing pads: the upper-middle platform, left-middle platform, right-middle platform, and lower-right ground. A pad is unavailable while the player is standing on it; the queued enemy uses another pad. Wave layouts remove platforms in stages, while Egg Waves restore the platform layout.
- The first waves use these counts: Wave 1 has 3 Bounders; Wave 2 has 4 Bounders; Wave 3 has 6 Bounders; Wave 4 has 3 Bounders and 3 Hunters; Wave 5 is an Egg Wave; Wave 6 has 3 Bounders and 3 Hunters; Wave 7 has 2 Bounders and 4 Hunters; Wave 8 has 6 Hunters and an immediate Pterodactyl; Wave 10 is an Egg Wave; Wave 12 is the last Bounder wave (2 Bounders and 6 Hunters); Wave 13 has 7 Hunters and an immediate Pterodactyl; Wave 15 is an Egg Wave; Wave 16 has 5 Hunters and 1 Shadow Lord; Wave 18 has 5 Hunters, 1 Shadow Lord, and 2 Pterodactyls; Wave 20 is an Egg Wave.
- Counts for unlisted waves between the listed milestones grow gradually. Wave 12 is the final wave with Bounders. Hunters and Shadow Lords increase after Wave 16; standard waves from Wave 37 onward contain only Shadow Lords. From Wave 60, eggs also hatch into Shadow Lords.
- Early waves send enemies one at a time with about a 2–3 second gap. Wave 20 onward uses pairs, and Wave 40 onward can send four at a time. The game allows up to 24 active enemy riders so those later wave sizes can appear without an old spawn cap.
- A defeated enemy drops an egg. If it is not collected, it hatches into a foot rider. A riderless enemy bird attempts a platform-aware pickup, then returns as the next enemy tier.
- Every fifth wave is an Egg Wave with 12 eggs placed on platforms. It clears when all enemy mounts, eggs, and hatchlings are gone. Pterodactyls then leave the arena. Clearing Wave 2 awards a 3,000-point survival bonus.
- On standard waves, a Pterodactyl arrives after 36 seconds; additional ones arrive every 30 seconds, up to three. Pterodactyl waves begin at Wave 8 and repeat every fifth wave after that. A precise lance hit to its mouth sends it away; otherwise it is dangerous to touch.

## Environmental hazards

- Waves 1–2 have a safe floor. Lava is exposed from Wave 3 and contact is fatal, while the bottom platform remains solid over it. The Lava Troll becomes active in Wave 4 and reaches farther as waves progress.
- Platform 3 disappears in Wave 6; platforms 1–3 are gone by Wave 7. By Wave 14 the upper and middle platforms have been removed, leaving the lower ledge and ground. Egg Waves restore the platforms; the bottom platform keeps its collision throughout.

## Scoring

- Bounder: 500 points; Hunter: 750; Shadow Lord: 1,500.
- Eggs award 250, 500, 750, then 1,000 points for each later egg caught. Catching an egg before it lands adds 500 points.
- Losing a player life subtracts 50 points, to a minimum of zero.

## Sprite notes

The sheet includes red, gray, and blue mounted rider cels and separate foot-rider sprites. The game reuses the red rider's walking and flying animation and recolors only the helmet pixels for gray and blue riders, preserving the ostrich animation and body colors. The Pterodactyl uses the flight cels from row 10 and the sizzling fade cels from row 11.

## Files

- `index.html` — game logic, controls, wave progression, and rendering
- `joust-spritesheet.png` — arena background and sprite atlas
