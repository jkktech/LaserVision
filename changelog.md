# Changelog

All versions below ship as a **full package** (`LaserVision-x.y.z-full.zip`), which contains `Start LaserVision.bat`, `Install add-ons.bat`, the `Test sheet` folder, `Docs` (User Manual and Install Guide PDFs) and the `LaserVision-x.y.z` program folder.
To update, unzip the new program folder next to the old one. The launcher always starts the newest version, and every version shares one `settings.json`.

## 0.7.20
### Added
- **Travel speed between marks** (Settings, default 200 mm/s). The laser used to move at the speed of the last job it ran, so after a slow cut on thick material it crawled between marks. LaserVision now sets the speed itself before every move.
- **Precise move speed** (Settings, default 30 mm/s). Used for moves under 5 mm: centring on a mark, the final approach step, jogs and calibration.
- Setting a speed to 0 leaves the laser's own speed alone. If the controller refuses the speed command, you get one warning and moves carry on at the old speed.

### Docs
- The manual's Settings table now covers the travel and precise speeds, the same-direction approach and the cut nudge.

## 0.7.19
### Added
- **New calibration Step 1: Camera orientation.** It measures how far the camera is turned and draws an arrow showing which way to rotate it towards the nearest 0/90/180/270°. This is useful for round endoscope cameras, which have no obvious "up". The old steps are renumbered: Step 2 is Scale, Step 3 is Offset (burns) and Step 4 is the Reference dot.

### Fixed
- "Lost the dot" during the scale test at 1280x720, even though the dot was in view. The app now predicts where the dot should be after each test move, retries, and saves a debug picture if it still can't find it.
- Before scale calibration, live dot detection searches the whole picture.

## 0.7.18
### Changed
- Burn calibration: if a burn is found less than 0.5 mm from the crosshair, the head no longer moves to re-centre it. Before, the head lined up and then shifted a moment later, so the burn had to be lined up again.

## 0.7.17
### Added
- **Free step size.** You can type any jog step in the new "Any step" box, for example 0.02 or 2.5 mm, and a 0.01 mm preset was added.
- **Shift + arrow key** jogs 0.01 mm, both in the main window and in calibration.

## 0.7.16
### Added
- **Check and accept each calibration burn by hand.** After a burn is found, it's centred under the crosshair with 3x zoom. You can nudge it with the arrow keys or click it in the picture until it's dead centre, then press **Accept**. If a burn isn't found automatically, the camera goes to where the burn should be so you can centre it yourself.
- Arrow keys jog the head while the calibration window is open.

## 0.7.15
### Added
- **Same-direction approach** (Settings, default 1 mm). The head always arrives at a mark or burn from the back-left, so belt slack and backlash are the same for every reading.
- **Cut nudge X / Y** (Settings). This shifts the whole cut by a small fixed amount if test cuts are always off the same way. Any nudge in use is shown in the Result box.

## 0.7.14
### Added
- **Double-click the bed view to move there.** With a calibrated camera, the camera picture centres on that spot. Without one, the red dot goes there.

## 0.7.13
### Added
- **Confirmed readings.** Each mark is measured again with the camera standing still until two readings agree, so a mark is never accepted from one shaky look. New settings: *Pictures averaged per reading* (6), *Readings must agree within* (0.02 mm) and *Pause after each mark* (0.5 s).
- The Result box shows each mark's confirmation and how many readings it took.

### Changed
- The "Camera rotation" setting is gone. It's handled automatically now, and odd angles such as 225° no longer cause an error when you save Settings.

## 0.7.12
### Added
- **Endoscope / any-angle camera support.** *Picture turn on screen* (Settings, default `auto`) turns the camera picture to match the bed view at any angle, for example −135°. You can also type a number of degrees.
- **Rough camera position entry** for the burn step (X/Y mm from the laser beam, a ruler guess is fine). This helps when the camera sits far from the head.
- If the camera's scale or angle changes noticeably after recalibration, the old offset and reference dot are cleared and you're asked to redo the burns.
- `camera_test.py --probe` lists which picture sizes and formats the camera really delivers, with fps and brightness.

### Changed
- The first burn search covers a wider area (25 mm).
- 3x zoom works with the turned picture.

## 0.7.11
### Added
- **Timing report.** After Auto-measure, the Result box shows total time, time spent moving (distance and average speed) and time spent waiting for the camera.

### Fixed
- Waiting for the camera picture to settle learns how much the picture normally flickers, so it no longer waits too long with noisy cameras. The maximum wait is now 3 s instead of 6 s.
- Practice mode: fixed occasional glitches when the live view and measuring ran at the same time.

## 0.7.10
### Changed
- Private details were removed from the package. There is no preset laser IP address any more: type your laser's IP in the IP box (the same one LightBurn uses), and you're reminded if it's empty.
- The full package now includes a `Docs` folder with the **User Manual** and **Install Guide** as PDFs.
- Manual screenshots were updated.
