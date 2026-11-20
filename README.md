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
Pick a course on the title screen. Each has 5 holes; **Grand Tour** plays all 20.

**🌳 Greenvale** (meadow, autumn, desert)
1. Meadow Run (par 4): raised green, pond left.
2. Lakeside Leap (par 3): carry over a lake.
3. Dragon Dogleg (par 5): elevated tee, two-lake dogleg.
4. Maple Island (par 3): island green reached by a wooden bridge.
5. Sunset Dunes (par 5): waste bunkers, cacti, oasis, plateau green.

**🌴 Coral Coast** (tropical: palms, turquoise water)
1. Palm Paradise (par 4): gentle S-bend past a lagoon.
2. Lagoon Carry (par 3): elevated tee over a huge lagoon.
3. Coconut Corridor (par 5): narrow snaking fairway between two ponds.
4. Reef Island (par 3): island green with a bridge.
5. Sunset Shores (par 4): dogleg left around the water.

**❄️ Frostpine Peaks** (snow: falling snow, snow-capped pines, icy ponds)
1. Glacier Drop (par 3): 28 m downhill tee shot.
2. Frozen Fork (par 4): a pond splits the fairway; lay up or carry.
3. Avalanche Alley (par 5): downhill-uphill rollercoaster.
4. Twin Ice Lakes (par 4, dusk): lakes on both sides.
5. Summit Finale (par 4): uphill to a raised summit green.

**🏜️ Canyon & Maple** (desert and autumn)
1. Red Rock Run (par 4): big waste bunkers, raised green.
2. Mesa Hop (par 3): carry the sand to a high mesa green.
3. Harvest Hollow (par 5): double dogleg through an autumn valley.
4. Maple Mirror (par 4, dusk): drive over a lake.
5. Canyon Climb (par 5): long desert finale from a high tee to a plateau.

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
| Swing | `Space` to start the meter, then lock power with `Space` (normal), `W` (topspin) or `S` (backspin). Add `Shift` for super spin |
| Curve | Hold `A` or `D` while locking power |
| Overswing | Lock above the white line for extra distance, with a risk of a wild curve |
| Special shot | `F` when the meter is full. Ignores wind and stuns rivals where it lands |
| Landing view | Hold `C` |
| Leave ball | `Esc` while addressing (Speed Golf) |
| Pause menu | `P`, `Esc`, or the ⏸ button: resume, restart hole, graphics, music, controls, quit |
| Music | `M` |
| Graphics quality | `G` toggles High (bloom, color grading, full grass) and Fast. The choice is remembered |

Coins refill stamina and charge your special meter. Water and out of bounds cost one penalty stroke.
