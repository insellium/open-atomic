# open-atomic — Milestones

Status: proposed acceptance gates for the [roadmap](ROADMAP.md). No gate is marked complete. Record task status and owners in issues; close a milestone using a working build, comparison results, and team review.

## M0 — Shared foundation

- Agree on the vision, initial platforms, decision process, and original-game comparison method.
- Compare source projects by subsystem, accuracy evidence, maintainability, and reuse rights; choose an implementation plan.
- Prepare reproducible baseline scenarios and a milestone-linked backlog with gameplay and main-menu work as equal immediate priorities.

**Done when:** contributors can follow one implementation direction and reproduce its baseline evidence.

## M1 — Playable local core and main menu

- A native build starts and finishes a local round with movement, bombs, flames, block destruction, deaths, and results.
- Build the full agreed [menu hierarchy](research/INTERFACE_NOTES.md) as selectable text with visible focus, keyboard/controller/pointer navigation, and working back navigation. Connect `Single → Botmatch`, basic Controls and Characters settings, Credits, and Exit. Make unfinished destinations clearly unavailable until their systems are ready.
- Compare essential timing and collisions with the original; record reproducible mismatches.

**Done when:** a player can navigate the agreed menu, configure basic local play, launch Botmatch, finish a round, and return to the menu; core behavior can be checked repeatedly.

## M2 — Original gameplay coverage

- Verify the original items, extras, player actions, bots, modes, match flow, and important edge cases.
- Connect `Single → Campaign` and reproduce original `.CAM` progression, rovers, ghosts, and configured AI counts.
- Record original bugs, intentional fixes, and remaining differences with evidence. Resolve material uncertainty before claiming parity.

**Done when:** representative original matches and campaigns pass the agreed comparison scenarios, with remaining differences explicitly reviewed.

## M3 — Moddable content

- Load stages, compatible text `.SCH` schemes, complete skins, PNG animations, and OGG audio using the [content requirements](research/CONTENT_LAYOUT_DRAFT.md).
- Connect Addons Stages/Schemes/Characters to installed-content browsing and make installed playable characters selectable through `Options → Characters`.
- Preserve separate frame pivots and step offsets. Reject invalid or incomplete declared content with useful errors.
- Implement stage music, animation cues, shared audio, per-player skin replacements, voice muting, and full eligible voice pools without legacy count limits.

**Done when:** another creator can install a new stage and skin and play them locally through the documented workflow.

## M4 — Authoring and package identity

- Provide an editor for independent pivot and step-offset adjustment, sequence preview, and safe INI saving.
- Implement stable package identity, versioning, computed hashes, validation, and conflict reporting.
- Provide a sample package and creator instructions covering stage extras, required animations, and audio events.

**Done when:** a creator can author, validate, and share content using the modern workflow.

## M5 — Expanded local play

- Extend the existing Campaign destination with longer playlists and additional enemy types.
- Support all three [grid modes](research/CONTENT_LAYOUT_DRAFT.md), including stage/scheme eligibility, camera behavior, spawns, extras, and AI movement.
- Implement motorcycle mounts with one-use blast protection; define and test consecutive, overlapping, and lingering-blast behavior.
- Keep the agreed original-game scenarios passing with extensions disabled.

**Done when:** extended campaigns, scrolling and Wide levels, and one-use motorcycle protection work in playtests without regressions in classic play.

## M6 — Local release candidate

- Refine the menu introduced at M1 and complete the [language and display requirements](research/INTERFACE_NOTES.md): all local destinations, English/Russian, adaptable layouts, CRT support, and selectable scaling/filtering.
- Validate navigation, text readability, HUD, and all field presentations at 640×480 in 4:3, a representative 16:9 resolution, and other aspect ratios.
- Supply target-platform builds, a documented asset distribution basis, regression results, and known differences. Online destinations are completed at M8.

**Done when:** testers outside the implementation team can install the build, configure it, play local matches and campaigns, and report reproducible issues.

## M7 — Network architecture decision

- Set responsiveness, stability, cost, and trust criteria before judging prototypes.
- Compare two through ten players over direct and relayed connections, including latency, loss, slow clients, and host/player departure.
- Record the chosen authority, transport, connection, and fallback model with measurements and limitations.

**Done when:** comparable experiments support one network implementation plan.

## M8 — Online custom-content alpha

- Online Start/Join opens working lobby and connection flows; matches and disconnect handling are stable.
- Verify agreed stages, schemes, skins, audio, and package hashes before play; obtain and verify missing permitted content.
- Playtest mixed custom content and up to ten players across supported connection paths, including shared motorcycle state when enabled.

**Done when:** a group can repeatedly finish online matches with matching gameplay and agreed presentation content on every client.
