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
