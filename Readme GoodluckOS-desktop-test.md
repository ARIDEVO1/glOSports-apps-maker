# goodluckOS Desktop & Input Tester

A diagnostic app for the **goodluckOS** handheld (GA36 / R36S clone, CodeZombie firmware). It runs from the kennel launcher and checks three things:

- **Input**: the D-pad, both sticks, the face buttons, shoulders, Start and Select, with live readouts.
- **Files**: it browses your home folder, previews images, and shows the first bytes of other files.
- **Pointer**: the left stick moves an on-screen cursor, which can be used to click buttons and list rows.

It's useful for checking a new device, a new controller, or whether an app's file access works on the device.

## Screen layout

- **Top bar**: app name and the control hints.
- **Left panel**: the current folder path, a "Home (~)" button, and a list of up to 12 entries. Folders show `[DIR]`, images show `[IMG]`.
- **Right panel**: the D-pad and stick widgets, the axis values, the cursor position, the last event, and four button indicators (A, B, X, Y) that light up while pressed.
- **Bottom bar**: the controls.
- **Preview window**: opens over the list when you open an image or file. Images are scaled to fit (up to 4x), on a checkerboard-style background so transparency shows.

## Controls

| Action | Gamepad | Keyboard |
|---|---|---|
| Move the list selection | D-pad up / down | Up / Down |
| Move the cursor | Left stick | Mouse (if connected) |
| Click / open a folder or file | A | Enter or Z |
| Open the selected item | X | — |
| Close the preview or the menu | B | X (keyboard) |
| Right-click menu | B (when nothing is open) | X (when nothing is open) |
| Go to home (~) | Y | — |
| Refresh the folder | (use the right-click menu) | R |
| Exit | Start + Select together | Esc |

The right-click menu has three items: **Jump to ~**, **Refresh Dir**, and **Close Preview**.

## What it reads

- Starts in your home folder. The app looks it up with `cd ~ && pwd` and falls back to `/mnt/HOME`.
- Folders and files come from `ls -1p`, read directly from disk.
- Images (`png`, `jpg`, `jpeg`, `bmp`, `tga`) are loaded and shown.
- Other files show their size and the first 280 bytes as text, with unreadable characters replaced by dots.
- It only reads. It never writes, moves or deletes anything.

## Install

1. Copy the `ports/` and `.local/` folders to the root of the device's storage (`/mnt/HOME`).
2. The app runs from `ports/desktop-test/run.sh`. It needs a LÖVE runtime, either:
   - bundled in `ports/desktop-test/` as `love` with its `lib/` folder, or
   - the OpenSEEK port installed next to it (`ports/openseek/`).
3. Open kennel, and launch **Desktop Tester** from the Ports category.

To test without the launcher, run `ports/desktop-test/run.sh` from a terminal. If the app fails to start, read `ports/desktop-test/run.log`.

## Files

```
.local/share/applications/desktop-test.puppy   launcher entry (Desktop Entry format)
.local/share/icons/desktop-test.png            128x128 icon
ports/desktop-test/run.sh                      starts the game
ports/desktop-test/game/main.lua               the tester
ports/desktop-test/game/conf.lua               window and module settings
ports/desktop-test/icon.png                    icon copy
ports/desktop-test/LICENSE.txt                 MIT licence
```

## Limits

- The file list shows 12 rows at a time. Scroll with the D-pad.
- Previews of non-image files show only the first 280 bytes.
- Some system folders may be blocked or empty.

## Licence

MIT. See `LICENSE.txt`. Copyright (c) 2026 goodluckOS Homebrew Community.
