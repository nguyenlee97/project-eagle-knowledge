# EaglePhone OS v6.2 — Đại tu toàn diện UI Smartphone, Typography Cỡ Lớn & Touchscreen Mouse QoL (05/11/2026)

- **Agent / Hội thoại:** Antigravity (`5bf38060-a2b9-481e-8236-b178c1e291ef`)
- **Phiếu công việc:** [`work-items/2026-11-04-antigravity-eaglephone-ui-overhaul-and-touch-qol.md`](work-items/2026-11-04-antigravity-eaglephone-ui-overhaul-and-touch-qol.md)
- **Đích tích hợp duy nhất:** `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`
- **Thư mục Staging & Backup:** `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\eaglephone-ui-v6-20261104\`
- **Trạng thái nghiệm thu kỹ thuật:** **PASS 100% (`v6.2`)** (DirectX 9 `1920×1080` in-game, `15/15` ảnh chụp kiểm tra bằng mắt thật trong `qa_screenshots_v6_2/`, nâng cỡ chữ lớn chuẩn desktop `scaleX 0.195..0.365 / scaleY 0.415..0.776` lấp đầy `80–88%` chiều ngang card/bong bóng/trang báo, khử sạch lỗi ký tự `•`/`@` của `CFont`, chuột cảm ứng `LMB` / `RMB Back` / `Mouse Wheel` thực thi trực tiếp qua `0x00CAFE60`, `0` lỗi Lua trong `cleo/EagleLuaErrors.log`, giữ nguyên 100% gói Presentation 03/11 và các feature song song `WaifuLink v4` + `Mondstadt Persona Chat / Contacts App 14`).

---

## 1. Nguyên nhân gốc khiến HUD EaglePhone cũ kém hấp dẫn & Giải pháp kiến trúc v6.0

1. **Mọi dòng chữ đều bị căn giữa cứng (`Font.SetJustify(2)`):**
   - Trong CLEO Redux Lua của GTA SA, `Font.SetOrientation(1)` (căn trái) lấy giới hạn lề phải từ biến toàn cục `CFont::m_fWrapx` tại `0x00C71A88` (mặc định engine để `0.0` khiến chữ bị ngắt dòng từng chữ cái nếu gọi trực tiếp).
   - **Giải pháp (`hud.lua`):** Xây dựng bộ hàm typography mới `DrawTextL` (ghi `Memory.WriteFloat(0x00C71A88, x + wrapW)` trước `Font.PrintString`), `DrawTextR` (`Font.SetOrientation(2)` + `0x00C71A8C`), và `DrawTextC`, mở khóa hoàn toàn bố cục căn trái/phải chuẩn điện thoại hiện đại.
2. **Banner / thẻ ATM bị bake chữ sẵn gây đè chữ (`ep_bn_*`, `ep_cd_atm`):**
   - Các ảnh thẻ ATM và banner cũ vẽ sẵn chữ mẫu làm chữ động từ Lua đè lên nhau; một số icon tròn nhân vật (`ep_ms_hutao`, `ep_ms_kirara`) bị lệch crop mặt lên trên.
   - **Giải pháp (`build_eaglephone_txd.py` + `ui_assets/`):** Dựng lại bộ **50 texture `ep_*`** sạch chữ 100% (`288` tổng số texture trong `models/hud.txd`), căn tâm khuôn mặt cho avatar tròn, thêm thẻ kim loại Titanium có chip EMV vàng `ep_cd_atm`, mặt nạ tròn `ep_ui_circle`, bóng 3D có highlight `ep_ui_ball`, và con trỏ chuột trắng viền đen `ep_ui_cursor`.
3. **HUD tiền/đồng hồ gốc GTA SA (`$50000`, `11:06`) vẽ đè lên thanh trạng thái điện thoại:**
   - **Giải pháp (`hud.lua`):** Khi `EaglePhoneState.open == "1"`, ẩn gọn cụm HUD góc trên bên phải của GTA SA (vẫn cập nhật `EagleLiveClock` và `EagleLiveMoney` trước khi `return`, và giữ nguyên minimap/radar góc dưới bên trái).
4. **Ngôn ngữ hiển thị mặc định:** Đặt mặc định Tiếng Anh (`self.lang = "en"`) theo yêu cầu người dùng để không bị gãy dấu tiếng Việt trong `CFont` GTA SA (vẫn giữ nút chuyển ngôn ngữ trong Settings).

---

## 2. Cơ chế Điện thoại Cảm ứng Chuột 144Hz (`Touchscreen Mouse & Scroll QoL`)

Hoạt động song song 100% với bộ phím truyền thống (`I/K/J/L`, `F9`, `F10`, `F6`, `Backspace/F8`) và bật/tắt tức thì bằng **`F5`**, **chuột giữa (`MMB`)** hoặc click trực tiếp vào pill **`TOUCH / KEYS`** trên thanh trạng thái điện thoại:

| Thành phần | Địa chỉ / Giao thức | Chức năng thực tế |
|---|---|---|
| **Tách camera GTA SA khi mở điện thoại** | `0x0053F509` (`CPad::UpdateMouse`) | `EagleCompanion.py` tự động vá `F3 A5 -> 90 90` (`2` byte NOP chặn copy `TempMouseControllerState -> NewMouseControllerState`) chỉ khi `phone_open == 1` và `touch_mode == True`; khôi phục `F3 A5` ngay lập tức khi đóng điện thoại (`F7`) hoặc tắt Touch (`F5`) để xoay camera & bắn súng bình thường. |
| **Đọc delta chuột & lăn chuột 144Hz** | `0x00B73404` (`CTempMouseControllerState`) | `hud.lua` đọc trực tiếp `lmb (+0)`, `rmb (+1)`, `mmb (+2)`, `wheelUp (+3)`, `wheelDn (+4)`, `dx (+12 float)`, `dy (+16 float)` từ DirectInput ở tốc độ khung hình game, di chuyển con trỏ `ep_ui_cursor` mượt 144Hz và tô sáng nút đang hover (`EagleTouchBox`). |
| **Hộp thư Touch Outbox Lua -> Python** | `0x00CAFE60 .. 0x00CAFE77` (`24` bytes, `<iiiiii`) | Gồm `(click_seq, act_code, act_arg, wheel_seq, wheel_delta, rmb_seq)`. Đã quét nhị phân toàn bộ `.cs`/`.asi` xác nhận không đụng `0x00CAFE00..1F` (`EagleCompanion`), `0x00CAFE20` (`RIDE`), `0x00CAFE30` (`WAIF`), và `0x00CAFE40` (`MCHT`). |
| **Thao tác chuột hỗ trợ** | `LMB` / `RMB` / `Wheel` / `MMB` | **Chuột trái (`LMB`):** mở app, đổi tab, chọn mã CK/Crypto, chọn kèo cược, mua vé số/cào vé, bấm chip trả lời nhanh hoặc mở ô gõ tin nhắn. **Chuột phải (`RMB`):** Back / quay lại màn trước. **Con lăn (`Wheel`):** cuộn bài báo `The Eagle Times`, cuộn danh sách thị trường, danh bạ và giải đấu. |

---

## 3. Chi tiết Đại tu Giao diện Từng Ứng dụng (`Apps 0..14`)

- **App 0 (`Springboard Home Screen`):** Khung `286×404` dễ đọc, Dynamic Island + thanh trạng thái trên cùng (`Giờ + 5G`, pill `TOUCH/KEYS` bấm được, `% HP`), thẻ kính mờ Status góc trên kèm avatar tròn nhân vật yêu thích (`ep_ms_*`), lưới **14 ứng dụng (`1..14`)** chia icon bo tròn sắc nét và thẻ mini `SOCIAL LINK` ở ô thứ 15.
- **App 1 (`Eagle NeoBank`):** Thanh thể lực `HP / Armor / Food / Energy`, thẻ kim loại tối màu **`EAGLE TITANIUM DEBIT`** (`ep_cd_atm`) có chip EMV vàng tách biệt hoàn toàn khỏi số dư `$5,500`, nút tăng/giảm tiền `[-]` `[+]` `[Keypad]`, lưới `2×2` ATM & Tiết kiệm lãi kép `+1.5%/ngày`, và thẻ `Credit Line` `$50K`.
- **Apps 2 & 3 (`Wall St Terminal` & `EagleCrypto Pro`):**
  - *Subpage 0 (`Watchlist`):* 8 dòng tài sản chuẩn Robinhood/TradingView — mã căn trái, tên công ty bên dưới, đường **mini-sparkline xanh/đỏ** ở giữa, giá căn phải và pill `%` xanh ngọc/đỏ thẫm.
  - *Subpage 1 (`OHLCV Chart`):* Biểu đồ **24 cây nến Nhật OHLC thực thụ** (râu nến High-Low + thân nến Open-Close xanh/đỏ + đường trung bình **MA7 vàng** & **MA20 xanh lam** + **24 cột Volume** bên dưới + nhãn giá trục phải), kèm 6 pill chế độ lệnh (`Buy Spot`, `Sell Spot`, `Long 5x`, `Short 5x`, `Long 20x`, `Short 20x`) và nút khớp lệnh nổi bật.
- **App 4 (`EagleBet Sportsbook`):** 5 tab giải đấu (`EPL`, `LALIGA`, `SERIE A`, `UCL`, `NBA`), 5 thẻ trận đấu có cụm 3 pill tỷ lệ cược `1 | X | 2` bấm trực tiếp để mở phiếu cược, và màn `Match Center` có 5 ô kèo (`1`, `X`, `2`, `Over`, `Under`) + bảng xếp hạng Top 4 + khay `Sticky Bet Slip` tính sẵn tiền thắng dự kiến.
- **App 5 (`EagleLotto Casino`):**
  - *Scratch:* Thẻ cào kim loại 3×3 (`Silver $20`, `Gold $100`, `Diamond $500`, `Royal $2K`) hiển thị đủ 9 ô biểu tượng ASCII sắc nét (`GEM`, `STAR`, `CROWN`, `$20`...) và sửa dứt điểm lỗi sinh nhầm 3 biểu tượng trùng nhau khi vé thua `$0`.
  - *6D / 2D:* 6 quả cầu vàng giải Đặc biệt + **bảng đủ 18 lô 2 số (`3×6`)** + 6 quả cầu xanh số người chơi chọn.
  - *Jackpot:* Bóng cầu 3D (`ep_ui_ball`) xanh dương cho `Mega 6/45`, 6 cầu đỏ + 1 cầu vàng đặc biệt cho `Power 6/55`, và 6 cầu xanh lục cho vé người chơi.
  - *Keno 0s:* Ma trận **20 quả bóng 3D (`2×10`)** phân màu Nhỏ (`01..40` xanh) / Lớn (`41..80` cam vàng), tổng điểm Tài/Xỉu, Chẵn/Lẻ, Ngũ Hành và Max3D quay tức thì `0s`.
- **App 6 (`The Eagle Times` Web Newspaper):** Nền giấy báo ấm `#F6F3EB` tương phản chữ mực đen tuyền căn trái sắc nét, Masthead tòa soạn, dải băng giá thị trường nền tối (`XAU`, `NVDA`, `BTC`), 6 tab chuyên mục bấm được (`WORLD`, `CULT`, `ACG`, `MARKET`, `CRYPTO`, `SPORT`), ảnh bìa sạch chữ, tiêu đề lớn 2 dòng + byline + nội dung chia đoạn cuộn bằng `Mouse Wheel` + tin liên quan màu xanh.
- **App 13 (`WaifuLink` Messenger) & App 14 (`Contacts` Social Link Directory + Remote DM):** Header kiểu Messenger/iMessage với avatar tròn + chấm xanh `● Online` + nút `< >` đổi nhân vật, bong bóng tin nhắn đến căn trái (kèm avatar tròn) và bong bóng tin nhắn đi màu xanh căn phải, 3 chip gợi ý trả lời nhanh bấm chuột trực tiếp, thanh soạn tin nhắn bo tròn (`Click / F6` gõ phím trực tiếp với AI), và danh bạ hợp nhất 16 nhân vật Mondstadt + Waifu có ghim GPS & nhắn tin từ xa (đồng bộ đầy đủ phông chữ lớn của nhánh `c71a77f9`).
- **Apps 7..12 (`Portfolio`, `BugRadar`, `Settings`, `GG Map`, `Paimon`, `EagleRide`):** Đồng bộ toàn bộ sang hệ header/card/button bo tròn v6.0 và hỗ trợ bấm chuột trực tiếp.

---

## 4. Manifest File Đã Đổi & SHA-256 Trước / Sau

Chi tiết đầy đủ lưu tại [`staging/project-eagle/eaglephone-ui-v6-20261104/manifest_after_v6.json`](../../staging/project-eagle/eaglephone-ui-v6-20261104/manifest_after_v6.json) (kèm `56` ảnh nguồn PNG trong `Project Eagle\gta sa gameplay-lab\ui_assets\`):

| File trong `gta sa gameplay-lab` | Size trước | SHA-256 trước (16 ký tự đầu) | Size sau (`v6.2`) | SHA-256 sau (`v6.2`) |
|---|---:|---|---:|---|
| `EagleCompanion.py` | 368,280 B | `bd58f3f46f8a85d3` | 411,007 B | `fbf9faa277e38ae6` |
| `hud.lua` | 157,902 B | `03e83dd4e1e723a5` | 197,046 B | `0f2118ae89502560` |
| `build_eaglephone_txd.py` | 23,990 B | `969fcf972684ea4a` | 31,759 B | `c6174b2644758ea0` |
| `models\hud.txd` | 5,282,640 B | `79babd373cce40a6` | 5,348,688 B | `f2f6474e10d6915c` |
| `models\txd\EAGLEUI.TXD` | 3,708,712 B | `6063e1114bfdd73a` | 3,774,760 B | `8622d3329a2b8b93` |
| `CUSTOM\EAGLEPHONE_UI.TXD` | 3,708,712 B | `6063e1114bfdd73a` | 3,774,760 B | `8622d3329a2b8b93` |

### Lệnh Deploy lại hoặc Rollback có Guard (giữ khóa `game-write`)

```powershell
# Kiểm tra và phục hồi về baseline trước v6 (có kiểm tra SHA-256 chống ghi đè thay đổi mới hơn):
python -X utf8 "C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\eaglephone-ui-v6-20261104\rollback_eaglephone_ui_v6.py"

# Hoặc deploy lại bản v6.0 từ staging:
python -X utf8 "C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\eaglephone-ui-v6-20261104\deploy_eaglephone_ui_v6.py"
```

---

## 5. Kết quả Kiểm thử Thực tế DirectX 9 (`1920×1080`) & Bộ Ảnh Bằng chứng

Đã chạy [`run_live_v6_qa.py`](../../staging/project-eagle/eaglephone-ui-v6-20261104/run_live_v6_qa.py) dưới khóa `ingame-runtime` (lưu kết quả máy đọc tại [`live_v6_2_qa_results.json`](../../staging/project-eagle/eaglephone-ui-v6-20261104/live_v6_2_qa_results.json)):
- **Kiểm tra bộ nhớ & Touch trực tiếp trong `gta_pe.exe`:**
  - Điện thoại đóng (`open=0`): `0x0053F509 == f3 a5` (chuột xoay camera GTA SA bình thường).
  - Điện thoại mở (`open=1, touch_active=1`): `0x0053F509 == 90 90` (tách camera sạch sẽ).
  - Bấm chuột trái Windows (`mouse_event` -> DirectInput -> `hud.lua` -> `0x00CAFE60`): `click_seq = 1, code = 1, arg = 8` (mở đúng icon đang hover).
  - Bấm chuột phải Windows (`RMB`): `rmb_seq = 1` (quay về màn trước).
  - Lăn con lăn chuột (`Mouse Wheel`) trên báo `The Eagle Times`: `wheel_seq = 1` (cuộn trang báo).
  - Đóng điện thoại (`F7`): `0x0053F509` khôi phục ngay về `f3 a5`.
  - `cleo/EagleLuaErrors.log`: **`0` lỗi**.
- **Bộ 15 ảnh DirectX 9 `1920×1080` bản `v6.2` đã kiểm tra trực quan (`staging/project-eagle/eaglephone-ui-v6-20261104/qa_screenshots_v6_2/`):**
  1. `01_home_springboard_touch.png` — Màn hình chính 14 icon cỡ chữ lớn (`0.210/0.446`) + thẻ Social Link + pill `TOUCH` + con trỏ chuột (không bị tiền `$50000` GTA đè).
  2. `02_neobank_atm_card.png` — Thẻ Titanium EMV NeoBank sạch chữ, số dư `$5,500` chữ siêu lớn (`0.365/0.776`) nằm gọn bên phải chip vàng, các nút ATM căn tâm dọc.
  3. `03_stocks_watchlist_sparklines.png` — Bảng giá Wall St 8 dòng cỡ chữ lớn kèm mini-sparklines xanh/đỏ và pill `%`.
  4. `04_stocks_ohlc_candlestick.png` — Biểu đồ 24 nến Nhật OHLC + râu nến + MA7/MA20 + 24 cột Volume (`NVDA`).
  5. `05_crypto_ohlc_candlestick.png` — Biểu đồ nến Nhật OHLC Crypto (`BTC`).
  6. `06_sportsbook_match_cards.png` — Danh sách 5 thẻ trận Premier League cỡ chữ đội bóng lớn + 3 nút kèo `1 | X | 2`.
  7. `07_sportsbook_betslip.png` — Match Center + Top 4 BXH + Sticky Bet Slip (`Pick: 1 (Home Win) [1.58x]`, đã khử lỗi ký tự `@`).
  8. `08_lottery_scratch_gold.png` — Vé cào 3×3 hiển thị đủ 9 ô chữ lớn (`$100`, `STAR`, `GEM`, `$250`, `CROWN`) và thông báo trúng thưởng.
  9. `09_lottery_xskt_18rolls.png` — Xổ số 6 số cầu vàng + ma trận 6 cột đều chiều ngang hiển thị đủ 18 lô 2 số cỡ chữ lớn (`0.245/0.520`).
  10. `10_lottery_jackpot_3dballs.png` — Cầu 3D màu `Mega 6/45` & `Power 6/55` chữ lớn rõ nét.
  11. `11_lottery_keno_20balls.png` — Bảng 20 bóng 3D Keno (`2×10`) xanh/vàng cam quay tức thì.
  12. `12_newspaper_paper_mode.png` — Giao diện báo mạng nền giấy `#F6F3EB` chữ đen căn trái (`The Eagle Times`), thân bài báo chữ lớn (`0.228/0.485`) phủ kín `~85%` chiều ngang trang báo.
  13. `13_waifulink_messenger_chat.png` — Khung chat Messenger `WaifuLink` hiển thị trọn vẹn 2 bong bóng 4 dòng cỡ chữ lớn (`0.218/0.464`) + 3 chip gợi ý + thanh nhập chat.
  14. `14_contacts_app14_list.png` — Danh bạ `Contacts` 16 nhân vật cỡ chữ lớn (`0.230/0.490`) kèm banner & chấm trạng thái.
  15. `15_contacts_app14_dm.png` — Nhắn tin từ xa qua `Contacts` với Venti cỡ chữ lớn rõ nét.

---

## 6. Nâng cấp `EaglePhone OS v6.3` (05/11/2026): Cuộn Lịch Sử Tin Nhắn (`App 13` & `App 14`) + Kiến Trúc Plugin Không Đụng Độ Cho 3 Task Song Song

- **Phiếu công việc v6.3:** [`work-items/2026-11-05-antigravity-eaglephone-chat-scroll-and-parallel-prompts.md`](work-items/2026-11-05-antigravity-eaglephone-chat-scroll-and-parallel-prompts.md)
- **Thư mục Staging & Backup v6.3:** `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\eaglephone-v63-chat-scroll-20261105\`

### 6.1. Cuộn lịch sử hội thoại đầy đủ (`WaifuLink App 13` & `Contacts App 14`)
- **Nguyên nhân trước v6.3:** SQLite đã lưu đầy đủ lịch sử trò chuyện (`data/dating_sim/waifulink.sqlite3` bảng `messages` và `data/project-eagle/character-chat/conversations.sqlite3` bảng `turn`), nhưng HUD cũ chỉ lấy `[-2:]` tin cuối ở `App 13` và 1 lượt cuối ở `App 14`.
- **Giải pháp v6.3:**
  - Bộ đóng gói bong bóng từ dưới lên (`Bottom-Up Viewport Bubble Packer`) đọc tới `120` tin nhắn theo thứ tự thời gian, tính chiều cao thực từng bong bóng (`1..5` dòng chữ cỡ lớn) và xếp tối đa `5` bong bóng (`wl_b1..wl_b5`, `ct_b1..ct_b5`) vừa khít khung nhìn mà không cắt chữ hay đè lên 3 chip gợi ý.
  - Thanh trạng thái đầu khung chat hiển thị `Latest X-Y / N` hoặc chuyển sang màu vàng `History X-Y / N` khi lướt xem tin cũ, đi kèm 3 nút cảm ứng bấm chuột trực tiếp (`Up`, `Dn`, `End`) và thanh cuộn dọc tỷ lệ thực (`wl_scroll_pct`, `ct_scroll_pct`) bên mép phải.
  - Hỗ trợ đồng thời **Con lăn chuột (`Mouse Wheel`)**, **Chuột cảm ứng (`Up / Dn / End`)**, và **Bàn phím (`I / K`, `PgUp / PgDn`, `Home / End`)**; tự động reset về `Latest` (`offset = 0`) khi gửi tin mới, nhận phản hồi AI hoặc đổi người chat.
  - Đã nghiệm thu DirectX 9 `1920×1080` dưới khóa `ingame-runtime` (`4/4` ảnh kiểm tra bằng mắt thật tại `staging/project-eagle/eaglephone-v63-chat-scroll-20261105/qa_screenshots_v63/`, `0` lỗi Lua).

### 6.2. Cổng cắm Module độc lập (`Zero-Conflict Hooks`) cho 3 Hội thoại Mở rộng Nội dung
Để 3 hội thoại kế tiếp có thể code và test đồng thời mà **không bao giờ phải sửa đè lên `EagleCompanion.py` hay `hud.lua`**, bản `v6.3` đã mở sẵn 3 cổng tự nhận diện:
1. **Task 1 (`Trading Historical Data` — chỉ sửa `eagle_historical_data.py` + `eagle_market_regimes_2010_2025.py`):** `EagleCompanion.py` tự động gọi `get_historical_ohlcv_window(asset, current_date, count=48)` và `step_live_market_candle(asset, current_date, open_price)` nếu module export, đồng thời sửa lỗi kẹt nến phẳng khi `a0 == a1` ở đầu thập niên 2010.
2. **Task 2 (`Web Newspaper` — chỉ sửa `eagle_news_en.py` + `eagle_news_archive_2010_2025.py` + `eagle_news_live_wire.py`):** `_generate_newspaper_with_hooks()` gọi trực tiếp `build_daily_newspaper_from_archive(..., extra_context=extra_ctx)` truyền bối cảnh live của Aether (`portfolio_stats`, `futures`, `lottery`, `cash`, `bank`, `stake_stats`), gỡ giới hạn cuộn `news_scroll`, hỗ trợ `paragraphs` / `body` / `subhead` / `byline` nhiều đoạn và vẽ thanh cuộn đọc báo dọc ở mép phải `App 6`.
3. **Task 3 (`App #15: EagleStake Online Casino` — chỉ tạo `eagle_stake_casino.py` + `cleo/EagleStakeHud.lua`):** Khi có `EagleStakeManager(base_dir)` trong `eagle_stake_casino.py`, `Springboard` tự động bật icon thứ 15 `EagleStake` (`stake_enabled == "1"`), chuyển tiếp `tick`, `step_simulation`, `on_open`, `on_back`, `move_vertical`, `adjust_horizontal`, `execute_primary`, `poll_hotkeys`, `on_wheel`, `on_touch(code=3|15, arg)`, `handle_action("stake_*")`, `build_hud_kv`, `build_web_projection`; `hud.lua` tự nạp nóng `cleo/EagleStakeHud.lua` (`DrawEagleStakeApp(cx, cy, cw, ch, isVi)`) qua `loadfile` + `pcall` theo `stake_hud_ver`.

### 6.3. Manifest SHA-256 Bản `v6.3` & Rollback Có Guard
Lưu tại [`staging/project-eagle/eaglephone-v63-chat-scroll-20261105/manifest_after_v63.json`](../../staging/project-eagle/eaglephone-v63-chat-scroll-20261105/manifest_after_v63.json):
- `EagleCompanion.py`: `430,129 B` (`sha256=92ad19beb48dba654a13578edb92fca5e3887d74c3aab40fefec97674cece529`)
- `eagle_mondstadt_chat_bridge.py`: `82,265 B` (`sha256=945586e998c9b292986b694872780cebc5a1ed3f13b09b83a98814a1bdca0195`)
- `hud.lua`: `206,696 B` (`sha256=0aa3f5a2202675b6eebe1a5f70702cb171397a090e111c7785e196dd8e25e3fc`)
- Rollback từ `v6.3` về `v6.2`: `python -X utf8 "C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\eaglephone-v63-chat-scroll-20261105\rollback_v63.py"`
