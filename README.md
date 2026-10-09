# Heli Rescue

A 3D rescue-helicopter game for young kids (around age 5), made for phones and tablets.

Fly a rescue helicopter over a big world of farms, cities, forests, mountains and coast. Missions pop up one after another: a farmer needs a doctor, hikers are stuck on a mountain, a ship is sinking, campers are lost in the forest. Fly there, winch the people aboard and bring them back to a rescue base. Keep an eye on the fuel gauge and refuel at a base.

Buttons let you change the weather and the time of day, switch the camera, or let the robot pilot fly.

- 🏠 in the corner goes back to the list of all games.

**Play:** https://tb-x.github.io/heli-rescue/

## Running locally

It is a single `index.html` with no build step. [three.js](https://threejs.org/) 0.170 and its addons load from jsDelivr through an import map. Serve the folder over HTTP, for example:

```bash
python -m http.server 8917
```

Then open http://localhost:8917. All sounds are synthesized in the browser.
