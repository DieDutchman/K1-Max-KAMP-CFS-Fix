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
3. **Link to printer.cfg:** Add this line to your main `printer.cfg` (or ensure your includes point to the new files):
   ```gcode
   [include /usr/data/printer_data/config/KAMP/KAMP_Settings.cfg]
