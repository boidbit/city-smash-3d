# City Smash 3D

A fast, casual 3D monster-rampage game built with [Three.js](https://threejs.org/). Grow bigger by smashing buildings, dodge helicopter gunfire, and smash every building in the city before the timer runs out to reach the next level.

## Intro

Pressing **Start** plays a short skippable intro (once per launch) as one continuous camera move: a person's view from a building window as the monster arrives, then out to a helicopter and the pilot's cockpit view, then down into the game.

## Levels

- Level 1: 106 buildings, 90 seconds. Clear the whole city to unlock the next level (progress is saved).
- Each level has 2.5% more buildings and 2.5% more helicopter pressure, plus 2 extra seconds.
- The monster starts each level 1% bigger and stronger (0.4% per level after level 10).
- The city's look changes every 5 levels: Sunset City, Sunny Day, Night Lights, Snow Day (then repeats).
- Win with 8+ seconds left for 2 stars, 15+ seconds left for 3 stars.

All of these numbers are constants near the top of the `levels` section in `index.html`.

**[Play it in your browser](https://talibmohd0099.github.io/city-smash-3d/)**

## Monster Dash mode

The start screen also offers **Monster Dash**, an endless 3-lane runner with the same monster, city and helicopters. Swipe (or A/D, ←/→) to change lanes and SMASH! towers and helicopters. See [`monster-dash/README.md`](monster-dash/README.md).

## Controls

- **Touch:** drag anywhere to move, tap **SMASH!** to slam the ground
- **Keyboard:** WASD / arrow keys to move, Space to slam

## Project structure

- `index.html` / `www/index.html` — the game itself (single self-contained HTML file)
- `monster-dash/index.html` / `www/monster-dash/index.html` — the Monster Dash mode (also a single self-contained HTML file)
- `android/` — the Capacitor-generated Android project
- `.github/workflows/build-apk.yml` — builds a signed release APK and Play Store AAB

## Getting the APK / AAB

Every push to `main` builds a signed release APK (published on the [Releases page](https://github.com/boidbit/city-smash-3d/releases)) and a Play Store AAB.

To make a build for the Play Store: **Actions → Build Release (APK + AAB) → Run workflow**, enter the version name (e.g. `1.2.0`) and, optionally, the version code (leave blank to use the run number), then download the `city-smash-3d-<version>-aab` artifact from the finished run and upload it in Play Console.

Signing needs these repository secrets: `KEYSTORE_BASE64`, `KEYSTORE_PASSWORD`, `KEY_ALIAS`, `KEY_PASSWORD`.

### Building locally

```bash
npm install
cp index.html www/index.html
mkdir -p www/monster-dash && cp monster-dash/index.html www/monster-dash/index.html
npx cap sync android
cd android
./gradlew assembleDebug
```

The APK will be at `android/app/build/outputs/apk/debug/app-debug.apk`.

## Editing the game

All City Smash code lives in `index.html`, and all Monster Dash code lives in `monster-dash/index.html`. After making changes, copy them into `www/` (as in the build steps above) before syncing Capacitor (the GitHub Actions workflow does this automatically).
