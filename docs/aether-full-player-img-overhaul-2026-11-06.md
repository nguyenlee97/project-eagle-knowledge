# Đại Tu Toàn Diện Nhân Vật Chính `model_id = 0` (`CJ → Traveler Aether` Hybrid `models/player.img` + Bộ Trang Phục 3D Genshin Mặc Định Tách Rời 3 Món) — 06/11/2026

> [!IMPORTANT]
> **Kế thừa & Hoàn tất trọn vẹn hạng mục cũ ngày 13/10/2026 (`cj-aether.md`):**
> Hạng mục thay nhân vật chính mặc định thành **Traveler Aether** (trước đây tạm dừng ở mức chọn tay qua menu `F2` `RZL-Trainer` `special01` trên bản `clean` cũ do thiếu hệ thống Mập/Ốm, thay quần áo, đội mũ và đồng bộ cắt cảnh) nay đã được **hoàn tất cả Phase 1 (Hybrid `player.img` `542/542` members) lẫn Phase 2 (Bộ trang phục 3D Genshin Impact gốc tách rời 3 món chuẩn native `CClothes` & tự động mặc định ngay khi vào New Game)** trực tiếp trên **`model_id = 0` (`player`)** của bản chơi hợp nhất `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`.

---

## 1. Tổng Quan Kiến Trúc Hướng C + Cách 1 (Native Modular 3-Part Genshin Traveler Outfit)

Thay vì dùng một ped nguyên khối (`AETHER.dff` đơn lẻ chỉ gắn được vào `special01` hoặc khóa chết vào `Slot 17` làm hỏng các cửa hàng quần áo), gói đại tu này tái cấu trúc toàn bộ **`542/542` thành phần trong `models/player.img`** (`152` file `.dff` + `390` file `.txd`), luật `data/clothes.dat` và script khởi tạo 1 lần `cleo/EagleAetherDefaultOutfit.cs`:

1. **Bộ Trang Phục 3D Genshin Impact Gốc Tách Rời 3 Món Chuẩn Native `CClothes` (`src/aether_genshin_outfit_builder.py` + `src/aether_head_builder.py` + `src/aether_deform.py`):**
   - Dùng **Lồng Biến Dạng Tỷ Lệ Liên Tục Không Rách Khớp (`Continuous Proportional Cage`)** thay cho biến đổi rời rạc từng xương `IBM_AE @ inv(IBM_CJ)` (vốn gây trượt khớp vai/bụng và cổ dài), đồng thời hạ đầu Aether xuống `-2.4 cm` (`chin Z_min = +0.5286` ngay trên cổ áo Genshin `Z_max = +0.5202`, khoảng hở cằm-cổ `0.84 cm`) và thu thon cổ GTA xuống `~8.0 cm` chuẩn anime HoYoverse:
     - **`Slot 0` — Áo Giáp & Áo Choàng Lữ Khách Genshin (`painter.dff` + `painter.txd` `512×512` `X8R8G8B8`):** Cổ áo trắng viền vàng hàn khít `0.000 mm` với cầu nối cổ 14 đỉnh (`head.dff` / `flatears.dff`), bảo toàn **100% mảng bụng trần `96` tam giác (`Mat 16` `Z=[0.096..0.237]`) + corset sẫm màu + đai lưng vàng kim đính đá (`Mat 11`)** ngay trong `painter.dff` (gán lại trọng số đùi `41/51` trên đai về `Spine(2)` để mặc chung với quần jeans GTA không bao giờ mất phần bụng hay biến dạng đai), làm mềm trọng số cổ giáp cẳng tay quanh khuỷu (`42% UpperArm + 58% ForeArm`) để gập khuỷu `80°–90°` không nhọn góc, cùng áo choàng sau lưng hai tà trắng-vàng (`Mat 13`). Luật **`HIDE painter hands`** trong `data/clothes.dat` tự động ẩn bàn tay trần `hands.dff` khi mặc áo Genshin và tự động khôi phục bàn tay trần khi đổi sang bất kỳ áo GTA nào khác.
     - **`Slot 2` — Quần Thụng Lữ Khách Genshin (`leathertr.dff` + `leathertr.txd` Anemo Gold + `leathertrchaps.txd` Hydro Midnight `256×512` `X8R8G8B8`):** Quần thụng phồng đùi kèm giáp hông phải (`Right-Hip Tasset`) phân cực mượt theo trọng số xương đùi HAnim (`41..44` vs `51..54`, loại bỏ hoàn toàn vệt kéo tam giác ở `Y = 0`), tích hợp đai lót eo trong khớp 16 đỉnh `0.000 mm` với `torso.dff` và **mesh bắp chân giải phẫu `116` tam giác trích từ `legs.dff` (`~10.2 cm`)** khớp 18 đỉnh `0.000 mm` với giày cổ thấp GTA (`sneaker*`) đồng thời nằm gọn 100% bên trong ống bốt cao Genshin. Luật **`IGNORE leathertr` / `ENDIGNORE leathertr`** trong `data/clothes.dat` (`6/8` ngăn xếp `IGNORE` của `gta_pe.exe` tại `0x005A451C`) giữ nguyên phom quần phồng Genshin khi đi bốt cao `biker`.
     - **`Slot 3` — Bốt Chiến Giáp Cao Cổ Genshin (`biker.dff` + `biker.txd` Trắng-Vàng gốc + 4 phối màu nguyên tố `cowboyboot.txd` Geo, `cowboyboot2.txd` Anemo, `boxingshoe.txd` Pyro, `snakeskin.txd` Electro `512×512` `X8R8G8B8`):** Đầy đủ giáp gối vàng kim phía trước, quấn ống quyển và đế bốt chạm chuẩn mặt đất `Z_min = -1.0420 m`.
2. **Tự Động Mặc Bộ 3D Genshin Ngay Khi Vào New Game (`cleo/EagleAetherDefaultOutfit.cs` — `561 B`, Zero Vòng Lặp Ngầm):**
   - Chạy đúng 1 lần khi vào game (giới hạn tối đa `45 × 150 ms = 6.75 s` rồi gọi `0A93` `end_custom_thread`, **tuyệt đối không có vòng lặp chạy ngầm gây tụt FPS hay xung đột shop/nhiệm vụ**).
   - Đọc trực tiếp `pClothesDesc->m_anTextureKeys`: nếu `Slot 0` đã có áo khác `HOODYAROCKSTAR` (ví dụ Load Save đang mặc bộ đồ người chơi tự phối), script thoát ngay lập tức (`0A93`) để bảo toàn 100% save của người chơi.
   - Chỉ khi khớp trọn bộ 5 món khởi đầu New Game của `main.scm` (`HOODYAROCKSTAR` + `GOATEE` + `JEANSDENIM` + `SNEAKERBINCBLK` + `CAPBLUE`), script tự động trang bị `("painter", "painter", 0)` + `("leathertr", "leathertr", 2)` + `("biker", "biker", 3)` + `("player_face", "head", 1)` qua opcode `087B` (đồng thời **mở khóa sẵn cả 3 món đồ Genshin trong Tủ đồ Safehouse** để thay đi mặc lại miễn phí bất kỳ lúc nào!), gỡ sạch mũ `capblue` qua `0784 (0, 0, 16)`, gọi `070D` (`rebuild_player`) + `0793` (`save_clothes_state`), rồi kết thúc hẳn thread (`0A93`).
3. **Biến Hình Cơ Thể Mập / Ốm / Cơ Bắp (`Fat` / `Normal` / `Ripped` — `0x005A4940`):**
   - Toàn bộ **`152/152` file `.dff`** (bao gồm cả 3 món đồ 3D Genshin `painter.dff`, `leathertr.dff`, `biker.dff`) đều chứa đúng **3 RenderWare `RpClump` (`0x1803FFFF`)** theo thứ tự `Clump 0 = Ripped`, `Clump 1 = Fat`, `Clump 2 = Normal` với pháp tuyến đỉnh mượt (`flags = 0x00010036`) và biên độ mở rộng bụng/hông `Clump 1` (`Fat`) ăn khớp tuyệt đối không lộ lớp lót trong.
4. **Kho Trang Phục Hybrid (`258` Quần Áo + `33` Tóc/Nhuộm Nguyên Tố Barbershop + `48` Hình Xăm + Đội Mũ Không Xuyên Tóc `flatears` + `22` Model Cắt Cảnh `cs_*.dff`):**
   - Bảo toàn trọn vẹn toàn bộ hệ thống da sáng anime đồng bộ 100%, gói trang phục HD Mondstadt/VIP, `33` kiểu tóc/nhuộm nguyên tố Barbershop (`alpha = 255`, khóa bảo vệ mống mắt vàng), `48` hình xăm, luật đội mũ `SETC <hat> head flatears -`, bím tóc sau 4 xương `Head→Neck→Spine1→Spine` và trọng số mặt mềm `Jaw`/`Brow`. Giữ nguyên 100% `data/shopping.dat`.

---

## 2. File Runtime Thay Đổi, Sao Lưu & SHA-256

- **Thư mục đích:** `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`
- **Thư mục staging, mã nguồn build & backup:** `D:\GTA Archive\Staging\project-eagle\cj-to-aether-player-img-20261106\`
- **Manifest giao dịch:** `D:\GTA Archive\Staging\project-eagle\cj-to-aether-player-img-20261106\manifest_before_after.json` *(bản snapshot Phase 1 được lưu riêng tại `backup/phase1_manifest_before_after.json`; các file gốc trước đại tu `backup/*.orig` được bảo toàn nguyên vẹn 100%)*

| File tương đối tại `gameplay-lab` | Trước khi cài (Size / SHA-256) | Sau khi cài (Size / SHA-256) | Ghi chú |
| --- | --- | --- | --- |
| `models/player.img` | `66,738,176` B<br>`077a6fb1da2940822e2d7aaf868c129789d165b3878da3eb5533c0cf50400e86` | `308,340,736` B<br>`8d2462a3812d223c560c6129f329f52ae6761b3185ba2615a5a6f199dea08f68` | Đủ `542/542` entries (`152` DFF 3-clump gồm bộ 3 món 3D Genshin tỷ lệ chuẩn HoYoverse + `390` TXD `BGRA32` HD) |
| `data/clothes.dat` | `5,317` B<br>`5fff15c81a5f8c32f4d3dff22ad6748c9b8c0a45af7b9f67e22fb2b9ae05c593` | `5,501` B<br>`f2c0ec1f285e62459293303c24e1899e3c24ca65de2ebc34800fc9fcb400a18b` | Luật `SETC <hat> head flatears -` + `HIDE painter hands` + `IGNORE leathertr` (`6/8` stack) |
| `cleo/EagleAetherDefaultOutfit.cs` | *(chưa tồn tại)* | `561` B<br>`d2fb11fca240d6864bbcd8b2e6da4807729984ef124c21ecb41cfdc761123286` | Script CLEO khởi tạo 1 lần tự động mặc bộ 3D Genshin khi New Game rồi `0A93` thoát hẳn |
| `data/shopping.dat` | `46,875` B<br>`93e640e29049ee9985185b7aaf1b2f3d11f8540ff8791a751632d6ba90d0bd4d` | `46,875` B *(giữ nguyên 100%)*<br>`93e640e29049ee9985185b7aaf1b2f3d11f8540ff8791a751632d6ba90d0bd4d` | Không sửa cấu hình giá/cửa hàng gốc |

---

## 3. Kết Quả Kiểm Thử 2 Giai Đoạn (Offline-First → Live DirectX 9)

### Part A — Kiểm Thử Nhị Phân & Giả Lập `CClothesBuilder` Ngoài Game (`100% PASS`)
- Script: `D:\GTA Archive\Staging\project-eagle\cj-to-aether-player-img-20261106\src\test_part_a_cclothes_emulator.py`
- Báo cáo JSON: `D:\GTA Archive\Staging\project-eagle\cj-to-aether-player-img-20261106\qa_offline\part_a_verification_report.json`
- **Kết quả:**
  - `542/542` thành phần đọc sạch; `152/152` DFF có đủ 3 morph clumps (`Ripped`, `Fat`, `Normal`), khớp đỉnh/tam giác, pháp tuyến hữu hạn khác 0, tổng trọng số xương chuẩn hóa `1.0`.
  - Độ hở đường nối cổ (`head`/`flatears` ↔ `torso` & `painter`), cổ tay, eo (`torso` ↔ `legs` & `leathertr`) và cổ chân (`legs` & `leathertr` ↔ `feet`/`sneaker`) đạt **`0.000000 m`** trên cả 3 trạng thái cơ thể.
  - Giả lập đầy đủ luật `HIDE` / `IGNORE..ENDIGNORE` / `SETC` trên toàn bộ **`258` trang phục cửa hàng**, **`33` kiểu tóc Barbershop** và **`48` hình xăm**: **`0` lỗi, `0` rò màu da cũ, `0` lộ lót eo ở cả `Normal`/`Ripped`/`Fat`**.
  - Kết xuất và kiểm tra bằng mắt thật **5 bảng Studio Render đa góc nhìn**: `qa_offline/sheet1_core_wardrobe.png`, `sheet2_morphs_and_barbershop.png`, `sheet3_hats_glasses_and_special.png`, `sheet4_genshin_default_and_mixmatch.png`, và **`sheet5_standing_pose_vs_original_aether.png`** (đối chiếu trực tiếp tư thế đứng `IDLE_STANCE` & gập khuỷu `80°` phóng đại `650 px/m` với `Aether.dff` gốc).

### Part B — Nghiệm Thu Trực Tiếp Trong Game `gta_pe.exe` DirectX 9 `1920×1080` (`100% PASS`)
- Script: `D:\GTA Archive\Staging\project-eagle\cj-to-aether-player-img-20261106\src\run_part_b_aether_ingame_qa.py`
- Báo cáo JSON & 9 ảnh chụp thực tế (`1920×1080`): `D:\GTA Archive\Staging\project-eagle\cj-to-aether-player-img-20261106\qa_ingame\`
  1. `01_newgame_default_genshin_front.png` & `02_newgame_default_genshin_back_cape_braid.png`: Khởi động **New Game** vào thế giới 3D, xác nhận nhân vật chính spawn tự nhiên ở **`model_id = 0`** và **`EagleAetherDefaultOutfit.cs` tự động mặc ngay bộ 3 món 3D Genshin Traveler Outfit** (`slot0=0xC8B4083D` `painter`, `slot2=0xC58D0A36` `leathertr`, `slot3=0x8956FDC5` `biker`, `hat=0x00000000` đã gỡ sạch mũ/râu New Game) trước khi bất kỳ script Python nào can thiệp! Áo choàng hai tà trắng-vàng và bím tóc vàng sau lưng hiển thị sắc nét, không xuyên mesh.
  2. `03_mixmatch_genshin_top_gta_jeans.png` → `09_vip_suit_wardrobe_switch_live.png`: Gọi trực tiếp hàm gốc `CClothes::RebuildPlayer` (`0x005A82C0`) trên luồng chính D3D9 (~`138.5 ms – 267.7 ms`/lần) kiểm chứng thực tế:
     - **Phối Áo 3D Genshin + Quần Jeans GTA + Giày Sneaker Đỏ (`03`):** Khăn choàng, áo choàng và găng tay Genshin phối mượt mà với quần jeans thường.
     - **Phối Áo Khoác Mondstadt (`field`) + Quần Thụng & Bốt Cao Genshin (`04`):** Luật `HIDE painter hands` tự động trả lại bàn tay trần sáng màu khi cởi áo Genshin!
     - **Phối Mũ Lưỡi Trai Đỏ (`flatears`) + Kính Râm + Áo Genshin + Quần Hydro (`leathertrchaps`) + Giày Sneaker Trắng (`05`):** Không xuyên tóc trên đỉnh mũ, cổ chân nối kín khít `0.000 mm` với giày cổ thấp GTA.
     - **Tóc Đỏ Pyro (`hairred`) Tại Barbershop + Áo Genshin + Bốt Đỏ Natlan (`boxingshoe`) (`06`):** Giữ nguyên đôi mắt vàng hổ phách đặc trưng của Aether.
     - **Biến Hình Max Muscle (`Ripped = 1000`) & Max Fat (`Fat = 1000`) Ngay Trên Bộ 3D Genshin (`07`, `08`):** Cơ ngực/vai nở săn chắc ở `Ripped` và bụng tròn mũm mĩm + má phúng phính chuẩn GTA SA ở `Fat`, không hở đường may hay lộ lót trong.
     - **Đổi Sang Bộ Vest Đen VIP Didier Sachs + Kính Râm + Đồng Hồ (`09`):** Chuyển qua lại giữa bộ 3D Genshin và toàn bộ tủ đồ GTA mượt mà 100%.
  3. **Kiểm tra chuyển động & hệ thống ngay trên bộ 3D Genshin (`model_id = 0`):** Đi bộ, chạy nước rút, nhảy vượt chướng ngại vật (`.COL` landing `PASS`), kiểm tra phân cấp xương `RpClump` (`6/6 PASS, 0 FAIL`), `EagleLuaErrors.log = 0`, và hậu kiểm `python eagle_doctor.py --doctor` đạt **`11/11 PASS, 0 WARN, 0 FAIL`**.

---

## 4. Hướng Dẫn Phục Hồi (Guarded Rollback)

Gói triển khai có script phục hồi độc lập kiểm tra SHA-256 hai chiều và khóa ghi `game-write.lock` (khôi phục nguyên trạng `models/player.img` + `data/clothes.dat` về bản gốc trước đại tu và tự động xóa sạch `cleo/EagleAetherDefaultOutfit.cs`; tự động chặn nếu file đã bị tác vụ khác sửa đổi về sau):

```powershell
# Kiểm tra trạng thái preflight (không ghi file):
python "D:\GTA Archive\Staging\project-eagle\cj-to-aether-player-img-20261106\rollback_aether_player_img.py" rollback-preflight

# Phục hồi nguyên trạng models/player.img, data/clothes.dat và xóa EagleAetherDefaultOutfit.cs (khi gta_pe.exe đã tắt):
python "D:\GTA Archive\Staging\project-eagle\cj-to-aether-player-img-20261106\rollback_aether_player_img.py" rollback
```
*(Hoặc chạy file tiện ích `D:\GTA Archive\Staging\project-eagle\cj-to-aether-player-img-20261106\Rollback_Aether_Player_Img.bat`).*
