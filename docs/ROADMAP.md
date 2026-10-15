# open-atomic — Roadmap

Status: proposed work order, with no release dates or completion claims. The current `OpenAtomic/` directory is a content-layout mockup. Existing source projects provide research and implementations to evaluate.

[VISION.md](VISION.md) owns direction; [MILESTONES.md](MILESTONES.md) owns acceptance criteria. Individual tasks, owners, and progress belong in issues and the project board.

## Work sequence

| Phase | Focus | Milestones |
| --- | --- | --- |
| 0. Shared foundation | Agree on scope, initial platforms, evidence, source reuse, and decision process. Prepare comparison scenarios and a backlog with gameplay and main-menu work as equal immediate priorities. | M0 |
| 1. Gameplay and main menu | Build the agreed text-menu hierarchy alongside a complete local round. Connect local actions as their systems become available; reproduce original mechanics, bots, campaign behavior, timing, and edge cases. Document bugs and deliberate fixes. | M1–M2 |
| 2. Modding | Implement readable content contracts, validation, shared/per-character audio, authoring tools, and package identity. | M3–M4 |
| 3. Expanded local play | Extend campaigns and enemies; add scrolling and Wide fields and motorcycle protection while retaining verified classic behavior. | M5 |
| 4. Release usability | Refine the existing menu and complete languages, adaptable display output, settings, and a distributable local build. | M6 |
| 5. Online play | Compare network prototypes, record the decision, then deliver lobbies, stable matches, and verified custom-content exchange. | M7–M8 |

Gameplay and main-menu development proceed together from Phase 1. Menu destinations connect progressively: Campaign during original-game coverage, Addons during modding, and Online Start/Join at M8. Playtesting, original-game comparisons, provenance checks, and documentation updates continue through every phase. Early architecture accounts for reproducible simulation and content identity; multiplayer implementation remains the final phase.

## Source work to evaluate

| Source | Main contribution to investigate |
| --- | --- |
| Original `BOMBRMAN` | Observable behavior and original data. |
| Mayerwin / Boom Buds | Gameplay simulation, mechanics, and rules for a native port. |
| Egerion | Native cross-platform architecture, reverse-engineering evidence, and network prototypes. |
| Elraro | Cross-platform implementation and reverse-engineering evidence. |
| Cpinan | Additional implementation and useful verified subsystems. |
| `ins` archive and FREDIT | Format research, visual corrections, and animation-authoring knowledge. |

No implementation foundation or network prototype has been selected by this roadmap. M0 establishes the reuse plan; M7 establishes the network design.

## Supporting requirements and research

| Reference | Owns |
| --- | --- |
| [Content notes](research/CONTENT_LAYOUT_DRAFT.md) | Stage/scheme compatibility, three grids, campaigns, motorcycles, skin completeness, audio behavior and event inventory, package proposals, and open content decisions. |
| [Animation draft](research/ANIMATION_INI_DRAFT.md) | PNG references, sequence steps, separate pivots and offsets, cues, and editor requirements. |
| [Interface notes](research/INTERFACE_NOTES.md) | Exact menu tree, languages, CRT and widescreen support, scaling and filtering. |
| [Network proposals](research/NETWORKING_PROPOSALS.md) | Ceotom's proposal, alternative models, and questions for measured comparison. |

These notes distinguish requirements, original-file observations, and proposals. Final metadata syntax, library choices, network authority, and motorcycle edge cases still require decisions and validation.
