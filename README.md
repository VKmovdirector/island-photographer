# The Island Photographer — build 5

Single-file web prototype of the Oone Films GDD v0.1: `index.html` (Three.js r128 from cdnjs, Google Fonts, nothing else).
Earlier builds are kept as `v1-topdown.html` and `v2-firstperson.html`. The plan this build follows is `PLAN-build3.md`.

## What build 5 adds

- Shift to run. A persistent objective line under the HUD with the chart pin pulsing for it. A press-and-doorstep sequence for every edition, and the paper on the doormat at home. Faces, head turns, a walking Tobias, a trotting dog, chimney smoke. Daily weather: clear, fog, or rain, with rain that darkens, mists the prints, and quiets the birds.

## What build 4 added

- **Marit's counter.** Talk to her, then buy or sell. Spare gear and film sell at half; prints tagged sell go on her postcard rack for quiet money the paper never hears about.
- **The angles quest** now lists each sample by name with where, when, and which page it belongs to.
- **Morning routine** at the front door: wipe the lens (a hazed lens costs sharpness all day), mount a lens, load film, eat.
- **Food meter.** Drops four an hour. Cupboard bread, Sigrún's eggs, tinned fish. Low food slows you and shakes the camera; empty and you cannot hold still.
- **The watch (N).** Wait fifteen minutes, an hour, the next band, or any hour up to 02:00.
- **Random events** on arrival and a dog on Main street.
- **People** tab in the journal with portraits, roles, descriptions, trust, and notes; each character has a distinct silhouette.
- `DESIGN.md` describes every mechanic with its numbers.

## What build 3 added

- **Low poly, cel shaded.** Toon materials with a three-step ramp, flat shading, inverted-hull outlines on props and people, a banded sky dome, and daylight that blends across the day instead of jumping. Trees are instanced. A camera sits in your hand when it is lowered, and the lens on it changes when you mount the 135mm.
- **Clock and bed.** A continuous clock from 06:00. Travel costs minutes by chart distance, talking five, developing thirty, waiting an hour; time in the field runs at one game minute per real second. The four bands (Morning, Midday, Evening, Night) drive light, phenomena, and where people are. The day ends only in bed at home after 19:00. Past 02:00 you collapse and lose the morning. Each night has a one-line dream.
- **Journal (J).** Open, done, and editions. Story quests (the house, the letter and the angles, the front page, the sedan, Aksel's boat), leads from rumors, stage checklists with hints, and a readable archive of every edition.
- **3D bag and shop (I).** Every item is a low-poly model turning on a stand: rangefinder, lenses, film, tripod, enlarger, key, letter, stone, samples. Marit's shop is now an interior with the items on shelves; look at one, press E, buy it, and it leaves the shelf.
- **Beyond the camera.** Samples appear where a phenomenon has been; the kitchen-table notebook matches them to his pages and makes each phenomenon come sooner or stay longer. From Attention tier 1 a sedan sweeps Main street when you carry undeveloped film: duck into the diner or lose the rolls. At trust 2 Aksel takes you out at dusk to shoot the base from the water. The enlarger (Marit, $80) lets you crop a print after the fact, trading grain for framing.
- **Sound.** Ambient beds per place and hour (wind, surf, rigging, trees, birds, the house clock, a night drone), one-shots for steps, the camera, film advance, zoom ring, tripod legs, doors, pages, the press, coins, and the sedan's engine. Phenomena cues duck the birds or the surf to silence.
- **Settings (Esc).** Volume, mute, mouse sensitivity, invert Y, mouse capture on or off. Saved per browser.

## Still from the deck

Hidden score vector at the shutter; the darkroom timer, print resolve, sting, and loupe discovery; the Courier's placement and pay; print day on the next band change; Attention, the sedan, the Tier 1 beat; three data-driven phenomena; single-slot autosave.

## Controls

WASD walk · mouse look (click once to capture) · E use / talk · M chart · I bag · J journal · C or right click raise camera · left click shoot · wheel zoom (135mm) · T tripod · Space wait · Esc lower camera, close, or settings · ` debug (F1 +$100, F2 +1 hour, F3 gear, F4 force spawn)
