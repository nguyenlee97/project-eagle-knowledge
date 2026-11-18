# Correlated Crash Report: `CRASH-2026-11-18_08-18-42`

- **Generated At**: `2026-11-18 08:18:43`
- **Crash Dump File**: `ProjectEagle_crashes/2026-11-18_08-18-42.log` (`2026-11-18 08:18:42`)
- **Classification**: **`EXIT_CLEANUP_HARMLESS`** (`LOW (On Game Exit)`)
- **Exception**: `0xC0000005: Access violation write` at `0x6234F6DD` in `std.data.dll (+0x0016F6DD)`
- **Last File Loaded**: `gta_pe.set` | **Last DLL**: `kernel32.dll`
- **Diagnosis (EN)**: Process exit cleanup crash in std.data.dll (+0x0016F6DD) after ExitProcess/LdrShutdownProcess. Happens when quitting GTA SA while ModLoader std.data.dll frees static hooks; does NOT affect gameplay.
- **Chẩn đoán (VI)**: Loi don bo nho luc bam Thoat Game trong std.data.dll (+0x0016F6DD) (sau ExitProcess/LdrShutdownProcess). Xay ra sau khi ban da dong game, KHONG anh huong qua trinh choi.

## 1. Gameplay Flight Recorder (Last Known State Before Exit/Crash)
- **Coordinates**: `(2697.89, -1609.80, 1653.09)` | **Heading**: `356.9°`
- **Zone / Area**: `Los Santos (SA) (LA01) - Sector LA` (`Int: 1 / Area: 1`)
- **Vehicle State**: `ON FOOT` | **Trail 5s**: `Trail 5s: -5s(2696,-1609,1653.1) -> -3s(2696,-1609,1653.1) -> Now(2698,-1610,1653.1)`
- **Streaming Memory**: `766.9 MiB / 768.0 MiB`

## 2. Native Callstack / Backtrace
```text
0x00000000: sub_6234F6DD in std.data.dll (+0x9de20000)
0x773BDC20: LdrShutdownProcess in ntdll.dll (+0x5dc20)
0x773BDB50: RtlExitUserProcess in ntdll.dll (+0x5db50)
0x754B6A20: ExitProcess in KERNEL32.DLL (+0x26a20)
0x63242470: DebugMenuEntrySetWrap in PECore.asi (+0xa2470)
0x63242470: DebugMenuEntrySetWrap in PECore.asi (+0xa2470)
0x63242470: DebugMenuEntrySetWrap in PECore.asi (+0xa2470)
0x63242470: DebugMenuEntrySetWrap in PECore.asi (+0xa2470)
```

## 3. Tail of `fastman92limitAdjuster.log` (Last 15 Lines)
```text
---------------------------------------------
Radar blip sprite filename loader: config was loaded. ms_numberOfTypeIDs = 200
---------------------------------------------
Vehicle audio loader is enabled
---------------------------------------------
Train type carriages loader is enabled. ms_numberOfTypeIDs = 24, ms_maxNumberOfVehiclesForType = 24.
---------------------------------------------
"Copy info to pad 1 from pad 0" is enabled now.
---------------------------------------------
FLA loading text is disabled.
---------------------------------------------
CThePluginPatches::RegisterPatcher executed.
---------------------------------------------
Number of memory changes made: 10172
---------------------------------------------
```

## 4. Tail of `cleo.log` (Last 15 Lines)
```text
18/11/2026 08:16:26.869
18/11/2026 08:16:26.869 Loading custom script 'cleo\PedsCountrySIde.qa'...
18/11/2026 08:16:26.871 Registering custom script named 'PedsCou'
18/11/2026 08:16:29.896
18/11/2026 08:16:29.896 [0A92] Starting new custom script cleo\PedsWalk2.qa from thread named 'startbp'
18/11/2026 08:16:29.896
18/11/2026 08:16:29.896 Loading custom script 'cleo\PedsWalk2.qa'...
18/11/2026 08:16:29.897 Registering custom script named 'PedsWal'
18/11/2026 08:16:38.113
18/11/2026 08:16:38.113 Unregistering custom script named 'wk2peds'
18/11/2026 08:16:38.113 Unregistering custom script named 'hmpeds'
18/11/2026 08:16:38.519
18/11/2026 08:16:38.519 Unregistering custom script named 'cspeds'
18/11/2026 08:16:38.636
18/11/2026 08:16:38.636 Unregistering custom script named 'stpeds'
```
