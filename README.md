# Creality K1 Max + CFS: Ultimate Hardware & Software Integration

This repository contains my optimized configuration for the **Creality K1 Max** and **CFS (Creality Filament System)**. It bridges the gap between factory firmware and professional-grade Klipper features, specifically for users running rooted setups with the Creality Helper Script.

## 🚀 Key Features
* **Zero-Y CR-Touch Integration:** Correctly configured offsets for the Zero-Y mount to ensure perfect bed meshing.
* **Spoolman Automation:** Real-time filament tracking that deducts usage automatically during multicolor prints.
* **UI-Driven Mapping:** A custom "Master Form" macro to set all 4 CFS slots at once via the dashboard pop-up.
* **Error-Free Toolchanging:** Custom `SELECT_T` logic to prevent `Key 57` and `Key 167` firmware conflicts.
* **KAMP (Klipper Adaptive Mesh & Purge):** Adaptive leveling for faster, more accurate print starts.

---

## 🛠️ Installation & Setup

### 1. Hardware Calibration (Zero-Y Mount)
If you are using the Zero-Y offset mount, you must ensure your Z-offset is saved to avoid collisions:
1. Start a test print.
2. Live-adjust your Z-offset via the dashboard until the first layer is perfect.
3. **Crucial:** Run `SAVE_CONFIG` in the console. This moves the offset from the temporary state to your `printer.cfg`.

### 2. Slicer Configuration
Update your filament change G-code in **OrcaSlicer** (or your preferred slicer) to talk to the new macros:
* **Printer Settings** > **Machine G-code** > **Change filament G-code**:
    ```gcode
    SELECT_T[next_extruder]
    ```

### 3. Spoolman Mapping
* **Session Mapping:** Click the `MAP_ALL_SPOOLS` button in your macro panel to assign IDs for your current project.
* **Persistent Mapping:** For filaments you leave in the CFS long-term, edit the top of `spoolman_cfs.cfg` so they load automatically on restart:
    ```gcode
    variable_slot0_id: 12  # Set your most-used Spool ID here
    ```

---

## 📜 Custom Macros & Commands

| Command | Description |
| :--- | :--- |
| `MAP_ALL_SPOOLS` | Opens a UI pop-up to map all 4 slots in one go. |
| `STATUS_SPOOL_MAP` | Displays current CFS-to-Spoolman assignments in the console. |
| `CLEAR_CFS_SPOOLS` | Resets all active mappings to 0. |

---

## ⚠️ Disclaimer & Safety
* **Physical Slack:** Ensure the PTFE tube leading from the CFS to the toolhead has a sufficient arc. If the tube is too short, it can physically lift the toolhead during high-speed movement, causing inconsistent Z-offsets and "phantom" first-layer issues.
* **Macro Conflict:** This config uses `SELECT_T` macros because the K1 firmware locks the default `T0-T3` commands. Attempting to rename them to standard `T` commands will trigger a firmware halt (`Key 167`).

---

## 🤝 Credits & Acknowledgments
This project is built upon the incredible work of the 3D printing community:

* **[Guilouz - Creality K1 Series Helper Script](https://github.com/Guilouz/Creality-K1-Series-Helper-Script)** - For the rooting foundations and base CFS logic.
* **[Donkie - Spoolman](https://github.com/Donkie/Spoolman)** - For the essential filament inventory database.
* **[kageiit - KAMP](https://github.com/kageiit/Klipper-Adaptive-Mesh-Purging)** - For the intelligent leveling and purging system.
* **[Creality](https://github.com/CrealityOfficial)** - For the K1 Max and CFS hardware platforms.

---

### 🚀 Happy Printing!
If this configuration helped you get your CFS running smoothly, please consider leaving a ⭐ on this repository!
