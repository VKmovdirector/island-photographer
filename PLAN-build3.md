# The Island Photographer — build 3 plan

Starting point: build 2 (first-person Three.js r128, single file, chart travel, topic dialogue, bag, simplified shooting).

## 1. Low poly, cel shaded

- Materials: swap MeshLambert for MeshToonMaterial with a 3-step gradient map (nearest-filter DataTexture) so light falls in bands. Flat shading on, low segment counts everywhere, a little vertex jitter on rocks, trunks and the cliff.
- Outlines: inverted hull (a back-face copy of each mesh, scaled 1.03, black). No post-processing, works with fog. Thin lines on props, none on the sea and sky.
- Sky: a gradient dome mesh with two or three hard bands instead of a flat clear color; fog color matched to the lowest band.
- Palette: one limited ramp per time band (morning fog greens, midday chalk, evening rust-green, night ink). Prints stay black and white.
- Performance: trees, rocks, fence posts and quay planks become InstancedMesh; the woods currently spend 400+ draw calls and outlines double that.
- Characters: chunky low-poly bodies (box coat, cylinder head, hat or hood), a two-pose idle sway, name labels kept.
- First-person prop: the camera body appears low in the frame when raised, and the mounted lens model swaps on it.

## 2. Quest log

- Data-driven QUESTS table: id, title, giver, stages, objectives (predicates on flags and state), rewards, and a "where and when" hint that also places a chart pin.
- Types: Leads (the current rumors), Story (the house, the letter, the cairn, the notebook, the front page), Daily (small loops: develop the roll, visit Marit).
- Journal panel on J: tabs Leads, Story, Done; objectives as a checklist; a "Journal updated" toast and a small sting when anything changes.
- Newspaper archive in the journal so past editions can be reread.

## 3. Mechanics beyond taking pictures

Pick three for build 3, keep the rest for later:

- Samples and the notebook. Physical traces at phenomenon sites (scorched grass, a feather, the stone). At the kitchen table, match samples and prints to notebook pages in a small matching game. Matches turn vague leads into precise ones and unlock the attic archive.
- Being tailed. From Attention tier 1 the sedan waits on the street. A short evasion beat: reach the diner or the footpath before the sedan's sweep catches you, or lose an undeveloped roll. Tier 3 adds the house search, which the hidden safe defeats.
- Aksel's boat. At trust 2 he takes you out at dusk. A moving platform, the harbor from the water, shots at the base fence from the sea. Hard shots, high story score.
- Darkroom crop. The enlarger upgrade lets you crop a print after the fact, trading resolution for framing. A small, satisfying second mini-game in the darkroom.
- Later: radio scanner tuning, the bell tower at three in the morning, lighthouse roof post, tourists at the harbor.

## 4. Inventory and shop in 3D

- Every item gets a procedural low-poly model: rangefinder body, 50mm and 135mm lenses, tripod, film canister, key, letter, stone. Thumbnails render once from those models at load.
- Bag screen: item grid on the left, a turntable viewport on the right showing the selected item slowly looping, with its stats and actions (mount, load, rewind, read).
- Marit's shop becomes a small 3D interior: counter, shelves, items on display stands that rotate. Look at one, press E for the detail card, buy, and it leaves the shelf.
- The camera in hand reflects what is mounted; the tripod appears in the frame when set.

## 5. Sound and ambience

- Ambient beds per location: wind and surf at the cliff, water slap and rigging at the harbor, wind in trees and distant birds in the woods, clock tick and creaks at home, gulls and a far engine on the street. Night adds the low drone; dawn brings the foghorn.
- One-shot sounds: footsteps by surface, camera raise and lower, film advance lever, zoom ring, tripod legs, doors, page turns, the press, coins.
- Cues as sound first: the birds stopping is a bed that ducks to silence; the flat sea drops the surf layer. Text cues stay for accessibility.
- Everything synthesized with WebAudio to stay single-file. If we move to a folder build, a small set of real samples replaces the synthesis.
- Settings overlay with master volume and mute.

## 6. Clock and going to bed

- Continuous clock from 06:00. Actions cost minutes: travel by chart distance (10 to 40), talking 5, developing a roll 30, waiting 60, field time at one game minute per real second.
- Time bands replace hard slots: Morning 06 to 11, Midday 11 to 16, Evening 16 to 20, Night 20 to 02. Light, fog and phenomenon windows interpolate across the band edges instead of jumping.
- The day ends only in bed at home. Past 02:00 the screen fogs and you collapse home, losing the morning. Being out late at high Attention tiers adds Attention.
- Sleep runs the print day, rumor expiry, a one-line dream card, and the morning routine.
- NPC schedules by band: Sigrún at the diner in the morning, Aksel on the boat at dusk, Tobias near the fence road at night, Marit closed at night. The chart shows expected arrival times.

## Other suggestions

- Reputation axis from the deck (Sensational vs Credible). The editor refuses front pages without corroboration; two prints of the same phenomenon unlock it.
- Weather and moon: fog, rain and storm change spawns and visuals; rain on the quay, wet lens spots.
- Settings: mouse sensitivity, invert Y, pointer lock on or off, remappable keys, gamepad support.
- Colorblind-safe focus bracket: shape change on lock, not only color.
- Photo polish: last-shot thumbnail flash, contact sheet before developing, a gallery of best prints.
- Code structure: split into src/ modules with a tiny concat script; the artifact still ships as one file.

## Order

- Phase A, look: cel shading, outlines, low-poly rework, instancing, first-person camera prop.
- Phase B, systems: clock and bed, NPC schedules, quest log, newspaper archive.
- Phase C, content: 3D bag and shop, samples and notebook, being tailed, Aksel's boat, darkroom crop.
- Phase D, feel: ambient beds and one-shots, settings, gallery.

## Decisions needed

- Clock model: action costs plus real time in the field (recommended), or fully real time.
- Delivery: stay single-file for the artifact (synth audio, procedural models), or move to a folder build with real samples.
- Which three non-photo mechanics go first.
- Look reference: flat bands with thin dark outlines (recommended) or heavier ink.
