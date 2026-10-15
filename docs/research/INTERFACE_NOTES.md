# Interface and Display — Working Notes

Status: product requirements for main-menu development alongside gameplay at M1, progressive destination integration at M2–M3, and release refinement at [M6](../MILESTONES.md). Menu artwork, visual styling, and the final layout still need design and playtests.

## Main menu

Use selectable text controls over optional artwork. Every enabled entry must lead to a working destination. Keyboard, controller, and pointer navigation need visible focus and selection.

```text
Single
  Campaign
  Botmatch
Online
  Start
  Join
Options
  Controls
  Characters
  Language
Addons
  Stages
  Schemes
  Characters
Credits
Exit
```

Build this hierarchy alongside the gameplay core at M1. Campaign connects at M2 through `Single → Campaign`; the original secret key combination is removed. Addons connects to installed content at M3; Online Start/Join becomes functional at M8. Clearly indicate unavailable destinations until they are implemented.

`Options → Characters` selects the player's character; `Addons → Characters` browses installed character content. Language is selected through Options. Display requirements below remain in scope; their controls are designed within the agreed navigation. The Unreal Tournament and Quake III screenshots supplied in discussion illustrate selectable menus; they do not establish a final visual style.

## Languages

English and Russian are the initial game languages. Spanish, Portuguese, and Japanese are subsequent targets. All player-facing interface text must be translatable; fonts and layout need suitable glyph coverage and room for translated labels. Project documentation remains in English regardless of the selected game language.

## Display and image scaling

Support arbitrary display aspect ratios at usable resolutions, including 16:9 and 4:3 CRT output at 640×480 or higher. Preserve sprite proportions and the intended gameplay viewport. Menus, HUD, and pointer coordinates adapt to the output; unused space may contain background or bars.

Monitor aspect ratio does not select a scheme mode. Classic keeps its field visible, NES scrolls, and Wide keeps its entire field on one screen. At 640×480, verify actual text readability, pointer targets, and all three field presentations.

| Setting | Choices and intended behavior |
| --- | --- |
| Scaling policy | Fit uses available space while preserving proportions. Integer uses whole-number pixel scaling where it fits. |
| Filter | Nearest preserves hard pixel boundaries; Bilinear provides smooth sampling. |
| Pixel-art scaling | Scale1x preserves source pixels; Scale2x, Scale3x, and Scale4x aim for subtle edge smoothing with crisp pixel-art output. Exact filter implementations need visual comparison. |

Only offer factors that work for the current output. If integer scaling cannot display the required field, offer Fit without cropping gameplay. Display settings change presentation, not map dimensions, collisions, or simulation timing.
