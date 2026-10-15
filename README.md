# open-atomic

An open-source reimplementation of Atomic Bomberman (1997), intended as a native C++20 game maintained by its community.

**Current focus: faithful gameplay and the main menu, developed together.** This repository currently contains the project plan and research notes; it does not yet provide a playable open-atomic build.

[Project board](https://github.com/users/insellium/projects/1) · [Issues and discussion](https://github.com/insellium/open-atomic/issues) · [Milestones](https://github.com/insellium/open-atomic/milestones)

## Direction

- Verify original rules, mechanics, bots, campaign behavior, and timing through comparison scenarios and playtests.
- Build the agreed selectable text menu alongside the gameplay core.
- Make modding accessible through folders, PNG, OGG, text schemes, and readable metadata.
- Add expanded campaigns, enemies, field modes, motorcycles, languages, and display options on top of the verified foundation.
- Implement online multiplayer last, including agreed custom content and matches of up to ten players.

## Plan and requirements

| Document | Purpose |
| --- | --- |
| [Vision](docs/VISION.md) | Shared goals and priorities. |
| [Roadmap](docs/ROADMAP.md) | Order of work and dependencies. |
| [Milestone criteria](docs/MILESTONES.md) | Reviewable outcomes M0–M8. |
| [Interface and display](docs/research/INTERFACE_NOTES.md) | Exact menu tree, languages, CRT/widescreen output, scaling and filters. |
| [Content and audio](docs/research/CONTENT_LAYOUT_DRAFT.md) | Stages, schemes, characters, campaigns, field modes, mounts, audio events, and package proposals. |
| [Animation draft](docs/research/ANIMATION_INI_DRAFT.md) | PNG animation steps with independent frame pivots and step offsets. |
| [Network proposals](docs/research/NETWORKING_PROPOSALS.md) | Options and measurements for the later network decision. |

## Working together

Use GitHub Issues to discuss features, report evidence, and agree on concrete tasks. The project board shows their status; repository milestones group them by outcome. Gameplay and main-menu tasks have equal immediate priority. Move work to In Progress only when implementation actually begins.

Record observations, expected behavior, comparison steps, and acceptance criteria in the relevant issue. Keep the documents aligned with agreed decisions. Check source reuse rights and asset provenance before importing material from the original game or reference projects.
