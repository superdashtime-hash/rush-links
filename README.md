# Rush Links — Speed Golf

A 3D arcade speed-golf game that runs entirely in the browser (one `index.html`, Three.js loaded from a CDN). No build step.

**Play it:** https://superdashtime-hash.github.io/rush-links/

## Play locally
Open `index.html` in a modern browser (Chrome, Edge, Firefox). If your browser blocks it from `file://`, serve the folder with any static server.

## Deploy to GitHub Pages
1. Create a new GitHub repository (for example `rush-links`).
2. Upload `index.html` (and this README) to the root of the `main` branch.
3. In the repo, go to **Settings → Pages**, set **Source** to *Deploy from a branch*, branch `main`, folder `/ (root)`, and save.
4. After a minute the game is live at `https://<your-username>.github.io/rush-links/`.

Or from a terminal:
```bash
git init && git add index.html README.md && git commit -m "Rush Links"
git branch -M main
git remote add origin https://github.com/<your-username>/rush-links.git
git push -u origin main
```

## Courses
Pick a course on the title screen. Each has 5 holes; **Grand Tour** plays all 25.

**🌳 Greenvale** (meadow, autumn, desert)
1. Meadow Run (par 4): raised green, pond left, a hoop over the pond corner and a boost strip short of the green.
2. Lakeside Leap (par 3): carry over a lake, with a hoop above it.
3. Dragon Dogleg (par 5): elevated tee, two-lake dogleg, and an island fairway in the first lake as a shortcut.
4. Maple Island (par 3): island green reached by a wooden bridge.
5. Sunset Dunes (par 5): waste bunkers, sandstone pillars, oasis, plateau green.

**🌴 Coral Coast** (tropical: palms, turquoise water)
1. Stepping Stones (par 4, new): a lagoon across the fairway with two island fairways to lay up on, a footbridge, and a hoop.
2. Lagoon Carry (par 3): elevated tee over a huge lagoon.
3. Coconut Corridor (par 5): narrow snaking fairway between two ponds, with boost strips and a hoop.
4. Reef Island (par 3): island green with a bridge.
5. Blowhole Bay (par 4, new): spring "blowholes" on the dogleg fling your ball (and you) toward the cove.

**❄️ Frostpine Peaks** (snow: falling snow, snow-capped pines)
1. Glacier Drop (par 3): 28 m downhill tee shot past an ice spire.
2. Frozen Fork (par 4, redesigned): a frozen lake you can play off. Balls skid across it, and open water waits beyond.
3. Avalanche Alley (par 5): downhill-uphill rollercoaster with ice seracs in the landing zone.
4. Twin Ice Lakes (par 4, dusk, redesigned): one lake is frozen and one is open water. Pick your side, and thread the hoop between them.
5. Ski Jump Summit (par 4, new): boost strips up the slope, a frozen pond, a spring, and spires guarding the summit green.

**🏜️ Canyon & Maple** (desert and autumn)
1. Hoodoo Pass (par 4, new): a slalom of red-rock pillars in the landing zone. Shape it around them.
2. Mesa Hop (par 3): carry the sand to a high mesa green, with gate pillars and a spring at the foot of the mesa.
3. Harvest Hollow (par 5): double dogleg through an autumn valley, with a hoop at the corner.
4. Maple Mirror (par 4, dusk, redesigned): a lake with an island fairway in the middle, a hoop above it, and a bridge.
5. Canyon Climb (par 5): long desert finale from a high tee to a plateau, with pillars and a boost strip.

**🎢 Rush Park** (new stunt course)
1. Launch Pad (par 4): boost strips, a high hoop, and twin springs that launch rolling drives.
2. Hoop Dreams (par 3): three hoops over a lake.
3. Sweeper Green (par 4): rotating sweeper bars guard the fairway and the green. Fly it in with backspin.
4. Pinball Alley (par 5): a field of springy bumpers, boost strips and springs.
5. Grand Finale (par 4): boosts, a sweeper, springs, hoops, and an island green.

## Course features
| Feature | Ball | Runner |
|---|---|---|
| 🟠 Spring pad | Launches the ball high; spin applies again on the next landing | Super jump |
| 💨 Boost strip | Speeds up a rolling ball along the arrows | Short speed boost |
| 🟡 Hoop | Fly through for +35% special meter (and −4 s in Speed Golf) | — |
| ⚠️ Sweeper | Rotating bar swats low or rolling balls | Knocks you down; jump over it |
| 🪨 Pillar / bumper | Deflects the ball (bumpers add extra bounce) | Blocks you (bumpers bounce you) |
| 🧊 Ice | Balls skid a long way; spin barely grips | You slide with momentum |
| 🏝️ Island fairway | Safe landing spot in the middle of a lake | — |

## Spin
- **Spin dial** (at your ball): `W`/`S` for top/backspin and `Z`/`X` for draw/fade. A tap moves it 25%; hold to sweep. `R` resets it. You can also click or drag the ball widget in the shot panel. The preview line shows the real curve, the landing ring, and a cyan ring where the ball will stop.
  - Backspin flies higher, lands softer, and checks or zips back on greens.
  - Topspin flies lower and runs out.
  - Draw/fade bends the flight and kicks the first bounce sideways. Long clubs bend more.
  - How much spin you get depends on your golfer's Control stat and your lie: the rough cuts it about in half, sand cuts it more (except with the sand wedge), and ice reduces it slightly.
- **Strike quality**: lock power in the green band (96–100%) for a PERFECT strike (+15% spin). Overswing gives extra distance, but the spin goes wild.
- **Spin Tap**: once per shot, while your ball is in the air before its first bounce, press `Z`/`X` to bend it left or right, `Q` to brake (add backspin), or `E` to release (add topspin). This works in both modes, even while you're running in Speed Golf.

## Modes
- **Speed Golf**: you and two AI rivals play at the same time. Run to your ball, dash, bump rivals, and use special shots. Score = time + 30 s per stroke.
- **Stroke Play**: classic golf. You're moved to your ball after each shot.

Rival skill (Easy / Normal / Hard) is chosen on the title screen.

## Online play (Firebase)
Press **🌐 ONLINE** on the title screen. One player creates a room and shares the 4-letter code (or the invite link); 2–4 players race Speed Golf together. Dash bumps and special-shot shockwaves hit other players too. The host picks the course and moves everyone to the next hole.

Online play uses a free Firebase Realtime Database:
1. Go to console.firebase.google.com, create a project, then **Build → Realtime Database → Create database**.
2. In the database **Rules** tab, paste this and publish:
   ```json
   { "rules": { "rooms": { "$code": { ".read": true, ".write": true } }, ".read": false, ".write": false } }
   ```
   Anyone with your page can create and join rooms. Nothing else in the database is readable.
3. **Project settings → Your apps → Web app (`</>`)**, then copy the `firebaseConfig` object.
4. Paste it into `const FIREBASE_CONFIG=null;` in `index.html` (replace `null` with the object), commit, and push. Everyone who opens your GitHub Page can then play online. To try it without editing the file, paste the config in the game under **🌐 ONLINE → Firebase setup**; that is saved only in your browser.

Firebase web config values are not secrets. Access is controlled by the rules above.

To test online play without Firebase, open `index.html?net=local` in two tabs of the same browser.

## Controls
| Action | Keys |
|---|---|
| Run / dash | `W A S D` / hold `Shift` (uses stamina) |
| Camera | Mouse drag, `←` `→`, `R` to face your ball |
| Address ball / jump | `Space` at your ball to address it; anywhere else it jumps. Jumping dodges bumps and special-shot shockwaves |
| Aim / club | `A` `D` (hold `Shift` for fine aim), `Q` `E` |
| Spin dial | `W` `S` top/backspin, `Z` `X` draw/fade, `R` reset, or click/drag the spin ball in the shot panel |
| Swing | `Space` to start the meter, `Space` to lock power. The green band is a PERFECT strike |
| Spin Tap | While your ball is in the air, once per shot: `Z` `X` bend, `Q` brake, `E` release |
| Overswing | Lock above the white line for extra distance, with a risk of a wild curve |
| Special shot | `F` when the meter is full. Ignores wind and stuns rivals where it lands |
| Landing view | Hold `C` |
| Leave ball | `Esc` while addressing (Speed Golf) |
| Pause menu | `P`, `Esc`, or the ⏸ button: resume, restart hole, graphics, music, controls, quit |
| Music | `M` |
| Graphics quality | `G` toggles High (bloom, color grading, full grass) and Fast. The choice is remembered |

Coins refill stamina and charge your special meter. Water and out of bounds cost one penalty stroke.
