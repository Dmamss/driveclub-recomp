# DriveClub Recomp on the Steam Deck

The Steam Deck runs the native Linux build (the AppImage): the game's code runs directly on the
Deck's CPU and the GPU commands go to Vulkan (RADV), with no Proton, Wine or emulator. The
launcher recognises the Deck (LCD and OLED) and adapts to it:

- **Steam Deck preset.** The first start on a Deck picks the *Steam Deck (1280x800)* quality
  preset: the 1280x800 (16:10) resolution patch so the picture fills the screen, 30 FPS (the PS4's
  frame rate, even on the 60 Hz panel), static mirrors, 2x texture filtering and HDR off. **Reset
  to defaults** goes back to it. It is under DISPLAY > Quality preset on any machine.
- **Gamepad control.** The launcher is driven with the Deck's controls, so it works in Gaming
  Mode where there is no mouse:

  | Button | Launcher |
  |---|---|
  | D-pad / left stick | move between rows |
  | A | choose, open a list, toggle |
  | B | back, close a list |
  | L1 / R1 | previous / next page (GAME, DISPLAY, ...) |
  | Start (☰) | PLAY |
  | View (⧉) | SAVE |

  The trackpads and touchscreen also work as a mouse. For a text field (player name, folder path),
  press **STEAM + X** for the on-screen keyboard. **Browse...** opens the launcher's own folder
  browser, which also works with the gamepad.
- **Fullscreen in Gaming Mode.** The launcher fills the screen there.

## Installing

1. Switch to **Desktop Mode** (STEAM button > Power > Switch to Desktop).
2. Download `driveclub-recomp-<version>-x86_64.AppImage` and put it in a folder of its own, for
   example `~/Games/DriveClub/`. The prepared game, settings, saves and logs go in `data/` next
   to it.
3. Copy **your own** game dumps next to it as `update/` (the 1.28 update, with `eboot.bin`) and
   `base/` (the base game, with `game000.dat`). They can also stay elsewhere, for example on the
   microSD card: choose them in the launcher with **Browse...**.
4. Make the AppImage executable: right-click > Properties > Permissions > *Is executable*, or in
   Konsole:

       chmod +x driveclub-recomp-*-x86_64.AppImage

5. Add it to the application menu, which also lists it in Steam:

       ./driveclub-recomp-*-x86_64.AppImage --install

6. In Steam (still in Desktop Mode): **Games > Add a Non-Steam Game to My Library...**, tick
   **DriveClub Recomp** and press **Add Selected Programs**. (Right-clicking the AppImage in the
   file manager and choosing *Add to Steam* does the same.)
7. Start it once from Desktop Mode, check the folders on the GAME page and press **PLAY**. The
   first start prepares the game files, which takes a moment.
8. Go back to **Gaming Mode**. DriveClub Recomp is in the library under *Non-Steam*.

### Controller layout in Steam

Keep Steam Input's **Gamepad** layout (the default for a non-Steam game): the game then sees an
Xbox-style controller and the launcher's *Controller buttons > Automatic* shows Xbox prompts. Pick
*PlayStation* there for the PS4 symbols. To skip the launcher, tick *Start the game when this
window opens* on the GAME page, or add `--play` to the launch options in the game's Steam
properties.

## Performance tips

- The Steam Deck preset is a starting point. With the frame rate steady you can try **60 FPS
  (deltatime)** on the DISPLAY page; in that case set the screen's refresh rate and frame limit in
  the Quick Access menu (… button > Performance) to match.
- On the 30 FPS preset, the Quick Access menu's frame limit can stay off.
- The OLED model has an HDR screen. The launcher's HDR option is off in the preset because the
  LCD model has none; on an OLED you can try it.
- FSR 3.1 (DISPLAY > Anti-aliasing) can render below 1280x800 and upscale, which helps when the
  GPU is the limit.
- F12's performance overlay needs a keyboard; Steam's own performance overlay (Quick Access >
  Performance) works everywhere.

## Troubleshooting

- **The launcher does not open in Gaming Mode.** Start it once from Desktop Mode to check that it
  runs, and look at `data/logs/` next to the AppImage.
- **Not detected as a Steam Deck** (or wrongly detected): set `DRIVECLUB_STEAM_DECK=1` (or `0`) in
  the launch options, for example `DRIVECLUB_STEAM_DECK=1 %command%`.
- **Paths and detection.** `./driveclub-recomp-*-x86_64.AppImage --selftest` prints the data
  folder, the game folders and `STEAM_DECK=1` when the Deck is recognised.
- **After moving the AppImage**, run `--install` again and add it to Steam again.
