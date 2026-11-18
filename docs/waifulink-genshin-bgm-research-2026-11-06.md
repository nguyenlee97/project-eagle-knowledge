# Nghiên Cứu Âm Nhạc Học Kho Genshin (`st_g02` + `D:\Music`) & Kiến Trúc `WaifuLink Genshin BGM Engine v1.0` (`2026-11-06`)

- **Hội thoại thực hiện:** Antigravity (`9531315d-c75c-4231-894e-5b3792256ce8`)
- **Bàn giao cho Hội thoại Orchestrator (`WaifuLink Card Hub v2.0`):** `35d5cf80-28f1-43e1-8e77-f60ee3d570c3`
- **Phiếu công việc:** [`work-items/2026-11-06-antigravity-waifulink-genshin-bgm-engine.md`](work-items/2026-11-06-antigravity-waifulink-genshin-bgm-engine.md)
- **Trang nghe thử trực tiếp (HTML5 Audio + Mô phỏng Auto-Ducking):** [`waifulink-genshin-bgm-audition-preview.html`](waifulink-genshin-bgm-audition-preview.html)
- **Danh mục nhạc nền chính thức:** [`data/project-eagle/dating-sim/bgm_catalog.json`](../../data/project-eagle/dating-sim/bgm_catalog.json) (`48` bản nhạc HOYO-MiX / Yu-Peng Chen, `sha256=ef0662adc9e6f1e5...`)
- **Engine độc lập:** [`Project Eagle/gta sa gameplay-lab/eagle_waifulink_bgm.py`](../../Project%20Eagle/gta%20sa%20gameplay-lab/eagle_waifulink_bgm.py) (`52,110 B`, `sha256=98ed257013cb4ebd...`)
- **Trạng thái hạn mức ảnh:** `0` lệnh gọi `image-generator` (bảo toàn 100% hạn mức tạo ảnh cho các hội thoại Story Quest chạy song song).

---

## 1. Kết Quả Khảo Sát Nguồn Nhạc & Đo Đạc Âm Thanh Học (DSP)

### 1.1. Kiểm toán thực tế các đài trong `tools/eagle-radio-studio/data/project.json`
- Kết quả đối chiếu từng file trong `project.json` và `music_library_cache.json` (`4,617` file trên `D:\Music`, giữ nguyên chế độ **100% chỉ đọc**) cho thấy:
  - **Đài `st_g02` (`Night-Wind Resonance FM` — Citlali Global, `80` bài)** là **đài duy nhất** trong `project.json` chứa kho OST Genshin Impact chính thống của **HOYO-MiX / Yu-Peng Chen** (`79/80` file là nhạc Genshin; duy nhất bài `#80` là cover Vocaloid tiếng Nhật).
  - Các đài xe hơi mang tên nhân vật Genshin khác (`st_g01 Wangsheng Butterfly FM`, `st_g03 Salon Solitaire Rain FM`, `st_g04 Komaniya Vocaloid FM`, `st_ch06`, `st_ch07`, `st_pr08`, `st_sa08`, `st_lc02`) thực chất được biên tập theo gu nhạc lái xe đường phố (V-Pop, K-Pop, J-Pop, Vocaloid, Hip-Hop), **không phù hợp** làm nhạc nền đọc Visual Novel.
  - Vì vậy, danh mục `bgm_catalog.json` lấy **`35` bản tinh hoa trực tiếp từ `st_g02` (`73%` tổng danh mục)** làm xương sống, và chỉ tuyển chọn thêm **`13` bản OST HOYO-MiX chính gốc** từ hai thư mục `D:\Music\Genshin New Music` & `D:\Music\Genshin Impact OST Relaxing (complete)` để bổ sung đầy đủ **2 bài Signature vùng miền** cho cả `6/6` bạn gái (`hutao`, `furina`, `citlali`, `columbina`, `kirara`, `vesna`).

### 1.2. Phương pháp đo đạc DSP (`analyze_genshin_bgm.py`)
Script [`staging/project-eagle/waifulink-bgm-20261106/analyze_genshin_bgm.py`](../../staging/project-eagle/waifulink-bgm-20261106/analyze_genshin_bgm.py) đã giải mã PCM `16 kHz mono` toàn bộ `128` ứng viên (`80` bài `st_g02` + `48` bài bổ trợ HOYO-MiX) bằng `ffprobe` + `ffmpeg`, xuất dữ liệu chi tiết ra `acoustic_analysis_results.json` với các chỉ số:
- `duration_sec` (yêu cầu cứng `>= 55.0s`, loại bỏ các đoạn jingle ngắn lặp vòng gây mỏi tai).
- `mean_volume_db` (mức năng lượng RMS toàn bài tính theo `dBFS`), `max_volume_db` (đỉnh biên độ).
- Phân bố cửa sổ năng lượng trượt `1 giây` (`median_1s_db`, `p90_1s_db`, `max_1s_db`) và **`late_surge_db = max_1s_after_15s - p25_first_20s`**: phát hiện chính xác các bản nhạc mở đầu êm nhưng giữa bài bùng nổ dàn trống trận, kèn đồng giao hưởng hoặc drop điện tử.
- `lead_silence_sec` / `tail_silence_sec`: phát hiện các file có khoảng lặng đầu bài quá dài làm trễ nhịp chuyển cảnh.

### 1.3. Lý do loại bỏ `45/80` file khỏi `st_g02` để bảo vệ trải nghiệm đọc VN & giọng Seiyuu

| Nhóm loại trừ | Các bài cụ thể trong `st_g02` (`#thứ_tự` — Tên bài & Thông số đo thực tế) | Lý do âm nhạc học / kỹ thuật |
| :--- | :--- | :--- |
| **1. Quá ngắn (`< 55s`)** | `#04 Another Day in Mondstadt` (`52.7s`), `#23 Lone Sojourner` (`50.2s`), `#43 La vaguelette - Musicbox` (`54.1s`) | Dưới ngưỡng `55s`, vòng lặp quá ngắn khi đọc các node Story Quest dài `15–20` beats. |
| **2. Có lời hát (Vocal / Opera / J-Pop)** | `#20 Devastation and Redemption` (`161.0s`, giọng hát Kinh kịch Vân Cẩm), `#44 La vaguelette` (`149.5s`, giọng hát tiếng Pháp Cécilia Cara), `#69 I Loved You` (`81.8s`, aria có lời), `#80 【MV】神のまにまに...` (`256.4s`, cover Vocaloid J-Pop) | Giọng hát có lời đè trực tiếp lên dải tần `300 Hz – 3.5 kHz` của giọng lồng tiếng Nhật (`wl_voice`) và gây phân tâm khi đọc thoại tiếng Anh. |
| **3. Bản gộp dài (`Compilation`)** | `#18 Genshin Impact` (`1,623.1s` ≈ `27 phút`, `.m4a` ghép nhiều bài) | Không thể kiểm soát tâm trạng từng cảnh nếu phát file tổng hợp 27 phút. |
| **4. Nhạc chiến đấu / Trailer Beat Drop / Giao hưởng kèn đồng lớn** | `#15 Interstellar Drift` (`mean = -13.4 dBFS`, `max = 0.0 dBFS`, nhạc trailer Citlali nổ beat điện tử), `#36 Inevitable Conflict` (`246.9s`, nhạc combat Enkanomiya), `#09 Dance of Sabzeruz` (`mean = -15.9 dBFS`, trống tabla lễ hội dồn dập), `#50 When Night Deepens, the Moon Falls` (`314.1s`, `max_1s = -10.3 dBFS`), `#61 Inazuma` (`329.8s`, `max_1s = -10.8 dBFS`, đại giao hưởng), `#76 Nod-Krai` (`272.9s`, `max_1s = -8.9 dBFS`, hợp xướng + kèn đồng cao trào) | Lấn át hoàn toàn không gian Visual Novel và phá vỡ sự êm ái khi đọc chữ đêm khuya. |
| **5. Trùng lặp & Cover bên thứ ba ngoài HOYO-MiX** | `#38 Tender Strength` (`trk_dfc23264`, bản sao trùng 100% với `#14 trk_4f8d9261`); `#13`, `#37`, `#47`, `#53` (*Beside Bed / Jordy Chandra* Lo-Fi beat covers); `#49 In the Desolate Hallway` (`lead_silence = 6.0s` đầu bài câm tiếng) và các bản đồng điệu dư thừa trong cùng vùng | Giữ thuần khiết **100% chất âm HOYO-MiX / Yu-Peng Chen chính hãng** (không pha tiếng trống snare Lo-Fi hip-hop), không trùng lặp bài và vào nhạc ngay lập tức (`lead_silence <= 2.0s`). |

---

## 2. Danh Mục 48 Bản Nhạc Tinh Hoa (`bgm_catalog.json`)

Tổng cộng **`48` bản nhạc** (`35` bài từ `st_g02` + `13` bài bổ trợ vùng miền từ `D:\Music`), thời lượng `56.1s – 180.3s`, được chuẩn hóa sẵn `base_mci_volume` (`199 .. 238 / 1000` xoay quanh chuẩn `220 / 1000`) dựa trên `mean_volume_db`:

### 2.1. Bảng Signature Track tại Sảnh Thẻ Bạn Gái (`hub_cozy` — `14` bài)

| Nhân vật | Bài Signature #1 | Bài Signature #2 | Màu sắc nhạc cụ & Ngữ cảnh |
| :--- | :--- | :--- | :--- |
| **Citlali** (`citlali`) | `trk_787af740` — *Lullaby of the New Moon (I): Somnias a Luna* (`st_g02 #01`, `129.3s`, `vol=207`) | `sup_493b320c` — *Soothing of Soul and Sand* (`Natlan Night-Wind`, `100.8s`, `vol=207`) | Đàn hạc sao đêm, guitar mộc & kalimba bộ tộc Chủ Nhân Gió Đêm. |
| **Hu Tao** (`hutao`) | `trk_69af44fb` — *Flows of Jade-Like Water* (`st_g02 #70`, `56.0s`, `vol=221`) | `sup_9bf94608` — *The Journey of Tea Leaves* (`Chenyu Vale`, `97.1s`, `vol=225`) | Cổ tranh (guzheng) & sáo tiêu ấm trà chiều trước hiên Vãng Sinh Đường. |
| **Furina** (`furina`) | `trk_8adb597b` — *Pluie sur la ville (Music Box)* (`st_g02 #17`, `80.1s`, `vol=211`) | `sup_68b7ed14` — *Il Crepuscolo di Poisson* (`Fontaine`, `103.5s`, `vol=208`) | Hộp nhạc pha lê & accordion chiều tà Fontaine thanh lịch, êm dịu. |
| **Columbina** (`columbina`) | `trk_32c1cb21` — *Columbina's Lullaby (Luna I)* (`st_g02 #30`, `180.2s`, `vol=221`) | `sup_b945877e` — *Per Amica Silentia Lunae* (`Nod-Krai`, `89.2s`, `vol=209`) | Khúc hát ru không lời của Thiếu Nữ Mặt Trăng & đàn hạc bạc (`surge = +2.4 dB`). |
| **Kirara** (`kirara`) | `trk_e76f9798` — *A Tranquil Town* (`st_g02 #16`, `68.2s`, `vol=232`) | `sup_358f4a9f` — *Kitsune's Mask* (`Inazuma`, `99.9s`, `vol=222`) | Đàn koto & acoustic gỗ thị trấn Inazuma yên bình, tươi sáng. |
| **Vesna** (`vesna`) | `sup_814ffd61` — *A Feast of Bread and Salt* (`Snezhnaya`, `98.6s`, `vol=206`) | `sup_cfafb464` — *Chattering Snowflakes* (`Winter Waltz`, `106.0s`, `vol=230`) | Đàn dây ấm bên lò sưởi Bắc Quốc & điệu waltz bông tuyết celesta dịu ngọt. |
| **Chung (Universal Cozy)** | `trk_3b24947c` — *Cozy Company* (`st_g02 #79`, `134.6s`, `vol=230`) | `trk_419495bc` — *Dusk in Mondstadt* (`st_g02 #26`, `108.8s`, `vol=229`) | Nhạc Ấm Trần Ca (Serenitea Pot) & hoàng hôn thành Mondstadt. |

### 2.2. Bốn nhóm tâm trạng Visual Novel & Story Quest (`34` bài)
1. **`vn_daily_sweet` (`9` bài — Đời thường ngọt ngào & tinh nghịch, Stage 1–3 / Chương 1–2):**
   - Từ `st_g02`: *A Sweet Smile* (`trk_46d1d9c2`), *Sunshine Beach* (`trk_b2523e0c`), *Dawn Winery Theme* (`trk_68ea11d9`), *Clear Sky over Liyue* (`trk_19f1faa8`), *Peaceful Wishes* (`trk_983ed863`), *Melody of Jellyfish* (`trk_2d0044bd`), *Another Hopeful Tomorrow* (`trk_33e76ff1`).
   - Bổ trợ vùng Fontaine/Snezhnaya: *Ann's Quiescent Residence* (`sup_907e6744`), *Clockwork Waltz* (`sup_6d64a4c2`).
2. **`vn_tender_romance` (`9` bài — Lãng mạn sâu lắng, Scene 4/4, Stage 4–5 & `END_TRUE / END_GOOD`):**
   - Từ `st_g02`: *Lovers' Oath* (`trk_328319ce`), *Tender Strength* (`trk_4f8d9261`), *Moonlike Smile* (`trk_b194a907`), *Maiden's Longing* (`trk_6c74198b`), *Dream of Scattered Petals* (`trk_eff297df`), *Le Souvenir avec le crepuscule (Music Box)* (`trk_afa3ffdf`), *Good Night, Liyue* (`trk_a1806a4e`), *Moon in One's Cup* (`trk_f69caa6d`).
   - Bổ trợ sao đêm Natlan: *Chasing Starlight With You* (`sup_50b0da58`).
3. **`vn_melancholy_memory` (`8` bài — Hoài niệm, mưa đêm, nội tâm cô độc & `END_NEUTRAL / END_BAD_1`):**
   - Từ `st_g02`: *Pluie sur la ville* (`trk_b3c6988e`), *Slight Distress* (`trk_d76ea040`), *Ruu's Melody* (`trk_65d2216f`), *Fragile Fantasy* (`trk_f643d363`), *Fading Memories* (`trk_853baa88`), *Say My Name* (`trk_5d73c718`), *Surging Reminiscence* (`trk_7fe7cbcb`).
   - Bổ trợ hồi ức Citlali: *Woven in the Smoke of Memory* (`sup_6d778798`).
4. **`vn_mystic_tension` (`8` bài — Huyền bí tĩnh lặng, điều tra, Combination Gate & `END_BAD_2`):**
   - Từ `st_g02`: *The Fading Stories (Qingce Night)* (`trk_8af62eb9`), *Contemporary Testimony* (`trk_200e1573`), *Blue Dream* (`trk_db3e4f9e`), *Snow-Buried Tales* (`trk_7637e539`), *Chatter Between Roots* (`trk_aafa4c9e`), *Illuminated Coral Palace* (`trk_60c90290`).
   - Bổ trợ Nod-Krai / Inazuma: *Enigma in the Lunar Cradle* (`sup_b5f2180d`), *In the Strange Realm of Sakura* (`sup_a2e07503`).

---

## 3. Kiến Trúc Kỹ Thuật `eagle_waifulink_bgm.py` (`Dual-MCI` + `Auto-Ducking` + `Short-Path Guard`)

1. **Cô lập tuyệt đối luồng OS cho Win32 MCI (`alias wl_bgm`):**
   - Win32 `winmm.dll -> mciSendStringW` ràng buộc context thiết bị theo từng OS thread. `WaifuLinkBGMEngine` tạo luồng daemon riêng `WaifuLinkBGMWorker` sở hữu độc quyền `alias wl_bgm` (`type mpegvideo`), hoàn toàn song song và không bao giờ đụng tới luồng `WaifuLinkJPVoiceWorker` (`alias wl_voice`).
2. **Giải quyết triệt để lỗi đường dẫn dài / Unicode / Cover Art ID3v2 / `.m4a` trên Win32 MCI:**
   - Bộ đệm ASCII sạch đã được dựng sẵn cho toàn bộ `48/48` bài tại `data/project-eagle/dating-sim/bgm_cache/<id>.mp3` (gỡ bỏ hoàn toàn ảnh bìa nhúng ID3v2 `-vn -map_metadata -1 -id3v2_version 0` vốn hay làm `mpegvideo` báo lỗi `277`, đồng thời chuyển mã sẵn 3 bài gốc `.m4a` sang `.mp3` `192 kbps` mà không chạm tới file gốc trên `D:\Music`).
   - Đối với mọi bài mới thêm động về sau, `resolve_mci_playable_path(...)` tự động thử `GetShortPathNameW` trước; nếu ổ `D:` tắt `8.3` hoặc `mciSendStringW` báo lỗi mở file, engine tự động sinh file cache `bgm_cache/trk_<hash>.mp3` bằng `ffmpeg` ngay lập tức.
3. **Hòa âm thông minh (`Smart Mixing`), `Auto-Ducking` & Chu kỳ sống (`Lifecycle`):**
   - **Âm lượng nền chuẩn hóa theo từng bài:** `~199 – 238 / 1000` (trung tâm `220 / 1000`).
   - **Zero-Latency Voice Auto-Ducking:** `eagle_waifulink_voice.py` phát tín hiệu callback `set_state_listener(bgm_engine.notify_voice_state)` ngay khi câu thoại tiếng Nhật bắt đầu/kết thúc (kết hợp kiểm tra dự phòng `is_currently_playing()`). `wl_bgm` hạ êm xuống **`85 / 1000` trong `150ms`**, giữ sau khi thoại dứt **`300ms`**, rồi nâng mượt trở lại mức nền trong **`260ms`**.
   - **Crossfade không chặn (`Non-Blocking Tick Fade`) & `EOF Auto-Next`:** Chuyển Mood thực hiện `fade-out 350ms` (có ngắt sớm nếu người chơi lướt nhanh) -> mở bài mới -> `fade-in 350ms` điều khiển bởi vòng lặp tick `30ms`. Khi vị trí phát đạt `>= length_ms - 250` hoặc `mode == stopped`, engine tự chuyển sang bài ngẫu nhiên khác cùng nhóm Mood mà không lặp lại bài vừa phát.
   - **Nhường đường tuyệt đối cho Pause Menu & RadioEx:**
     - Đọc trực tiếp `0x00BA67A4` (`CMenuManager::m_bMenuActive`) qua `GTAProcessBridge.try_attach()` + `read_u8`: bấm `ESC` vào Pause Menu tự `pause wl_bgm`, quay lại game tự `resume wl_bgm`.
     - Khi bắt đầu **Free Roam Chauffeur Outing** hoặc bấm `[Backspace]` thoát giao diện về thế giới 3D ngoài đường: tự `fade-out` và `close wl_bgm` hoàn toàn (`playing = False, volume = 0`), bảo đảm **0% xung đột với đài RadioEx trên xe**.
4. **Suy luận tự động Mood ổn định cấp Node (`infer_vn_bgm_bucket`):**
   - Không cần sửa bất kỳ dòng nào trong `eagle_story_quest_<char>.py` hay `eagle_waifulink_v4_<char>.py`.
   - Đối với Story Quest 5 Chương: ánh xạ chính xác 5 kết cục (`END_TRUE / END_GOOD -> vn_tender_romance`, `END_NEUTRAL / END_BAD_1 -> vn_melancholy_memory`, `END_BAD_2 -> vn_mystic_tension`) và phân tích toàn bộ nội dung `node` (`title`, `location`, `day_label`, toàn bộ `beats` trong node) để **giữ ổn định 1 nhóm Mood xuyên suốt cả Node**, không bị nhảy nhạc giữa từng câu thoại. Hỗ trợ sẵn trường ghi đè tùy chọn `bgm_bucket` trên `node` hoặc `beat`.

---

## 4. Hợp Đồng Tích Hợp Sẵn Sàng Cho `WaifuLink Card Hub v2.0` (Hội thoại `35d5cf80-...`)

### 4.1. Trường `bgm_telemetry` trong `GET /api/state` (cả ở cấp cao nhất lẫn `state["dating_sim"]["bgm_telemetry"]`)
```json
{
  "playing": true,
  "muted": false,
  "track_id": "trk_787af740",
  "track_title": "Lullaby of the New Moon (I): Somnias a Luna",
  "ascii_title": "Lullaby of the New Moon (I): Somnias a Luna",
  "ascii_now_playing": "BGM: Lullaby of the New Moon (I): Somnias a Luna",
  "mood_bucket": "hub_cozy",
  "volume": 207,
  "base_volume": 207,
  "master_volume_pct": 100,
  "ducked": false,
  "paused_by_menu": false,
  "mci_ok": true,
  "play_count": 1,
  "active_context": true,
  "mode": "hub",
  "char_id": "citlali",
  "region": "Natlan / Night-Wind Global",
  "origin": "st_g02",
  "position_ms": 4820,
  "length_ms": 129312,
  "last_error": ""
}
```

### 4.2. Các khóa ASCII sạch xuất sẵn trong `cleo/EaglePhoneHUD.dat` & `EaglePhoneState.lua`
Đợt nâng cấp `hud.lua` cho **WaifuLink Card Hub v2.0** có thể đọc trực tiếp ngay mà không cần sửa lại Python:
- `EaglePhoneState.wl_bgm_playing`: `"1"` hoặc `"0"`
- `EaglePhoneState.wl_bgm_muted`: `"1"` hoặc `"0"`
- `EaglePhoneState.wl_bgm_ducked`: `"1"` hoặc `"0"`
- `EaglePhoneState.wl_bgm_id`: mã bài hiện tại (VD `"trk_787af740"`)
- `EaglePhoneState.wl_bgm_title`: tên bài sạch ASCII 100% tối đa `48` ký tự
- `EaglePhoneState.wl_bgm_bucket`: `"hub_cozy"` | `"vn_daily_sweet"` | `"vn_tender_romance"` | `"vn_melancholy_memory"` | `"vn_mystic_tension"`
- `EaglePhoneState.wl_bgm_vol`: âm lượng MCI thực tế `0..1000`
- `EaglePhoneState.wl_bgm_master_pct`: âm lượng tổng người chơi chọn `0..100`
- `EaglePhoneState.wl_bgm_bar`: chuỗi hiển thị sẵn cho thanh Header (VD `"BGM: Lullaby of the New Moon (I): Somnias a Luna"`, `"BGM: MUTED (...)"`, hoặc `"BGM: OFF"`).

### 4.3. HTTP Endpoints & Actions điều khiển nhạc nền
- **`GET /api/dating/bgm`** -> trả về `{"ok": true, "bgm_telemetry": {...}}`.
- **`POST /api/dating/bgm`** -> nhận `{"action": "next" | "mute" | "volume" | "sync", "muted": bool, "pct": 0..100}`.
- **`POST /api/action`** -> hỗ trợ các action `wl_bgm_next` (hoặc `dating_bgm_next`), `wl_bgm_mute` (`dating_bgm_mute`), `wl_bgm_volume` (`dating_bgm_volume`, kèm `pct` / `volume_pct`).

---

## 5. Bằng Chứng Nghiệm Thu (Part A Offline + Part B Live In-Game) & Phục Hồi (Rollback)

### 5.1. Kiểm thử Part A Offline (`staging/project-eagle/waifulink-bgm-20261106/test_part_a_bgm_offline.py` — `100% PASS`)
- Mở thật qua Win32 `mciSendStringW`: **`48/48` bài đạt `err == 0`** và đọc được `status wl_bgm length` hợp lệ (`56,059 ms .. 180,270 ms`).
- Kiểm chứng fallback tự sinh cache động từ file `.m4a` tên chứa ký tự Unicode `˚✧₊` -> tự chuyển sang `trk_dyn_unicode_m4a.mp3` và phát `err == 0`.
- Kiểm chứng chọn đúng Signature Track cho cả `6/6` bạn gái ở `hub_cozy`, kiểm chứng song song `wl_bgm` + `wl_voice` (`225 -> 85 -> 225`), kiểm chứng phân phối `44` node của `eagle_story_quest_hutao.py` (`15 vn_daily_sweet`, `12 vn_mystic_tension`, `9 vn_melancholy_memory`, `8 vn_tender_romance`) ổn định `100%` giữa các beat trong cùng node.

### 5.2. Kiểm thử Part B Live In-Game dưới `ingame-runtime.lock` (`run_part_b_ingame_qa.py` -> `part_b_live_ingame_qa.json` — `100% PASS`)
1. **Menu `[F9]` trước nhà bạn gái:**
   - Nhà Citlali: `mci_ok = True, playing = True, mood_bucket = "hub_cozy"`, tự chọn đúng bài chủ đề *Lullaby of the New Moon (I): Somnias a Luna* (`trk_787af740`).
   - Bấm phím `[F9]` thật trước cửa nhà Hu Tao: tự chuyển mượt sang bài chủ đề Liyue *Flows of Jade-Like Water* (`trk_69af44fb`), xuất đúng `wl_bgm_playing = "1"` & `wl_bgm_bar` trong `EaglePhoneHUD.dat`.
2. **Chuyển cảnh Scenario VN & Story Quest 5 Chương:**
   - Scenario VN Hu Tao: Scene `1/4` phát *Clear Sky over Liyue* (`vn_daily_sweet`) -> sang Scene `4/4` crossfade êm sang *Moon in One's Cup* (`vn_tender_romance`).
   - Story Quest Hu Tao (*"Where the Papilio Rests"*): `N01` (*Fetor in the Bamboo Mist* — Đồi Vô Vọng lúc nửa đêm) tự phát *The Fading Stories (Qingce Night)* (`vn_mystic_tension`) -> qua `N02` ban ngày tại Liyue crossfade sang *Clear Sky over Liyue* (`vn_daily_sweet`) -> bấm `wl_bgm_next` chuyển sang bài không lặp *Another Hopeful Tomorrow* (`trk_33e76ff1`).
3. **Phát đồng thời Giọng Nhật (`wl_voice`) + `Auto-Ducking` (`wl_bgm`) & Cờ Pause Menu `0x00BA67A4`:**
   - Trước câu thoại: `wl_bgm` ổn định ở `223 / 1000` (`ducked = False`).
   - Khi Seiyuu Rie Takahashi cất tiếng (`voice_telemetry.play_count` tăng `11 -> 12`, `is_playing = True`): `wl_bgm` hạ mượt xuống đúng **`85 / 1000` (`ducked = True`)**, hai alias chạy song song mượt mà không chặn nhau.
   - Sau khi câu thoại kết thúc: `wl_bgm` tự động nâng mượt trở lại **`223 / 1000` (`ducked = False`)**.
   - Bật cờ RAM `0x00BA67A4 = 1`: `paused_by_menu = True`; trả về `0`: tự `resume` (`paused_by_menu = False`).
4. **Thoát `[Backspace]` ra thế giới 3D & Lái xe Free Roam nhường RadioEx:**
   - Bấm `[Backspace]` đóng Story Quest: `playing = False, volume = 0` (`BGM: OFF`).
   - Từ Menu `[F9]` bắt đầu **Free Roam Outing**: `playing = False, mode = "freeroam", volume = 0` ngay lập tức để nhường 100% âm thanh xe cho RadioEx; sau khi hoàn tất chuyến đi về thế giới 3D vẫn giữ `playing = False`.
5. **Độ sạch hệ thống:** `cleo/EagleLuaErrors.log` = **`0` lỗi**; `python eagle_doctor.py` đạt **`11/11 PASS, 0 WARN, 0 FAIL (88ms)`**. Đã tắt sạch `gta_pe.exe` + `EagleCompanion.py`, khôi phục nguyên trạng SQLite DB / settings / `EaglePhoneHUD.dat` và giải phóng khóa.

### 5.3. Manifest SHA-256 Trước/Sau & Lệnh Rollback Có Guard
- Manifest lưu tại: [`staging/project-eagle/waifulink-bgm-20261106/backups/wire_manifest.json`](../../staging/project-eagle/waifulink-bgm-20261106/backups/wire_manifest.json)
  - `eagle_waifulink_voice.py`: `e1128d055b6bcb5d...` -> `a46feb4101946932...`
  - `eagle_dating_sim.py`: `23e2c150e06d3ace...` -> `d0022d3e2864c395...`
  - `eagle_story_quest.py`: `a8c5dca51e8adb77...` -> `deb27befbbab98c5...`
  - `EagleCompanion.py`: `4ed217a31494084c...` -> `9efc93f8e7a1b039...`
- Lệnh phục hồi an toàn (tự giữ `game-write.lock` và kiểm tra SHA-256 để không bao giờ ghi đè lên chỉnh sửa mới hơn của hội thoại khác — đã test thực tế `PASS`):
  ```powershell
  python "C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\waifulink-bgm-20261106\rollback_waifulink_bgm_wire.py"
  ```
