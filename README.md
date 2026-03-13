# Creality K1 Max + CFS: Hardware Optimization & Spoolman Integration

This repository contains an optimized configuration for the **Creality K1 Max** and **CFS (Creality Filament System)**. This setup is specifically designed to bypass the common "Key 60" firmware error by using direct Slicer-to-CFS communication while maintaining full **Spoolman** database synchronization.

## 🚀 Key Features
* **Zero-Y CR-Touch Integration:** Specific offsets for the Zero-Y mount to ensure perfect bed meshing and first-layer consistency.
* **Spoolman Automation:** Real-time filament consumption tracking and active spool marking in your Spoolman database.
* **Key 60 Bypass:** Uses conditional Slicer G-code to call native CFS commands directly, avoiding Klipper "Internal Error" crashes caused by nested macros.
* **KAMP (Klipper Adaptive Mesh & Purge):** Integrated support for smart leveling and purging.

---

## 🛠️ Installation & Setup

### 1. Klipper Configuration
1. Upload `spoolman_cfs.cfg` to your printer's configuration folder.
2. In your `printer.cfg`, add the following line: 
   `[include spoolman_cfs.cfg]`
3. Ensure your `moonraker.conf` is configured to communicate with your Spoolman server.

### 2. OrcaSlicer Setup (Required for CFS Stability)
To prevent the `Key 60` internal error, this setup bypasses the use of `SELECT_T` macros in favor of direct calls. 

In OrcaSlicer, navigate to **Printer Settings** > **Machine G-code** > **Change filament G-code** and paste:

```gcode
; Update Spoolman Data
SYNC_SPOOLMAN SLOT=[next_extruder]

; Trigger Native CFS Load (Direct Call to bypass Key 60)
{if next_extruder == 0}
  BOX_LOAD_MATERIAL_WITH_MATERIAL TNN=T1A
{elsif next_extruder == 1}
  BOX_LOAD_MATERIAL_WITH_MATERIAL TNN=T1B
{elsif next_extruder == 2}
  BOX_LOAD_MATERIAL_WITH_MATERIAL TNN=T2A
{elsif next_extruder == 3}
  BOX_LOAD_MATERIAL_WITH_MATERIAL TNN=T2B
{endif}
```
### 3. Hardware Calibration (Zero-Y Mount)
If you are using a Zero-Y offset mount:

Z-Offset: Live-adjust your Z-offset during your first test print. Once perfected, run SAVE_CONFIG in the console.

PTFE Slack: Ensure the PTFE tube leading from the CFS to the toolhead has enough slack to prevent the tube from pulling on the toolhead at the front of the bed, which can cause Z-offset inconsistencies.

Command,Description
MAP_ALL_SPOOLS,"Manually assign Spoolman IDs to CFS slots (e.g., MAP_ALL_SPOOLS SLOT0=12 SLOT1=5)."
STATUS_SPOOL_MAP,Prints the current CFS-to-Spoolman ID assignments in the console.
SYNC_SPOOLMAN,Manually triggers an active spool update in the Spoolman database for a specific slot.
CLEAR_CFS_SPOOLS,Resets all slot assignments to 0.

🤝 Credits & Acknowledgments
Guilouz - Creality K1 Series Helper Script

Donkie - Spoolman

kageiit - KAMP

Creality Official Klipper Repo

🚀 Status: Feature Complete & Stable
The "Key 60" error is resolved by moving tool-change logic from Klipper macros to the Slicer's conditional G-code.

