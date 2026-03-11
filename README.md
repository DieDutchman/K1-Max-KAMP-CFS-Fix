🚀 K1 Max Ultimate Setup: KAMP + CFS + Zero Y-Offset CR-Touch
This repository contains a fully tested, "production-ready" configuration for the Creality K1 Max. It solves the notorious Key 61, Key 60, and Key 172 errors that occur when combining KAMP with the rooted Helper Script.

🛠️ Hardware Requirements
Printer: Creality K1 Max

AMS: CFS (Creality Filament System)

Probe: CR-Touch using this Zero Y-Offset Mount.

Note: Using a Zero Y-Offset mount significantly improves bed mesh accuracy.

📁 Repository Structure
/KAMP: Contains adaptive meshing, smart parking, and the fixed Line_Purge_CRTouch.cfg.

/Config_Files:

printer.cfg: Includes tuned stepper limits and [bltouch] offsets for the Zero-Y mount.

box.cfg: Essential logic for the CFS integration.

gcode.macro.cfg: Custom macros including the CX_PRINT_DRAW_ONE_LINE fix.

❌ Resolved Issues
Key 61 (Unknown Command): Fixed by promoting macros from private (_) to public and using absolute include paths.

Key 172 (Recursion Error): Fixed the infinite loop in LINE_PURGE by removing self-referencing calls.

Key 60 (Internal Error): Resolved conflicts between KAMP and the factory CX_PRINT_DRAW_ONE_LINE macro.

CFS Priming: Optimized the purge sequence to ensure the CFS is fully primed near the print area.

📥 Installation
Mount the Hardware: Print and install the CR-Touch using the Printables link.

Upload Configs: Place the KAMP and Config_Files folders into your /usr/data/printer_data/config/ directory.

Link to printer.cfg: Add this line to your main printer.cfg:

G-Code
[include /usr/data/printer_data/config/KAMP/KAMP_Settings.cfg]
Slicer Setup: Enable Exclude Objects in OrcaSlicer or Creality Print and set your Start G-Code to:

G-Code
START_PRINT EXTRUDER_TEMP=[nozzle_temperature_initial_layer] BED_TEMP=[bed_temperature_initial_layer]
⚠️ Disclaimer & Safety
USE AT YOUR OWN RISK. This setup modifies physical travel limits.

Verify Limits: Move your toolhead manually to X0 Y0 and X300 Y300 to ensure the CR-Touch doesn't hit the frame.

Z-Offset: You must calibrate your Z-Offset after installing the new mount before your first print.

How to use this for your GitHub:
Go to your GitHub repo.

Click the Edit (pencil) icon on README.md.

Delete everything and paste the text above.

Commit changes.

This looks like a professional-grade resource now! Would you like me to help you double-check the x_offset and y_offset values in your printer.cfg to make sure they match that specific "Zero Y" mount before you upload?
