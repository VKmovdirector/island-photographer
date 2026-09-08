# The Island Photographer — Design Document (build 4)

Working title. Oone Films. This document describes every mechanic in the current prototype as built, with the numbers the code uses. It follows the GDD v0.1 brief and records where the build departs from it.

## 1. Premise and tone

A former reporter inherits his grandfather's house on a North Atlantic island of about two thousand people. He arrives by ferry at dusk with a suitcase and a film camera. His first roll, shot at the lighthouse, holds something he did not see. The island's paper buys it. From there every publication changes the island and draws attention from a military base behind a fence, from researchers, and from men in plain sedans.

Tone: quiet, foggy, cosmic dread rather than horror. The fog comes in against the wind. The sea goes flat like a held breath. The church spire is too tall for the town and the door is locked from the inside. The grandfather's letter says "do not print the angles." Humor comes from the locals; dread comes from what is in the prints. No jump scares.

Pillars, from the deck: the print knows more than the viewfinder; every publication changes the island; gear is progression, not stats; fame against safety; soft failure.

## 2. The loop

One in-game day is one loop. Morning routine at the house, leads from people, travel by chart, a stakeout or shoot, develop in the basement, sell at the Courier or quietly to Marit, buy gear, sleep. The paper goes out when the time band changes after a sale. Attention rises with what is published. Rumors spawn from editions and from people.

A full day takes roughly ten to fifteen minutes of real time.

## 3. World and locations

All locations are first-person 3D, low poly, cel shaded (three-step toon ramp, flat shading, dark hull outlines on props and people, banded sky dome). Travel happens through an admiralty chart (M).

- **Grandfather's house** (interior). Bed, kitchen table with the letter and notebook, cupboard, camera bag, print shelf, basement door (darkroom), attic stair (nailed shut), front door. A wall clock shows the game time.
- **Main street.** Diner (Sigrún), the Courier (Halldór), school, houses, the church with an over-tall spire. Street lamps at night. A dog with one white ear by day. The sedan and the Man from Attention tier 1.
- **Harbor.** Quay with lamp posts, Aksel's boat, a moored boat, the ferry, Marit's shop door, the harbor road. The sedan after the first front page.
- **Marit's shop** (interior). Counter, shelves with turning item models. Trade happens at the counter through dialogue.
- **Lighthouse cliff.** Plateau above the sea, the tower with a beam at dusk and night, rocks, a cairn of scratched stones, gulls, a fishing boat far out.
- **North woods.** Instanced spruce forest, the base fence with signs, a searchlight tower that sweeps once at night.
- **Aksel's boat.** A moving deck at dusk or night along the base shore: hangar, fence, lights, searchlight. Reached through Aksel at trust 2.

## 4. Clock, bands, and the day

Continuous clock from 06:00. Time costs:

| Action | Minutes |
|---|---|
| Travel by chart | 8 + distance/14 (15 to 40) |
| Talking, per topic | 5 |
| Developing a roll | 30 |
| Wipe the lens | 3 |
| Eating | 10 |
| Waiting (watch) | as chosen |
| Field time | 1 game minute per real second |
| Boat trip | 50 out, 40 back |

Bands: Morning 06:00 to 11:00, Midday to 16:00, Evening to 20:30, Night after. Light, fog, sky, and phenomenon windows blend across band edges. People follow schedules by band (section 12). The paper goes out on the next band change after a sale, deferred until you are back in town.

The day ends only in bed at the house, after 19:00. Each night shows a one-line dream. Past 02:00 you collapse and wake on the kitchen floor at 10:30. Sleeping hungry (food under 20) wakes you at 07:30.

**Morning routine.** The first time you use the front door before noon, the routine panel opens: wipe the lens, mount a lens, load or swap film, eat from the cupboard. A hazed lens costs 14 percent sharpness all day and shows a haze in the viewfinder.

**The watch (N).** Grandfather's pocket watch, shown as a turning model. Wait 15 minutes, an hour, until the next band, or until any hour up to 02:00. In a zone this counts as a stakeout and advances the phenomenon timers.

## 5. Food

A meter from 0 to 100, starting at 70, dropping 4 per hour. Eating: cupboard bread once a day (+35), Sigrún's eggs and coffee ($4, +60), coffee ($1, +15), tinned fish from Marit ($3, +40, eaten from the bag). Under 30: walking 25 percent slower and handheld shake 70 percent worse. Under 10: you cannot hold still, so the woods entity will not come. Sleep costs 10.

## 6. Movement and interaction

WASD walks, the mouse looks (pointer lock on click, can be turned off in settings). E uses whatever you face within about 2.5 metres. Bounds and obstacle circles keep you on the plateau, the quay, the road, the deck. Footsteps by surface, a small head bob.

## 7. Camera and shooting

C or right click raises the camera. The view narrows to a 3:2 frame with the focal length's field of view. Autofocus settles on whatever sits under the bracket; the view softens while it hunts and the bracket turns green and tightens when it locks. Left click shoots one exposure. The wheel zooms 50 to 135 mm when the 135 is mounted. T sets the tripod (not on the boat). A light pill reads DARK, DIM, LIGHT OK, or BRIGHT.

**Film.** Rolls of 12. ISO 100 (daylight) and ISO 400 (dusk and night, grainy by day). A partly shot roll can be rewound to an exposed roll and developed.

**Score vector at the shutter** (hidden until the print):

- exposure error = log2(light × ISO × shutter / 100); shutter is 1 handheld, up to 4 on the tripod (long exposure chosen automatically).
- focus error = |1/focus − 1/subject distance| × 12 × (focal/50)²; sharpness factor 1 − 1.4 × error.
- motion blur = subject speed × shutter × (tripod 0.2 else 1) × √(focal/50), 1.6× on the boat.
- resolution = 0.3 + 0.7 × (subject width fraction / 0.03), capped at 1.
- sharpness = 100 × focus × blur × exposure × resolution, × 0.86 with a hazed lens.
- framing = 55 percent subject size (ideal 10 to 50 percent of frame width) + 45 percent nearness to a rule-of-thirds point.
- subject (rarity) = category rarity × 1.75 until a clear print (sharpness 60+) of that category exists, × 0.85 per previous publication of the category.
- story = 20 for a phenomenon (10 mundane) + 40 landmark in frame + 30 base fence in frame + 20 for a second shot of the same phenomenon within ten seconds.
- composite = 0.4 sharpness + 0.2 framing + 0.3 subject + 0.1 story.

The print is captured from a second render that includes print-only objects.

## 8. Phenomena

| Id | Category, rarity | Where, when | Trigger | Visible? | Sample |
|---|---|---|---|---|---|
| Object over the water | sky object, 40 | Lighthouse cliff, boat; Morning, Midday, Evening | timer every 12 to 24 s, window 4 to 8 s | tiny at 50 mm, readable at 135 | feather, wrong color |
| Light beneath the harbor | light, 45 | Harbor, boat; Night | timer every 28 to 48 s, window 5 to 7 s | yes, dim: needs ISO 400 and the tripod | wet stone |
| The Tall Thing | entity, 80 | North woods; Evening, Night | hold still 4 s on the tripod, window 6 s | print only | scorched needles |

Cues: the water goes flat (surf ducks to silence), the birds stop (bird bed ducks). Moving during the entity's window ends it. The day-one lighthouse roll guarantees the object in one of exposures 3 to 8 if the sky is in frame. When a window ends, the phenomenon leaves its sample nearby with a "?" marker, once per game.

## 9. Darkroom

Basement, unlocked when you come home with something to develop (a key appears on the table). Choose a roll, agitate against a timing bar (generous the first time), release in the green zone; early or late costs 10 sharpness. Prints resolve one at a time, blurred to sharp. A low sting and a music drop mark any print holding an anomaly. The loupe zooms 2.6×; an anomaly is marked UNKNOWN only when the loupe finds it. Undiscovered anomalies sell as local color. Tags: keep, sell, discard.

Prints are black and white with paper tone, grain by ISO and light, blur by sharpness, brightness gained for correctly exposed low-light frames.

**Enlarger crop.** With the enlarger ($80), drag a 3:2 rectangle on a print. Framing is recomputed from the new subject size and position; sharpness falls by the crop factor to the power 0.7; grain grows. One crop per print.

## 10. The Island Courier

Halldór rates a print on the four scores and places it: composite under 40 page 6 (base $20), 40 to 69 page 3 ($40), 70 and up front page ($120). Pay = base × editor mood (0.8 to 1.3) × repeat penalty (1.0 first of a category, 0.6 second, 0.3 after, unless 25 sharper than the best sold) × (0.75 + 0.5 × composite/100). Sold prints queue for the next edition. The edition is a generated newspaper page with a headline and story by category and placement, readable later in the journal.

Attention per publication: page 6 +2, page 3 +5, front page +12; −4 per day without an edition. The meter appears after the first front page. At 20 (tier 1) a sedan parks by the house and the Man appears on Main street.

## 11. Marit's counter

Talk to Marit, choose "See what you have" or "I have something to sell." Buy: 135 mm lens $60, tripod $40, enlarger $80, ISO 400 $15, ISO 100 $8, tinned fish $3. Sell: spare gear and film at half price. Prints tagged sell go on her postcard rack for $6, $9 (sharp), or $14 (with a found anomaly). Marit's money is quiet: nothing is published and Attention does not move. This is the deck's quiet buyer.

## 12. People, trust, dialogue

Every named character has a greeting that changes with the story and a set of topics. Some topics need trust. Trust rises one per day on the first conversation and by giving prints (Aksel, a print of his boat). Topics can give rumors, set flags, or open the counter or the desk.

| Name | Role | Where, by band |
|---|---|---|
| Sigrún | runs the diner | Main street, Morning to Evening |
| Halldór | editor of the Courier | Main street, Morning to Evening |
| Aksel | fisherman, harbor master | Harbor, Morning, Evening, Night |
| Marit | camera shop | Shop, Morning to Evening |
| Tobias | twelve, sneaks near the base | Main street Midday and Night, woods at Evening |
| The Man | unknown | Main street after tier 1 |

Each has a distinct silhouette: Sigrún's apron, Aksel's height and rope, Tobias's size and cap, Marit's glasses, Halldór's newspaper and cane, the Man's coat. The journal's People tab keeps a portrait, role, description, trust, and notes from what they have told you.

## 13. Journal and quests

J opens the journal: Open, Done, People, Editions. Quests are data with stages, each a predicate on game state, with a hint for the current stage. Any change posts a toast and a chime.

- The house with one lamp: sleep, read the letter, develop a roll.
- Before the fog lifts (Sigrún): shoot the lighthouse in the morning, develop, find the object, show Halldór.
- Something sharp (Halldór): a front page.
- The angles (the letter): the cairn stone to page 4, then the feather, the wet stone, and the scorched needles each matched to its page, then the attic (next build).
- The light under the quay (Aksel) and What stands still (Tobias): the two night leads.
- The sedan: escape it once.
- Aksel's boat: go out at dusk.

## 14. Rumors and leads

A rumor is a soft quest: source, zone, time band, hint, confidence, expiry in days. Sigrún gives the lighthouse on day one; the first edition unlocks Aksel's and Tobias's leads. Leads show on the chart as ringed pins and in the journal. Reader tips arrive as random events after an edition.

## 15. Samples and the notebook

After a phenomenon's window ends, a sample appears where it was: the feather on the grass ahead, the wet stone at the quay edge, the needles where it stood. Pick it up with E. At the kitchen table, click a sample, then a page. A correct match unlocks the page's text and tunes the phenomenon: the object comes every 7 to 14 seconds, the harbor light every 16 to 30 with an 8 to 10 second window, the entity needs 2.5 seconds of stillness and stays 9. The cairn stone matches page 4 and points at the attic.

## 16. The sedan

From Attention tier 1, entering Main street with undeveloped film starts the sedan at the far end, moving at 1.7 m/s. An engine sound and a cue warn you. If it comes within 2.7 metres the Man takes every undeveloped roll, politely. Reaching the diner door ("Duck into the diner") lets it pass and completes the quest stage. Developing before you walk Main street avoids it entirely.

## 17. Aksel's boat

At trust 2, in Evening or Night, "Take me out on the water." The deck rolls, handheld shake is 2.6× worse, the tripod is not allowed. The shore moves past: the base hangar (subject rarity 30, story bonus for the fence), the fence, lights, the searchlight. The object and the harbor light can appear from the water. Ask Aksel to turn back to return.

## 18. Random events and life

On arriving somewhere (once per place per band, 40 percent chance) a short event may play: the dog, a stranger's folded note (a reader tip), men in good coats outside the Courier (+1 Attention), the ferry horn, chalk marks on Aksel's wheelhouse, something knocking under the quay at night, a thermos and stool left on the cliff (+1 Attention), a tourist in a yellow coat, a fox, a truck with its lights off on the fence road, an envelope under the door, the telephone that is not connected, Marit's clock that runs slow on foggy days.

## 19. Sound

Synthesized in WebAudio. Beds by place and hour: wind, surf, rigging creaks, trees, birds, street murmur, the house clock, a night drone. One-shots: steps, camera raise and lower, film advance, zoom ring, tripod legs, shutter, doors, pages, the press, coins, journal chime, the sedan's engine, the foghorn. Cues duck the birds or the surf. Volume and mute in settings.

## 20. Settings and saving

Esc: volume, mute, mouse sensitivity, invert Y, mouse capture. Single-slot autosave in the browser at every travel, sale, sleep, and journal change. Continue from the title.

## 21. Controls

WASD walk · mouse look · E use or talk · M chart · I bag · J journal · N watch · C or right click camera · left click shoot · wheel zoom · T tripod · Space wait · Esc lower camera, close, settings · backtick debug (F1 +$100, F2 +1 hour, F3 gear, F4 force a phenomenon).

## 22. Departures from the GDD v0.1

- Pay uses base × (0.75 + 0.5 × composite/100) so the tutorial smudge lands near $40 and a front page near $120; the deck's formula gave about $10.
- Page thresholds 40 and 70 instead of 60 and 80, with the rarity first-capture bonus persisting until a clear print exists, so the 135 mm path can still reach a front page.
- Print day is the next band change after a sale, not a fixed evening.
- Undiscovered anomalies sell as local color; discovery is the player's job.
- Focus error is measured in diopters, so far subjects forgive and near ones need the lock.
- Trust, samples, a notebook, the sedan tail, the boat, the enlarger crop, food, the watch, and random events are in; researchers, weather, tourism, and the endgame are not yet.

## 23. Next

The attic and archive (matching old prints to sites), weather and moon, the Sensational versus Credible reputation axis with corroboration, researchers at tier 2, the house search and the safe, the radio scanner, the bell tower at three in the morning, a folder build with real samples and models.
