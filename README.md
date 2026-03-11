# 🚀 KAMP Fix for Creality K1 Max (CFS + CR-Touch Optimized)

This repository provides a verified, "loop-free" configuration for **KAMP (Klipper Adaptive Meshing & Purging)** on the Creality K1 Max. 

## 🛠️ Hardware Setup
- **Printer:** Creality K1 Max
- **Probe:** CR-Touch (Modified Mount)
- **AMS:** CFS (Creality Filament System)
- **Firmware:** Rooted Klipper (Helper Script based)

## ❌ Errors This Fixes
- **Key 61:** "Unknown command: LINE_PURGE" 
- **Key 172:** "Macro LINE_PURGE called recursively" (Infinite loop crash)
- **Internal Error:** `CX_PRINT_DRAW_ONE_LINE` conflicts.

## 📥 Installation

1. Download this repository and upload the files to your `/usr/data/printer_data/config/KAMP/` directory.
2. In your main **`printer.cfg`**, you only need to add this one line if it is not already there:
   ```gcode
   [include Helper-Script/KAMP/KAMP_Settings.cfg]
   
## ⚠️ Critical Hardware Settings (CR-Touch & Stepper Limits)

This setup modifies the physical travel limits of the K1 Max to accommodate the CR-Touch sensor and the CFS system. **Do not use these values without verifying your physical clearances!**

### 📍 CR-Touch Offsets (In printer.cfg)
The `[bltouch]` section has been tuned for the specific CR-Touch mount (https://www.printables.com/model/1073375-cr-touch-mount-k1-k1maxk1c-zero-y-offset). 
* **Note:** Ensure your `x_offset` and `y_offset` match your specific printed bracket.

### 📏 Stepper Limit Changes
We adjusted `position_max` and `position_endstop` in the `[stepper_x]` and `[stepper_y]` sections. 
* This prevents the toolhead from crashing into the frame now that the CR-Touch adds extra width/depth to the assembly.

### 📦 CFS Integration (box.cfg)
The `box.cfg` file contains the essential logic for the **Creality Filament System**. This ensures that filament loading/unloading doesn't conflict with KAMP's adaptive purging.
