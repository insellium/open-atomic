# Roadmap

Start with the base, gameplay port and main menu. Finish and release the local game before developing online.

[Discuss the plan](https://github.com/insellium/open-atomic/issues/24). Issue numbers below identify cards; they do not set the work order.

## 1. Base, gameplay and main menu (M0–M1)

1. [Build the C++20 base](https://github.com/insellium/open-atomic/issues/3) from Egerion and elraro. Choose the useful parts of each and resolve overlapping implementations in one application.
2. [Port Erwin / mayerwin’s Boom Buds gameplay](https://github.com/insellium/open-atomic/issues/1) to that base: mechanics, game logic, rules and timing.
3. [Build the main menu](https://github.com/insellium/open-atomic/issues/2) alongside the gameplay port. Launch Botmatch, finish a local round and return to the menu.

Begin [comparison scenarios and playtests](https://github.com/insellium/open-atomic/issues/4) and [license checks](https://github.com/insellium/open-atomic/issues/5) during integration. Continue both as code and content are added.

## 2. Complete the original game (M2)

- [#6 Original mechanics and bots](https://github.com/insellium/open-atomic/issues/6): all power-ups, extras, player actions and match rules.
- [#7 Original campaign](https://github.com/insellium/open-atomic/issues/7): CAM playlists, enemies and progression through Single → Campaign.
- [#8 Original bug fixes](https://github.com/insellium/open-atomic/issues/8): reproduce and document each intentional correction.

Compare these features with the original before moving on to modding and new gameplay features.

## 3. Modding and tools (M3–M4)

- [#9 Stages and schemes](https://github.com/insellium/open-atomic/issues/9).
- [#10 Character skins](https://github.com/insellium/open-atomic/issues/10).
- [#11 PNG animations and INI settings](https://github.com/insellium/open-atomic/issues/11).
- [#12 Sound effects and voices](https://github.com/insellium/open-atomic/issues/12).
- [#13 Animation editor](https://github.com/insellium/open-atomic/issues/13).
- [#14 Mod packages and versions](https://github.com/insellium/open-atomic/issues/14).

Creators should be able to make, install and share a stage or skin using the documented formats. Connect the Addons menu as these loaders become available.

## 4. Local additions and release (M5–M6)

- [#15 Custom campaigns and enemies](https://github.com/insellium/open-atomic/issues/15).
- [#16 Scrolling and Wide maps](https://github.com/insellium/open-atomic/issues/16).
- [#17 Motorcycles with blast protection](https://github.com/insellium/open-atomic/issues/17).
- [#18 Language support](https://github.com/insellium/open-atomic/issues/18).
- [#19 Display and scaling options](https://github.com/insellium/open-atomic/issues/19).
- [#20 Local release](https://github.com/insellium/open-atomic/issues/20).

Finish local menu destinations and settings. Give testers outside the team a build they can install, play and report problems with.

## 5. Online, last (M7–M8)

- [#21 Choose the network architecture](https://github.com/insellium/open-atomic/issues/21) after testing Ceotom’s proposal and the existing alternatives.
- [#22 Add online multiplayer](https://github.com/insellium/open-atomic/issues/22), lobbies and matches with up to ten players.
- [#23 Share custom content](https://github.com/insellium/open-atomic/issues/23) and verify that all players use matching packages.

Start this stage after the local release. Keep the Online menu entries unavailable until their features work.

## Where the work comes from

| Source | Role in open-atomic |
| --- | --- |
| Egerion and elraro | Parts of the native C++20 base. Choose and integrate components individually where they overlap. |
| Erwin / mayerwin’s Boom Buds | Mechanics, game logic, rules and gameplay to port to C++20. |
| Original BOMBRMAN | Reference for behavior, timing, formats and comparisons. |
| Cpinan and the ins research archive | Additional research and code to consult when needed. |
| FREDIT | ANI, pivot and offset research, and guidance for the future animation editor. |

The source projects still need component-level review. We have chosen the integration direction; library choices, duplicate implementations and individual ports need decisions as we work.

## Details

[Milestone checks](MILESTONES.md) · [Menu and display](research/INTERFACE_NOTES.md) · [Content and audio](research/CONTENT_LAYOUT_DRAFT.md) · [Animation format](research/ANIMATION_INI_DRAFT.md) · [Network proposals](research/NETWORKING_PROPOSALS.md)

OpenAtomic/ is a content-layout mockup. The listed features are planned work.
