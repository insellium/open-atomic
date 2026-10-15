# PNG Animation and Pivot Format — `animation.ini` Draft

Status: proposed open-atomic content contract, based on a read-only inspection of the original `BOMBRMAN/DATA/ANI` files and FREDIT. No loader or pivot editor is implemented yet. This document specifies the small, useful part of ANI for PNG-based content; it is not a byte-for-byte ANI translation.

## What the original files actually contain

An ANI file has a shared image-frame library and one or more named sequences. A sequence contains ordered states (steps), and each state refers to one or more library frames. The image itself stores a hotspot (called a pivot below). Each state placement also stores its own offset. Both coordinates matter for reproducing a placement: a frame can have the correct pivot and still appear in the wrong place if its step offset is lost. The original files additionally carry palette/key-color data, a cell box, optional geometry and user values, and fields whose purpose is unrelated to the PNG workflow.

A read-only survey of the 95 supplied ANI files found 2,327 image frames, 249 sequences, and 3,416 states. Only three states have more than one placement. These examples show why a PNG filename is not necessarily the same thing as a sequence step:

| Original sequence | States | Distinct images used | Observation |
| --- | ---: | ---: | --- |
| `WALK.ANI` / `walk north` | 15 | 15 | One ANI contains several direction sequences. |
| `BOMBS.ANI` / `bomb regular green` | 18 | 10 | Images repeat to make the return half of the cycle. |
| `CORNER0.ANI` / `cornerhead 0` | 50 | 31 | A long animation reuses images. |
| `PUP1.ANI` / `pickup west` | 10 | 10 | A single sequence can map directly to one leaf folder. |

The original ANI state-header values `30` and `65535` **do not control playback speed** in the game. The original game advances an animation counter according to the object or player action; it selects a state using that counter and the sequence length. FREDIT's Loop switch is an editor playback setting and is not serialized into ANI. Therefore, do not interpret `30` as milliseconds, frames per second, or a duration, and do not interpret `65535` as an end marker. See the verified timing analysis in `Egerion - open-atomic-bomberman-97-main/docs/re/facts.md` and FREDIT's `docs/stage3-format.md`.

## Scope and folder rule

Each leaf animation folder contains its PNG files and one `animation.ini`. The folder identifies the action and variant, for example `skins/bomberman/walk/up/`, `skins/bomberman/die/1/`, or `game/bombs/simple/`. A multi-sequence ANI is split into the corresponding leaf folders. The filenames `001.png`, `002.png`, etc. are a convention, not a fixed frame count or the playback order.

Version 1 has **one rendered PNG per sequence step**, with a frame pivot and a separate step offset. This avoids the original chunk structure while retaining both placement coordinates. The three original multi-placement states need a case-by-case visual check during conversion: use the first image where that is what the original game renders, or flatten the visible composition to a PNG where it actually renders multiple layers. A later format version may add explicit layers if a real use case needs them.

## Proposed version 1 syntax

```ini
[animation]
version = 1

[frame.001]
file = 001.png
pivot_x = 20
pivot_y = 34

[frame.002]
file = 002.png
pivot_x = 17
pivot_y = 31

[step.001]
frame = 001
offset_x = 0
offset_y = 0

[step.002]
frame = 002
offset_x = -2
offset_y = 3

[step.003]
frame = 001
offset_x = 1
offset_y = 0
```

`[frame.<id>]` declares a PNG and **its own pivot**. `[step.<number>]` refers to a declared frame ID and gives **that use of the frame** its own offset. Steps play in ascending numeric order. The example has three steps but only two image files; steps 001 and 003 reuse the same PNG and pivot with different offsets. Frame IDs need only be unique within this INI. Step numbers start at `001` and are contiguous. Playback order must never be inferred from directory listing order.

The pivot is a signed integer pixel coordinate measured from the PNG's top-left corner: `x` grows rightward, `y` downward. It may be negative or lie outside the image bounds. The offset is a signed integer pixel displacement relative to the game-object anchor for one step: positive `x` moves the image rightward; positive `y` moves it downward. The runtime places the image with:

```text
image top-left = game object anchor + step offset - frame pivot
```

The pivot locates a reference pixel in the image; the offset then moves that frame's particular occurrence. Differently sized or cropped images can remain aligned at the same object anchor without losing intentional motion. Cropping from the old image's `(crop_x, crop_y)` requires `new_pivot = old_pivot - (crop_x, crop_y)` while leaving all step offsets unchanged. Reuse one frame ID with different step offsets when identical pixels need different placements; do not overwrite a shared pivot to achieve a step-specific move.

### Evidence from two `WALK.ANI` versions

The supplied original `WALK.ANI` and the corrected version have 60 frames and five sequences each. All 60 image payloads are identical. The corrected file changes 54 frame hotspots and 56 state offsets. In `walk east`, step 1 keeps frame 0's hotspot at `(56, 97)` but changes its offset from `(0, 14)` to `(-1, 18)`. Relative to the same object anchor, the image top-left therefore changes from `(-56, -83)` to `(-57, -79)`. A pivot-only INI would lose that four-pixel vertical and one-pixel horizontal adjustment. This is a file-level comparison and the placement formula used by FREDIT; original game draw paths must still be checked in playtests when claiming exact visual parity.

The game chooses the animation step from its action-specific phase. Walking can be distance-driven; other actions may advance on simulation ticks, loop, hold, or finish according to gameplay rules. Version 1 deliberately has **no `duration_ms`, `fps`, or `loop` key**. Such keys would falsely suggest that ANI supplied the original cadence. If a later feature needs author-controlled time-based animation, it should introduce an explicit clock and duration rule rather than repurpose the original inert field.

## Optional sound cues

An animation may declare effects on particular **steps**, not on PNG files, because one PNG may be used at several moments:

```ini
[cue.001]
step = 002
event = player.idle.fidget
repeat = each_cycle
```

`event` names an **effect** in the shared sound bank. The source player's equipped skin may replace that event's audio; otherwise the shared effect plays. This also works for `die`, `cornerhead`, and other actions. The voice-lines-off setting does not mute animation effect cues. `repeat = each_cycle` fires on each transition into that step, including after a sequence wraps; `repeat = once_per_activation` fires at most once between entering and leaving the animation. A held step does not repeatedly retrigger its cue. Cue ordering is by ascending numeric cue key when several cues share a step. The event is attributed to the player who owns the animation. The exact audio event registry and override-file syntax are specified separately from this INI.

## Validation rules

- The file must have `[animation]` with `version = 1`, at least one `[frame.<id>]`, and at least one step.
- Every frame must name one readable PNG in the same animation folder. Reject absolute paths and `..` traversal. Each PNG path is declared only once so it has one unambiguous pivot.
- `pivot_x` and `pivot_y` are required signed 32-bit integers; do not clamp them to image bounds or derive them from canvas size at load time.
- Step sections are numbered with contiguous positive integers. Each requires one valid `frame` reference and signed 32-bit `offset_x` and `offset_y` values. Repeated frame references with different offsets are valid; unused frame declarations are an error.
- Cue step references and repeat values must be valid. Every cue event must resolve in the shared sound bank or the source skin's valid override.
- For a skin, every required action folder and every leaf `animation.ini` must be present. A missing PNG, invalid INI, or missing declared sound override rejects the entire skin with a path-specific error.

PNG alpha replaces ANI's palette and transparent key-color machinery. Collision shapes, gameplay movement, and player position are not inferred from transparent pixels or pivots. ANI `RECT`, `POIN`, cell-box, palette, and user-value chunks are not copied into version 1 without a demonstrated gameplay need.

## Future PNG pivot editor

The editor should open one leaf animation folder, display every referenced PNG on a checkerboard at integer zoom, and draw the frame pivot, the common game-object anchor, and the selected step's displaced pivot (`anchor + offset`). It needs separate controls for the shared frame pivot and the selected step offset. Dragging or entering numeric `x/y` values must update only the selected field in `animation.ini`; it must not silently crop or rewrite the PNG. Previous/next-step overlay at the common anchor should make unwanted visual jumps obvious, including steps that reuse the same PNG with different offsets.

It should preserve frame IDs, step order, step offsets, and sound cues when saving; support undo/redo; validate missing and corrupt files; and save the INI safely without changing unrelated entries. An optional trim command must apply `new_pivot = old_pivot - crop_top_left`, keep every offset unchanged, and show the result before saving. Importing original ANI files can be a separate converter workflow; the first editor only needs PNG and INI.

## Evidence and limits

- `FREDIT/src/ani_document.cpp` parses original frames, hotspots, sequences, states, and placements.
- `FREDIT/src/preview.cpp` renders a placement at `offset - hotspot` in its preview.
- `FREDIT/src/import_process.cpp` shifts the hotspot when trimming a frame.
- `FREDIT/docs/stage3-format.md` documents that Loop is editor-only.
- `Egerion - open-atomic-bomberman-97-main/docs/formats/ani.md` and `docs/re/facts.md` document the original game's distinct rendering and pacing paths.

FREDIT previews each placement at `offset - hotspot`. Existing reverse-engineering notes suggest that the original game does not apply placement offsets uniformly across all draw paths; a verified flame-arm path uses them, while the ordinary blit path may not. The open-atomic INI keeps both fields independently and applies its explicit formula. ANI conversion should inspect the relevant original draw path and compare representative output with the original game before claiming visual parity; it must not silently discard an ANI offset or fold it into a pivot.
