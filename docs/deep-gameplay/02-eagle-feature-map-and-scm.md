# 02. Bản đồ Tính năng Có sẵn của Project Eagle v1.3 & Giải phẫu `main.scm` / `script.img`

- **Mục tiêu:** Xác định chính xác những hệ thống gameplay, thế giới, kinh tế, nghề nghiệp, UI và lưu trữ **đã được tích hợp sẵn trong Project Eagle v1.3** để tái sử dụng hoặc nối khớp, tránh viết trùng lặp hay làm hỏng biến toàn cục của Eagle.
- **Nguồn bằng chứng:** Phân tích bytecode [`data\script\main.scm`](file:///C:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20clean/gta%20sa%20clean/data/script/main.scm) (`4,849,743` bytes), 89 script trong [`data\script\script.img`](file:///C:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20clean/gta%20sa%20clean/data/script/script.img), bảng chuỗi [`text\american.gxt`](file:///C:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20clean/gta%20sa%20clean/text/american.gxt) (144 bảng, 18.401 chuỗi), [`cleo\cleo_text\*.fxt.off`](file:///C:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20clean/gta%20sa%20clean/cleo/cleo_text/SCM_TEXT.fxt.off), và [`data\Changelog.txt`](file:///C:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20clean/gta%20sa%20clean/data/Changelog.txt).

---

## 1. Cấu trúc Độc đáo của `data\script\main.scm` trong Project Eagle v1.3

Theo [`data\Changelog.txt:156`](file:///C:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20clean/gta%20sa%20clean/data/Changelog.txt#L156) (*"Moved all CLEO scripts to main.scm"*), nhóm phát triển Project Eagle v1.3 đã biên dịch toàn bộ các hệ thống gameplay tùy biến của Stars & Stripes (S&S) trực tiếp vào `main.scm` thay vì để rời dưới dạng file `.cs` trong thư mục `cleo\`:

1. **Vùng Biến Toàn cục Mở rộng (`Global Variable Space`):**
   - `main.scm` cấp phát **`63,960` bytes** (`0x000008..0x00F9E0`) tương ứng với **`15,990` biến toàn cục 32-bit** (gấp ~3,9 lần giới hạn ~4.096 biến của GTA SA gốc).
   - Để lưu được khối biến này vào file save `.b`, [`fastman92limitAdjuster_GTASA.ini:514`](file:///C:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20clean/gta%20sa%20clean/fastman92limitAdjuster_GTASA.ini#L514) đã đặt `Saveblock size = 66000`.
2. **Bảng Symbol Sanny Builder đính kèm ở cuối file (`0x482EF6..0x4A004F`):**
   - Phát hiện quan trọng: Ở cuối `main.scm` có nguyên vẹn bảng symbol của trình biên dịch Sanny Builder gồm **`5,598` tên biến toàn cục** ánh xạ trực tiếp sang index biến!
   - Ví dụ:
     - `$SKIPTOGAMEMODE` = index `13183` (`0x337F`, byte offset `0xCDFC`)
     - `$ETS_MAIN_CONTRACT1..4` = index `14460..14463` (`0x387C..0x387F`)
     - `$ETS_MAN_SLOT1..3` = index `13748, 13758, 13759`
     - `$PEPROPERTY1..6_BOUGHT` = index `15061..15066` (`0x3AD5..0x3ADA`)
     - `$FOODSHOP_RST1..4_COST` = index `15636..15639` (`0x3D14..0x3D17`)
     - `$X_ATM_CASH` = index `12403` (`0x3073`, byte offset `0xC1CC`)
3. **Tổng số luồng và nhiệm vụ:**
   - **255 luồng `03A4` (`script_name`)** được khai báo trong `main.scm`.
   - **89 streamed scripts (`.scm`)** trong `data\script\script.img`.
   - **147 mission offsets** trong header `main.scm`.

> [!WARNING]
> Vì `main.scm` đã sử dụng tới biến toàn cục số `15,989` (sát trần `Saveblock size = 66000` bytes $\approx$ `16,500` biến), **mọi hệ thống mod mới tuyệt đối KHÔNG được dùng biến toàn cục SCM (`$var`) chưa kiểm soát**, mà phải dùng biến cục bộ của luồng (`0@...31@`), bộ nhớ cấp phát động trong C++ ASI, hoặc lưu vào sidecar file riêng!

---

## 2. Bản đồ Tính năng Có sẵn trong Project Eagle v1.3 (Đối chiếu 4 Trụ cột Gameplay)

| Tính năng / Hệ thống | Thành phần thực thi | Offset / File chứng cứ | Cơ chế hoạt động thực tế (Đã xác minh qua Bytecode & GXT) | Khác biệt so với GTA SA gốc & Ý nghĩa với dự án |
| --- | --- | --- | --- | --- |
| **Chọn Chế độ Chơi (`STARTGM`)** | `main.scm` + `pe_database.ini` | `main.scm` `0x02DE31..0x032A79`; [`cleo\starsandstripes\pe_database.ini`](file:///C:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20clean/gta%20sa%20clean/cleo/starsandstripes/pe_database.ini) | Dùng opcode `0AF0` đọc `SkipToGamemode` từ `pe_database.ini` vào `$SKIPTOGAMEMODE` (`13183`): `0` = Intro Storyline (Sweet & David tại Rose City), `1` = Freeroam (mặc định), `2` = Discovery, `3` = America Truck Simulator. | Cho phép nhảy thẳng vào Freeroam toàn bản đồ Mỹ mà không bị khóa cầu/thành phố. |
| **Interaction Menu (`MENU_INTERACT`)** | `main.scm` | `main.scm` `0x05F6F6..0x060C67`; GXT `INTE001..040` | Mở bằng phím **`M`** khi đứng yên. Sử dụng native menu GTA SA (`08D4` `CREATE_MENU`, `08DB` `SET_MENU_COLUMN`). Gồm 3 nhánh: (1) *Clothing & Accessories* (Hats, Glasses, Chains, Watch + cử chỉ), (2) *Progression* (% hoàn thành, danh sách Vehicle/Asset/Oddjob/Contract/Collectibles), (3) *Map & Blips* (bật/tắt icon Race, Asset, Oddjob, Dealership). | **Cảnh báo xung đột phím:** Phím `M` khi đứng yên đã bị `MENU_INTERACT` chiếm dụng. Không dùng phím `M` đơn lẻ cho mod mới. |
| **Sự nghiệp Lái xe tải & Quản lý Công ty (`ETS`)** | `main.scm` | `main.scm` `0x03CDC8..0x040498` (`ETS`, `ETS_DRAWTEXT`, `ETS_MISSION`, `ETS_REPAIRSHOP`); GXT bảng `ETS` (`ETS001..074`) | Hệ thống mô phỏng kiểu *Euro Truck Simulator 2*: Văn phòng công ty (`Your Office`), Gara 3 slot xe tải (`Vehicle Slot 1..3`), Mua/Bán xe (hoàn 50%), Thuê/Sa thải tối đa 3 tài xế NPC (`Employee Slot 1..3` với chỉ số `% Accident chance` và `-minutes Delivery speed`), 4 hợp đồng vận chuyển (`Contract 1..4`) có thời hạn ngày (`Contract Expires in ~1~ days`), và tính năng **`Sleep (Pass Day)`** (`ETS048` / `ETS047`: *"You slept, a day has passed"*) kèm menu save (`03D8`). | **Nền tảng vàng cho Life Sim & Kinh tế:** Eagle đã có sẵn khái niệm ngủ qua ngày, thuê nhân viên chạy việc theo ngày và hợp đồng có hạn. |
| **Tài sản tạo doanh thu (`X_ASSETS`) & Bất động sản (`PEBPROPERTY`)** | `main.scm` | `main.scm` `0x038E4E..0x03C712` (`X_ASSETS`), `0x061017..0x061B0A` (`PEBPROPERTY`) | Quản lý hàng chục cơ sở kinh doanh khắp LS, SF, LV, LC, VC, Cottonmouth, Rose City (`X_ASSETS_LS_SPRUNK`, `X_ASSETS_VC_PRINTWORKS`, `X_ASSETS_LC_NIGHTCLUB`, `X_ASSETS_VINYARD`...) và các pickup thu tiền định kỳ (`X_ASSET_*_PICKUP`), cùng 6 bất động sản (`$PEPROPERTY1..6_BOUGHT`). | Có sẵn hệ thống sở hữu tài sản và thu tiền thụ động tại pickup. |
| **Safehouse & Khách sạn gửi xe (`XSAVE`, `X_HOTEL`)** | `main.scm` | `main.scm` `0x054ADD..0x055946` (`XSAVE`), `0x03C712..0x03CBB2` (`X_HOTEL`), `PSAVEANC`, `PSAVEIBY`, `PSAVECCH` | Mở rộng hệ thống safehouse tại các bang mới và khách sạn *Majestic Hotel Royal Park* tại Cottonmouth (`CMHOT1..5`) cho phép mua phòng (`HSUITE`) và đỗ/giữ xe. | Có thể kết nối với hệ thống nhà ở/ngủ nghỉ của Life Sim. |
| **Cửa hàng Đồ ăn Mở rộng (`pefoods.scm` & `junkfud.scm`)** | `script.img` + `data\shopping.dat` | `script.img` `pefoods.scm` (`0x06B800`, 14.336 B); `main.scm` `$FOODSHOP_RST1..4_COST`; GXT `BSPEFD1..4`, `FZPEFD1..4` | Bổ sung các tiệm ăn mới (như *World of Coq*, *Well-Stacked Pizza*, *Burger Shot*, *Cluckin' Bell* mở rộng) với menu chọn món (`FOOD_H`), animation ăn (`EAT_PIZZA`, `EAT_BURGER`), trừ tiền và hồi máu/tăng calories (giới hạn nôn mửa `$VOMITPE_CHECKER`). | Đã có chuỗi cửa hàng ăn nhanh hoạt động; có thể hook hoặc đọc trạng thái ăn uống để nạp vào thanh Hunger/Thirst của Life Sim. |
| **Hệ thống Bay Thương mại Liên bang (`usaplane.scm`)** | `script.img` + `S&S\AirportBlips.ipl` | `script.img` `usaplane.scm` (`0x087800`, 102.400 B); `PECore.asi` (`IplExt` `arpt`) | Máy bán vé máy bay (`TICKET MACHINE`) tại các sân bay trên toàn quốc: chọn điểm đi (`DEPARTURE`), điểm đến (`DESTINATION`), giá vé (`PRICE`), mua vé và bay/xem cảnh bay hoặc skip. | Phương thức di chuyển đường dài hợp thức hóa việc đi du lịch/công tác giữa các thành phố. |
| **Hệ thống Phà Liên bang & Nghề phụ (`LC_side_mission`, `VC_side_mission`...)** | `main.scm` | `main.scm` `LIMO_DRIVER` (`0x064BC0`), `TRASHMASTER` (`0x0657D6`), `CHERRY_POPPER` (`0x063CE4`), `TERRAIN4X4`, `VOLTTRUCK`, `DOHERTY_GARAGE` | Hệ thống phà chở khách ($\$800$/chuyến), lái xe Limousine (lưu cấp độ vào `Stat 413`), xe chở rác *Trash Dash*, bán kem, trường bắn 5 cấp độ (mở khóa hồi máu tự động 50% `HPREG01`), cướp tiệm Vice City (`VC_ROBBING`), giao Pizza/Noodle (`VC_PIZZA`, `LCS_PIZZA`, `LCS_NOODLE`). | Nguồn thu nhập đa dạng cho tầng công việc (Jobs) trong game. |
| **Đại lý Bán xe (`CAR_DEALERSHIP`) & Xuất nhập khẩu (`X_IMPEX`)** | `main.scm` | `main.scm` `CAR_DEALERSHIP` (`0x061B0A..0x063CE4`), `X_IMPEX` (`0x052940..0x054ADD`); `pe_model_ids.ini` | Đại lý trưng bày và bán xe theo phân khúc (SUV, Sedan, Sport, Muscle, Lowrider), cho phép lái thử (`Test Drive`), chọn màu, lắp Hydraulics, chọn Variant 1-6; bảng danh sách 32 xe Import/Export (`$X_IMPEX_WANTED01..32`). | Tích hợp trực tiếp với trụ cột Kinh tế & Tài sản cá nhân. |
| **Máy rút tiền ATM (`X_ATM`) — *Phát hiện đính chính quan trọng*** | `main.scm` | `main.scm` `0x055946..0x05E05E` (`34,584` B) | **KHÔNG PHẢI hệ thống tài khoản ngân hàng!** Giải mã bytecode tại `0x05DFC0..0x05E05E` chứng minh `X_ATM` chỉ tạo các object cây ATM (`model 2942` `kmb_atm1`) và NPC đứng rút tiền (`$X_ATM_RANDOM_PED`). Khi người chơi đập/bắn vỡ ATM (`$X_ATM_health < 1`), model đổi sang ATM hỏng (`3067`), NPC bỏ chạy (`05DC`), và rơi ra cọc tiền pickup (`02E1`) ngẫu nhiên từ **$\$300$ đến $\$500$** (`0209`). | **Khoảng trống xác nhận:** Project Eagle **chưa có** tài khoản ngân hàng, gửi/rút tiền, lãi suất hay menu giao dịch tại cây ATM. Ta có thể tận dụng chính tọa độ/model `2942` của các cây ATM này để mở UI Ngân hàng khi bấm phím tương tác! |
| **Máy nhắn tin Pager (`X_PAGER` & Opcode `0x3200`)** | `PECore.asi` + `main.scm` | `main.scm` `0x04F916..0x052940`; `PECore.asi` `Pager` module | `main.scm` gọi `054C` (`use_gxt_table 'XPAGER'`) rồi gọi custom opcode `0x3200` (`pager_add_message 'PAGE001' 140 3 0`) để đẩy thông báo chữ chạy lên máy nhắn tin góc trái màn hình. | **Điểm nối UI tuyệt vời:** Có thể dùng Pager hoặc thông báo kiểu smartphone/pager để báo tin tức thị trường, kết quả vé số/cá cược, hoặc tin nhắn từ NPC AI! |
| **Bảng chữ điện tử LED (`Scrollbars`)** | `PECore.asi` + `data\scrollbars.dat` | [`data\scrollbars.dat`](file:///C:/Users/LENOVO/Desktop/GTA/Project%20Eagle/gta%20sa%20clean/gta%20sa%20clean/data/scrollbars.dat) | Hiển thị chữ chạy điện tử trên các tòa nhà (Type 0=Financial, 1=Traffic, 2=Cinema, 3=Airport...) với tag động `<TIME>`, `<TEMP>`, `<WEATHER>`, `<TUNNEL>`, `<BRIDGE>`. | Có thể nghiên cứu hook chuỗi hiển thị của Scrollbars (Type 0 Financial) để chạy bảng giá cổ phiếu/crypto hoặc tỷ số thể thao ngay trên tòa nhà trong phố! |
| **Cá cược Đua ngựa (`OTB` / Inside Track)** | `main.scm` + `script.img` | `main.scm` `OTB` (`0x3CB284`); `script.img` `otb_msc.scm` (`0x059800`), `otb_stf.scm` (`0x05D800`) | Máy cá cược đua ngựa *Inside Track Betting* gốc của GTA SA vẫn được giữ nguyên trong `main.scm` và `script.img`. | Chưa có vé số kiến thiết/Vietlott hay cá cược bóng đá/bóng rổ; cần xây mới hoàn toàn. |

---

## 3. Tổng hợp Những Gì CHƯA CÓ trong Project Eagle v1.3 (Khoảng trống cho 4 Trụ cột)

Dựa trên kiểm tra toàn diện `PECore.asi`, `main.scm`, `script.img`, và `data\`, những tính năng sau **hoàn toàn chưa tồn tại** trong bản Eagle hiện tại và sẽ là phạm vi xây dựng mới của kiến trúc mod:

1. **Life Sim:**
   - Chưa có thanh nhu cầu cơ thể liên tục (**Đói / Khát / Buồn ngủ / Vệ sinh / Năng lượng** — vanilla SA chỉ có `Fat`, `Stamina`, `Muscle` và cảnh báo đói sau 48 giờ in-game).
   - Chưa có hệ thống **Nhiên liệu phương tiện (Fuel) & Trạm xăng (Gas Stations)** tương tác đổ xăng.
   - Chưa có hệ thống **Đi siêu thị mua nhu yếu phẩm mang về / Túi đồ (Inventory)** (cửa hàng ăn hiện tại là mua và ăn ngay tại quầy).
   - Chưa có **Lịch sinh hoạt hằng ngày tại nhà riêng** (ngủ theo giờ mong muốn ngoài chế độ ETS, tắm rửa, thay đồ tại tủ, ăn đồ dự trữ trong tủ lạnh).
2. **Kinh tế, Ngân hàng & Đầu tư:**
   - Chưa có **Tài khoản ngân hàng (Checking / Savings)**, giao dịch gửi/rút/chuyển khoản tại cây ATM (`kmb_atm1`), thẻ ngân hàng, hay tách biệt tiền mặt (`Cash`) với số dư tài khoản (`Bank Balance`).
   - Chưa có **Thị trường Chứng khoán (Stocks) & Crypto**, biểu đồ giá, danh mục đầu tư (Portfolio), cổ tức hay sự kiện kinh tế vĩ mô/vi mô tác động lên giá.
3. **Vé số & Cá cược Thể thao (Lottery & Sports Betting):**
   - Chưa có **Vé số (Lottery)** mua theo kỳ quay giờ cố định, dò số, lưu lịch sử vé và lĩnh thưởng.
   - Chưa có **Nhà cái Thể thao (Sportsbook)** cho bóng đá, bóng rổ với kèo chấp/tài xỉu/1X2, lịch thi đấu và thanh toán tự động.
4. **AI NPC & Kết nối Internet / Dữ liệu Thời gian thực:**
   - Chưa có cơ chế **Trò chuyện tự do với NPC**, bộ nhớ tương tác cá nhân (Memory), tính cách (Persona) hay nhiệm vụ động do AI sinh ra.
   - Chưa có cầu nối (IPC / Sidecar) lấy dữ liệu thời tiết, tin tức, giá tài sản hay lịch/kết quả thể thao từ internet đưa vào thế giới game.
