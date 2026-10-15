# Vision

We want to make Atomic Bomberman (1997) popular and open to its community again. Doom and Quake are the reference for a game that people keep playing, modifying and maintaining for years.

## Start with the base and main menu

Build one native C++20 game from the useful parts of Egerion and elraro. Port Erwin / mayerwin’s Boom Buds mechanics, game logic, rules and gameplay into that base. Build the main menu alongside the gameplay port.

Check movement, timing, collisions, bombs and match rules against the original. Use regular playtests to find differences. Document original bugs and agreed fixes, including the bomb-pickup animation.

The first playable result is a local match launched through Single → Botmatch, with a return to the menu after the round. Complete the original mechanics, bots and campaign next.

## Make modding easy

Creators should work with folders, PNG, OGG and readable text settings. Keep editable .SCH schemes and import original .CAM campaigns. Remove the fixed palette and the old limits on stages, sound slots and loaded voice clips.

Require complete skins with all agreed animations. Keep a separate pivot for each frame and an offset for each animation step. Provide an editor for positioning them.

Use shared effects and voices across skins. Let individual skins replace selected events for their own players. Let players mute voices while keeping sound effects, including effects tied to die, idle and cornerhead. Keep all installed clips in each effective voice group eligible every match.

## Add the planned local features

After the original game and modding work, add longer campaigns, new enemies and the three map modes: classic 15×11, scrolling NES 15×31 for Campaign, and Wide 35×17 on one screen. Motorcycles absorb one damaging bomb blast.

Use selectable text menus with the agreed [menu structure](research/INTERFACE_NOTES.md). Support English and Russian first, then Spanish, Portuguese and Japanese. Adapt the game to 16:9, 4:3 CRT displays at 640×480 or higher, and other aspect ratios, with selectable scaling and filtering.

## Develop online last

Finish and playtest a local release before working on online. Then compare network designs, including Ceotom’s proposal, and choose one using measured results. Support up to ten players and native sharing of compatible custom content.

## Work as one team

Follow the agreed work order. Discuss changes in [the project discussion](https://github.com/insellium/open-atomic/issues/24), keep decisions in the relevant tasks, and run playtests throughout development. Check source licenses and asset attribution as code and content are brought in. Keep project documents in English.

Read the [roadmap](ROADMAP.md) for task order and [milestones](MILESTONES.md) for completion checks.
