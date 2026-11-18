# Wibu menu staged installation

**03/11 — Presentation DONE / user runtime PASS:** người dùng xác nhận toàn bộ thay đổi hoạt động hoàn hảo. [Project state / điểm vào cho agent](../presentation-current-state.md).178ảnh đã duyệt/cài, loading2s/menu4s, nhạc random+tự đổi bài, true intro bypass. Đã dọn40file build/QA/cache tạm; giữ nguồn/artwork/TXD/ASI/backup. Không còn việc chờ trong task này.

**03/11 — Đã cài menu tự đổi bài / true intro skip:** [Bàn giao và rollback](../loading-screens/menu-autonext-no-intros-2026-11-03.md). Hết bài chọn ngẫu nhiên bài khác, không ghi default; bỏ qua hai trạng thái movie trước decoder. Chỉ đổi WibuMenu+state;178TXD, timer2s/4s, playlist/INI, PECore/exe/movie giữ nguyên. Build/native probes/hash/rollback-preflight đạt; chưa mở game, chờ user test. Nguồn hiện tại `staging/project-eagle/menu-autonext-no-intros-20261103`.

**Current installation03/11/2026:** [Approved178 library + timed rotation](../loading-screens/library-install-2026-11-03.md) is installed to gameplay-lab. Current source/deploy/rollback is `staging/project-eagle/art-library-install-20261103`; loading2s/menu4s and original menu music retained. The legacy32-file/clean instructions below are historical; do not rerun against the current installation.

**Current revision:** the render/audio fix has been installed after the user closed the game. All 32 live hashes match; the user's INI is byte-identical to its pre-update backup, and 74 protected files are unchanged. History: `backups/project-eagle/wibu-menu-installs/install-20261022-051017-453`. Runtime confirmation is pending the user's own test. See `render-audio-fix.md`. On updates the installer preserves the live INI, so its hash may intentionally differ from the package default.

The install and rollback scripts target only the audited main-clean folder:

`C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa clean\gta sa clean`

They verify `gta_sa.exe` against the recorded SHA-256 before doing anything and
refuse work if a GTA process is running or if target directories contain a
reparse point. All package sources must resolve beneath
`staging/project-eagle/wibu-menu/dist`. The scripts write no game files during
preflight.

## Prepare the staged package

After the plugin build, final config, 23 cover TXDs, logo TXD, and five menu
audio tracks are in `staging/project-eagle/wibu-menu/dist`, regenerate the
hash manifest:

```powershell
& .\staging\project-eagle\wibu-menu\scripts\prepare_menu_install_manifest.ps1
```

The manifest is written to
`staging/project-eagle/wibu-menu/dist/wibu-menu-install-manifest.json`. It
contains one SHA-256 and size for each allowed source, the fixed game identity,
and explicit missing/extra file lists. It is marked complete only when the
exact 32-file package exists: `WibuMenu.asi`, one config, 23 cover TXDs, the
logo TXD, five MP3 tracks, and `plugins/wibu-menu/audio-runtime/wibu-bass.dll`.
Extra package files also make it incomplete. The initial install was 31 files;
the updater accepts that complete prior state for migration.

## Install

Review the read-only preflight first, then run the installer when ready:

```powershell
& .\staging\project-eagle\wibu-menu\scripts\install_menu.ps1 -PreflightOnly
& .\staging\project-eagle\wibu-menu\scripts\install_menu.ps1
```

The installer copies only the exact allowlist into the game root and
`plugins/wibu-menu`. An initial install refuses an existing `WibuMenu.asi` or
data folder unless a valid Wibu-owned install state proves the files belong to
this package. Updates back up every existing owned file first, including the
latest mutable `wibu-menu.ini`; unknown files in an owned folder are preserved.
Each copy is checked against the staging hash manifest. It then compares a
before/after protection snapshot of root ASIs, executables, DLLs and config files,
LOADSCS base/overlay TXDs, and radio files/config (`data/radio.dat`,
`models/txd/radio.txd`, `audio/PE/RADIO`, radio-named configs, including
`PECore.ini`).

Install state is written to
`plugins/wibu-menu/.wibu-menu-install-state.json`. History and update backups
are written under
`backups/project-eagle/wibu-menu-installs/install-<timestamp>`.
The installer does not launch the game.

## Roll back

```powershell
& .\staging\project-eagle\wibu-menu\scripts\rollback_menu.ps1 -PreflightOnly
& .\staging\project-eagle\wibu-menu\scripts\rollback_menu.ps1
```

Rollback uses only the recorded owned paths. It removes a file only when its
current hash matches the install state. The menu config is mutable through F6;
rollback saves its latest contents under
`backups/project-eagle/wibu-menu-installs/rollback-<timestamp>/latest-config/`
before removing it, even when its hash has changed. Modified non-config files
and unknown files are preserved and listed in the rollback report. It never
recursively deletes the Wibu data folder.

Install and rollback reports include the protected snapshot comparison and
file actions. The final install succeeded with all 31 live hashes matching and
74 protected files unchanged. Rollback preflight passed; rollback itself has
not been executed. History: `backups/project-eagle/wibu-menu-installs/install-20261022-045110-497`.
