# Báo Cáo Kiểm Toán Hiện Trạng, Giới Hạn Kỹ Thuật & Dư Địa Mở Rộng (`gta sa gameplay-lab`)

- **Ngày khảo sát:** `2026-11-05` (`Asia/Saigon`)
- **Agent thực hiện:** Antigravity (`bb001448-6058-4366-8516-2343f455720e`)
- **Đích khảo sát:** `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab` (chỉ đọc 100%, không can thiệp runtime, không mở `gta_pe.exe`)
- **Phiếu công việc:** [`docs/project-eagle/work-items/2026-11-05-antigravity-game-state-and-technical-limits-audit.md`](work-items/2026-11-05-antigravity-game-state-and-technical-limits-audit.md)

---

## 1. Tóm Tắt Điều Hành (Executive Summary)

Tính đến sáng **05/11/2026**, bản hợp nhất `gta sa gameplay-lab` đang ở trạng thái **khỏe mạnh và ổn định (`eagle_doctor 11/11 PASS`, `0` lỗi Lua, cả 2 khóa `game-write` và `ingame-runtime` đều mở sạch)** sau hàng loạt đợt tích hợp lớn (6 cầu cao tốc liên lục địa, Đảo Nhật Bản `WIBU-01`, Quần thể `Mondstadt M0–M2 + 7 nội thất`, Quận Bắc Chicago `INLAND-03A`, `1,638` skin NPC + `25` Custom Ped IDs, `EaglePhone OS v6.3` 15 ứng dụng cảm ứng chuột 144Hz, `WaifuLink v4.0` 6/6 bạn gái `810` CG + thoại JP, `Mondstadt Persona Chat` 14 nhân vật + AI `gpt-6-luna`, `Presentation` 178 ảnh và 13 đài Radio).

Về câu hỏi **"Còn nhồi nhét được bao nhiêu feature nữa và bị giới hạn bởi cái gì?"**, kiến trúc hiện tại của Project Eagle là **Kiến trúc Lai (Hybrid 32-bit RenderWare Engine + 64-bit Out-of-Process Python Sidecar)** nên câu trả lời tách làm **2 tầng rõ rệt**:

1. **Tầng Sidecar 64-bit + Thin HUD (`EagleCompanion.py`, SQLite, AI LLM, Smartphone Apps, Visual Novel, Story Quest rẽ nhánh, Mini-games, Báo chí/Tài chính, Voice/CG truyền qua Ping-Pong TXD):**
   - **Gần như KHÔNG BỊ GIỚI HẠN BỞI ENGINE GTA SA** — có thể nhồi thêm **hàng chục ứng dụng mới, hàng trăm kịch bản Story Quest rẽ nhánh và hàng vạn ảnh CG / câu thoại** mà không tốn thêm dù chỉ `1 MB` bộ nhớ 32-bit của `gta_pe.exe` (do CG/Sprite dùng cơ chế ghi đè 2 khe Ping-Pong cố định `WLCG0/1.TXD` & `MCSP0/1.TXD`, còn logic chạy ở Python 64-bit ngoài luồng).
2. **Tầng Tài nguyên 3D Nội tại của Engine GTA SA (`gta_pe.exe` 32-bit: Map/Lục địa 3D, Tòa nhà, Skin NPC, Xe cộ, CLEO threads, Shared Memory):**
   - **Còn dư địa lớn nhưng bị chặn bởi 5 rào cản kỹ thuật cụ thể**, đứng đầu ngay lúc này không phải là engine mà là **ổ `C:\` chỉ còn trống `15.40 GiB` (`3.2%`)**, kế đến là **trần cứng bộ nhớ ảo 32-bit `4.0 GiB VAS` (`Memory available = 2,800 MiB`)**, **`BuildingPool` đã dùng `74.9%` (`74,870 / 100,000` — tăng được trong INI)**, **dải ID `< 65,535` cho vật thể có va chạm `.COL3` (còn trống `17,408` ID — đủ xây ~`50–100` quận/vùng đất mới)**, và **khe nhớ dùng chung `0x00CAFE00..0x00CAFFFF` chỉ còn `392 bytes` cuối trước vùng Read-Only `.rsrc` (`0x00CB0000`)**.

---

## 2. Phân Tách Bằng Chứng Kiểm Chứng (Theo Quy Tắc Dự Án)

Để đảm bảo tính trung thực kỹ thuật tuyệt đối, báo cáo tách bạch 3 mức bằng chứng:
- **[ĐO TRỰC TIẾP TRÊN ĐĨA / BINARY 05/11]:** Đọc từ PE header `gta_pe.exe`, `fastman92limitAdjuster_GTASA.ini`, `fastman92limitAdjuster.log`, `PECore.ini`, `PECore.log`, `cleo.log`, 77 kho `.img`, 191 tệp `.ide`, 276 tệp `.ipl`, `SanViveLuaHudSA.asi`, mã nguồn `EagleStreamingFix.c` và dung lượng ổ `C:`/`D:`.
- **[ĐÃ KIỂM CHỨNG RUNTIME TRONG GAME TRƯỚC ĐÓ]:** Đối chiếu từ telemetry RAM thực tế đã ghi nhận trong `docs/project-eagle/crash-reports/` (`latest-doctor-report.md` lúc `08:21 05/11/2026`, `forensic-snapshot-latest.json`, `live-scene-audit-latest.md`, `hang-2026-11-01_19-21-53.json`) và các báo cáo QA DirectX 9 `1920×1080`.
- **[LÝ THUYẾT CẤU HÌNH LOADER / CHƯA MỞ GAME TRONG PHIÊN NÀY]:** Các ngưỡng tối đa do Fastman92 Limit Adjuster 7.7 / PECore tài liệu hóa trong `.ini` nhưng chưa ép tải tới ngưỡng cực hạn trong game; phiên khảo sát này chỉ đọc nên không tự khởi chạy `gta_pe.exe`.

---

## 3. Hiện Trạng Phần Cứng, Đĩa Cứng & Quy Mô Bản Lab (`05/11/2026`)

### 3.1. Cấu hình máy chủ & Dung lượng lưu trữ `[ĐO TRỰC TIẾP]`
| Thành phần | Thông số thực đo | Đánh giá tác động |
|---|---|---|
| **CPU** | `AMD Ryzen 7 4800H` (`8 nhân / 16 luồng`) | Đa nhân rất khỏe cho Python Sidecar / AI / Worker GPS của `PECore`; tuy nhiên luồng render D3D9 của `gta_pe.exe` vẫn phụ thuộc hiệu năng đơn nhân (single-thread). |
| **RAM vật lý** | `16 GB` (`15.37 GiB` khả dụng) | Đủ cho `gta_pe.exe` (`~3.0–3.6 GiB`) + Python Sidecar + trình duyệt/OS, nhưng sẽ cần Pagefile trên ổ `C:` nếu mở thêm công cụ nặng cùng lúc. |
| **GPU / VRAM** | `NVIDIA GeForce GTX 1650` (`4,096 MiB` VRAM) + `AMD Radeon iGPU` (`512 MiB`) | `4 GB VRAM` dư sức cho màn hình `1920×1080` nếu texture nén chuẩn `DXT1/DXT5`, nhưng sẽ nghẽn nếu lạm dụng texture `RGBA32` không nén `2K/4K`. |
| **Ổ cứng `C:\` (Runtime)** | Tổng `475.69 GiB` \| Đã dùng `460.29 GiB` \| **Còn trống `15.40 GiB` (`3.2%`)** | 🔴 **BÁO ĐỘNG ĐỎ (Nút thắt số 1 hiện tại)**: Quá sát đáy an toàn cho một game có archive `11.79 GiB` và Windows Pagefile! |
| **Ổ cứng `D:\` (Archive)** | Tổng `1,862.98 GiB` \| Đã dùng `888.22 GiB` \| **Còn trống `974.77 GiB` (`52.3%`)** | 🟢 **Cực kỳ dồi dào** (còn gần `1 TB` trống). |

### 3.2. Phân rã dung lượng vật lý của Workspace trên ổ `C:\` `[ĐO TRỰC TIẾP]`
- `Project Eagle/` (`gta sa gameplay-lab`): **`36.04 GiB`** (`3,509` files vật lý, 10 thư mục gốc là NTFS junction nội bộ):
  - `S&S/` (bản đồ đa bang & kho ped gốc/mod): **`17.63 GiB`** (riêng `COMPONENTPEDS.img` = **`11.79 GiB` / `4,224` entries**).
  - `audio/` (nhạc radio, SFX, streams): **`15.43 GiB`** (`audio/PE` = `12.19 GiB`, `SFX` = `2.13 GiB`, `streams` = `1.11 GiB`).
  - `custom/` (Mondstadt, WIBU-01, INLAND-03A, EagleRide, Waifu/Mondstadt peds, Group A/B1): **`1.44 GiB`**.
  - `cleo/` (`75` file `.cs`, `4` file `.s`, `94` file `.qa`, Lua state): **`396.83 MiB`**.
  - `anim/` (`269.39 MiB`), `models/` (`237.51 MiB`), `plugins/` (`226.45 MiB`), `modloader/` (`105.47 MiB`), `data/` (`59.03 MiB`).
- `ProjectEagleModPack/` (thư mục gói mod cũ còn nằm vật lý trên `C:`): **`10.29 GiB`** (`5,670` files).
- `staging/` (các thư mục staging vật lý chưa chuyển sang `D:`, lớn nhất là `dryxio-tools` `1.20 GiB`, `loading-batches` `764 MiB`, `menu-batches` `713 MiB`, `loading-screens` `564 MiB`): **`5.69 GiB`** (`30,608` files).
- `docs/` (`1.84 GiB`), `data/` (`0.44 GiB`, riêng `dating-sim/media` 810+ CGs = `423.94 MiB`), `tools/` (`0.13 GiB`).

> **Khuyến nghị giải phóng ngay ~`15 GiB` trên ổ `C:`:** Di chuyển `ProjectEagleModPack/` (`10.29 GiB`) và các thư mục `staging/project-eagle` đã nghiệm thu xong (`~4.5 GiB`) sang `D:\GTA Archive\` kèm NTFS junction giống đợt 22/10 sẽ nâng dung lượng trống ổ `C:` từ `15.4 GiB` lên **`~30+ GiB`** ngay lập tức mà không đụng bất kỳ file runtime nào.

---

## 4. Bảng Kiểm Toán Chi Tiết: Trần Kỹ Thuật vs. Mức Đang Dùng & Dư Địa Còn Lại

### 4.1. Bộ nhớ Tiến trình 32-bit, Streaming & Kho `.IMG`
| Hạng mục giới hạn | Loại trần | Trần cấu hình / Trần cứng | Mức đang dùng thực tế | % Đã dùng | Dư địa & Ghi chú kỹ thuật |
|---|---|---|---|---:|---|
| **Không gian địa chỉ ảo `gta_pe.exe` (`x86 LAA`)** | **CỨNG TUYỆT ĐỐI** | **`4,096 MiB` (`4.0 GiB`)** *(thực dụng `~3.6 GiB` do phân mảnh DLL)* | `~1.3 – 2.2 GiB` khi chơi thông thường *(tăng theo cảnh)* | `~35–60%` | **Trần sinh tử số 1 của engine 32-bit.** Gồm EXE + Pools + D3D9 Managed copies + Streaming. Không thể nâng vượt `4 GiB` nếu không port engine sang 64-bit. |
| **FLA `Memory available` (Streaming RAM)** | **Mềm (Kịch khung LAA)** | **`2,800 MiB`** (`0xAF000000`, đã vá unsigned `JB/JAE` bởi `EagleStreamingFix.asi`) | Thực đo `540 – 670 MiB` tại 1 quận (`19.3% – 23.9%`) `[RUNTIME ĐÃ ĐO]` | `~24%` | **Không nên tăng quá `2,800 MiB`** vì phần dư `~1.2 GiB` của 4 GiB VAS phải chừa cho EXE, Pools, PECore GPS (`28 MB`), BASS và bản sao `D3DPOOL_MANAGED` của DirectX 9. |
| **Số lượng kho `.IMG` (`gta.dat` + `default.dat`)** | **Mềm (FLA)** | **`512` kho `.img`** | **`77` kho `.img`** trên đĩa (`70` khai báo qua `.dat`) | **`15.0%`** | **Còn trống `~435` kho `.img`!** Đủ gắn thêm hàng trăm Sector bản đồ hoặc gói nhân vật/xe cộ mới. |
| **Dung lượng tối đa 1 file `.IMG` đơn lẻ** | **Cứng / Cấu hình** | FLA Enhanced IMG đang bật (`COMPONENTPEDS.img` đạt **`11.79 GiB` / `6,181,128` sectors**); cờ `#Increase the IMG archive size limit = 1` (`32 GB`) hiện đang comment | Lớn nhất: `COMPONENTPEDS.img` (`11.79 GiB`), thứ nhì: `game_cc.img` (`759 MiB`) | — | **Khuyến nghị:** Không nhồi thêm vào `COMPONENTPEDS.img`; mọi nhân vật/map mới hãy tách ra các `.img` riêng `< 2 GiB` theo Sector/Feature (vừa build nhanh vừa tránh rủi ro tràn offset công cụ cũ). |
| **Số xe nạp đồng thời (`DesiredLoadedVeh`)** | **Mềm (FLA + PECore)** | `35` xe (ràng buộc `< Cargrp 63` và `< VehicleStructs 55,000`) | `35` chủng loại xe lưu chuyển quanh người chơi | — | Giữ ở mức `35` để tránh lặp lại lỗi đói bộ nhớ streaming (`BUG-007`). |

### 4.2. Bảng Phân Bổ ID (`IDE` / `.COL3` / `FLA ID Limits`)
| Nhóm ID / Định nghĩa | Trần hiện tại (`FLA .ini`) | Đang dùng thực tế `[ĐO TRỰC TIẾP]` | % Đã dùng | Trần cứng định dạng & Dư địa mở rộng |
|---|---|---:|---:|---|
| **Tổng File IDs (`CStreamingInfo`)** | `350,410` (đã vá `int32_t`) | `~95,693` entries trong 77 `.img` | `27.3%` | Rất rộng; FLA có thể nâng tiếp nếu cần (chỉ tốn ~`24 B`/ID trong RAM). |
| **Tổng Model IDs (`FILE_TYPE_DFF`)** | `200,000` (`0 .. 199,999`) | **`63,840`** ID duy nhất (`max ID = 180,577`, `0` xung đột chéo IDE) | **`31.9%`** | **Còn trống `136,160` ID tổng thể.** |
| **Model ID có va chạm `.COL3` (`uint16`)** | **CỨNG `65,534`** *(do header `.COL3` dùng `uint16` cho `model_id`)* | `48,126` ID đã dùng trong `[1..65,534]` | **`73.4%`** | **Còn trống chính xác `17,408` ID dưới `65,535`!** Các dải liền mạch lớn nhất: `33994..35822` (`1,829`), `54219..55999` (`1,781`), `46396..48011` (`1,616`), `18702..19999` (`1,298`), `64412..65534` (`1,123`), `15065..15999` (`935`), `49448..49999` (`552`). Với ~`150–350` model/quận, **đủ xây thêm `50 – 100` quận/khu vực mới!** *(Các mesh LOD không có `.COL3` có thể đẩy lên ID `> 65,535` để tiết kiệm dải thấp).* |
| **`IDE: objs` (Static Objects)** | `200,000` (`Type 1`) + `7,000` (`Type 2`) | **`59,514`** | `29.8%` | Còn dư `> 140,000` định nghĩa object. |
| **`IDE: tobj` (Timed Day/Night Objects)** | `5,000` | **`607`** | `12.1%` | Còn dư `4,393` object phát sáng theo giờ đêm/ngày. |
| **`IDE: peds` (Ped Models)** | `10,000` *(và `< Killable IDs 95,000`)* | **`1,712`** (`max ID = 49,447`) | **`17.1%`** | **Còn nhét thêm được `8,288` nhân vật 3D mới** (ví dụ toàn bộ dàn nhân vật Genshin/HSR/ZZZ/WuWa/Anime cũng chưa tới 500 người!). Dải `49448..49999` đang trống liền mạch `552` slot cho Custom Peds. |
| **`IDE: cars` (Vehicle Models)** | `2,000` *(và `handling.cfg` = `1,024` car + `128` bike + `128` air + `128` boat)* | **`1,476`** (`max ID = 30,679`) | **`73.8%`** | **Còn trống `524` mẫu xe 3D mới** trước khi cần nâng `Vehicle Models` và `handling.cfg lines` trong `fastman92limitAdjuster_GTASA.ini`. |
| **`IDE: weap` (Weapon Models)** | `512` | **`438`** (`max ID = 32,677`) | **`85.5%`** | Còn trống **`74` mẫu vũ khí** (có thể nâng trong FLA nếu cần thêm vũ khí). |
| **Texture Archives (`FILE_TYPE_TXD`)** | `65,000` | `19,415` tệp `.txd` trong `.img` | `29.9%` | Còn trống `~45,500` slot `.txd`. |
| **Collision Archives (`FILE_TYPE_COL`)** | `65,000` | `735` tệp `.col` | `1.1%` | Còn trống `> 64,000` slot `.col`. |
| **Binary IPL (`FILE_TYPE_IPL`)** | `2,560` | `244` tệp `_stream*.ipl` | `9.5%` | Còn trống `2,316` slot binary `.ipl`. |
| **`object.dat` (Dynamic/Breakable Info)** | `2,048` | `< 900` | `< 45%` | Chỉ dùng cho đồ vật đập vỡ/vật lý động; nhà cửa/địa hình tĩnh không tốn bảng này. |

### 4.3. Engine Pools & Không Gian Thế Giới (`48 × 48 km`)
| Pool / Giới hạn bản đồ | Trần hiện tại (`FLA .ini`) | Thực đo trên đĩa / Live RAM `[RUNTIME ĐÃ ĐO]` | % Đã dùng | Đánh giá & Khả năng nới trần |
|---|---|---:|---:|---|
| **`BuildingPool` (`IPL: Buildings`)** | **`100,000`** | **`74,870`** live RAM (`85,861` tổng dòng `inst` text IPL cho cả Building + Dummy) | **`74.9%`** | 🟠 **Cần theo dõi:** Hiện còn trống **`~25,130` công trình tĩnh** (đủ xây **~`40–50` quận cỡ `INLAND-03A`** vì `INLAND-03A` chỉ tốn `512` instances). Nếu xây đại lục lớn vượt `90,000`, chỉ cần tăng `Buildings = 160000` trong INI (tốn thêm ~`3.4 MiB` RAM). |
| **`DummyPool` (`IPL: Dummies`)** | `50,000` | **`11,180`** live RAM | `22.4%` | Rất thoáng (còn trống `~38,800` dummy có hiệu ứng đèn 2DFX). |
| **`ColModelPool`** | `128,000` | **`41,940`** live RAM | `32.8%` | Còn trống `~86,000` ColModels. |
| **`PedPool` (NPC sống quanh người chơi)** | `3,800` | Thường `15 – 120` NPC đồng thời | `< 4%` | Dư dả tuyệt đối (giới hạn thực tế là CPU AI chứ không phải pool). |
| **`VehiclePool` (Xe sống quanh người chơi)** | `1,000` | Thường `10 – 80` xe đồng thời | `< 8%` | Dư dả tuyệt đối (lưu ý Replay gốc GTA SA hỏng khi `> 256`, đã chấp nhận). |
| **`ObjectPool` (Vật thể động)** | `70,000` | `71 – 300` live RAM | `< 0.5%` | Dư dả tuyệt đối. |
| **`EntryExits` (`IPL: enex` cửa ra vào)** | `2,500` | `1,120` trong text IPL | `44.8%` | Còn thêm được **`~1,380` cửa nội thất (`ENEX`)** mới! |
| **`Water Quads` (`data/water.dat`)** | `30,100` quads (`9,999` list) | **`2,030`** dòng `water.dat` | `~20.3%` | Còn thêm được `~7,900` vùng mặt nước (nhớ luôn đặt tọa độ số chẵn để tránh lỗi chia cho 0 tại `0x006E9210`). |
| **Kích thước Bản đồ Thế giới (`World Bounds`)** | **`48,000 × 48,000 m`** (`[-24,000 .. +24,000]`) | Rộng lớn; còn nhiều vùng biển & ít nhất **3–4 quỹ đất trống nội địa `Zero-3D`** + vùng biển Tây/Nam cho Teyvat | `~35–40%` diện tích có 3D | `9,216` ô `radar.img` (`96×96`) và `4,096` ô `paths.img` (`64×64`) đã phủ sẵn toàn khung `48×48 km`; xây ở đâu chỉ cần thay đúng tile radar và path của vùng đó. |

### 4.4. Scripting, LuaJIT HUD, Shared Memory Caves & Sidecar 64-bit
| Thành phần | Giới hạn kỹ thuật | Hiện trạng sử dụng `[ĐO TRỰC TIẾP]` | Đánh giá & Quy tắc an toàn |
|---|---|---|---|
| **CLEO Running Scripts (`SCM LIMITS`)** | **`320` luồng chạy đồng thời** | Đăng ký `92`, tự tắt `18` -> **`~74` luồng đang chạy (`23.1%`)** | **Còn thêm được `~240` script CLEO nữa.** Tuy nhiên, ưu tiên gộp nhiều NPC vào **1 cầu CLEO chung** (như `EagleMondstadtChatBridge.cs` quản lý 30 NPC bằng 1 luồng duy nhất) để giữ CPU nhẹ và dễ bảo trì. |
| **Vùng nhớ dùng chung `_rwdseg` (`0x00CAFE00..0x00CAFFFF`)** | **CỨNG `512 bytes`** từ `0x00CAFE00` đến `0x00CAFFFF` *(ngay sau đó `0x00CB0000` là `.rsrc` **READ-ONLY**!)* | Đã dùng `0x00CAFE00..0x00CAFE77` (`120 bytes` cho Companion/Dialogue/Paimon, Ride, Waifu, Mondstadt `MCHT`, Touchscreen) | 🟡 **Rất quan trọng:** Từ `0x00CAFE78` tới `0x00CAFFFF` còn **`392 bytes`** (và vùng trước `0x00CAF200..0x00CAFDFF` còn `3,072 bytes`). Mọi bridge mới **chỉ được ghi `8 bytes` (`Magic 4B + HeapPtr 4B`)** tại đây, cấp phát payload thực trên Heap (`allocate_memory`), **tuyệt đối không tràn sang `0x00CB0000`**. |
| **Giao thức `MCHT v2` (`EagleMondstadtChatBridge.cs`)** | `npc_capacity = 30` (`768 B` trên Heap) | **`14 / 30` NPC** (`46.7%`) | Còn gắn ngay được **16 nhân vật tương tác 3D mới** không cần sửa `.cs`; khi vượt 30 chỉ cần nâng struct Heap lên `64` hoặc `128` NPC. |
| **In-Game UI (`SanViveLuaHudSA.asi` + `hud.lua`)** | Chạy **`LuaJIT 2.1`** (`200` biến `local`/hàm, `60` upvalues/hàm); giới hạn `CFont` ASCII không chứa `~ \| * @` | `hud.lua` = `206 KB` (`4,414` dòng, `0` lỗi runtime) + cơ chế tách file `loadfile("cleo/EagleStakeHud.lua")` | Nhờ cơ chế cắm plugin file rời của `EaglePhone OS v6.3` và `LuaJIT 2.1`, **có thể viết thêm hàng chục App/UI mới ở file `.lua` riêng** mà không làm phình `hud.lua` hay chạm trần `200 local variables`. |
| **Texture UI (`models/hud.txd` + Ping-Pong TXDs)** | Mỗi TXD nên giữ gọn (`< 15–20 MiB`) | `hud.txd` = `5.35 MiB` (`300` icon), `WLCG0/1.TXD` = `2×2.0 MiB`, `MCSP0/1.TXD` = `2×1.0 MiB` | Cơ chế Ping-Pong 2 slot giúp **hiển thị vô hạn ảnh CG / Sprite nhân vật từ ổ cứng mà tổng RAM trong game cố định chỉ mất `~6 MiB`!** |
| **Python Sidecar (`EagleCompanion.py` + `SQLite` + `opencode2api`)** | Tiến trình **64-bit độc lập** ngoài `gta_pe.exe` | Đang chạy mượt ở `< 1–3 ms`/tick cho 51 mã tài chính, 35,064 bài báo, 6 bạn gái, 14 NPC AI | **Không có trần engine!** Phụ thuộc duy nhất vào ổ đĩa lưu trữ và quota API AI (`gpt-6-luna` / `image-generator` nội bộ `100` hình / `5h`). |

---

## 5. Danh Sách "Luật Cứng Vi Mô" Của Engine (Vi Phạm Là Crash Dù Còn Thừa RAM)

Khi tiếp tục nhồi thêm nội dung mới, chỉ cần tuân thủ tự động bộ quy tắc kiểm định đã đúc kết qua thực chiến sau đây thì game sẽ không bị văng:

1. **Vật liệu Mesh `.DFF` (`numMaterials`):** Bắt buộc **`<= 136` materials / 1 atomic** (`CVisibilityPlugins::RenderFadingAtomic` tại `0x00732480` cấp phát mảng tĩnh `char[136]` trên stack; vượt `136` sẽ ghi đè EIP gây crash `0xFFFFFFFF`).
2. **Đỉnh Mesh & Xương Nhân vật:** Tối đa **`<= 65,535` vertices / geometry**; static building tuyệt đối không chứa chunk `RpSkin`/`RpHAnim`; mọi skin Ped đi đường hoặc tương tác bắt buộc đúng **bộ khung `32` xương chuẩn GTA SA** và RenderWare version stamp **`0x1803FFFF` (`3.6.0.3`)**.
3. **Định dạng `.TXD`:** Bắt buộc `platformId = 9` (`D3D9`), kích thước cạnh là **lũy thừa của 2 (`Power-of-Two`)**, ưu tiên nén **`DXT1` (không alpha) / `DXT5` (có alpha)** để bảo vệ trần `2,800 MiB` Streaming và `4 GB VRAM`.
4. **Độ dài tên file & `.COL3`:** Tên entry trong `.IMG` **`<= 23` ký tự**; tên trong `.COL3` **`<= 21` ký tự** (quy ước dự án `<= 19`); kích thước 1 mục `.COL3` **`< 92,768` bytes**; tọa độ đỉnh cục bộ trong `.COL3` **`< ±250.0m`** (chia ô địa hình `<= 256m × 256m`); **không tạo mục `.COL3` rỗng cho model LOD**.
5. **Cờ Damage `4096` & Tọa độ `water.dat`:** Model `.dff` có nhánh `*_dam` phải bật cờ `4096` trong `.ide`; mọi hình chữ nhật nước trong `water.dat` phải có kích thước cạnh là **số nguyên chẵn**.
6. **Chuỗi văn bản HUD (`CFont`):** Lọc sạch 100% các ký tự điều khiển `~`, `|`, `*`, `@` và ký tự ngoài ASCII 7-bit trước khi đẩy vào `hud.lua` để tránh crash `CFont::ParseToken` (`0x00727B45`).

---

## 6. Ước Lượng Định Lượng: Chúng Ta Còn Nhét Thêm Được Bao Nhiêu Nữa?

Nếu thực hiện bước dọn/chuyển ~`15 GiB` dữ liệu cũ trên ổ `C:` sang ổ `D:` (nơi còn trống **`974.77 GiB`**), trò chơi còn đủ sức chứa **đồng thời tất cả** khối lượng mở rộng sau đây mà không chạm trần 32-bit của GTA SA:

- **Bản đồ & Quốc gia 3D mới:** Thêm được **`5 – 8` quốc gia/lục địa cỡ Mondstadt** HOẶC **`40 – 80` khu đô thị mới cỡ `INLAND-03A` Bắc Chicago** (nhờ còn trống `17,408` ID `< 65,535`, `>430` khe `.img`, `1,380` cửa `ENEX`, và `BuildingPool` nâng được lên `160k–200k`).
- **Nhân vật Anime/Game 3D mới (`Custom Peds`):** Thêm được **`500 – 2,000+` nhân vật 3D độc lập** (còn trống `8,288` slot `Ped Models`, đóng gói vào các `.img` riêng).
- **Phương tiện 3D mới:** Thêm ngay được **`~500` mẫu xe/mô tô/máy bay/tàu thuyền** với cấu hình hiện tại (và nâng tiếp được qua FLA).
- **Bạn gái `WaifuLink` / Nhân vật `Persona Chat` / `Story Quests` rẽ nhánh:** Thêm được **`20 – 50+` nhân vật có cốt truyện rẽ nhánh đầy đủ, hàng nghìn kịch bản Visual Novel, hàng vạn ảnh CG 16:9 và hàng chục giờ lồng tiếng JP** (lưu trên ổ `D:` nối junction, truyền vào game qua khe Ping-Pong TXD tốn `0 MB` RAM tăng thêm trong `gta_pe.exe`).
- **Ứng dụng Smartphone (`EaglePhone OS`) & Hệ thống Gameplay/Kinh tế/Mini-game:** Thêm được **`20 – 50+` ứng dụng mới** (lưới Springboard phân trang + tách file `.lua` riêng trên `LuaJIT 2.1` + xử lý hoàn toàn ở Python Sidecar 64-bit).

---

## 7. Đề Xuất 3 Việc Nhẹ Nên Làm Để Mở Khóa Tối Đa Dư Địa

1. **Giải phóng ngay ~`15 GiB` cho ổ `C:\` (Ưu tiên cao nhất):** Chuyển `ProjectEagleModPack/` (`10.29 GiB`) và các thư mục `staging/project-eagle/` cũ đã đóng gói xong sang `D:\GTA Archive\` kèm NTFS junction; đồng thời quy hoạch thư mục media CG / Voice mới nằm vật lý trên `D:\`.
2. **Đóng băng `COMPONENTPEDS.img` ở mức `11.79 GiB` hiện tại:** Không nhồi thêm asset mới vào `COMPONENTPEDS.img`; mọi đợt thêm NPC/nhân vật mới tiếp tục đi theo hướng `custom_mods.img` hoặc tạo `custom_chars_batch2.img` riêng (`< 1–2 GiB`/file).
3. **Chuẩn hóa bảng đăng ký địa chỉ `_rwdseg` (`0x00CAF200..0x00CAFFFF`):** Ghi cố định sơ đồ cấp phát slot `8-byte [Magic + HeapPtr]` vào `shared-agent-workflow.md` để mọi agent sau khi viết cầu CLEO mới không bao giờ ghi đè lên nhau hoặc chạm mốc Read-Only `0x00CB0000`.
