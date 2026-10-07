# Changelog

All versions below ship as a **full package** (`LaserVision-x.y.z-full.zip`), which contains `Start LaserVision.bat`, `Install add-ons.bat`, the `Test sheet` folder, `Docs` (User Manual and Install Guide PDFs) and the `LaserVision-x.y.z` program folder.
Times are when each package was built (US Central). To update, unzip the new program folder next to the old one. The launcher always starts the newest version, and every version shares one `settings.json`.

## 0.7.25 — 2026-10-07 10:29 CDT
### Changed
- The layer presets file is now read again **only when you load a cut file or press Start over**. The automatic check every 2 s and the check before Save from 0.7.24 are removed, to keep file reads down. After changing the presets in LightBurn, press **Start over**.

## 0.7.24 — 2026-10-07 09:38 CDT
### Fixed
- **The layer presets file is read again** instead of only once at start-up. This happens when you load a cut file, press **Start over**, and automatically within about 2 s after you save the file in LightBurn. The layer dropdowns show the new names and speed/power, and the layer you picked for each colour is kept. If the file changed just before **Save**, you're asked to check the colour choices first.

## 0.7.23 — 2026-10-06 14:56 CDT
### Added
- **"Now:" bar** above the status line, showing what the machine is doing at this moment with a running timer. Examples: *Mark 2 of 4: moving head to X 300.2, Y 749.3 (224 mm)*, *waiting for the camera picture to settle*, *taking picture 3/6*, *measuring the circle*, *confirming*, *short pause before moving on*. Calibration steps, burns, jogs and moves are covered too. The bar turns yellow if one step takes more than 12 s, so you can tell stuck from busy.

## 0.7.22 — 2026-10-06 14:45 CDT
### Added
- **Shape detection for marks with little or no contrast.** If no dark or coloured mark of the expected size is found, LaserVision looks for the round **outline** of a mark of that size, lighter or darker than the material. This covers black on black (gloss on matte), white on black and embossed marks. It fits the circle from its edge all the way round. **Mark detection** = `shape` in Settings forces it.

### Changed
- Measuring a mark only looks at the part of the picture around where the mark should be, which makes each reading faster.

## 0.7.21 — 2026-10-06 14:25 CDT
### Added
- **Mark detection setting** (auto / brightness / colour, default auto). On coloured material, LaserVision also reads marks by their **colour** as well as by how dark they are. Marks on glitter, metallic or textured sheets sparkle so much that their brightness is all over the place, which pulled the reading off-centre. On coloured material, auto uses whichever view sees the mark more steadily. White material works exactly as before.

## 0.7.20 — 2026-10-06 11:35 CDT
### Added
- **Travel speed between marks** (Settings, default 200 mm/s). The laser used to move at the speed of the last job it ran, so after a slow cut on thick material it crawled between marks. LaserVision now sets the speed itself before every move.
- **Precise move speed** (Settings, default 30 mm/s). Used for moves under 5 mm: centring on a mark, the final approach step, jogs and calibration.
- Setting a speed to 0 leaves the laser's own speed alone. If the controller refuses the speed command, you get one warning and moves carry on at the old speed.

### Docs
- The manual's Settings table now covers the travel and precise speeds, the same-direction approach and the cut nudge.

## 0.7.19 — 2026-10-06 10:48 CDT
### Added
- **New calibration Step 1: Camera orientation.** It measures how far the camera is turned and draws an arrow showing which way to rotate it towards the nearest 0/90/180/270°. This is useful for round endoscope cameras, which have no obvious "up". The old steps are renumbered: Step 2 is Scale, Step 3 is Offset (burns) and Step 4 is the Reference dot.

### Fixed
- "Lost the dot" during the scale test at 1280x720, even though the dot was in view. The app now predicts where the dot should be after each test move, retries, and saves a debug picture if it still can't find it.
- Before scale calibration, live dot detection searches the whole picture.

## 0.7.18 — 2026-10-06 10:26 CDT
### Changed
- Burn calibration: if a burn is found less than 0.5 mm from the crosshair, the head no longer moves to re-centre it. Before, the head lined up and then shifted a moment later, so the burn had to be lined up again.

## 0.7.17 — 2026-10-06 09:12 CDT
### Added
- **Free step size.** You can type any jog step in the new "Any step" box, for example 0.02 or 2.5 mm, and a 0.01 mm preset was added.
- **Shift + arrow key** jogs 0.01 mm, both in the main window and in calibration.

## 0.7.16 — 2026-10-06 09:09 CDT
### Added
- **Check and accept each calibration burn by hand.** After a burn is found, it's centred under the crosshair with 3x zoom. You can nudge it with the arrow keys or click it in the picture until it's dead centre, then press **Accept**. If a burn isn't found automatically, the camera goes to where the burn should be so you can centre it yourself.
- Arrow keys jog the head while the calibration window is open.

## 0.7.15 — 2026-10-05 18:27 CDT
### Added
- **Same-direction approach** (Settings, default 1 mm). The head always arrives at a mark or burn from the back-left, so belt slack and backlash are the same for every reading.
- **Cut nudge X / Y** (Settings). This shifts the whole cut by a small fixed amount if test cuts are always off the same way. Any nudge in use is shown in the Result box.

## 0.7.14 — 2026-10-05 18:07 CDT
### Added
- **Double-click the bed view to move there.** With a calibrated camera, the camera picture centres on that spot. Without one, the red dot goes there.

## 0.7.13 — 2026-10-05 17:55 CDT
### Added
- **Confirmed readings.** Each mark is measured again with the camera standing still until two readings agree, so a mark is never accepted from one shaky look. New settings: *Pictures averaged per reading* (6), *Readings must agree within* (0.02 mm) and *Pause after each mark* (0.5 s).
- The Result box shows each mark's confirmation and how many readings it took.

### Changed
- The "Camera rotation" setting is gone. It's handled automatically now, and odd angles such as 225° no longer cause an error when you save Settings.

## 0.7.12 — 2026-10-05 17:35 CDT
### Added
- **Endoscope / any-angle camera support.** *Picture turn on screen* (Settings, default `auto`) turns the camera picture to match the bed view at any angle, for example −135°. You can also type a number of degrees.
- **Rough camera position entry** for the burn step (X/Y mm from the laser beam, a ruler guess is fine). This helps when the camera sits far from the head.
- If the camera's scale or angle changes noticeably after recalibration, the old offset and reference dot are cleared and you're asked to redo the burns.
- `camera_test.py --probe` lists which picture sizes and formats the camera really delivers, with fps and brightness.

### Changed
- The first burn search covers a wider area (25 mm).
- 3x zoom works with the turned picture.

## 0.7.11 — 2026-10-05 12:58 CDT
### Added
- **Timing report.** After Auto-measure, the Result box shows total time, time spent moving (distance and average speed) and time spent waiting for the camera.

### Fixed
- Waiting for the camera picture to settle learns how much the picture normally flickers, so it no longer waits too long with noisy cameras. The maximum wait is now 3 s instead of 6 s.
- Practice mode: fixed occasional glitches when the live view and measuring ran at the same time.

## 0.7.10 — 2026-10-05 08:44 CDT
### Changed
- Private details were removed from the package. There is no preset laser IP address any more: type your laser's IP in the IP box (the same one LightBurn uses), and you're reminded if it's empty.
- The full package now includes a `Docs` folder with the **User Manual** and **Install Guide** as PDFs.
- Manual screenshots were updated.
