# Eagle Pre-Flight Doctor & Crash Audit Report

- **Timestamp**: `2026-11-17 18:26:53` (`128 ms`)
- **Overall Status**: **`PASS`** (`11/11 PASS`, `0 WARN`, `0 FAIL`)

## 1. 10-Point System Health Checks
| ID | Check Name | Status | Details |
| :--- | :--- | :---: | :--- |
| `01_CORE_BINARIES` | Core Binaries & ASI Patches | **`PASS`** | gta_pe.exe, PECore.asi, EagleStreamingFix.asi (10240B), CLEO+.cleo, WibuMenu.asi=OK |
| `02_STREAMING_BUDGET` | Streaming Memory & Vehicle Cap | **`PASS`** | FLA Memory available = 1536 MiB (1536 MiB optimal for 32-bit 4GB VAS; <=1920 safe) | PECore NumDesiredLoadedVeh = 35 |
| `03_GPS_GRAPH_PEGG` | GPS Routing Graph (pecore_gps_graph.pegg) | **`PASS`** | PEGG (hdr=32B, node=64B, edge=48B): 148,603 nodes, 253,122 edges (28,235,856B) |
| `04_MAP_MOUNTS_CACHE` | gta.dat Mounts & EagleMapIndex.cache | **`PASS`** | Checked 538 mounts (0 missing) | Cache: OK |
| `05_LUA_HUD_HEALTH` | SanViveLuaHudSA (hud.lua) & Error Trap | **`PASS`** | hud.lua (264,292 chars, ErrorTrap=Active) | Logged Lua Runtime Errors: 0 |
| `06_UI_TEXTURES` | EaglePhone v5.0 TXD & Web Assets | **`PASS`** | models/hud.txd (11,027,664B) | ui_assets/*.png: 61 files |
| `07_PAIMON_COMPANION` | Paimon Companion Service (App 11) | **`PASS`** | paimon_status.json (configured=True, backend=openai_compatible, err='none') |
| `08_VISUAL_POSTFX` | SkyGfx & EaglePostFXTune Config | **`PASS`** | EaglePostFXTune.cs=OK, EaglePostFXTune.ini=OK, skygfx1.ini=OK |
| `09_WRITE_LOCK` | Coordination Game-Write Lock | **`PASS`** | Unlocked (Clean) |
| `10_CRASH_AUDIT` | ProjectEagle_crashes History Audit | **`PASS`** | Total logs: 184 (Recent 15: 3 Gameplay, 12 Exit-only) | Latest: 2026-11-17_17-05-42.log -> EXIT_CLEANUP_HARMLESS | Last Gameplay: 2026-11-17_02-17-08.log -> MODEL_STREAMING_OR_RIG_FAULT |
| `11_ISLAND_BRIDGES_GPS` | 3D Island Bridges & GPS Unification | **`PASS`** | CUSTOM_MODS.ipl: 212 3D bridge spans + WIBU-01 Seto Ohashi: 18 suspension spans | PEGG nodes=148,603 (Comp #0=142,743) |

## 2. Recent Crash Logs Classification (`ProjectEagle_crashes/`)
| Log File | Timestamp | Classification | Fault Module & Address | Last File Loaded |
| :--- | :--- | :--- | :--- | :--- |
| `2026-11-17_17-05-42.log` | `2026-11-17 17:05:42` | `EXIT_CLEANUP_HARMLESS` | `0x6229F6DD` in `std.data.dll (+0x0016F6DD)` | `gta_pe.set` |
| `2026-11-17_10-52-38.log` | `2026-11-17 10:52:38` | `EXIT_CLEANUP_HARMLESS` | `0x6229F6DD` in `std.data.dll (+0x0016F6DD)` | `\\?\pipe\discord-ipc-9` |
| `2026-11-17_05-36-25.log` | `2026-11-17 05:36:25` | `EXIT_CLEANUP_HARMLESS` | `0x6229F6DD` in `std.data.dll (+0x0016F6DD)` | `gta_pe.set` |
| `2026-11-17_05-17-36.log` | `2026-11-17 05:17:36` | `EXIT_CLEANUP_HARMLESS` | `0x6229F6DD` in `std.data.dll (+0x0016F6DD)` | `cleo/EagleHudFast_1.lua` |
| `2026-11-17_03-29-46.log` | `2026-11-17 03:29:46` | `EXIT_CLEANUP_HARMLESS` | `0x6229F6DD` in `std.data.dll (+0x0016F6DD)` | `gta_pe.set` |
| `2026-11-17_03-01-32.log` | `2026-11-17 03:01:32` | `EXIT_CLEANUP_HARMLESS` | `0x6229F6DD` in `std.data.dll (+0x0016F6DD)` | `gta_pe.set` |
