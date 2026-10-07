# LaserVision
LaserVision: camera print-and-cut for LightBurn + Ruida (Thunder) lasers

I print acrylic items, then cut them out on my Thunder Nova 51. Lining the cut up with the print by hand was slow and never quite exact. So I (AI DID IT!) built a small Windows app that uses a USB camera on the laser head to find the registration marks and line everything up for me.

[image 1: how it works]

How it works

The customer's cut PDF has 3 or more small black dots (0.25 in), staggered so the sheet's orientation can't be mixed up. Open the PDF, and LaserVision finds the marks and cut lines automatically.
Lay the printed sheet on the bed, roughly straight. Jog the camera near the first mark and press Auto-measure. The head visits each mark, centres the camera on it and measures where it really is.
LaserVision works out how the sheet actually sits on the bed, including rotation, offset and any print scaling. It then writes an aligned LightBurn file that uses your own layer presets from an existing .lbrn2 file.
Save + open in LightBurn, or Save + CUT to start the job after a confirmation.

[image 2: main window] [image 3: camera finding a mark] [image 4: bed view before and after]

What else it does

Calibration: done once. A quick scale test, then 5 low-power pulse burns tell it exactly where the beam fires compared with the camera.
Camera check: after every job it checks whether the camera has been bumped or the mount is sagging.
Cut file checks: it warns about doubled or overlapping cut lines (from traced or outlined strokes) and about prints that came out scaled.
Per-colour layers: each cut-line colour can go on its own layer, be left out, or be shown as a reference only.
Reg marks on T1: they're added on a tool layer, so you see them in LightBurn but they're never cut.
Help: a built-in manual (F1), plus a PDF install guide and user manual.

[image 5: calibration]

What you need: Windows 10/11, LightBurn, a Ruida controller on the network, a USB camera on the head (I use an Arducam B0205 at first, then switched to a endoscope), and Python (the install guide walks through it).

Link to Endoscope Camera used: https://www.amazon.com/dp/B09B716SK3 <br>
Link to the Arducam B0205 originally used: https://www.amazon.com/dp/B0829HZ3Q7 <br>
Included in the files is the mount I used for the endoscope camera.  This was built for my Thunder 51 so you may need to make changes.

On my machine the test sheet cut right on the printed lines for every shape. Happy to hear how it works on other machines.

Needed install instructions and manual are in the zip file.
I will not support this project as I don't have time.
You may suggest things, I will try and add them as I see fit for my needs.
ENJOY!
