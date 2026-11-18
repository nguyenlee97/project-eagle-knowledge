# Hạng Mục 4 — Hồ Sơ Bàn Giao & Prompt Khởi Tạo Hội Thoại Mới: Xây Dựng **Đảo Đô Thị Nhật Bản Độc Lập Tại `WIBU-01` (`Project Japan Landmarks + Kerorin Capital + Akihabara`)**

- **Ngày lập**: `2026-10-23`
- **Tác giả**: `Antigravity`
- **Mục tiêu của Hội thoại mới**: Lắp ráp và biên dịch **Hạng mục Map Mở Rộng Đầu Tiên** từ các bản mod **GTA San Andreas gốc (`Native .DFF / .TXD / .COL / .IDE / .IPL`)** đã bóc tách sẵn trên ổ `D:\`, đặt thành một **Quần Đảo Đô Thị Nhật Bản Độc Lập tại vùng biển trống `WIBU-01` (`MKLAS` — đầu Nam Cầu Cao Tốc #5)**, hoàn toàn không đụng chạm (`0%` xung đột) với 27 bang `S&S` hay nhánh xây dựng Map Genshin (`Mondstadt Vertical Slice`).

---

## 1. Tại Sao Đây Là Hạng Mục Mở Màn Hoàn Hảo Nhất?

1. **100% Tài nguyên GTA San Andreas gốc (`Native RenderWare Assets`)**:
   - Không cần chuyển đổi từ `.OBJ` Unity hay tự dựng lưới va chạm từ con số 0 như nhánh Genshin: toàn bộ mặt đường nhựa, vỉa hè, cao ốc, cửa hàng điện tử Akihabara, Tháp Tokyo, cây Hoa Anh Đào đều đã có sẵn `.DFF`, `.TXD`, `.COL` và `.IPL` chuẩn GTA SA.
2. **Vùng biển cô lập `WIBU-01` (`MKLAS`, Tây Nam Los Santos) — `0%` Xung đột & Đã có sẵn Cầu Cao Tốc #5**:
   - Khu vực `X = [-2500 .. +100], Y = [-6100 .. -4500]` đang có **`0` vật thể 3D** (`0%` đụng chạm với Los Santos hay `GROUP_A_MODS.IMG`).
   - Đã được nối sẵn với đất liền (Nam Whetstone / Angel Pine `(-1387.0, -2932.0, 45.0)`) bằng **Cầu Cao Tốc 3D #5 (`BR-5`, dài `1,619m`, `42` nhịp 3D + `23` node GPS)** hạ cánh tại **`(-1390.4, -4551.2, 23.4)`**.
   - Đặc biệt: Trong `data\pecore_gps_graph.pegg` tại `WIBU-01` đã có sẵn **`2,106` node đường bộ (`Comp #11` — `2,095` đoạn đường)** nối trực tiếp vào đầu Nam Cầu #5!

---

## 2. Danh Mục Tài Nguyên Đầu Vào Đã Có Sẵn Trên Ổ `D:\` (`Donor Library`)

Toàn bộ tài nguyên đã được tải và giải nén sẵn tại `D:\GTA Archive\Mod Donor Library\`:

| STT | Thành Phần Đưa Vào Đảo Nhật Bản `WIBU-01` | Đường Dẫn Vật Lý Trên Ổ `D:\` | Cấu Trúc File Gốc | Dải Model ID Sạch Đã Cấp Phát |
|---:|---|---|---|---|
| **1** | **Đảo Đô Thị `Kerorin Capital 1.0` (`ZZPuma #153898`)** — Phần nền đảo, đường phố, cầu nội khu & khu phố Nhật Bản | `D:\GTA Archive\Mod Donor Library\ky2-urban-buildings\153898_kerorin_capital\` | `49` `.dff` (`kero_part_0..48`), `kero.txd` (`100.3 MB`), `kero.col` (`6.07 MB`), `kero.ide` (`49` models), `kero.IPL` (`80` instances, `bad_quats = 0`) | **`11800 .. 11848`** (`49` IDs — thay cho dải gốc `14901..14982` bị trùng `S&S`) |
| **2** | **Khu Phố Điện Tử `Akihabara Electronic Town` (`#155560`)** — Phố Sega GiGO, LaOX, Ishimaru, nhà ga, đèn tín hiệu | `D:\GTA Archive\Mod Donor Library\ky2-urban-buildings\155560_akihabara_electronic_town\` | `75` `.dff`, `akihabara.col` (`1.63 MB`), `860` `.png` textures, `akihabara.ide` (`75` models), `akihabara.IPL` (`75` instances) | **`11850 .. 11924`** (`75` IDs — thay cho dải gốc `2..3141` đụng `peds.ide`!) |
| **3** | **Tháp `TorreTokyo` (`Tokyo Tower` từ `Project Japan 3.1` Module `012`)** | `D:\GTA Archive\Mod Donor Library\project-japan\PJ_3.1_FULL_EXTRACTED\Modloader\Project Japan 3.1\Map\012 TorreTokyo By Misaki Modding & MrAndres5555\` | `Abase1..3.dff`, `lodabase1.dff`, `Abase.txd`, `Abase3.txd`, `abase.col`, `001.IDE`, `001.IPL` | **`3194 .. 3197`** (`4` IDs — thay cho `18631..18634` đụng `SAMP.ide`) |
| **4** | **Lâu Đài Cổ Nhật Bản (`#101385`) & Tòa Nhà `Kawaiiboutique` (`#175652`)** | `D:\GTA Archive\Mod Donor Library\ky2-urban-buildings\101385_japanese_castle_cj_house\` & `175652_japanese_building_v2\` | `carlshou1_lae2.dff` + `sunrise09_lawn.dff/.txd` tách độc lập | **`3198 .. 3199`** (`2` IDs) |
| **5** | **14 Cây Hoa Anh Đào Tuyển Chọn (`Sakura Trees` từ `Project Japan 3.1` Module `011`)** | `D:\GTA Archive\Mod Donor Library\project-japan\PJ_3.1_FULL_EXTRACTED\Modloader\Project Japan 3.1\Map\011 Cherry tree by Miyata Lee\` | Chọn `14` model cây Sakura đẹp nhất + `bsor_*.txd` | **`3200 .. 3213`** (`14` IDs độc lập — không ghi đè cây cọ Vice City!) |

---

## 3. Lộ Trình Kỹ Thuật 5 Bước Cho Hội Thoại Mới

1. **Bước 1 — Khớp nối Tọa độ (`Coordinate Translation & Bridge 5 Alignment`)**:
   - Đo đạc chính xác cao độ mặt đường và điểm đầu vào của `Kerorin Capital` (`X = [-65.6..398.8], Y = [201.5..615.3]`) cùng `Akihabara Electronic Town` (`439m × 251m`).
   - Tính toán vector tịnh tiến $(\Delta X, \Delta Y, \Delta Z)$ để đại lộ dẫn vào `Kerorin Capital` nối liền khít 100% (`0mm` bậc thang) với nhịp cuối của **Cầu Cao Tốc #5 tại `(-1390.4, -4551.2, 23.4)`**, tiếp nối sang khu phố `Akihabara Electronic Town` và quảng trường **Tháp Tokyo (`TorreTokyo`)** ở trung tâm đảo.
2. **Bước 2 — Chuẩn Hóa `.TXD` & Kiểm Tra Giới Hạn `.COL` (`92,768 bytes / model`)**:
   - Đóng gói `860` file `.png` của `Akihabara Electronic Town` thành `akihabara_town.txd` chuẩn PC (nén `DXT1`/`DXT5` có mipmaps, tối ưu dung lượng `kero.txd` từ `100.3 MB` xuống `< 25 MB` bằng DXT1/DXT5).
   - Kiểm tra từng khối `.col` trong `kero.col` (`6.07 MB` / `49` models) và `akihabara.col` (`1.63 MB` / `75` models) đảm bảo **không có bất kỳ single collision model nào vượt quá giới hạn `Collision size = 92,768 bytes` (`~90.6 KB`)** của `fastman92limitAdjuster_GTASA.ini` (dòng 577). Nếu khối `.col` nào `> 90 KB`, tự động tối ưu hoặc tách `FaceGroups`.
3. **Bước 3 — Cấp Phát ID Sạch (`11800..11924` & `3194..3213`), Chuẩn Hóa Quaternion & Tạo LOD**:
   - Sinh `wibu01_japan_island.ide` và `wibu01_japan_island.ipl` với `100%` Quaternion chuẩn hóa ($\|\mathbf{q}\| = 1.0$, tuân thủ ngưỡng độ dốc `0x005381D5` của `gta_pe.exe`).
   - Đặt Tháp Tokyo (`3194..3197`), Lâu đài Nhật (`3198`), `Kawaiiboutique` (`3199`) và trồng các hàng cây Hoa Anh Đào (`3200..3213`) dọc đại lộ chính của đảo bằng `Raycasting` xuống mặt `.col`.
4. **Bước 4 — Đóng Gói `wibu01_japan_island.img` Trong Staging & Kiểm Toán Bằng Blender 3D**:
   - Đóng gói toàn bộ vào `D:\GTA Archive\Staging\wibu01-japan-island-2026-10-23\wibu01_japan_island.img`.
   - Chạy bài kiểm toán nhị phân 5 bước (`IDE/IPL/COL/TXD/IMG`) và kết xuất **ảnh chụp phối cảnh 3D thực tế bằng Blender 4.5 + DragonFF** tại điểm nối Cầu Cao Tốc #5 vào Đảo `Kerorin + Akihabara + Tháp Tokyo` để nghiệm thu trực quan.
5. **Bước 5 — Sẵn Sàng Tích Hợp 1-Click Vào `gta sa gameplay-lab` (Kèm Script Rollback)**:
   - Chuẩn bị script cài đặt an toàn (có giữ khóa `game-write.lock` và `Rollback_Wibu01_Japan_Island.bat`) để người dùng lái xe từ Los Santos qua Cầu #5 vào thẳng Đảo Nhật Bản.

---

## 4. 📋 Prompt Khởi Tạo Để Dán Vào Hội Thoại Mới

Khi bấm **`+` (New Conversation)** ở thanh bên trái, bạn chỉ cần copy và dán đoạn prompt dưới đây:

```markdown
Hãy đọc `AGENTS.md`, `docs/project-eagle/shared-agent-workflow.md` và hồ sơ bàn giao `docs/project-eagle/item4-wibu01-japan-island-handover-and-prompt-2026-10-23.md` để thực thi ngay Hạng mục mở màn: **Xây dựng Quần Đảo Đô Thị Nhật Bản Độc Lập tại `WIBU-01` (`MKLAS` — đầu Nam Cầu Cao Tốc #5)** từ các bản mod GTA SA gốc đã giải nén sẵn trên `D:\GTA Archive\Mod Donor Library\` (`Kerorin Capital 1.0 #153898`, `Akihabara Electronic Town #155560`, `Tháp TorreTokyo 012`, `Lâu đài Nhật #101385`, `Kawaiiboutique #175652` và `Cây Hoa Anh Đào 011`).

Yêu cầu thực hiện trọn vẹn 5 bước trong staging `D:\GTA Archive\Staging\wibu01-japan-island-2026-10-23\` (chưa ghi vào `gta sa gameplay-lab` cho tới khi kiểm toán xong):
1. Khớp nối cao độ & tọa độ mặt đường của `Kerorin Capital` + `Akihabara Electronic Town` liền khít với điểm tiếp đất phía Nam của Cầu Cao Tốc #5 tại `(-1390.4, -4551.2, 23.4)`.
2. Đóng gói/tối ưu `.TXD` chuẩn DXT1/DXT5 (đặc biệt gom 860 file `.png` của Akihabara thành `.txd` PC và nén gọn `kero.txd`), kiểm tra mọi khối `.COL` đơn lẻ đều `< 92,768 bytes` (`fastman92limitAdjuster`).
3. Cấp phát đúng dải ID sạch (`11800..11848`, `11850..11924`, `3194..3213`), chuẩn hóa 100% Quaternion trong `.IPL`, đặt Tháp Tokyo và trồng cây Hoa Anh Đào dọc đại lộ bằng Raycasting.
4. Đóng gói `wibu01_japan_island.img` + `.ide` + `.ipl` + `.col`, chạy kiểm toán nhị phân tự động và render bộ ảnh phối cảnh 3D thực tế bằng Blender 4.5 + DragonFF để nghiệm thu.
```
