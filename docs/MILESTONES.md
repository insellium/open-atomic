# Milestones

M0–M1 cover the first stage: the native base, gameplay port and main menu. M2–M6 cover the remaining local work. Online is M7–M8, after the local release.

Use these checks to decide when a milestone is ready. Track progress in [Issues](https://github.com/insellium/open-atomic/issues) and discuss work order in [#24](https://github.com/insellium/open-atomic/issues/24).

## M0 — Shared foundation

- Choose the Egerion/elraro components to combine and record their source and reuse requirements.
- Put the chosen native components in one C++20 build that opens a window, reads input and loads basic assets.
- Identify where the Boom Buds gameplay port will connect to the application.
- Prepare repeatable original-game comparisons and initial platform setup instructions.

Complete when contributors can build the base and start integrating gameplay and the menu into it.

## M1 — Playable local core and main menu

- Port the initial Boom Buds mechanics, logic and rules to C++20 in the combined base.
- Finish a classic 15×11 local round with movement, bombs, flames, block destruction, deaths and results.
- Build the agreed [text menu](research/INTERFACE_NOTES.md), with keyboard, controller and pointer navigation, visible selection and back navigation.
- Connect Botmatch, basic Controls and Characters settings, Credits and Exit. Show unfinished destinations as unavailable.
- Compare movement, collision and bomb timing with the original and record differences.

Complete when a player can launch Botmatch from the menu, finish a round and return to the menu in the native build.

## M2 — Original gameplay coverage

- Complete and compare all original power-ups, extras, player actions, bots and match rules.
- Open Campaign from Single and reproduce CAM playlists, rovers, ghosts, bot counts and progression.
- Document original bugs, agreed fixes and remaining differences.

Complete when the agreed original-match and campaign comparisons pass, and the team has reviewed remaining differences.

## M3 — Moddable content

- Load stages, compatible text SCH schemes, complete skins, PNG animations and OGG audio.
- Browse stages, schemes and characters in Addons; select a character in Options.
- Keep frame pivots and step offsets separate, and report invalid or missing content by file.
- Support stage music, animation sound cues, shared audio, individual skin replacements, voice muting and all eligible voice clips each match.

Complete when another creator can install a new stage and skin and play them locally using the instructions.

## M4 — Authoring and package identity

- Provide an editor for frame pivots, step offsets and sequence preview, with safe INI saving.
- Give packages stable IDs, versions, calculated hashes, validation and conflict reports.
- Provide a sample package and instructions for stages, extras, animations and audio.

Complete when a creator can make, validate and share a working package.

## M5 — Expanded local play

- Add longer campaigns and new enemy types.
- Support classic 15×11, scrolling NES 15×31 for Campaign, and Wide 35×17 on one screen, with compatible stages and schemes.
- Add motorcycles with one-use blast protection and test consecutive, overlapping and lingering blasts.
- Rerun original-game checks with extensions disabled.

Complete when the new campaigns, map modes and motorcycles work in playtests without breaking classic play.

## M6 — Local release candidate

- Finish local menu destinations, settings and English/Russian language support.
- Check the menu, HUD, controls and map views on 4:3 CRT output at 640×480, 16:9 and other aspect ratios, with the supported scaling and filters.
- Provide platform builds, setup and asset instructions, comparison results and known differences.
- Run playtests with people outside the implementation team.

Complete when testers can install the build, configure it, play local matches and campaigns, and report reproducible problems.

## M7 — Network architecture decision

- Begin after the local release, then set responsiveness, stability, running cost and trust requirements.
- Test Ceotom’s proposal and rollback alternatives with 2–10 players, direct and relayed connections, latency, loss and slow clients.
- Test player disconnects and host departure; record the chosen authority, transport, connection and relay design.

Complete when the team can explain its network choice using the comparison results.

## M8 — Online custom-content alpha

- Connect Online → Start and Join to working lobbies and supported connection paths.
- Finish repeated matches with up to ten players and handle disconnects.
- Agree on stage, scheme, skin and audio versions and hashes before play; obtain and verify missing content that may be shared.
- Test mixed custom content, skin audio and motorcycle state across clients.

Complete when a group can repeatedly finish online matches with matching gameplay state and the agreed custom content.
