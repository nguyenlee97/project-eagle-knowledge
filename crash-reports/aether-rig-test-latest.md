# Aether Main Character In-Game Rig & Action Verification Report

- **Timestamp**: `2026-11-06 11:15:59` (`3654 ms`)
- **Origin Coords**: `(1480.80, -1676.00, 14.05)`
- **Overall Result**: **`Aether Rig & Action Test WARN: 5/6 PASS (3654ms)`**

| Step ID | Check Name | Status | Details |
| :--- | :--- | :---: | :--- |
| `01_CLUMP_AND_MODEL_RAM` | Aether RpClump, Model Info & Collision in RAM | **`PASS`** | ped_ptr=0x23925020, model_id=0, m_pRwObject=0x342636C0, TXD_slot=45 |
| `02_WALK_IMPULSE` | Walk Movement & Ground Contact Stability | **`PASS`** | Moved 0.87m smoothly | dz=+0.00m |
| `03_SPRINT_IMPULSE` | Sprint Response & Seam Continuity | **`WARN`** | Sprinted 0.76m | End Z=14.05m |
| `04_JUMP_AND_LAND_COL` | Jump Arc & Solid .COL Landing Check | **`PASS`** | Peak dZ=+5.58m, Landed Z=19.08m (Start Z=14.05m) |
| `05_WEAPON_AND_STATE` | Weapon Slot, PedState & Hierarchy Integrity | **`PASS`** | ActiveSlot=0, WeaponType=0, PedState=1, RwObject=0x342636C0 |
| `06_CAMERA_AND_SCREENSHOT` | Camera Tracking & Live Frame Capture | **`PASS`** | Camera=OK, Screenshot=aether-rig-verification-latest.png (2953.1 KB) |

## Live Verification Screenshot (`1920x1080`)
![Aether Verification](bug-snapshots/aether-rig-verification-latest.png)
