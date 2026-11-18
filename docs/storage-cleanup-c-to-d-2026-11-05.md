# Dọn Dẹp Ổ C: Chuyển Dữ Liệu Nguội Sang `D:\GTA Archive` Kèm NTFS Junction (`2026-11-05`)

## 1. Tóm tắt kết quả

- **Mục tiêu**: Giải phóng dung lượng ổ NVMe `C:` (trước khi dọn chỉ còn `15.44 GiB` / `3.2%`, sát ngưỡng an toàn `~12.8 GiB` của `deploy_skins.py` cho `COMPONENTPEDS.img`) mà **không đụng chạm bất kỳ file runtime nào** của `gta sa gameplay-lab` và không làm gãy bất kỳ đường dẫn hay script rollback nào.
- **Kết quả dung lượng thực tế (`shutil.disk_usage`)**:
  - **Ổ `C:` (NVMe SSD `475.69 GiB`)**: tăng từ **`15.44 GiB`** trống lên **`29.90 GiB`** trống (**giải phóng `+14.48 GiB`** ngay sau khi dọn).
  - **Ổ `D:` (USB HDD `1,862.98 GiB`)**: giảm từ **`974.77 GiB`** trống xuống **`960.31 GiB`** trống (`51.5%` còn trống).
- **Quy mô kiểm chứng**:
  - Đã di chuyển **`25/25` thư mục** (`1` kho tư liệu gốc `ProjectEagleModPack` + `24` thư mục `staging/project-eagle/*` đã hoàn tất).
  - Tổng cộng **`9,198` file duy nhất** (`1,225` thư mục con, **`15,488,443,871` bytes = `14.42 GiB`**) đã được chép qua file tạm `.migration-part`, băm `SHA-256` hai chiều (lúc chép + đọc lại từ đĩa `D:` đối chiếu 100%), kiểm tra nguyên trạng bản gốc trên `C:` trước khi `unlink()`, xóa thư mục rỗng bằng `rmdir()` và nối lại **NTFS Junction** tại đúng đường dẫn cũ trên `C:`.
- **Journal & Script thực thi**:
  - Kế hoạch đích: [`staging/project-eagle/storage-migration-2026-11-05/roots.json`](../../staging/project-eagle/storage-migration-2026-11-05/roots.json)
  - Công cụ chuyển xác minh: [`staging/project-eagle/storage-migration-2026-11-05/move_storage.py`](../../staging/project-eagle/storage-migration-2026-11-05/move_storage.py)
  - Biên bản `SHA-256` đầy đủ (`9,198` file): `staging/project-eagle/storage-migration-2026-11-05/migration.json`

---

## 2. Những gì ĐƯỢC GIỮ VẬT LÝ trên ổ `C:` (Không chuyển sang Junction)

Để đảm bảo tốc độ load game/build tối đa và tuyệt đối không vi phạm các hàm chặn reparse point (`_assert_no_reparse` / `root.resolve() == root`), các thành phần sau vẫn nằm **vật lý 100% trên NVMe `C:`**:

1. **Toàn bộ bản chơi runtime**: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab` (`0` file bị sửa đổi).
2. **Công cụ, dữ liệu điều phối & sao lưu nóng**: `tools/`, `data/project-eagle/`, `backups/project-eagle/`, `docs/`.
3. **Các thư mục `staging/project-eagle/*` có guard chống reparse point hoặc đang giữ vai trò nguồn rollback trực tiếp**:
   - `art-library-install-20261103` (`176.79 MiB` — gọi `_assert_no_reparse` trên `R`)
   - `menu-autonext-no-intros-20261103` (nguồn plugin `WibuMenu.asi` mới nhất + rollback active)
   - `art-library-review-20261101` & `presentation-closeout-20261103` (gallery/manifest duyệt 178 ảnh)
   - `startup-intros-20261101` (`85.58 MiB` — `manage_intro.py` gọi `_assert_no_reparse(HERE, ROOT)`)
   - `menu-music-random-20261023` & `menu-music-studio-20261023`
   - `merge-clean-to-lab-2026-10-22` (`merge_game.py` kiểm `root.resolve() == root`)
   - `storage-migration-2026-10-22` & `storage-migration-2026-11-05` (biên bản di chuyển ổ đĩa)
   - `dryxio-tools` (`1,225.24 MiB` — chứa `6` junction con lồng bên trong và `25,479` file cache nhỏ; giữ trên SSD để tránh chậm IOPS trên USB HDD).

---

## 3. Danh sách 25 thư mục đã chuyển sang `D:\GTA Archive` (kèm NTFS Junction tại `C:`)

| # | Đường dẫn Junction tại `C:\Users\LENOVO\Desktop\GTA\` | Đích vật lý trên `D:\GTA Archive\` | Số file | Dung lượng (`MiB`) |
|---:|---|---|---:|---:|
| 1 | `ProjectEagleModPack` | `D:\GTA Archive\ProjectEagleModPack` | 5,670 | 10,539.61 |
| 2 | `staging/project-eagle/loading-batches` | `D:\GTA Archive\Staging\project-eagle\loading-batches` | 806 | 763.95 |
| 3 | `staging/project-eagle/menu-batches` | `D:\GTA Archive\Staging\project-eagle\menu-batches` | 600 | 713.16 |
| 4 | `staging/project-eagle/loading-screens` | `D:\GTA Archive\Staging\project-eagle\loading-screens` | 349 | 563.76 |
| 5 | `staging/project-eagle/mondstadt-persona-chat-20261104` | `D:\GTA Archive\Staging\project-eagle\mondstadt-persona-chat-20261104` | 123 | 359.04 |
| 6 | `staging/project-eagle/mondstadt-batch1-sucrose-diona-amber-eula-20261105` | `D:\GTA Archive\Staging\project-eagle\mondstadt-batch1-sucrose-diona-amber-eula-20261105` | 86 | 338.72 |
| 7 | `staging/project-eagle/waifulink-kirara-qa-20261104` | `D:\GTA Archive\Staging\project-eagle\waifulink-kirara-qa-20261104` | 124 | 242.51 |
| 8 | `staging/project-eagle/vanilla-gf-hsr-zzz-20261104` | `D:\GTA Archive\Staging\project-eagle\vanilla-gf-hsr-zzz-20261104` | 34 | 168.50 |
| 9 | `staging/project-eagle/bug-006-007-fix-2026-10-23` | `D:\GTA Archive\Staging\project-eagle\bug-006-007-fix-2026-10-23` | 26 | 155.92 |
| 10 | `staging/project-eagle/waifulink-jp-voice-20261104` | `D:\GTA Archive\Staging\project-eagle\waifulink-jp-voice-20261104` | 348 | 149.18 |
| 11 | `staging/project-eagle/eaglephone-ui-v6-20261104` | `D:\GTA Archive\Staging\project-eagle\eaglephone-ui-v6-20261104` | 203 | 143.12 |
| 12 | `staging/project-eagle/wibu-menu` | `D:\GTA Archive\Staging\project-eagle\wibu-menu` | 149 | 131.20 |
| 13 | `staging/project-eagle/island-bridges-gps-fix-2026-10-23` | `D:\GTA Archive\Staging\project-eagle\island-bridges-gps-fix-2026-10-23` | 11 | 78.94 |
| 14 | `staging/project-eagle/loading-art-refresh-20261101` | `D:\GTA Archive\Staging\project-eagle\loading-art-refresh-20261101` | 38 | 66.33 |
| 15 | `staging/project-eagle/waifulink-citlali-qa-20261104` | `D:\GTA Archive\Staging\project-eagle\waifulink-citlali-qa-20261104` | 35 | 54.91 |
| 16 | `staging/project-eagle/waifulink-hutao-qa-20261103` | `D:\GTA Archive\Staging\project-eagle\waifulink-hutao-qa-20261103` | 50 | 50.00 |
| 17 | `staging/project-eagle/character-noelle-fischl-20261028` | `D:\GTA Archive\Staging\project-eagle\character-noelle-fischl-20261028` | 146 | 42.53 |
| 18 | `staging/project-eagle/waifulink-vesna-qa-20261105` | `D:\GTA Archive\Staging\project-eagle\waifulink-vesna-qa-20261105` | 40 | 41.72 |
| 19 | `staging/project-eagle/waifulink-columbina-qa-20261104` | `D:\GTA Archive\Staging\project-eagle\waifulink-columbina-qa-20261104` | 43 | 37.71 |
| 20 | `staging/project-eagle/waifulink-furina-qa-20261104` | `D:\GTA Archive\Staging\project-eagle\waifulink-furina-qa-20261104` | 26 | 35.31 |
| 21 | `staging/project-eagle/gameplay-lab-poc` | `D:\GTA Archive\Staging\project-eagle\gameplay-lab-poc` | 103 | 32.59 |
| 22 | `staging/project-eagle/eagletimes-expansion-20261105` | `D:\GTA Archive\Staging\project-eagle\eagletimes-expansion-20261105` | 37 | 20.99 |
| 23 | `staging/project-eagle/eaglestake-casino-20261105` | `D:\GTA Archive\Staging\project-eagle\eaglestake-casino-20261105` | 26 | 15.13 |
| 24 | `staging/project-eagle/paimon-agent-20261025` | `D:\GTA Archive\Staging\project-eagle\paimon-agent-20261025` | 101 | 13.33 |
| 25 | `staging/project-eagle/trading-data-depth-20261105` | `D:\GTA Archive\Staging\project-eagle\trading-data-depth-20261105` | 24 | 12.75 |
| **Tổng** | **25 NTFS Junctions** | **`D:\GTA Archive\...`** | **9,198** | **14,770.91 MiB (`14.42 GiB`)** |

---

## 4. Kiểm chứng hậu kỳ (Đã chạy thực tế)

1. **Kiểm tra Junction & Topology (`25/25 PASS`)**: Mọi đường dẫn gốc trên `C:` đều mang cờ `FILE_ATTRIBUTE_REPARSE_POINT`, `Path.resolve()` khớp chính xác đích trên `D:\GTA Archive`, đọc thư mục qua đường dẫn `C:` bình thường và `hardlink_topology_verified = true`.
2. **Presentation Rollback Preflight (`PASS`, read-only)**:
   - `python staging/project-eagle/menu-autonext-no-intros-20261103/deploy_plugin.py rollback-preflight` -> `{"result": "rollback_preflight_passed", "runtime_written": false}`.
   - `art-library-install-20261103/deploy_library.py` (`sources()` + `guard()`) -> **`PASS`**: xác nhận trọn bộ `180` payload đóng gói và toàn bộ **`178/178` file ảnh gốc** (đọc xuyên qua các junction `loading-batches`, `menu-batches`, `loading-screens`, `wibu-menu`, `loading-art-refresh-20261101`) khớp `SHA-256` 100%.
3. **Kiểm tra sức khỏe Runtime (`eagle_doctor.py`)**:
   - `python "Project Eagle/gta sa gameplay-lab/eagle_doctor.py"` -> **`11/11 PASS, 0 WARN, 0 FAIL`**.
