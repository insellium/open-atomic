# open-atomic — Vision

Status: working project charter for team discussion.

## Purpose

Bring Atomic Bomberman (1997) back as an open, community-maintained game with faithful gameplay, accessible modding, and lasting online play. Doom and Quake are references for longevity and creator freedom. Build one coherent native C++20 reimplementation from verified findings across existing projects.

## Priorities

1. **Develop faithful gameplay and the main menu together.** These are the two immediate priorities. Movement, timing, bombs, items, extras, bots, match flow, and campaign rules are judged against the original through repeatable comparisons and active playtests. Build the selectable text menu alongside the playable core using the agreed [menu structure](research/INTERFACE_NOTES.md). Record original bugs and intentional fixes explicitly.
2. **Make content easy to create and share.** Use folders, PNG, OGG, and readable metadata. Preserve text `.SCH` schemes and import original `.CAM` campaigns. Remove the fixed palette and legacy stage-count, sound-slot, and voice-pool limits. Players should be able to use the same agreed custom content together.
3. **Expand and improve the game.** Add campaign enemies, scrolling and Wide fields, motorcycle protection, complete localization, and adaptable display output after the original foundation is trustworthy. Refine the menu as its destinations become available.
4. **Implement multiplayer last.** Support matches of up to ten players and native custom-content agreement. Select the network model through measured prototypes. Early simulation and content design must support that later work.

## Intended experience

A match retains the original game's feel. Creators can add stages, schemes, characters, animations, and audio without manual editing of legacy image or sound formats. Shared audio supports replacements for individual characters, an independent voice-mute option, and all installed voice clips remaining eligible each match.

Campaign is directly accessible in Single. Expanded rules support additional enemies, a scrolling NES field, a single-screen Wide field, and motorcycles that absorb one damaging bomb blast. Original gameplay remains available for play and comparison.

Menus use selectable text. English and Russian are initial languages; Spanish, Portuguese, and Japanese are later targets. Display output adapts to different aspect ratios, including 16:9 and 4:3 CRT use at 640×480, with selectable scaling and filtering.

## Working together

Evaluate each source project's accuracy, maintainability, evidence, and reuse rights before adopting a subsystem. Boom Buds is a gameplay reference for porting mechanics and rules; its website is outside the intended port. Keep original game materials distinct from distributable project assets.

Contributors follow the shared priorities, record disputed decisions, and run regular playtests. Use issues for tasks and ownership. Change the vision when the team changes direction.

[ROADMAP.md](ROADMAP.md) defines work order. [MILESTONES.md](MILESTONES.md) defines completion criteria. Detailed requirements and research are linked from the roadmap.
