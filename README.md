# Heli Rescue

A 3D rescue-helicopter game for young kids (around age 5), made for phones and tablets.

Fly a rescue helicopter over a big world of farms, cities, forests, mountains and coast. Missions pop up one after another: a farmer needs a doctor, hikers are stuck on a mountain, a ship is sinking, campers are lost in the forest. Fly there, winch the people aboard and bring them back to a rescue base. Keep an eye on the fuel gauge and refuel at a base.

Buttons let you change the weather and the time of day, switch the camera, or let the robot pilot fly.

- 🏠 in the corner goes back to the list of all games.

**Play:** https://tb-x.github.io/heli-rescue/

## Play offline (add to Home Screen)

On iPhone or iPad, open the game in Safari, tap **Share → Add to Home Screen**, then open it once from the new icon while online. After that it starts full screen and works without internet. Changes arrive on their own: the next online launch downloads them and the one after shows them.

(How: `manifest.webmanifest` gives the icon and full-screen mode; `sw.js`, a service worker, keeps a copy of every file the game uses, including three.js, its add-ons and the font. The icons `icon-180.png` and `icon-512.png` are rendered from `icon.svg` in headless Chrome.)

## Running locally

It is a single `index.html` with no build step. [three.js](https://threejs.org/) 0.170 and its addons load from jsDelivr through an import map. Serve the folder over HTTP, for example:

```bash
python -m http.server 8917
```

Then open http://localhost:8917.

## Sound

Sound is off until you tap the 🔇 **Sound** button. Then:

- A dispatcher talks on the radio (a squelch blip, then her voice): she welcomes you, calls out each mission ("A ship is sinking!", then "Follow the orange arrow!"), warns about low fuel and running out, says when a rescue is complete and when a new mission is coming in, and mentions rain, storms, snow, night and morning.
- The pilot talks in the cockpit: taking off, spotting the people, "Hold steady!" at the winch, "Got one!" as each person comes aboard, "Everyone is on board!", "Nearly there!", landing, filling up the tank, and which pilot is flying when you switch the robot on or off.
- Effects: the winch whirring, a clip on the harness, a splash for people lifted out of the sea, the ship's horn as you get close, a low-fuel beep, the fuel pump, and a cheer when people are saved.
- Lines take turns and never talk over each other: chatter (weather, "Got you!") is skipped when someone is already talking, mission calls and fuel warnings go first.
- The rotor, rain, wind and thunder are synthesized in the browser. If a recorded clip can't load (for example when the page is opened straight from disk), the effect falls back to a synthesized chime or stays quiet, and the line is read by the device's own voice.

Tuning knobs (named constants in the Audio section of `index.html`):

- `VOICE_VOL`, `SFX_VOL`, `CLIP_TRIM`: how loud the voices and effects are, with per-clip trims.
- `VOICE_WAIT`: how long a line may wait for its turn before it's dropped (important lines wait twice as long).
- `LOAD_WAIT`: how long a line waits for its clip to finish loading before the device voice reads it instead.
- `NEAR_SITE`, `NEAR_BASE`: how close (in metres) to the rescue site the pilot spots the people, and to the base he says "Nearly there!".
- `ASSET_V`: bump after replacing any file in `assets/`.

## Audio credits

All recorded clips are in `assets/` and were made with ElevenLabs on the Creator plan (paid), 2026-11-22. They aren't licensed for reuse.

| Files | Tool and voice | What |
| --- | --- | --- |
| `voice/d-*.mp3` (18 lines: ship, swimmer, hikers, skier, campers, roof, farmer, welcome, newmission, arrow, lowfuel, outoffuel, complete, goodnight, goodmorning, rain, storm, snow) | ElevenLabs text to speech, `eleven_multilingual_v2`, stock voice Jessica | The dispatcher on the radio |
| `voice/p-*.mp3` (17 lines: takeoff, seethem, hangon, hold, gotone, gotyou, upyoucome, welcomeaboard, aboard, nearly, landing, hooray, refill, full, great, robot, you) | ElevenLabs text to speech, `eleven_multilingual_v2`, stock voice Roger | The pilot |
| `sfx/winch.mp3`, `sfx/clip.mp3`, `sfx/splash.mp3`, `sfx/cheer.mp3`, `sfx/fuel.mp3`, `sfx/horn.mp3`, `sfx/lowfuel.mp3`, `sfx/squelch.mp3` | ElevenLabs sound effects, `eleven_text_to_sound_v2` | Winch, harness clip, splash, cheer, fuel pump, ship's horn, low-fuel beep, radio squelch |
