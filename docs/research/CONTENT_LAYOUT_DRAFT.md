# Content Layout — Working Notes

Status: working requirements and research for [M3–M5](../MILESTONES.md). Format syntax and implementation choices remain proposals where explicitly indicated.

## Content roles

| Path | Intended role |
| --- | --- |
| `data/stages/<name>/` | Stage art, music, effects, `extra.ini`, supported grid modes, and eligible schemes. |
| `data/schemes/*.sch` | Text schemes for block layout, spawn points, original scheme settings, and an optional grid-mode declaration. |
| Campaign definitions (location to decide) | Ordered levels, titles, stage/scheme references, and enemy rosters; import original text `.CAM` files. |
| `data/skins/<name>/` | Player animations and optional replacements for shared audio events. |
| `data/game/` | Shared bombs, flames, extras, power-ups, and other match art. |
| `data/sounds/` | Shared default effects and voice groups. |

The mockup files are empty placeholders. A file path shows intent, not implemented behavior or proof that the content set is complete.

## Stage and scheme

Keep `.SCH` as the familiar editable text format. A small scheme can be sent before a network match and checked by hash; installed stage art and music should be checked as a package. Discover stages from folders rather than a fixed `VALUELST.RES` count. Each stage may provide its own `music.ogg`.

The original install has 67 `.SCH` files, each with **11 rows of 15 cells**. Open-atomic treats an omitted scheme grid mode as **classic** 15×11. An explicit mode must match the row count, row width, spawn coordinates, and stage capability. After a stage is selected, the scheme picker shows only its eligible schemes with a matching grid mode; imported original stages may allow all classic schemes to preserve their existing combinations. The exact allowlist metadata and `.SCH` mode directive are not yet finalized.

| Grid mode | Width × height | Intended presentation | Availability |
| --- | --- | --- | --- |
| `classic` | 15×11 | Original fixed-screen field | Default for legacy `.SCH`; basis for original-game parity. |
| `nes` | 15×31 | Scrolling field | Campaign only. |
| `wide` | 35×17 | Entire field visible on one screen | Special stages and schemes. |

The larger modes are open-atomic extensions. Camera movement, stage art, extras, explosion reach, spawn placement, and enemy pathfinding must use the declared dimensions rather than assuming 15×11.

Display aspect ratio is separate from scheme dimensions. See [interface and display requirements](INTERFACE_NOTES.md) for viewport, CRT, language, and scaling behavior.

`extra.ini` is intended to describe special-cell placement independently of `.SCH` block layout. Original `EXTRA*.RES` files are text and provide examples of arrows (`-A,S,2,2`), linked teleports (`-W,1,0,2,2,3`), trampolines (`-T,2,2` and random `-T,H,H`), and conveyors (`-C,E,2,2`). Negative coordinates can count from the far edge. A converter must preserve directions, links, and random placement semantics. The final `extra.ini` syntax is still undecided.

Original art for these objects is in `EXTRAS.ANI` and `CONVEYOR.ANI`; the new package uses PNG animations. If random trampolines are permitted online, their positions must be agreed by every participant.

## Campaign source and extension

The original `DATA/RES` contains `SIMPLE.CAM`, `GHOSTS.CAM`, and `CROUTON.CAM`. Each is a text playlist of `-C` records. Each record names a campaign level, uses a numeric original stage (`levelno`) and a `.SCH` name, and configures rover count/speed, ghost count/speed, AI count, and an AI-difficulty field that the original format comments call unused. The original entry path uses five `C` presses on the local player setup screen. Open-atomic keeps the campaign content and gameplay but replaces that shortcut with `Single → Campaign`; the secret key sequence is not retained.

Open-atomic can extend campaign definitions with stable stage/scheme references and new enemy types while still importing the original `.CAM` records. New fields and their text syntax need a separate design; do not reinterpret the original nine fields to mean something else. NES-sized scrolling levels are limited to Campaign. Wide levels can be used by stages designed for that mode. Campaign progression must validate that each referenced scheme is eligible for its stage and grid mode.

## Optional motorcycle mount

A Louie-inspired motorcycle is an open-atomic gameplay extension, enabled by a mode or stage rather than imposed on original-behavior comparisons. It grants one-use protection from a bomb blast that would otherwise damage its rider: that hit destroys the motorcycle and the rider survives. Without the motorcycle, subsequent damaging blasts use ordinary player rules. Mount possession and shield consumption are gameplay state and must agree across players in an online match.

Acquisition, movement changes, interactions with non-blast hazards, and how one shield handles overlapping or lingering blasts need explicit rules and playtests before implementation.

## Skin and animation

A skin requires every action group: `cornerhead`, `die`, `idle`, `kick`, `pickup`, `warp`, `stun`, `stand`, `standbomb`, `taunt`, `throw`, `walk`, and `walkbomb`. Every required animation leaf needs `animation.ini` and its referenced PNG files. A missing required folder, INI, frame, or declared audio override rejects the whole skin with a path-specific error; incomplete skins do not silently borrow default frames. Required directions and minimum variant counts still need a precise rule.

The [animation format draft](ANIMATION_INI_DRAFT.md) specifies a pivot for each PNG and an offset for each sequence step. Its placement formula is `object anchor + step offset - frame pivot`. Repeated steps may use the same PNG with different offsets. This preserves the distinction demonstrated by the two supplied `WALK.ANI` versions. Gameplay determines animation cadence; the original ANI state-header values are not milliseconds or FPS.

## Audio behavior

- Shared default effects and voice groups apply to all skins. A skin may replace individual event sounds or voice groups only for a player using that skin. Events therefore carry their source player; other players keep their own replacements or shared defaults.
- Animation steps may trigger additional effects, including `die`, `idle`, and `cornerhead`. An event mapping identifies the sound independently of an original `SOUNDLST.RES` numeric slot.
- A local voice-lines setting mutes voice clips, including skin replacements, but leaves sound effects and animation cues audible.
- Every installed clip in the effective voice group remains eligible. At the start of each match, a fresh random order is generated per source player and event group; the pool reshuffles after exhaustion. Voice selection must not consume gameplay simulation randomness.
- New stages and sound events have no fixed legacy count. Audio is included in the containing package's content hash for online verification.

The original `SOUNDLST.RES` supports a sound tied to a death animation. Its fixed slots and the original load-time reduction of voice pools are behavior to improve, not limits to retain.

### Event inventory from the initiator's SOUNDLST.RES

Source reviewed: `initiator-provided SOUNDLST.RES`. These are its annotated event uses, not a finalized open-atomic event registry. Slot IDs are evidence about the old mapping; open-atomic does not require those numeric ranges.

| Event family | Annotated uses and slots |
| --- | --- |
| Menu voices | Title callout 2800; quitting 2600. |
| Menu effects | Selection 20–21; denied action 40–41; enter/exit 10. |
| Music | Title 1000; menu 1010; menu pages 1020; Game Over 1030 (marked nonworking by the author); network 1040; draw/end/editor 1130. Stage music entries across 1100–1149 are commented out except 1130. |
| Bomb handling | Drop 100–101; kick 120–123; stop 130–132; punch 150–151; bounce after grab/punch 160; grab 170–175. |
| Bomb effects | Jelly bounce 135–137; explosions 200–202; stun 360–363. |
| Environment | Hurry wall drops 140–142; trampoline 350–353; teleport 1330–1332. |
| Animation and disease effects | Specific death-animation sounds 341–349; poop effects 550–554. |
| Roulette | Tick 1300; good item 1310; bad item 1320. |
| Gameplay voices | Death screams 300–304; post-death taunts 700–708; huge-bomb-string taunts 1200–1201; Hurry callouts 2700–2704. |
| Power-up audio | Pickup 400–404; Awesome milestone 1400–1406, annotated as the seventh pickup and every third thereafter. |
| Match result voices | Draw 1700; winner 2000. |
| Disease voices | Generic 2300; Molasses 3000; Crack 3050; Constipation 3100; Poops 3150; Short Flame 3200; Crack Poops 3250; Short Fuze 3300; Swap Players 3350; Reversed Controls 3400; Leprosy 3450; Invisible 3500; Duds 3550. |

The taunt rows 700–708, huge-bomb rows 1200–1201, and Hurry rows 2700–2704 contain no clip names in this file. The post-death comment says seven slots but lists nine rows. These annotations do not establish actual playback behavior. Voice headings contain some `SFX_` clips, and effect headings contain some `V_` clips; the new registry must classify a clip as voice or effect explicitly for the voice-mute setting. Values 1099 and 2900 are annotated as technical placeholders, not audio categories.

## Package identity

The current proposal for installable stages and skins is a readable stable ID, a human-readable version, and a hash computed from package contents. For example, `author.skin.red-bomber`, `1.0.0`, and SHA-256. The author should not have to calculate the hash manually. Equal IDs and versions with different hashes indicate a conflict. A `.SCH` can remain one text file with a separately verified hash instead of requiring a package manifest.

Before an online match, peers need the selected stage and skin package identities and the scheme text/hash. Missing permitted packages can then be obtained and verified. Download sources and which materials may be redistributed require separate decisions.

## Decisions still needed

1. Final `extra.ini` syntax and the rules for stage-specific art overrides.
2. Minimum skin variants, required directions, and frame-count rules.
3. Stable audio event names, voice/effect classification, and per-skin override metadata.
4. Package manifest, dependency and hashing rules, plus safe user-data and download locations.
5. A distributable base-asset plan that keeps original game materials separate from community-created content.
6. The precise `.SCH` grid-mode directive, stage-to-scheme eligibility rule, and extended campaign enemy syntax.
7. Motorcycle acquisition, movement, hazard interactions, and overlapping-blast behavior.

The mockup also lacks real content for its existing item, bomb, extra, HUD, and audio folders. These are implementation tasks under the milestones, not reasons to add more empty directories now.
