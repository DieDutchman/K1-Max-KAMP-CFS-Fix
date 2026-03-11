# 🚀 K1 Max Ultimate Setup: KAMP + CFS + Zero Y-Offset CR-Touch

This repository contains a fully tested, "production-ready" configuration for the Creality K1 Max. It solves the notorious **Key 61**, **Key 60**, and **Key 172** errors that occur when combining KAMP with the rooted Helper Script while using the CFS.

## 🛠️ Hardware Requirements
* **Printer:** Creality K1 Max
* **AMS:** CFS (Creality Filament System)
* **Probe:** CR-Touch using this **[Zero Y-Offset Mount](https://www.printables.com/model/1073375-cr-touch-mount-k1-k1maxk1c-zero-y-offset)**.
    * *Note: Using a Zero Y-Offset mount significantly improves bed mesh accuracy and eliminates tilt-related calculation errors.*

## 📁 Repository Structure
* **/KAMP**: Contains adaptive meshing, smart parking, and the fixed `Line_Purge_CRTouch.cfg`.
* **/Config_Files**: 
    * `printer.cfg`: Includes tuned stepper limits and `[bltouch]` offsets specifically for the Zero-Y mount.
    * `box.cfg`: Essential logic and macros for the **CFS** (Creality Filament System) integration.
    * `gcode.macro.cfg`: Custom macros including the safety "dummy" `CX_PRINT_DRAW_ONE_LINE` fix.

## ❌ Resolved Issues
* **Key 61 (Unknown Command):** Fixed by promoting macros from private (`_`) to public and ensuring path visibility.
* **Key 172 (Recursion Error):** Fixed the infinite loop in `LINE_PURGE` caused by the macro calling its own name.
* **Key 60 (Internal Error):** Resolved conflicts between KAMP and the factory-coded `CX_PRINT_DRAW_ONE_LINE` macro.
* **CFS Priming:** Optimized the sequence to ensure the CFS is fully primed near the print area after a filament load.

## 📥 Installation

1. **Mount the Hardware:** Print and install the CR-Touch using the [Printables mount](https://www.printables.com/model/1073375-cr-touch-mount-k1-k1maxk1c-zero-y-offset).
2. **Upload Configs:** Place the `KAMP` and `Config_Files` folders into your `/usr/data/printer_data/config/` directory.
3. **Link to printer.cfg:** Add this line to your main `printer.cfg`:
   ```gcode
   [include /usr/data/printer_data/config/KAMP/KAMP_Settings.cfg]
4. **Slicer Setup:** * Enable **Exclude Objects** in OrcaSlicer or Creality Print.
   * Set your **Machine Start G-Code** to:
   ```gcode
   START_PRINT EXTRUDER_TEMP=[nozzle_temperature_initial_layer] BED_TEMP=[bed_temperature_initial_layer]
   
## 🔧 Recommended START_PRINT Sequence
To ensure the CFS and KAMP work in harmony, use this logic in your `START_PRINT` macro:

```gcode
[gcode_macro START_PRINT]
gcode:
    {% set BED_TEMP = params.BED_TEMP|default(60)|float %}
    {% set EXTRUDER_TEMP = params.EXTRUDER_TEMP|default(200)|float %}
    M140 S{BED_TEMP}            # Start heating bed
    G28                         # Home all axes
    M190 S{BED_TEMP}            # Wait for bed
    BED_MESH_CALIBRATE          # KAMP Adaptive Meshing
    SMART_PARK                  # KAMP Smart Park near object
    M109 S{EXTRUDER_TEMP}       # Wait for nozzle
    LINE_PURGE                  # KAMP Adaptive Purge (CFS Priming)
```

## ⚠️ Disclaimer & Safety
**USE AT YOUR OWN RISK.** This setup modifies physical travel limits.
* **Verify Limits:** After installing, move your toolhead manually to `X0 Y0` and `X300 Y300` to ensure the CR-Touch doesn't strike the frame.
* **Z-Offset:** You **must** recalibrate your Z-Offset/Probe Calibration after installing the new mount before your first print to avoid bed damage.

---
**Credits:** Created to help the K1 Max community integrate KAMP, CFS, and CR-Touch sensors seamlessly.
