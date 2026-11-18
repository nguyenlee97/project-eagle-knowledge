# Khảo sát kỹ thuật 4 tính năng: Trading, Sport Bet, Xổ số và News (`EagleTimes`)

- **Ngày khảo sát:** 2026-11-04
- **Đích khảo sát (Canonical Runtime):** `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`
- **Phạm vi:** Chỉ đọc mã nguồn và tài nguyên thực tế (`0` thay đổi runtime).

> [!IMPORTANT]
> **Cảnh báo lệch nguồn (Source Drift):** Bản chạy thực tế trong `Project Eagle\gta sa gameplay-lab\` (`EagleCompanion.py` 7.035 dòng, `hud.lua` 3.046 dòng, `eagle_phone_ui.py` 2.899 dòng, cập nhật 03–04/11/2026 với Paimon Agent, App 12 EagleRide, App 13 WaifuLink v4) **mới hơn rất nhiều** so với `staging\project-eagle\gameplay-lab-poc\` (bản cũ tháng 10 – 02/11). Mọi đợt cải thiện sắp tới **bắt buộc tách nhánh từ `Project Eagle\gta sa gameplay-lab\`**, tuyệt đối không copy đè từ `gameplay-lab-poc` cũ.

---

## 1. Kiến trúc dùng chung & Luồng dữ liệu

Bốn tính năng kinh tế – thông tin nằm trên **EaglePhone v5.0** (Apps `2, 3, 4, 5, 6, 7`), vận hành qua mô hình Sidecar đa luồng:

1. **Core Engine (`EagleCompanion.py`):**
   - `sim_worker` chạy mỗi **2,0 giây** (`step_simulation`, dòng `3841–3935`): cập nhật nến OHLC 24 mã tài sản, kiểm tra thanh lý Futures, cộng nhích Jackpot Vietlott, tự động mở thưởng XSKT (`16:30`) & Vietlott (`18:00`) theo giờ GTA SA.
   - `hotkey_worker` chạy mỗi **25ms** (`poll_ingame_hotkeys`, dòng `2241–2735`): bắt phím Win32 khi cửa sổ `gta_pe.exe` đang active và không pause (`F7` bật/tắt điện thoại, `I/K/J/L` điều hướng, `F9/Enter/U` xác nhận, `F10/O` thao tác phụ, `F8/Backspace` quay lại, `F6` mở bàn phím nhập số tiền / dãy số vé).
2. **Đồng bộ RAM GTA SA (`GTAProcessBridge`):**
   - Đọc/ghi trực tiếp tiền mặt CJ/Aether tại `0x00B7CE50` & `0x00B7CE54` (`modify_cash`), giờ/phút game tại `0x00B70153` / `0x00B70152`, và mailbox 24-byte `0x00CAFE00`.
   - Mọi lệnh mua Spot, mở Futures, đặt kèo Sport Bet, mua vé số đều **trừ trực tiếp Cash RAM**, và khi chốt lời / thắng kèo / trúng số đều **cộng thẳng vào Cash RAM** (không qua tài khoản Bank App 1).
3. **Đồng bộ thời gian lịch sử (`01/01/2010` → `31/12/2025`):**
   - Biến `self.day` (`1..5844`, tương ứng 16 năm).
   - Tăng `+1` ngày khi đồng hồ GTA SA bước qua nửa đêm (`last_game_hour >= 22` sang `0..2`, dòng `3676`), khi ngủ ở App 1 (`sleep_rest`), hoặc khi tua lịch ở App 6 (`advance_day`: `-1, +1, +7, +30` ngày).
4. **3 kênh giao diện & AI Agent:**
   - **In-Game HUD (`hud.lua` + `SanViveLuaHudSA.asi`):** Đọc file ping-pong `cleo/EaglePhoneState_0.lua` / `_1.lua` do `_write_hud_dat` xuất ra. Toàn bộ chuỗi HUD bị ép về ASCII không dấu qua `to_clean_viet_ascii()` do giới hạn `CFont` của GTA SA.
   - **Web Companion (`eagle_phone_ui.py` tại `http://127.0.0.1:8765`):** Poll `GET /api/state` mỗi 1,5s và gửi lệnh qua `POST /api/action`. Hỗ trợ song ngữ Việt/Anh có dấu đầy đủ.
   - **Paimon Agent (`eagle_dialogue/phone_tools.py` & `paimon_context.py`):** Cho phép người chơi ra lệnh giọng nói/chat cho Paimon xem giá, mua/bán cổ phiếu/crypto, đặt kèo thể thao, mua vé số và tóm tắt báo ngày.
5. **Lưu trữ bền vững (`eagle_dialogue/wallet_store.py` & `paimon_host.py`):**
   - Hàm `install_wallet` monkey-patch `_write_hud_dat` (`L6994`) để lưu nguyên tử 21 trường (`day`, `cash`, `bank`, `savings`, `loan`, `stocks_market`, `crypto_market`, `futures`, `standings`, `fixtures`, `lottery`, `portfolio_stats`, ...) vào `cleo/EagleDialogue/phone-wallet.json` (giới hạn `4 MB`).
   - *Lưu ý đồng bộ:* Khi attach vào game, `sync_player_state` (`L3668`) ghi đè `self.cash = live["cash"]` từ RAM GTA SA. Do đó nếu người chơi không save game GTA SA mà thoát ra, tiền mặt `cash` quay về theo save game, trong khi `stocks_market`, `crypto_market`, `futures`, `bank`, `savings`, `lottery` và `day` vẫn giữ trạng thái mới nhất trong `phone-wallet.json`.

---

## 2. Chi tiết từng tính năng & Các lỗi / giới hạn đã xác minh

### 2.1. Trading & Portfolio (App 2: Phố Wall & Vàng, App 3: Crypto, App 7: Portfolio)

- **Danh mục 24 mã (`eagle_historical_data.py`, `L20–305`):**
  - **App 2 (16 mã):** 6 Hàng hóa/Đá quý (`XAU`, `XAG`, `XPT`, `DIAMOND`, `RUBY`, `WTI`) + 10 Cổ phiếu Mỹ (`AAPL`, `MSFT`, `NVDA`, `TSLA`, `AMZN`, `GOOG`, `NFLX`, `META`, `AMD`, `BRK`).
  - **App 3 (8 mã):** `BTC`, `ETH`, `LTC`, `XRP`, `DOGE`, `BNB`, `ADA`, `SOL`.
- **Công thức định giá & Nến OHLC (`L308–317`, `EagleCompanion.py` `L3843–3874`):**
  - Giá mục tiêu ngày (`target`) nội suy tuyến tính giữa hai mốc giá thực tế đầu năm `anchors[year]` và `anchors[year + 1]` theo `day_of_year / 365.0`.
  - Mỗi 2 giây sinh 1 cây nến mới (giữ tối đa **48 cây nến = 96 giây**):
    - Lực kéo hồi quy (mean-reversion): `pull = ((target - o) / max(o, 0.0001)) * 0.15`
    - Nhiễu biến động: `shock = random.gauss(pull, vol * 0.45)`
    - Giá đóng cửa: `c = max(0.00001, o * (1.0 + shock))`
- **Cơ chế giao dịch (`execute_trade`, `L4215–4375`):**
  - **Spot (`spot_buy` / `spot_sell`):** Đòn bẩy 1x, cộng dồn số lượng `qty` và giá vốn `spot_cost`, hỗ trợ bán một phần hoặc bán hết (`sell_all_spot`), **0% phí giao dịch, 0% trượt giá (slippage/spread)**.
  - **Futures (`fut_long` / `fut_short`):** Isolated Margin. Giá cháy tài khoản:
    - `LONG`: `liq_price = entry * (1.0 - 0.92 / lev)`
    - `SHORT`: `liq_price = entry * (1.0 + 0.92 / lev)`
    - Quét thanh lý mỗi 2s dựa trên `c["low"] <= liq_price` (Long) hoặc `c["high"] >= liq_price` (Short). Không có phí Funding, không có phí đóng/mở lệnh, không có Limit Order hay Chốt lời/Cắt lỗ tự động (`TP/SL`).

#### Lỗi & Điểm nghẽn của Trading:
1. **Biết trước tương lai (Deterministic Hindsight Exploit) + Tua lịch:** Vì `anchors` bám cứng lịch sử thật 2010–2025 và lực kéo `0.15` giữ giá luôn sát `target`, người chơi biết chắc chắn `BTC`, `NVDA`, `TSLA`, `SOL` sẽ tăng hàng trăm/nghìn lần. Kết hợp nút tua `+30d` ở App 6, người chơi có thể đánh `LONG 50x` ăn chắc 100%.
2. **Lỗi nhảy giá khi qua ngày / tua lịch (`_advance_chronological_day`, `L3797–3802`):** Khi đổi ngày, hàm gán thẳng `asset["price"] = target` mà **không sinh nến chuyển tiếp, không cập nhật lại `spot_val` ngay**, và **không quét thanh lý biến động giữa kỳ** (chỉ kiểm tra giá đích ở nhịp 2s tiếp theo).
3. **Mua được coin/cổ phiếu chưa ra đời với biểu đồ đi ngang (`L3852–3855`):** Năm 2010, `ETH` (ra mắt 2015), `BNB`/`ADA` (2017), `SOL` (2020), `META` (IPO 2012) đều giữ `a0 == a1` → biểu đồ phẳng lỳ nhưng App 2/3 vẫn cho phép mua tích trữ hoặc mở Long 50x từ năm 2010 (trong khi `paimon_context.py` có bảng `KNOWN_AFTER` để chặn Paimon nhắc tới chúng!).
4. **Nhãn `% 24h` thực chất chỉ là biến động 96 giây (`L3868–3869`):** `delta_pct` được tính so với `candles[0]["o"]` (cách đó 48 nhịp × 2s = 96 giây), không phải giá mở cửa đầu ngày hay 24h trước.
5. **Lệch cấu hình đòn bẩy giữa HUD, Web và Paimon:** In-Game HUD (`TRADE_MODES`, `L93–116`) dùng `5x, 10x, 25x, 50x`; Web UI (`eagle_phone_ui.py`, `L597–603`) lại để `2x, 5x, 10x, 20x, 50x`; còn `phone_tools.py` (`L278`) chỉ nhận `1, 5, 10, 25, 50`.
6. **Giới hạn HUD khi mở nhiều lệnh Futures cùng nhóm (`L3334–3337`, `L5636`):** Sub-page chi tiết trên HUD chỉ hiển thị và cho phép bấm `F9/F10` đóng phần tử đầu tiên `grp_futs[0]` (hoặc đóng sạch toàn bộ ở App 7), không chọn đóng từng lệnh riêng lẻ trên HUD được.

---

### 2.2. Sport Bet (App 4: EagleBet Sportsbook)

- **Cấu trúc giải đấu (`eagle_historical_data.py`, `L323–449`):**
  - **5 giải đấu:** `EPL` (Ngoại Hạng Anh), `LALIGA`, `SERIE_BUND` (Serie A & Bundesliga), `UCL` (Champions League), `NBA` (Bóng rổ Mỹ).
  - Mỗi giải có **12 CLB** với chỉ số sức mạnh tĩnh `strength` (`72..92`), đá vòng tròn 5 cặp/ngày/giải = **25 trận/ngày**.
  - Mùa giải kéo dài `266` ngày (`38 vòng × 7 ngày`), ẩn năm lịch sử trên UI để tránh người chơi tra cứu tỷ số thật.
- **Tỷ lệ kèo (Odds) & Kèo cược:**
  - Kèo `1X2`: Tính từ chênh lệch sức mạnh có cộng lợi thế sân nhà `diff = (home_str + 3) - away_str`.
  - Kèo Tài/Xỉu (`OVER` / `UNDER`): Mốc `2.5` bàn cho bóng đá, `210.5` điểm cho NBA; tỷ lệ ăn cố định cứng `1.90x`.
  - Kèo chấp Châu Á (`hcap`) có tính toán và hiển thị trên thẻ trận đấu nhưng **chưa có nút đặt cược**.

#### Lỗi nghiêm trọng & Điểm nghẽn của Sport Bet:
1. **Lộ trước tỷ số trận đấu trong JSON API & Ví (`eagle_historical_data.py` `L414–420`, `EagleCompanion.py` `L5244`):**
   - Ngay lúc khởi tạo lịch thi đấu đầu ngày, hàm `generate_daily_fixtures_for_date` đã tung xúc xắc sẵn tỷ số `h_base` và `a_base` (theo seed `day_index * 9973 + 2010`) rồi lưu trực tiếp vào từng object trong `self.fixtures`.
   - Endpoint `/api/state` trả nguyên `self.fixtures` xuống trình duyệt (và lưu vào `phone-wallet.json`). Chỉ cần mở F12 DevTools tab Network là thấy rõ tỷ số `h_base - a_base` trước khi xuống tiền!
2. **Lỗi mất trắng tiền cược cũ khi đặt đè (`place_sport_bet`, `L4420–4441`):**
   - Trên Web UI hoặc HUD, nếu một trận đã có `m["active_bet"]`, khi người chơi bấm đặt tiếp một kèo khác vào cùng trận đó, hàm `place_sport_bet` **trừ thêm tiền mặt mới rồi ghi đè `m["active_bet"]` mà không hoàn lại tiền cược cũ**! (Trong `phone_tools.py` `L318`, Paimon đã phải tự viết thêm câu chặn lỗi này ở tầng ngoài).
3. **Kèo Hòa (`DRAW x14.0`) của giải NBA là bẫy 0% thắng (`L408` vs `L5250–5251`):**
   - UI vẫn cho phép đặt cửa `DRAW` ở giải NBA với odds `14.0x`, nhưng trong `_resolve_fixture`, nếu `league == "NBA"` và `hs == as_`, code tự cộng `hs += 2` (Hiệp phụ thắng cho đội nhà) → cửa Hòa NBA **không bao giờ có thể thắng** (và còn làm đội nhà ăn kèo chấp/1X2 thiên vị).
4. **Giờ bóng lăn (`kickoff`) chỉ để trang trí:** Dù mỗi trận có giờ `15:00`, `17:30`, `20:45`..., vòng lặp đồng hồ GTA SA **không tự động cho đá và trả thưởng khi tới giờ**, mà chỉ tất toán khi người chơi bấm nút `Sim Match / Sim All` thủ công hoặc đợi qua `00:00` nửa đêm.
5. **Cày tiền vô hạn & Lệch bảng xếp hạng (`sim_one_match`, `L5327–5339`):**
   - Mỗi lần bấm `Đá Ngay` (`replace=True`), trận vừa đá xong lập tức được thay thế bằng một trận bốc ngẫu nhiên từ tương lai (`day + randint(1, 30)`). Người chơi có thể ngồi bấm cày hàng trăm trận trong 1 ngày, làm số trận đã đấu (`pts`, `w`, `d`, `l`) trên Bảng xếp hạng tăng vọt vô hạn; đồng thời khi sang mùa giải mới (mỗi 266 ngày), `self.standings` **không hề được reset về 0**.
6. **Thiếu chiều sâu cá cược:** Chưa có Cược Xiên (Parlay/Accumulator), chưa đặt được Kèo Chấp Châu Á (`Handicap`), không đặt được nhiều loại kèo (VD vừa đánh Đội nhà vừa đánh Tài) trên cùng 1 trận, và không có tường thuật diễn biến phút thi đấu trực tiếp (Live Match Ticker).

---

### 2.3. Xổ số — EagleLotto (App 5: 4 Phân trang)

- **Sub-page 0 — Vé cào 3x3 tức thì (`buy_scratch_card`, `L4443–4525`):**
  - 4 mệnh giá (`$20, $50, $100, $500`), hỗ trợ cào lẻ 1 vé hoặc Combo 5/10 vé. Xác suất có thưởng `32%` (EV hoàn trả khoảng `~55%–59%`).
- **Sub-page 1 — XSKT Miền Nam & Lô Đề 16:30 (`buy_lottery_ticket`, `_run_lottery_draw`):**
  - `XSKT_6D` (vé cứng `$10`, Độc đắc `$200,000`), Đề đầu đuôi 2 số `LODE_DE` (`x70`), Bao lô 18 giải `LODE_LO2` (`x3.5`/nháy), Ba càng `LODE_3CANG` (`x400`). Tự quay lúc `16:30` giờ game.
- **Sub-page 2 — Vietlott Điện Toán 18:00 (`buy_vietlott_ticket`):**
  - `MEGA_645` (`$10`/vé, Jackpot khởi điểm `$1.25M`), `POWER_655` (`$10`/vé, JP1 `$3.2M`, JP2 `$350k`), cùng `MEGA_BAO7` và `POWER_BAO7` (`$70`/vé = tổ hợp 7 vé con). Jackpot cộng dồn mỗi 2 giây và cộng thêm % doanh thu vé. Tự quay lúc `18:00` giờ game.
- **Sub-page 3 — Keno 20/80 & Max 3D Pro quay nhanh 0s (`play_keno`, `L4647–4715`):**
  - Rút ngẫu nhiên 20 bóng từ `01..80` (Keno) hoặc hai bộ 3 chữ số (Max 3D Pro).

#### Lỗi nghiêm trọng & Điểm nghẽn của Xổ số:
1. **BUG NGHIÊM TRỌNG — 5 nút Keno Ngũ Hành trên Web UI nuốt tiền 100%, tỷ lệ thắng 0% (`eagle_phone_ui.py` `L810–814` vs `EagleCompanion.py` `L4671`):**
   - Giao diện Web tách 5 nút riêng: `KENO_KIM`, `KENO_MOC`, `KENO_THUY`, `KENO_HOA`, `KENO_THO` (ghi `x2.4`).
   - Nhưng hàm `play_keno` trong backend `EagleCompanion.py` (`L4671`) chỉ kiểm tra `elif mode == "KENO_NGUHANH":`! Khi bấm bất kỳ nút nào trong 5 nút Ngũ Hành trên Web, tiền vẫn bị trừ ngay nhưng không rơi vào nhánh `if/elif` nào → **100% báo trượt dù tổng điểm đúng hệ Ngũ Hành**! (Trong khi trên HUD chỉ có 1 dòng gộp `KENO_NGUHANH` tự thắng nếu tổng rơi vào cực Kim `<=695` hoặc cực Thổ `>=925`).
2. **Lỗi lệch mã vé cào `$100` trên Web (`eagle_phone_ui.py` `L735` vs `EagleCompanion.py` `L4448`):**
   - Nút Web gửi `tier: 'GOLD_100'`, trong khi `tiers_cfg` của backend đặt tên là `'DIAMOND_100'`. Kết quả là bấm mua vé cào `$100` trên Web bị fallback ngầm về vé `SILVER_20` (`$20`)!
3. **Lỗi hiển thị lưới Vé cào 3x3 khi trượt (`L4485–4486`):**
   - Khi vé trượt (`prize == 0`), code rải ngẫu nhiên `[random.choice(symbols) for _ in range(9)]` từ 7 biểu tượng. Theo xác suất tổ hợp, khoảng **~35% số vé thua vẫn vô tình xuất hiện 3 biểu tượng giống hệt nhau** trên bảng 3x3 (ví dụ 3 viên kim cương `💎` hoặc 3 tờ `$250`), gây hiểu lầm là game lỗi không trả thưởng.
4. **Cắt cụt bảng 18 giải Lô trên giao diện & Tỷ lệ ăn Bao Lô quá thấp (`L5366`, `L5431`):**
   - Khi quay XSKT, `win_lo18` quay đủ 18 giải 2 số, nhưng dòng `5366` cắt `self.lottery["last_xskt_lo18"] = win_lo18[:10]`. Nếu con lô của người chơi nổ ở giải thứ 11–18, người chơi không thấy số của mình trên bảng kết quả! Ngoài ra hệ số `x3.5`/nháy cho 18 giải có kỳ vọng toán học `EV = 18 × 0.01 × 3.5 = 0.63` (nhà cái ăn dày 37%, thấp hơn nhiều so với lô truyền thống ~`x3.67` = 27 ăn 99).
5. **Sai lệch định giá vé chờ quay trong Portfolio (`L5681` & `eagle_phone_ui.py` `L1966`):**
   - `_compute_portfolio_summary` tính cứng `lotto_pending_cost = len(active_tickets) * 10`. Nếu người chơi đánh Đề/Lô `$10,000` hoặc mua Bao 7 (`$70`), tài sản ròng (Net Worth) bị tụt ảo mất `$9,990` cho đến lúc quay thưởng, và Web UI cũng hiển thị cứng nhãn `(Vé $10)`.

---

### 2.4. News — Nhật Báo `EagleTimes` (App 6)

- **Kho dữ liệu song ngữ:**
  - **Tiếng Việt (`eagle_news_archive_2010_2025.py`, 20.019 dòng):** Rất đồ sộ và giàu cảm xúc hoài niệm, gồm **590 bài báo đúng ngày sự kiện lịch sử** (trải trên 567 ngày đặc biệt) + **1.152 bài báo theo tháng** (`16 năm × 12 tháng × 6 chuyên mục`) + 16 mô tả kỷ nguyên `ERA_META`.
  - **Tiếng Anh (`eagle_news_en.py`, 694 dòng):** Chỉ là bản rút gọn sơ sài (~25 mốc ngày lớn). Hàm `_build_en_pools()` (`L668–690`) nhân bản **cùng 1 câu tiêu đề và tóm tắt duy nhất cho cả 12 tháng trong năm** (`"January 2010: ..."` → `"December 2010: ..."` giống hệt nhau). Vì ngôn ngữ mặc định của engine là `lang = "en"`, người chơi để tiếng Anh sẽ thấy báo lặp đi lặp lại suốt cả năm!
- **Cấu trúc chuyên mục:**
  - Kho gốc có **6 chuyên mục** (`world`, `life_net`, `anime_game`, `finance`, `crypto`, `sports`), nhưng giao diện App 6 (cả HUD lẫn Web) ép gộp thành **4 mặt báo** (`Desk 1` nối `world + life_net`, `Desk 3` nối `crypto + anime_game`).

#### Lỗi & Điểm nghẽn của News (`EagleTimes`):
1. **Tin tức hoàn toàn tách rời khỏi nền kinh tế (Zero Gameplay Coupling):**
   - Báo chí hiện chỉ đọc văn bản tĩnh từ kho lưu trữ cộng thêm dòng ticker giá hiện tại ở cuối câu. Tin chấn động (ví dụ sàn Mt.Gox sập, COVID-19 03/2020, Bitcoin ETF, đội bóng vô địch/chấn thương...) **chưa hề tạo ra cú sốc biến động giá (catalyst/volatility), tin đồn (rumor) hay gợi ý kèo thể thao**.
2. **Hạn chế hiển thị trầm trọng trên In-Game HUD (`L3429–3442`):**
   - Màn hình HUD App 6 chỉ vẽ được tối đa **5 dòng × 58 ký tự ASCII không dấu** (`news_c1..c5`) cho mỗi mặt báo và không có thanh cuộn đọc tiếp (scroll), khiến phần lớn nội dung bài báo dài và phần gộp chuyên mục thứ 2 bị cắt mất.
3. **Lỗ hổng "Cỗ máy thời gian" ngay trong App Đọc Báo (`L2901–2906`, `L3425`):**
   - Dòng 2 của App 6 đặt bộ nút `Time Jump` (`-1d, +1d, +7d, +30d`) cho phép nhảy lùi về quá khứ (`-1d`) hoặc tua nhanh hàng tháng trời hoàn toàn miễn phí ngay trong lúc đang giữ vị thế tài chính và hưởng lãi tiết kiệm kép `+1.5%/ngày` ở App 1!
4. **Sót chuỗi Tiếng Việt cứng trên Web UI khi bật Tiếng Anh (`eagle_phone_ui.py`):**
   - Nhiều badge và danh sách render động bằng JS trong Apps `2–7` (`Tài Sản Ròng`, `0 mã`, `0 lệnh`, `Đá Ngay`, `Chờ quay thưởng • Vé $10`...) viết cứng tiếng Việt không qua hàm dịch theo `STATE.lang`.

---

## 3. Tổng hợp định hướng cải thiện tiềm năng (Đầu vào cho bước thiết kế)

| Nhóm hệ thống | Các hạng mục sửa lỗi (Bugfix) cần ưu tiên | Ý tưởng nâng cấp chiều sâu Gameplay |
| :--- | :--- | :--- |
| **1. Trading & Portfolio** | - Sửa nhảy giá `_advance_chronological_day` (cập nhật nến + quét thanh lý xuyên ngày).<br>- Ẩn/khóa giao dịch các mã chưa IPO/launch theo năm (`IPO/Listing Calendar`).<br>- Tính đúng `% 24h` theo giá mở cửa đầu ngày.<br>- Đồng bộ mốc đòn bẩy giữa HUD / Web / Paimon và cho phép chọn đóng từng lệnh Futures trên HUD. | - **Chế độ Hybrid Price Engine:** Kết hợp xu hướng vĩ mô lịch sử với kịch bản biến động ngẫu nhiên / sự kiện bất ngờ để chống học thuộc giá.<br>- Thêm **Phí giao dịch / Spread nhỏ**, lệnh **TP / SL (Chốt lời / Cắt lỗ tự động)** và **Limit Order**.<br>- Bổ sung cổ phiếu thế giới GTA / Teyvat hoặc sự kiện chia cổ tức (Dividends). |
| **2. Sport Bet** | - **Ẩn tuyệt đối `h_base`/`a_base`** khỏi `/api/state` và chỉ sinh kết quả lúc trận đấu thực sự diễn ra.<br>- Sửa lỗi ghi đè mất tiền cược cũ; cho phép nhiều vé cược độc lập.<br>- Bỏ cửa Hòa (`DRAW`) cho giải NBA (chuyển sang Moneyline 2 cửa).<br>- Chặn cày vô hạn trận trong ngày & reset BXH khi hết mùa 266 ngày. | - **Tự động đá theo giờ `kickoff` trong game** kèm **Live Score phút `1'..90'`**.<br>- Mở khóa đặt cược **Kèo Chấp Châu Á (Handicap)**, **Cược Xiên (Parlay 2–5 trận)** và **Tỷ số chính xác**.<br>- Phong độ đội bóng (`Form` 5 trận gần nhất / chấn thương) biến thiên theo mùa thay vì chỉ số tĩnh. |
| **3. Xổ số (EagleLotto)** | - **Sửa ngay 5 nút Keno Ngũ Hành** (`KIM/MOC/THUY/HOA/THO` x2.4 hoặc chuẩn xác theo bảng tổng điểm Ngũ Hành) và mã vé cào `DIAMOND_100`.<br>- Đảm bảo vé cào thua không sinh 3 ô trùng nhau.<br>- Hiển thị đủ 18 giải Lô XSKT & lưu đúng mệnh giá gốc từng vé vào Portfolio. | - Hiệu ứng **lật từng ô vé cào 3x3** trên Web/HUD thay vì hiện kết quả khô khan.<br>- Cân bằng lại tỷ lệ trả thưởng Lô Đề sát thực tế Việt Nam (`Lô 2 số ~x3.67`, thêm **Lô Xiên 2 / Xiên 3**).<br>- Lưu bảng lịch sử các kỳ mở thưởng và vé trúng lớn. |
| **4. News (`EagleTimes`)** | - Biên tập lại kho tin Tiếng Anh `eagle_news_en.py` (tương xứng kho Việt, xóa nhân bản 12 tháng giống nhau).<br>- Tách đủ **6 chuyên mục riêng** và thêm **cuộn trang đọc bài dài** trên HUD.<br>- Khóa hoặc tách chế độ `Time Travel` khỏi gameplay kinh tế chuẩn. | - **Breaking News gắn trực tiếp vào Gameplay:** Tin nóng trong ngày tạo hiệu ứng lên cổ phiếu/crypto liên quan (Market Catalyst) hoặc hé lộ thông tin chấn thương/phong độ trước giờ bóng lăn (Insider Tip).<br>- Thông báo Toast khi có tin chấn động mới đầu ngày. |
