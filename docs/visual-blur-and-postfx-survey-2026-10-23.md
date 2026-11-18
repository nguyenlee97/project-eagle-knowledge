# Khảo sát hiệu ứng nhòe hình khi trời nắng gắt và khi chạy xe nhanh trên Project Eagle (`gameplay-lab`)

**Ngày khảo sát:** 23/10/2026  
**Phạm vi:** Chỉ đọc cấu hình, log và disasm thực tế trên `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab` (`gta_pe.exe`, `PECore.asi`, `skygfx.asi`, `skygfx1.ini`, `stream.ini`, `PECore.ini`, `data\timecyc_ss.dat`, `cleo\RZL-Trainer.cs`, `cleo\RZL-Trainer.ini`). Chưa sửa file runtime của game.

---

## 1. Tổng quan nguyên nhân

Hiện tượng hình ảnh bị nhòe mạnh khi trời nắng gắt và khi chạy xe nhanh trên **Project Eagle (`gta sa gameplay-lab`)** không đến từ một thiết lập đơn lẻ mà là sự cộng hưởng của **4 cơ chế PostFX** đang cùng bật:

| Hiện tượng | Cơ chế gây nhòe | Thành phần điều khiển thực tế trong `gameplay-lab` | Trạng thái hiện tại |
| :--- | :--- | :--- | :--- |
| **1. Trời nắng gắt bị nhòe sáng / chói lóa (Bloom / Glow)** | **Radiosity (Shader Bloom)** — hạ độ phân giải khung hình (`1 << radiosityFilterPasses`) rồi cộng tính các vùng sáng vượt ngưỡng `Limit` đè lên màn hình | `PECore.asi` hook `CPostEffects::Render` tại `0x00704D5E` & `0x00704FB4` (`0x1010A570` → `0x1010A9E0`), nhận tham số từ `skygfx1.ini` (`doRadiosity`, `radiosityFilterPasses`, `radiosityIntensity`) và cột `Intensity`/`Limit` trong `data\timecyc_ss.dat` | **Đang bật** (`doRadiosity=1`, `pe_bRadiosity 1`, `radiosityFilterPasses=2` (4x downsample), `radiosityIntensity=35`) |
| **2. Trời nắng gắt bị nhòe gợn sóng / rung mờ (10:00–18:00)** | **Heat Haze FX (Ảo ảnh nhiệt mặt đường)** — cắt 150 dải ngang màn hình dịch lệch ngẫu nhiên và vẽ đè với độ mờ `alpha = 80` (`0x008D50E8`) | Hàm vẽ gốc `CPostEffects::HeatHazeFX` (`0x00701780`), nhưng điều kiện kích hoạt bị `PECore.asi` thay thế hoàn toàn tại `CWeather::Update` (`0x0072B850` → `0x1011CE00`) dựa theo cột `WeatherInfo == 2` trong `data\timecyc_ss.dat` | **Đang bật** cho 23 kiểu thời tiết nắng/nắng gắt (`WeatherInfo = 2`). Tùy chọn `DisableHeat` của `RZL-Trainer` bị vô hiệu hóa do `PECore.asi` đã thay `CWeather::Update` |
| **3. Nhòe lưu ảnh / bóng mờ kéo dài ở Vice City, Liberty City** | **VCS / VC / III / LCS Motion Trails** — trộn khung hình cũ vào khung hình mới + 4-pass blur (riêng `VCS`) | `PECore.asi` (`0x10109BC0`, `0x10109670`, `0x1010AEF0`) tự bật khi cột `ColorFilter` trong `data\timecyc_ss.dat` là `III`, `VC`, `VCS` hoặc `LCS` | **Đang bật tự động** theo vùng thời tiết (`VC`/`III`: intensity `50`; `VCS`: intensity `30` + 4-pass blur; `LCS`: intensity `70`) |
| **4. Chạy xe nhanh bị nhòe (Radial Speed Blur + Rung camera)** | **SpeedFX (`CPostEffects::SpeedFX`)** — vẽ chồng khung hình lệch tâm theo tốc độ xe với độ mờ `m_SpeedFXAlpha` (`0x008D5104`) nhân màu `PostFX1`/`PostFX2` | Hàm gốc `0x007030A0` (gọi từ `0x00704E8A`), điều khiển bởi `0x008D5100` (`Speed Blur FX`) và `0x008D5104` (`Speed Blur alpha`). Có hỗ trợ tắt trong `cleo\RZL-Trainer.ini` | **Đang bật** (`0x008D5100 = 1`, `0x008D5104 = 36`; trong `RZL-Trainer.ini` đang để `DisableMotionBlur = 0`) |

---

## 2. Chi tiết kỹ thuật từng cơ chế

### 2.1. Tương tác giữa `skygfx.asi` và `PECore.asi` trong `CPostEffects::Render`

Qua kiểm tra binary và `PECore.log`:
1. Khi khởi động, `skygfx.asi` (`0x1000DC5E..0x1000DD24`) cài hook vào 4 vị trí trong `CPostEffects::Render`:
   - `0x00704D1F` (`ColourFilter`)
   - `0x00704D49` (`DarknessFilter`)
   - `0x00704D5E` (`Radiosity` nhánh 1)
   - `0x00704FB4` (`Radiosity` nhánh 2)
2. Sau đó, khi `TimecycPatch = true` trong `PECore.ini`, `PECore.asi` (`0x10108EC0..0x10109037`) **ghi đè lên chính 4 địa chỉ hook trên** để trỏ về pipeline shader riêng của `PECore.asi`:
   - `0x00704D1F` → `PECore.asi!0x10109BC0` (ColorFilter + Motion Trails)
   - `0x00704D49` → `PECore.asi!0x1010A270` (DarknessFilter)
   - `0x00704D5E` & `0x00704FB4` → `PECore.asi!0x1010A570` (Radiosity + VCS Bloom)
3. Tuy nhiên, trước khi gọi vào `0x00704FB4` (`PECore.asi!0x1010A570`), code của `gta_pe.exe` tại `0x00704F61..0x00704FB3` vẫn kiểm tra biến toàn cục `CPostEffects::m_bRadiosity` (`0x00C402CC`) và đẩy 4 tham số lên stack:
   - `[ebp+8]`: `intensityLimit` (`0x00B7C53C`, nạp từ cột `Limit` của `data\timecyc_ss.dat`)
   - `[ebp+0xC]`: `CPostEffects::m_RadiosityFilterPasses` (`0x008D510C`)
   - `[ebp+0x10]`: `CPostEffects::m_RadiosityRenderPasses` (`0x008D5110`)
   - `[ebp+0x14]`: `CPostEffects::m_RadiosityIntensity` (`0x008D5118`)
4. Các biến `0x00C402CC`, `0x008D510C`, `0x008D5110`, `0x008D5118` được `skygfx.asi` (`0x1000D1E0`) đồng bộ liên tục từ file `skygfx1.ini` (và có thể nạp lại nóng trong game bằng phím **`F11`** theo `keyReload=0x7A`).

### 2.2. Heat Haze FX và lý do `DisableHeat` của RZL-Trainer không hoạt động

- Trong `PECore.asi` (`0x1011DE70..0x1011DF6A`), hàm `CWeather::Update` tại `0x0072B850` bị thay thế bằng `PECore.asi!0x1011CE00`, đồng thời 5 tham chiếu tới `CWeather::HeatHazeFXControl` (`0x4DF464`, `0x7136D2`, `0x716B12`, `0x716C92`, `0x716EA3`) được chuyển hướng sang `0x00C81300`.
- Tại `0x1011D8C5..0x1011D9A0`, `PECore.asi` đọc cột **`WeatherInfo`** (cột thứ 2 từ cuối trong `data\timecyc_ss.dat`). Nếu `WeatherInfo == 2` và giờ trong game từ `10h` đến `18h`, `PECore.asi` gán `CWeather::HeatHaze` (`0x00C812DC`) = `1.0f`, kích hoạt `CPostEffects::HeatHazeFX(1.0f, false)` tại `0x00705116`.
- Trong `cleo\RZL-Trainer.cs` (offset `0x11125B` / `0x1ABF70`), tùy chọn `DisableHeat = 1` ghi byte `0xEB` vào địa chỉ `0x0072C1B7` (nằm giữa hàm `CWeather::Update` gốc của GTA SA). Do `PECore.asi` đã nhảy khỏi `0x0072B850` ngay đầu hàm, đoạn code tại `0x0072C1B7` không bao giờ được thực thi.

### 2.3. Speed Blur FX khi chạy xe nhanh

- Tại `0x00704D7B..0x00704E8F` trong `gta_pe.exe`, khi `CPostEffects::m_bSpeedFX` (`0x008D5100`) != 0, game tính vận tốc phương tiện của người chơi và gọi `CPostEffects::SpeedFX` (`0x007030A0`).
- Độ mạnh của lớp nhòe tốc độ phụ thuộc vào:
  - `CPostEffects::m_SpeedFXAlpha` (`0x008D5104`, mặc định `36` / `0x24`, phạm vi `0..255`).
  - Giá trị Alpha của `PostFX1` và `PostFX2` trong `data\timecyc_ss.dat` (nhiều dòng `SUNNY`/`EXTRASUNNY` của `SA` đang đặt Alpha = `255`).
- Trong `cleo\RZL-Trainer.cs` (offset `0x45CBB` / `0x1AE9B2`), thiết lập `DisableMotionBlur = 1` trong `cleo\RZL-Trainer.ini` dùng opcode `0A8C` ghi `0` trực tiếp vào `0x008D5104` (`m_SpeedFXAlpha`). Khác với `DisableHeat`, cơ chế này **hoạt động hoàn toàn bình thường** trên `gameplay-lab` vì `PECore.asi` không thay thế `CPostEffects::SpeedFX`.

---

## 3. Các phương án Tune giảm nhẹ hoặc Tắt theo nhu cầu

### 3.1. Giảm hoặc tắt nhòe khi trời nắng gắt

1. **Giảm độ chói/nhòe sáng Radiosity (Bloom) trong `skygfx1.ini` (Khuyên dùng khi muốn tune nhẹ xuống):**
   - Mở `skygfx1.ini`, tìm 3 dòng cuối (dòng 128–130 đang bị comment bằng dấu `;`):
     ```ini
     radiosityFilterPasses=1      ; Giảm từ 2 xuống 1 để giảm độ loang nhòe (downsample 2x thay vì 4x)
     radiosityRenderPasses=1      ; Giữ nguyên 1
     radiosityIntensity=15        ; Giảm từ mặc định 35 xuống 12..18 để nắng dịu hơn
     ```
   - Có thể chỉnh rồi bấm **`F11`** ngay trong game để xem kết quả tức thì.
   - Nếu muốn **tắt hẳn** Radiosity: đổi `doRadiosity=0` ở dòng 67 của `skygfx1.ini` (và `pe_bRadiosity 0` ở dòng 11 của `stream.ini`).

2. **Giảm hoặc tắt hiệu ứng gợn sóng nhiệt mặt đường (Heat Haze 10h–18h):**
   - **Cách A (Không cần thêm script — sửa `data\timecyc_ss.dat`):** Đổi cột `WeatherInfo` (cột áp chót) từ `2` sang `1` ở các kiểu thời tiết nắng (`WTH_EXTRASUNNY_*`, `WTH_SUNNY_LV`, `WTH_SUNNY_COUNTRYSIDE`, `WTH_SUNNY_DESERT`...). Khi `WeatherInfo = 1`, trời vẫn nắng và giữ nguyên màu sắc/SunGlare nhưng không bật lớp nhòe biến dạng `HeatHazeFX`.
   - **Cách B (Tune nhẹ độ nhòe Heat Haze bằng CLEO hoặc chỉnh trong game):** Giảm giá trị `m_HeatHazeFXIntensity` tại địa chỉ `0x008D50E8` (int32, mặc định `80` / `0x50`) xuống `20–30`, hoặc giảm độ lệch `m_HeatHazeFXRandomShift` tại `0x008D50EC` (mặc định `12`) xuống `3–4`.

3. **Thử nghiệm trực tiếp bằng Debug Menu ẩn của `PECore.asi` (`Ctrl + M`):**
   - Trong `PECore.ini`, nếu tạm bật `DeveloperMode = true` dưới mục `[SETTINGS]`, vào game bấm **`Ctrl + M`** sẽ mở bảng điều khiển trực tiếp của Project Eagle:
     - Nhánh **`PECore | PostFX`**: có đầy đủ nút bật/tắt và thanh trượt `Radiosity enabled`, `VCS trails`, `Trails intensity`, `Speed Blur FX`, `Speed Blur alpha` (`0..255`).
     - Nhánh **`PECore | Timecyc`** → `Open Timecyc Editor`: cho phép kéo giảm `Radiosity Intensity`, `Radiosity Limit`, `PostFX 1/2 Alpha` theo thời gian thực và bấm **Save timecyc** để lưu xuống `data\timecyc_ss.dat`.

### 3.2. Giảm hoặc tắt nhòe khi chạy xe nhanh (Speed Blur)

1. **Tắt hẳn bằng cấu hình có sẵn (`cleo\RZL-Trainer.ini`):**
   - Mở `cleo\RZL-Trainer.ini`, tại mục `[VehicleOptions]` (dòng 125–126):
     ```ini
     DisableMotionBlur           =1
     VehicleCameraShake          =1   ; (Tùy chọn: đặt =1 nếu muốn tắt luôn rung lắc camera khi chạy nhanh)
     ```
   - Hoặc bấm **`F2`** trong game → `Vehicle Options` → bật `Disable Motion Blur`.
2. **Tune giảm nhẹ thay vì tắt hẳn:**
   - Thay vì đưa `0x008D5104` (`CPostEffects::m_SpeedFXAlpha`) về `0`, có thể đặt giá trị này ở mức **`12`–`18`** (bằng một nửa mặc định `36`) qua thanh trượt `Speed Blur alpha` trong menu `Ctrl + M` (`PECore | PostFX`) hoặc bằng một script CLEO 1 dòng tự nạp khi vào game.

---

## 4. Kết quả triển khai Tune giảm nhẹ (23/10/2026)

Theo yêu cầu của người dùng (*"tune giảm nhẹ thôi, nó cũng có tính aesthetic của riêng nó chỉ là làm game hơi khó chơi xíu"*), bản tinh chỉnh nhẹ đã được áp dụng vào `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab` mà **không chỉnh sửa bất kỳ file binary gốc nào** (`gta_pe.exe`, `gta_sa.exe`, `PECore.asi`, `skygfx.asi` giữ nguyên 100% SHA-256):

| Hiệu ứng | Tham số / Địa chỉ | Giá trị gốc (Eagle) | Giá trị sau khi Tune nhẹ | Tác dụng thực tế |
| :--- | :--- | :--- | :--- | :--- |
| **Radiosity Downsample** (`skygfx1.ini`) | `radiosityFilterPasses` (`0x008D510C`) | `2` (4x downsample) | **`1`** (2x downsample) | Giữ viền vật thể sắc nét hơn dưới trời nắng gắt, không bị loang nhòe rộng |
| **Radiosity Bloom Intensity** (`skygfx1.ini`) | `radiosityIntensity` (`0x008D5118`) | `35` | **`15`** (~43% gốc) | Giữ ánh nắng ấm đặc trưng của PS2/Shader Radiosity nhưng không gây chói lóa trắng màn hình |
| **Sunny Heat Haze Opacity** (`EaglePostFXTune.cs/.ini`) | `m_HeatHazeFXIntensity` (`0x008D50E8` & init immediate `0x00701487`) | `80` (`0x50`) | **`28`** (35% gốc) | Giữ gợn nhiệt mỏng nhẹ buổi trưa (10:00–18:00), loại bỏ hiện tượng bóng đôi nhòe chữ/đường |
| **Sunny Heat Haze Shimmer Speed** (`EaglePostFXTune.cs/.ini`) | `m_HeatHazeFXSpeedMin/Max` (`0x008D50EC`/`0x008D50F0` & init `0x00701497`/`0x007014A7`) | `12` / `18` | **`6` / `10`** | Chuyển tốc độ gợn sóng nhiệt từ mức giật nhanh (`HEAT_HAZE_0`) về mức êm dịu (`HEAT_HAZE_1`) |
| **High-Speed Motion Blur** (`EaglePostFXTune.cs/.ini`) | `m_SpeedFXAlpha` (`0x008D5104`) | `36` (`0x24`) | **`14`** (~39% gốc) | Giữ cảm giác lướt gió khi phóng nhanh nhưng vẫn nhìn rõ mặt đường và chướng ngại vật |

### Cách tinh chỉnh nóng trong lúc chơi (Live Tuning)
- **Chỉnh độ nhòe tốc độ cao & gợn nắng Heat Haze:** Mở file [`Project Eagle/gta sa gameplay-lab/cleo/EaglePostFXTune.ini`](../../Project%20Eagle/gta%20sa%20gameplay-lab/cleo/EaglePostFXTune.ini), đổi số rồi lưu lại — script `EaglePostFXTune.cs` tự động đọc lại mỗi `1.5` giây ngay trong game mà không cần khởi động lại.
- **Chỉnh độ chói nắng Radiosity:** Mở file [`Project Eagle/gta sa gameplay-lab/skygfx1.ini`](../../Project%20Eagle/gta%20sa%20gameplay-lab/skygfx1.ini) (3 dòng cuối), lưu lại và bấm phím **`F11`** trong game để `skygfx.asi` nạp lại ngay lập tức.

### Phục hồi (Rollback về nguyên trạng trước khi tune)
```powershell
python "C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\postfx-blur-tuning-2026-10-23\build_and_deploy.py" rollback
```
Xem thêm [phiếu công việc bàn giao](work-items/2026-10-23-antigravity-postfx-blur-tuning.md) và [`manifest.json`](../../staging/project-eagle/postfx-blur-tuning-2026-10-23/manifest.json).
