# Bộ Công Cụ Kiểm Thử & Pháp Y Trong Game Theo Yêu Cầu (On-Demand Zero-Overhead In-Game Test & Forensic Suite)

- **Ngày triển khai**: `25/10/2026`
- **Target**: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`
- **Staging & Backup**: `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\in-game-test-suite-2026-10-25`
- **Phiếu bàn giao**: [`work-items/2026-10-25-antigravity-in-game-test-suite.md`](work-items/2026-10-25-antigravity-in-game-test-suite.md)

---

## 1. Nguyên Tắc Thiết Kế: `0%` Ảnh Hưởng Gameplay Mặc Định & `$0` Chi Phí Token (Không Dùng Computer Use)

1. **Tắt hoàn toàn khi chơi bình thường (`0%` Overhead Default)**:
   - Mặc định khi khởi động game, `EagleInGameTestSuite` ([`eagle_ingame_tester.py`](../../Project%20Eagle/gta%20sa%20gameplay-lab/eagle_ingame_tester.py)) hoàn toàn **ngủ đông (dormant)** — không tạo luồng chạy ngầm, không đọc `CPools` hay `CStreaming` trong lúc chơi.
   - Chỉ kích hoạt **theo yêu cầu (on-demand)** khi:
     - Người chơi bấm **`Ctrl + F11`** trong game để báo bug (chạy tức thì trong `< 80ms`), hoặc
     - Agent (Codex / Antigravity) hoặc người chơi chủ động gọi lệnh test qua CLI ([`eagle_doctor.py`](../../Project%20Eagle/gta%20sa%20gameplay-lab/eagle_doctor.py)) hoặc bấm nút trên Web UI (`http://127.0.0.1:8765` $\rightarrow$ App 8).
2. **Đọc/Ghi Trực Tiếp Cấu Trúc Engine Trong RAM (`GTA SA 1.0 US` + `Fastman92 Limit Adjuster 7.7`)**:
   - Tự động đọc địa chỉ động từ `fastman92limitAdjuster.log`:
     - `CModelInfo::ms_modelInfoPtrs` (`0x03E52020`, `200,000` DFF slots)
     - `CStreaming::ms_aInfoForModel` (`0x0411E020`, 20-byte `CStreamingInfo` với patch `int32_t base ID`, `LoadState` tại `+0x08`)
     - Dải ID: `DFF = 0..199999`, `TXD = 200000..264999`, `COL = 265000..329999`.

---

## 2. Chi Tiết 4 Mô-đun Kiểm Thử Trong Game

### Mô-đun 1: Forensic Bug Bundle, Camera Look-At X-Ray & Window Screenshot (`Ctrl + F11` / `--snapshot`)
- **Đọc Ma Trận Camera (`TheCamera` `0x00B6F028` & `CCam[0]` `0x00B6F19C`)**:
  - Lấy chính xác tọa độ mắt camera `(cx, cy, cz)`, vector hướng nhìn chuẩn hóa `(fx, fy, fz)`, góc phương vị, góc ngẩng và `FOV`.
- **Tia X-Quang Tâm Ngắm (`find_camera_lookat_targets`)**:
  - Kết hợp quét các vật thể động đang sống trong RAM (`PedPool`, `VehiclePool`, `ObjectPool`) và lưới không gian `.IPL` (`spatial_grid` `50m` + `coarse_large_grid` `200m`) dọc theo tia ngắm camera.
  - Xác định **Vật thể/NPC số 1 ngay trong tâm ngắm (`crosshair_target`)** kèm trạng thái nạp thực tế trong RAM (`ram_dff_loaded`, `ram_txd_loaded`, `ram_col_loaded`, số mặt tam giác `.COL` đang nạp trong `CCollisionData`).
- **Chụp Ảnh Cửa Sổ Game Không Phụ Thuộc Thư Viện Ngoài (`capture_game_window_png`)**:
  - Dùng Win32 GDI `BitBlt` (từ DWM Screen DC theo khung `ClientToScreen`) + `PrintWindow(PW_RENDERFULLCONTENT)` dự phòng, tự nén ra file `.png` chuẩn (`zlib` + `struct`) trong `< 35ms` tại [`docs/project-eagle/crash-reports/bug-snapshots/`](crash-reports/bug-snapshots/).
- **Báo cáo xuất ra**: [`docs/project-eagle/crash-reports/forensic-snapshot-latest.md`](crash-reports/forensic-snapshot-latest.md).

### Mô-đun 2: Live RAM Scene & Streaming Auditor (`--audit-scene`)
- Kiểm toán toàn bộ các model tĩnh (`.IPL`) và thực thể động (`PedPool`, `VehiclePool`) trong bán kính `55m` quanh nhân vật (hoặc tự dịch chuyển tới tọa độ `(X, Y, Z)` cần kiểm tra rồi trả nhân vật về chỗ cũ):
  - **`UNLOADED_RAM_TXD`**: Model `.dff` đang hiển thị (`m_pRwObject != 0`), nhưng slot `.txd` tương ứng trong `CStreaming::ms_aInfoForModel` có `LoadState != 1` (gây lỗi trắng xóa texture trong game).
  - **`MISSING_RAM_COL`**: Vật thể cận cảnh (`<= 35m`, không phải cây/decal/LOD) nhưng trong RAM `m_pColModel == NULL` hoặc `m_pColData == NULL` (`0` triangles / `0` boxes).
  - **`INVISIBLE_PED_NO_RWOBJECT` / `INVISIBLE_VEHICLE_NO_RWOBJECT`**: NPC hoặc xe đang tồn tại trong Pool gần người chơi nhưng `m_pRwObject == 0` (tàng hình).
- **Báo cáo xuất ra**: [`docs/project-eagle/crash-reports/live-scene-audit-latest.md`](crash-reports/live-scene-audit-latest.md).

### Mô-đun 3: In-Game Bot Runner — Route Crawler (`--crawl`) & Aether Rig Checklist (`--test-aether`)
1. **Physics Route Crawler (`--crawl`)**:
   - Điều khiển Aether tự chạy dọc theo chuỗi waypoint qua bộ giải vật lý thật của GTA SA (xoay ma trận hướng nhìn + giữ nguyên vận tốc rơi tự nhiên `vz` của engine + kích xung `CPad` `0x00B73458` mà không chiếm chuột/bàn phím của máy).
   - Tự phát hiện:
     - **`FALL_THROUGH_COL`**: Rơi xuyên sàn/cầu (`vz < -0.25` hoặc tụt `Z > 3.5m` dưới mặt đường) $\rightarrow$ tự chụp ảnh hiện trường + dump RAM!
     - **`STUCK_WALL_OR_SEAM`**: Kẹt gờ `.COL` hoặc tường vô hình (di chuyển `< 0.22m` sau `0.85s` chạy liên tục) $\rightarrow$ tự chụp ảnh hiện trường + xác định vật thể chắn trước mặt!
   - **Báo cáo xuất ra**: [`docs/project-eagle/crash-reports/route-crawler-latest.md`](crash-reports/route-crawler-latest.md).
2. **Aether Main Character 6-Step Rig & Action Test (`--test-aether`)**:
   - Kiểm tra tự động 6 bước đối với nhân vật chính Aether trong game:
     `01_CLUMP_AND_MODEL_RAM`, `02_WALK_IMPULSE`, `03_SPRINT_IMPULSE`, `04_JUMP_AND_LAND_COL`, `05_WEAPON_AND_STATE`, `06_CAMERA_AND_SCREENSHOT`.
   - **Báo cáo xuất ra**: [`docs/project-eagle/crash-reports/aether-rig-test-latest.md`](crash-reports/aether-rig-test-latest.md).

### Mô-đun 4: Visual Contact Sheet (`--inspect-landmarks`) & NPC Archive/RAM Inspector (`--inspect-npcs`)
1. **Visual & RAM Contact Sheet (`--inspect-landmarks WIBU01_TOUR | BRIDGES_6`)**:
   - Tự động đi qua các góc nhìn chuẩn của địa danh/cầu đường, chờ nạp stream, kiểm toán RAM, chụp ảnh `.png` từng điểm, trả người chơi về vị trí xuất phát và xuất bảng ảnh đối chiếu trực quan tại [`docs/project-eagle/crash-reports/visual-inspection-latest.html`](crash-reports/visual-inspection-latest.html) & [`.md`](crash-reports/visual-inspection-latest.md).
2. **NPC / Ped Slot Inspector (`--inspect-npcs`)**:
   - Kiểm tra danh sách Ped ID (mặc định gồm 6 slot trùng archive `66, 155, 167, 179, 180, 205` + cảnh sát `280, 285, 287` + mọi NPC đang spawn quanh người chơi): đối chiếu file `.IDE`/`.IMG` trên đĩa với trạng thái `CModelInfo`, `CStreamingInfo` và các bản thể đang sống trong `PedPool` RAM.
   - **Báo cáo xuất ra**: [`docs/project-eagle/crash-reports/npc-inspection-latest.md`](crash-reports/npc-inspection-latest.md).

---

## 3. Bảng Lệnh CLI Cho Agent & Người Dùng

```powershell
# 1. Chụp hiện trường + Tia X-Quang Camera + Ảnh PNG cửa sổ game ngay tại vị trí hiện tại
python "C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\eagle_doctor.py" --snapshot

# 2. Kiểm toán trạng thái nạp .DFF/.TXD/.COL thực tế trong RAM quanh nhân vật (hoặc tại tọa độ X,Y,Z)
python "C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\eagle_doctor.py" --audit-scene
python "C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\eagle_doctor.py" --audit-scene "-1390.4,-4551.2,23.4"

# 3. Chạy Bot tự đi bộ dò lỗi khe nối .COL / tường vô hình trên cầu WIBU-01 hoặc tọa độ tùy chọn
python "C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\eagle_doctor.py" --crawl WIBU01_BRIDGE_SEAM
python "C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\eagle_doctor.py" --crawl "-1390.4,-4530,23.5;-1390.4,-4570,23.4"

# 4. Chạy bài test 6 bước kiểm tra Rig & chuyển động của nhân vật chính Aether
python "C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\eagle_doctor.py" --test-aether

# 5. Chụp bộ ảnh Contact Sheet HTML nghiệm thu nhanh địa danh / cầu đường trong game
python "C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\eagle_doctor.py" --inspect-landmarks WIBU01_TOUR

# 6. Kiểm toán các slot NPC trên đĩa (.IDE/.IMG) và trong RAM (PedPool + CStreaming)
python "C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\eagle_doctor.py" --inspect-npcs
```

---

## 4. Phục Hồi (Rollback Bit-for-Bit)

Nếu cần gỡ bỏ bộ công cụ In-Game Test Suite và khôi phục `EagleCompanion.py`, `eagle_debug_system.py`, `eagle_doctor.py`, `eagle_phone_ui.py` về đúng hash trước khi cài:
```powershell
python "C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\in-game-test-suite-2026-10-25\rollback_ingame_test_suite.py"
```
Hoặc chạy [`Rollback_InGame_Test_Suite.bat`](../../staging/project-eagle/in-game-test-suite-2026-10-25/Rollback_InGame_Test_Suite.bat).
