# Báo Cáo Khảo Sát Chuyên Sâu & Bàn Giao Kiến Trúc Chicago (`INLAND-03A` & `PRA\CHICAGO`) — 16/11/2026

- **Ngày lập**: `2026-11-16`
- **Hội thoại thực hiện**: `b2313015-e01f-424c-a419-f07a4165323c` (`Antigravity`)
- **Work-Item liên kết**: `docs/project-eagle/work-items/2026-11-16-antigravity-fix-chicago-crash-and-lag.md`
- **Staging & Rollback**: `staging/project-eagle/fix-chicago-crash-and-lag-20261116/`
- **Đích triển khai**: `Project Eagle/gta sa gameplay-lab`
- **Đối tượng đọc tiếp theo**: Hội thoại đại tu `M3` (`Bridge 1 Carcer ↔ Chicago` + khu Nam/Downtown Chicago `PRA\CHICAGO`) và các tác vụ xây dựng khu vực mở rộng ngoài `[-3000..3000]`.

---

## 1. Bản Đồ Phân Tầng Không Gian Chicago Trong `Project Eagle`

Vùng **Chicago / Windy Bay** trong `gameplay-lab` hiện được chia làm **2 phân khu kỹ thuật hoàn toàn khác nhau** tại vĩ tuyến nối **`Y = 10027.9`**:

| Phân khu | Tọa độ thế giới `(X, Y, Z)` | Nguồn tài nguyên (`gta.dat` / `S&S`) | Hiện trạng kỹ thuật (16/11/2026) |
| :--- | :--- | :--- | :--- |
| **Nam / Downtown Chicago (`PRA\CHICAGO`)** | `X ∈ [5600..7600]`, `Y ∈ [8750..10027.9]`, mặt cầu Đông `Bridge 1` nối từ `Carcer West` vào tại `X ≈ 7090..8770, Y ≈ 9720` | `S&S\Data\Maps\PRA\CHICAGO\chicago.{ide,ipl}` + `S&S\CDIMAGES\andreas\chicago.img` | Bản port thô của S&S: nhiều đoạn hầm/đường chìm xuyên nhà (`wb_road47.dff`), thiếu texture mặt đường/vỉa hè, lỗi khớp cao độ tiếp giáp đầu Tây `Bridge 1`. **Đây là phạm vi trọng tâm của đợt sửa `M3` sắp tới.** |
| **Bắc Chicago (`INLAND-03A` — Sakura & Academy District)** | `X ∈ [5630..6980]`, `Y ∈ [10027.9..11260]`, cốt nền đô thị chuẩn `Z = 14.40m` (nền pad), `Z = 14.50m` (mặt nhựa đại lộ), `Z = 14.65m` (vỉa hè đá nâng cao) | `CUSTOM/inland03a_sakura_chicago.{ide,ipl,col,img}` + 3 script CLEO `Inland03a{TrafficFlow,SakuraLife,CrowdB}.cs` | Gồm `9` tấm nền (`in03_pad_r0..r2_c0..c2`), `9` phân khu đại lộ bàn cờ (`in03_rd_r0..r2_c0..c2`), `5` dốc hàn nối Nam–Bắc (`in03_south_ramps` `ID 12288` tại `X = 5822.7, 6105.8, 6319.2, 6510.0, 6728.4` khớp xuống cao độ đường `PRA\CHICAGO` tại `Y = 10027.9`), `20` tổ hợp công trình/trường học/sân khấu/cao ốc (`857` thực thể IPL: `568` Near + `289` LOD, `0` lỗi `lod_index`). **Chi nhánh Sàn Chứng Khoán Bắc Chicago (`wallstreet_poi_chi`) đặt tại `(6339.00, 10523.60, 14.45)` trước tòa `in03_akiba_twr1` (`ID 12244`).** |

---

## 2. Giải Phẫu Pháp Y Chuỗi Nhân Quả Chung Của Cả 2 Bug Ở Bắc Chicago

Điểm phát hiện quan trọng nhất của đợt khảo sát này: **Bug B (đứng một lát tụt còn `23.0 FPS` / `43.5ms` tại `(6325.33, 10541.25)`) và Bug A (crash `0x49646550` khi chạm mũi tên vàng vào Sàn Chứng Khoán `(6339.00, 10523.60, 14.45)`) không phải hai lỗi rời rạc mà là hai mắt xích của CÙNG MỘT chuỗi quá tải bộ nhớ `CStreaming`!**

### 2.1. Nguyên nhân gốc của Bug B1 (Lag nặng `23.0 FPS` & tràn `857.1 MiB / 768.0 MiB` Streaming)

Khi đo đạc trực tiếp các file `.dff`/`.txd` bên trong `CUSTOM/inland03a_sakura_chicago.img` tại đúng tọa độ ảnh chụp của người dùng `(6325.33, 10541.25, 15.50)`:
1. **Lỗi nhân bản Full-Detail DFF + Near TXD làm LOD `1500m`**:
   - Trong script dựng ban đầu (`build_inland03a_sakura_district.py` dòng `978–981`), toàn bộ `39` model LOD công trình (`ID 12320..12386`, đặt `270` thực thể khắp Bắc Chicago với `ddist = 1500m`) đã ghi nguyên xi bản copy chưa giảm lưới của `clean_dff` gốc (lên tới `77,530` tam giác/model!) và trỏ thẳng vào `.txd` gốc (`12–23 MiB`/file) thay vì dùng vỏ hộp kiến trúc nhẹ chung `in03_urban_txd`.
   - Hệ quả: Đứng ở giữa đại lộ `Sakura Central Blvd`, game phải vẽ đồng thời **`917,481` tam giác LOD ở cự ly `299..1500m`** (`lod_casacampo` `221,179` tris, `lod_new_mansion` `163,968` tris, `lod_nagato_hall` `149,055` tris, `lod_car_showrm` `99,671` tris...) cộng thêm **`878,743` tam giác Near (`<= 299m`)** = **`1,796,224` tam giác/khung hình**!
2. **Lưới khung siêu nhỏ của biển `in03_miku_sign.dff` (`ID 12265`)**:
   - Riêng 1 model `in03_miku_sign.dff` chứa `77,530` tam giác (`4` thực thể gần người chơi = **`310,120` tam giác**), trong đó phần neon nhân vật Miku (`mat=1`, `Hatsune_Neon`) chỉ có **`5,978` tam giác**, còn **`71,428` tam giác** ở `mat=0` (`candysign1_256`) là các nan lồng sắt li ti diện tích `< 0.015 m²` không nhìn thấy bằng mắt thường từ mặt đường.
3. **Gánh nặng `.txd` không nén & texture `2048–4096px`**:
   - `inland03a_sakura_chicago.img` chứa `140.00 MiB` dữ liệu `.txd` (trong đó có `25` texture `32-bit BGRA` không nén như `PD_R_C_67772` `1024x1024` = `5.33 MiB`/texture và `6` texture `2048–4096px`). Vì mọi LOD `1500m` đều tham chiếu `.txd` chi tiết gần, chỉ cần đứng ở Bắc Chicago 15–25 giây là `CStreaming` buộc phải nạp **`31` file `.txd` (`115.20 MiB`) + `31.63 MiB` `.dff`**, cộng thêm `44` skin `MISSION_CHAR` anime/Genshin từ 2 script đám đông -> đẩy `CStreaming::ms_memoryUsed` vọt lên **`857.1 MiB / 768.0 MiB`** (vượt trần `VAS_FLOOR_AVAIL_BYTES = 768 MiB`)!

### 2.2. Giải phẫu pháp y Crash `0x49646550` (`"PedIntelligence"`) khi vào Sàn Chứng Khoán (`Bug A`)

Từ `ProjectEagle_crashes/2026-11-16_05-03-36.log` và disassembly `gta_pe.exe`:
- **Thanh ghi lúc nổ**:
  - `EIP = 0x49646550` -> đổi sang ASCII little-endian (`50 65 64 49`) chính là 4 ký tự đầu của chuỗi **`"PedIntelligence"`** nằm trong `.rdata` tại `0x00863C60`!
  - `EDX = 0x00863C40` -> chính là địa chỉ **`CPlaceable::vftable`** trong `gta_pe.exe`! Tại `0x00863C40 + 0x20` (`vtbl[8]`, vị trí hàm ảo `CEntity::DeleteRwObject`), `CPlaceable` không có hàm thứ 8 (chỉ có 2 hàm ảo destructor), nên bộ nhớ `.rdata` ngay sau `CPlaceable::vftable` chứa chuỗi `"PedIntelligence"` (`*(DWORD*)(0x00863C40 + 0x20) == 0x49646550`)!
  - `ECX = 0x2561E6F8`, `Return Address = 0x00409172` (ngay sau lệnh `8B 11 FF 52 20` = `mov edx, [ecx]; call dword ptr [edx+20h]` tại `0x0040916D` trong `CStreaming::DeleteAllRwObjects`, được gọi từ `03CB: LOAD_SCENE 2052.0 -1600.0 999.95` của `EagleWallStreetBridge.cs` khi chuyển cảnh vào nội thất Sàn Chứng Khoán `ID 15100`!).
- **Cơ chế hình thành con trỏ ma `0x2561E6F8` (`*ECX = 0x00863C40`)**:
  1. Người chơi vừa ghé chi nhánh Sàn CK San Fierro (`sector 445, 503`), sau đó đến Bắc Chicago và đứng đủ lâu để các LOD `1500m` đẩy `CStreaming::ms_memoryUsed` lên `857.1 MiB / 768.0 MiB`.
  2. `CStreaming` kích hoạt thu hồi khẩn cấp (`RemoveLeastUsedModel`) và đuổi khối va chạm `.COL` của khu San Fierro ra khỏi RAM **trước khi** `CIplStore::RemoveIpl` hủy các thực thể `CBuilding` thuộc binary-IPL của San Fierro.
  3. Khi `CIplStore::RemoveIpl` chạy hàm hủy `CBuilding::~CBuilding -> CEntity::Remove()`, `CEntity::GetBoundRect()` (do đã mất `.COL`!) trả về khung bao suy biến quanh tâm thực thể thay vì khung bao đầy đủ, khiến vòng lặp tháo liên kết bỏ sót một ô lưới lân cận `CSector[445, 503].m_buildings` (`EBP = 0x0D` trên vùng sector mở rộng của `$fastman92limitAdjuster.asi`).
  4. Sau đó hàm hủy cơ sở `CPlaceable::~CPlaceable` ghi đè `*0x2561E6F8 = 0x00863C40` (`CPlaceable::vftable`). Con trỏ `0x2561E6F8` nằm im trong `CSector[445, 503].m_buildings` cho tới đúng khoảnh khắc người chơi bước vào mũi tên vàng Sàn CK Bắc Chicago -> `03CB: LOAD_SCENE` gọi `CStreaming::DeleteAllRwObjects()` quét toàn bộ `960 × 960 = 921,600` ô sector trên bản đồ -> chạm `0x2561E6F8` -> gọi `[0x00863C40 + 0x20]` -> nhảy thẳng vào `"PedIntelligence"` (`0x49646550`)!

### 2.3. Nguyên nhân gốc của Bug B2 (Xe giật cục trên đường, tài xế bị bắn & NPC đi dưới lòng đường)

1. **Xe giật khựng 3.3 lần/giây (`Inland03aTrafficFlow.cs` cũ)**:
   - Tại `Y = 10540` (nằm ngoài giới hạn `[-3000..3000]` của hệ thống node xe gốc GTA SA), script cũ dùng vòng lặp `300ms` gọi cưỡng bức `0175: SET_CAR_HEADING` + `04BA: SET_CAR_FORWARD_SPEED` lên mọi xe đang chạy!
   - Mỗi lần `0175` thực thi, ma trận xoay 3D của thân xe bị reset cứng (xóa sạch độ nhún phuộc pitch/roll và góc đánh lái bánh trước), còn `04BA` ép vận tốc tức thời — tạo hiện tượng xe "giật khựng / kéo thun" liên tục trên mặt đường.
   - Đồng thời script cũ **thiếu kiểm tra `0118: IS_CHAR_DEAD`** trên tài xế (khi người chơi bắn gục tài xế trong xe, tài xế vẫn thỏa `00DB: IS_CHAR_IN_CAR` nên xác chết tiếp tục bị ép phóng xe hoặc xe biến mất đột ngột) và có lỗi gọi đúp `009B: DELETE_CHAR` khi `23@ == d_var@`.
2. **Giải pháp chuẩn trong engine `gta_pe.exe` (`05D1` với `mode = 2`)**:
   - Disassembly hàm xử lý opcode `0x05D1` (`TASK_CAR_DRIVE_TO_COORD`, `0x00490649 -> 0x0063CE00 -> 0x0064553A -> 0x0041CFB0`) chứng minh: khi truyền `driveMode = 2`, GTA SA gán `MISSION_GOTOCOORDS_STRAIGHT` (`9`) và chạy `CCarAI::GetCarToGoToCoorsStraight`. Chế độ này điều khiển chân ga, phanh, bánh lái và hệ thống treo ở **60 FPS vật lý thuần túy**, có tránh chướng ngại vật (`drivingStyle = 2`) và **HOÀN TOÀN KHÔNG tra cứu `CPathFind`** — hoạt động hoàn hảo ở mọi tọa độ `X, Y > 10000`!
3. **Hình học mặt cắt ngang đại lộ & vỉa hè (`Inland03aSakuraLife.cs` & `Inland03aCrowdB.cs`)**:
   - Đại lộ Bắc–Nam (`X = 5822.7, 6105.8, 6319.2, 6510.0, 6728.4`): lòng đường nhựa rộng `±12.0m` (`Z = 14.50m`), vỉa hè lát đá nâng cao nằm ở `±12.0m .. ±15.5m` (`Z = 14.65m`), hàng cây anh đào trồng dọc `±14.2m .. ±14.4m` (thân cây rộng `±0.38m`).
   - Đại lộ Đông–Tây (`Y = 10027.9, 10200, 10480, 10750, 11080`): lòng đường nhựa `±11.0m`, vỉa hè `±11.0m .. ±14.2m`.
   - Trước đây các NPC được đặt ở độ lệch `±8.6m .. ±10.4m` — tức là đi bộ ngay giữa làn xe ô tô (như thấy rõ trong ảnh chụp của người dùng)!

---

## 3. Tổng Hợp Các Bản Vá Đã Triển Khai (`16/11/2026`)

| Hạng mục | File đã cập nhật | Chi tiết kỹ thuật & Kết quả đo kiểm |
| :--- | :--- | :--- |
| **1. Vá gốc Crash `0x49646550` toàn cục ở tầng Engine (`ASI v4`)** | `EagleStreamingFix.asi` (`10,240 B`, CRT-free chỉ import `KERNEL32.dll`) | Bổ sung `SafeCallEntityDeleteRwObject` (`__fastcall`, bảo toàn `EBX/ESI/EDI/EBP`, `RET` chuẩn) và gắn tự động trên main thread (`ClearStreamingChannelErrorState`, sau khi `usedBytes > 32 MiB` để không xung đột patch khởi động của `$fastman92limitAdjuster.asi`) lên **toàn bộ 13 điểm gọi ảo `vtable+0x20` (`DeleteRwObject`) trong `CStreaming`**: `9` điểm 5-byte (`0x0040916D`, `0x0040919D`, `0x004091DD`, `0x00409301`, `0x0040933D`, `0x0040937F`, `0x00409502`, `0x0040955E`, `0x004095B2`) và `4` điểm 7-byte (`0x00407AA4`, `0x004098F5`, `0x00409997`, `0x00409A44`). Khi gặp node ma `*entity == 0x00863C40` (`CPlaceable::vftable`), hàm vô hiệu hóa ngay cờ va chạm/render (`bUsesCollision = 0, bImBeingRendered = 1`) và bỏ qua an toàn; đồng thời bỏ qua cực nhanh các thực thể có `m_pRwObject == NULL` và xác thực địa chỉ vtable/code trước khi gọi. |
| **2. Xe chạy vật lý mượt 60 FPS & xử lý bắn tài xế** | `cleo/Inland03aTrafficFlow.cs` (`11,823 B`) | Xóa bỏ 100% lệnh ép `0175`/`04BA` trong vòng lặp xe sống (`:VALV`), chuyển sang `05D1 ... mode=2 style=2` (`MISSION_GOTOCOORDS_STRAIGHT`) một lần duy nhất lúc spawn (`> 34m` cách người chơi). Bổ sung kiểm tra `8118` (`NOT IS_CHAR_DEAD`): nếu người chơi bắn gục tài xế, gọi `00AD: SET_CAR_CRUISE_SPEED 0.0` để xe tự trôi dừng lại tự nhiên theo quán tính vật lý và chỉ thu hồi khi khuất tầm nhìn (`> 85m` & `82CA`). Khắc phục triệt để lỗi gọi đúp `009B` khi `23@ == d_var@`. |
| **3. Chuyển 100% NPC lên vỉa hè phân làn & giảm 45% RAM skin** | `cleo/Inland03aSakuraLife.cs` (`15,499 B`), `cleo/Inland03aCrowdB.cs` (`11,023 B`) | Đưa toàn bộ người đi bộ ra khỏi mặt nhựa lên đúng vỉa hè lát đá (`Z = 14.68m`), tách làn hai chiều né hoàn toàn hàng cây anh đào (`±14.2..14.4m`): trục Bắc–Nam đi ở **`±12.7m` (hướng Bắc)** và **`±15.3m` (hướng Nam)**; trục Đông–Tây đi ở **`±11.9m` (hướng Đông)** và **`±13.5m` (hướng Tây)**. Tinh gọn danh sách `MISSION_CHAR` từ `44` xuống **`24` skin đặc sắc** (`-45%` RAM/xương nhân vật), nhịp kiểm tra `1000ms` và tự cấp lại lệnh đi bộ `05D3` nếu NPC đứng khựng (`02A0`). |
| **4. Đại tu LOD, Mesh Miku & nén `.txd` (chống tràn Streaming & tụt FPS)** | `CUSTOM/inland03a_sakura_chicago.ide` (`6,910 B`), `CUSTOM/inland03a_sakura_chicago.img` (`150.34 MiB`) | • Thay toàn bộ `39` model `lod_*.dff` (`12320..12386`) từ `26.29 MiB` (`917,481` tris lúc render) xuống **`83.0 KiB` tổng cộng** (`10–20` tris/model, chỉ dùng `in03_urban_txd` ở `ddist = 1050m`, giữ nguyên 100% `.ipl` và `.col`).<br>• Tối ưu `in03_miku_sign.dff`: lọc nan lồng sắt `< 0.015 m²` ở `mat=0`, giữ nguyên **100%** biển neon Miku `Hatsune_Neon` (`5,978` tris, `1024x1024`), giảm từ `77,530 -> 13,026` tris (`3.12 MiB -> 0.72 MiB`).<br>• Nâng cấp mip lossless cho `45` texture DXT quá khổ và nén `25` texture `32-bit BGRA` sang `DXT1/DXT5` (`140.00 MiB -> 96.90 MiB` tổng TXD). |
| **5. Nhận diện tự động chữ ký Crash `0x49646550`** | `eagle_debug_system.py` (`96,577 B`) | Bổ sung phân loại `STREAMING_EVICTION_DANGLING_PLACEABLE_VTABLE` vào `EagleDoctor` / `CrashCorrelator` để tự động nhận diện `0x49646550` / `0x00863C40` trong lịch sử crash. |

### Bảng đối chiếu chỉ số đo thực tế tại `(6325.33, 10541.25)` (Trước vs Sau)

| Chỉ số kỹ thuật tại `(6325.33, 10541.25)` | Trước khi sửa | Sau khi sửa (`16/11/2026`) | Mức cải thiện |
| :--- | ---: | ---: | ---: |
| Tam giác LOD công trình ở xa (`lod_tris`) | `917,481` tris | **`5,730` tris** | **`-99.38%`** |
| Tam giác chi tiết gần (`near_tris`) | `878,743` tris | **`189,747` tris** | **`-78.41%`** |
| **Tổng tam giác cảnh `INLAND-03A` mỗi frame** | **`1,796,224` tris** | **`195,477` tris** | **`-89.12%`** |
| Số lượng `.txd` công trình phải nạp đồng thời | `31` files (`115.20 MiB`) | **`10` files (`22.58 MiB`)** | **`-80.40%` (`-92.62 MiB`)** |
| Dung lượng `.dff` phải nạp đồng thời | `31.63 MiB` | **`4.37 MiB`** | **`-86.18%` (`-27.26 MiB`)** |
| Số lượng skin `MISSION_CHAR` ghim trong RAM | `44` skins | **`24` skins** | **`-45.45%`** |
| Dung lượng gói `inland03a_sakura_chicago.img` | `222.06 MiB` | **`150.34 MiB`** | **`-71.72 MiB`** |

---

## 4. Cẩm Nang Bàn Giao Cho Hội Thoại Đại Tu `M3` (`Bridge 1` & Nam Chicago `PRA\CHICAGO`)

Khi hội thoại sửa `M3` (`BUG-M3-*`: hành lang cầu `Bridge 1 Carcer ↔ Chicago` và khu Nam Chicago `PRA\CHICAGO` tại `Y < 10027.9`) bắt đầu làm việc, cần tuân thủ **5 nguyên tắc kỹ thuật rút ra trực tiếp từ thực chiến Bắc Chicago**:

1. **Ranh giới khớp nối Bắc–Nam Chicago (`Y = 10027.9`)**:
   - Tuyệt đối giữ nguyên cao độ và vị trí 5 dốc nối `in03_south_ramps` (`ID 12288`) của Bắc Chicago tại `Y = 10027.9` trên 5 trục `X = 5822.7, 6105.8, 6319.2, 6510.0, 6728.4`. Khi nâng cấp hoặc thay mặt đường `wb_road*` bên phía `PRA\CHICAGO` (`Y < 10027.9`), hãy khớp mép Bắc của `PRA\CHICAGO` đúng vào cao độ chân dốc tại `Y = 10027.9` để xe chạy xuyên suốt từ `Bridge 1` (`Y ≈ 9720`) lên thẳng Sàn Chứng Khoán Bắc Chicago (`6339.00, 10523.60, 14.45`) không có gờ vấp.
2. **Quy tắc vàng về LOD công trình mới (`ddist > 300m`)**:
   - **CẤM TUYỆT ĐỐI** tái sử dụng file `.dff` gốc hoặc `.txd` gốc của công trình Near làm model LOD `1000–1500m`. Mọi model `lod_*` mới ở `M3` bắt buộc phải là vỏ hộp/khối giản lược (`<= 40` tam giác) và dùng chung **một `.txd` đô thị nhẹ duy nhất (`<= 1.5 MiB`)** để không bao giờ kéo hàng chục `.txd` nặng vào `CStreaming`.
3. **Quy tắc vàng về nén `.txd`**:
   - Mọi texture đóng gói vào `.txd` mới phải nén `DXT1` (không alpha) hoặc `DXT5` (có alpha) bằng `texconv.exe`, kích thước tối đa `512x512` (chỉ giữ `1024x1024` cho biển hiệu chữ lớn đặc biệt). Không bao giờ để lọt định dạng `32-bit BGRA` (`d3dfmt = 0x15`) vào `.img`.
4. **Quy tắc điều khiển giao thông ngoài vùng `[-3000..3000]`**:
   - Tại Chicago (`X ≈ 5800..8000, Y ≈ 9000..11200`), nếu dùng CLEO tạo luồng xe động trên cầu `Bridge 1` hoặc đại lộ Nam Chicago, **dùng `05D1: TASK_CAR_DRIVE_TO_COORD ... mode=2 style=2`** (`MISSION_GOTOCOORDS_STRAIGHT`), tuyệt đối không dùng vòng lặp cưỡng bức `0175` + `04BA`, và luôn kiểm tra `8118` (`NOT IS_CHAR_DEAD`) cho tài xế.
5. **Bảo vệ Streaming & `.COL` Sector**:
   - `EagleStreamingFix.asi` v4 hiện đã bảo vệ toàn bộ 13 điểm gọi `DeleteRwObject` trong `CStreaming` trên toàn bản đồ (bao gồm cả binary IPL của vanilla SA, S&S và custom map). Khi sửa `.col` hoặc `.ipl` của `PRA\CHICAGO`, luôn đảm bảo bounding box/sphere của `.COL3` bao trùm khít 100% hình học `.DFF` và không vượt quá giới hạn `±245m` quanh tâm local.
