# Báo Cáo Bàn Giao — Hệ Thống Lồng Tiếng Nhật (`WaifuLink JP Voice Engine v1.0`) Cho Project Eagle (`gta sa gameplay-lab`)

- **Ngày thực hiện:** `2026-11-04` (`Asia/Saigon`)
- **Agent / Hội thoại:** Antigravity / `9999181a-572a-42c8-ae19-fa06cc60d90f`
- **Phiếu công việc:** `docs/project-eagle/work-items/2026-11-04-antigravity-waifulink-jp-voicelines.md`
- **Game đích tích hợp:** `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`
- **Thư mục dữ liệu âm thanh:** `C:\Users\LENOVO\Desktop\GTA\data\project-eagle\dating-sim\voices\`
- **Thư mục staging, script build & QA:** `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\waifulink-jp-voice-20261104\`
- **Tuân thủ phạm vi dùng chung:** Giữ nguyên tuyệt đối gói Presentation `03/11` (`WibuMenu.asi`, `models/fronten2.txd`, `models/fronten3.txd`, startup/audio/loading), `models/hud.txd`, `data/peds.ide`, và các module kịch bản riêng (`eagle_waifulink_v4_furina.py`, `eagle_waifulink_v4_citlali.py`, `eagle_waifulink_v4_columbina.py`).

---

## 1. Tổng Quan Hạng Mục Hoàn Thành

1. **Bộ Giọng Tiếng Nhật Studio (`144` file `.wav` thật — `24` file × `6` nhân vật):**
   - Tải từ kho voice-over tiếng Nhật của Genshin Impact (`static.wikia.nocookie.net` qua MediaWiki API), cắt khoảng lặng tự nhiên theo hơi thở (`1.28s – 5.42s`), chuẩn hóa `44,100 Hz, 16-bit PCM` với peak `-1.8 dBFS` và fade-in/out mượt để không bao giờ bị cụt âm cuối hay nổ loa.
   - Đóng gói đầy đủ metadata tại `data/project-eagle/dating-sim/voices/manifest.json` (`144` bản ghi kèm `sha256`, `duration_sec`, `bytes`, `seiyuu`, `source_ogg`, `jp_text`, `romaji`).

| `char_id` | Nhân vật | Seiyuu (CV) | Nguồn giọng Studio | Số file | Nhóm cảm xúc (`Voice Buckets`) |
|---|---|---|---|---:|---|
| `hutao` | Hu Tao | **Rie Takahashi (高橋李依)** | `VO_JA_Hu_Tao_*.ogg` | `24` (`3 × 8`) | Đủ `8/8` buckets |
| `furina` | Furina de Fontaine | **Inori Minase (水瀬いのり)** | `VO_JA_Furina_*.ogg` | `24` (`3 × 8`) | Đủ `8/8` buckets |
| `citlali` | Citlali | **Asami Tano (田野アサミ)** *(credit chính thức Genshin JP)* | `VO_JA_Citlali_*.ogg` | `24` (`3 × 8`) | Đủ `8/8` buckets |
| `columbina` | Columbina | **Lynn (りん)** | `VO_JA_Columbina_*.ogg` | `24` (`3 × 8`) | Đủ `8/8` buckets |
| `kirara` | Kirara | **Sayumi Suzushiro (鈴代紗弓)** | `VO_JA_Kirara_*.ogg` | `24` (`3 × 8`) | Đủ `8/8` buckets |
| `vesna` | Vesna | **Aya Endo (遠藤綾)** *(chọn cố định chất giọng nữ quý tộc tinh nghịch từ kho Yelan JP do Wiki chưa có file `.ogg` của Vesna, lọc sạch 100% tên riêng Liyue/Yelan)* | `VO_JA_Yelan_*.ogg` | `24` (`3 × 8`) | Đủ `8/8` buckets |

2. **8 Nhóm Cảm Xúc (`Voice Buckets`) & Quy Tắc Ngắt / Cooldown:**
   - `greet_doorstep`: Tự phát khi lại gần cửa nhà waifu `<= 22m` hoặc mở House Visit Event Selector (`[F9]`); cooldown `25.0s`, `interrupt=False` (không lặp spam khi đứng gần hoặc đi ra vào liên tục).
   - `vn_sweet_happy`: Cảnh VN / trả lời tin nhắn / nhận quà vui vẻ, ngọt ngào, chọn đáp án `BEST` (`interrupt=True`).
   - `vn_shy_blush`: Cảnh VN / chat đỏ mặt, bối rối, ngại ngùng (`tsundere` / `flustered`, `interrupt=True`).
   - `vn_playful_tease`: Cảnh VN / chat trêu chọc, tinh nghịch hoặc nhắc hỏi lại khi gõ lạc đề (`interrupt=True`).
   - `vn_tender_love`: Cảnh kết lãng mạn `Scene 4/4` (`PASSED`) và câu thoại tâm tình sâu lắng (`interrupt=True`).
   - `outing_cruise`: Phát khi bắt đầu lên ghế phụ xe mui trần `575 Broadway` và thoại dạo phố êm ái sau `40s` (`cooldown=40.0s`, `interrupt=False`).
   - `outing_bump_rescue`: Phản ứng khẩn cấp khi xe đụng tụt máu (`CVehicle +0x4C0` giảm `>= 15 HP`) hoặc khi `EagleWaifuBridge.cs` sơ tán khỏi xe cháy `< 250 HP` (`cooldown=3.5s`, **luôn ghi đè khẩn cấp `interrupt=True`**).
   - `outing_arrive_photo`: Khi lái xe tới đích hẹn hò (`S-Rank` / `A-Rank`) hoặc khi nhận ảnh kỷ niệm `Time-Apart Milestone Photo Drop`.

3. **Engine Phát Bất Đồng Bộ `eagle_waifulink_voice.py`:**
   - Chạy trên luồng nền nhẹ riêng biệt qua Windows `winmm.dll` (`mciSendStringW` ưu tiên driver `mpegvideo` để điều chỉnh âm lượng mượt `0..1000`, tự động fallback sang `waveaudio` / `PlaySoundW` nếu cần).
   - Tự động đọc cờ Pause Menu của `gta_pe.exe` tại địa chỉ `0x00BA67A4` (`CMenuManager::m_bMenuActive`): tạm dừng ngay clip đang phát (`pause`) khi mở Pause Menu, phát tiếp (`resume`) khi quay lại game, và từ chối phát câu mới khi đang ở menu (`skipped="game_paused"`).
   - API cấu hình trực tuyến `GET/POST /api/dating/voice_settings` (và action `dating_voice_settings`), lưu bền vững tại `data/project-eagle/dating-sim/voice_settings.json` (`voice_enabled=True`, `voice_volume=80`).
   - Xuất telemetry thời gian thực tại `/api/state` -> `dating_sim.voice_telemetry` (`play_count`, `per_char_counts`, `per_bucket_counts`, `last_voice_played`, `recent_history`).

---

## 2. Kết Quả Kiểm Thử Độc Lập & Kiểm Thử Thực Tế In-Game

### A. Kiểm Thử Offline 100% File Audio & Unit Test (`test_voice_engine_offline.py` — NGOÀI KHÓA)
- **Kết quả:** `100% PASS` (`staging/project-eagle/waifulink-jp-voice-20261104/offline_voice_audit_report.json`).
- **Kiểm định vật lý `144/144` file `.wav`:**
  - Dung lượng nhỏ nhất: `110.3 KB` (`> 10 KB` yêu cầu).
  - Thời lượng thực tế: `1.28s – 5.42s` (nằm gọn trong khung tự nhiên `1.0s – 6.0s`).
  - `144/144` mã băm `SHA-256` duy nhất (0 file trùng lặp).
  - Độ lệch chuẩn biên độ `std_amp >= 600` và biến thiên bao hình giọng nói `env_cv >= 0.22` (chứng minh 100% giọng người nói thật, 0 file câm hay sóng sin đơn điệu).
  - `144/144` file mở, đọc thời lượng và phát thành công qua `winmm.dll` `mciSendStringW`.
- **Unit Test hành vi `WaifuLinkVoiceEngine`:** Xác nhận chuyển cảnh VN `1/4 -> 2/4 -> 3/4 -> 4/4` ngắt câu cũ tức thì, cooldown `25s`/`40s`/`3.5s` chuẩn xác, `outing_bump_rescue` ghi đè khẩn cấp, cờ Pause `0x00BA67A4` tạm dừng/khôi phục đúng, và lưu `voice_settings.json`.

### B. Kiểm Thử Thực Tế DirectX 9 (`run_live_jp_voice_qa.py` — DƯỚI `ingame-runtime.lock`)
- **Kết quả:** **`33/33` assertions PASS (`Exit Code 0`, `play_count = 17`)**, báo cáo JSON chi tiết tại `staging/project-eagle/waifulink-jp-voice-20261104/live_jp_voice_qa_report.json`.
  1. **Cấu hình `/api/dating/voice_settings` & Mute Guard:** `GET` trả đúng `voice_enabled=True, voice_volume=80`; khi `POST` tắt tiếng (`voice_enabled=False`) thì `play_count` giữ nguyên `0`; bật lại lưu JSON chuẩn xác.
  2. **Ngữ cảnh 1 — Lại gần cửa nhà Waifu (`<= 22m` Chinatown SF):** Tự động phát `hutao/greet_doorstep_03.wav` (`3.28s`, `play_count = 1`); đi ra `> 30m` rồi quay lại ngay trong `< 25s` không phát lặp nhờ cooldown `25s`.
  3. **Ngữ cảnh 2 — Đi qua đủ 4 cảnh Visual Novel (`Scene 1/4 -> 2/4 -> 3/4 -> 4/4`):** Mỗi lần chuyển cảnh ở `< 0.5s` đều ngắt mượt câu trước (`interrupt=True`), tăng `play_count` tuần tự `2 -> 3 -> 4 -> 5`, và cảnh kết `Scene 4/4` (`PASSED`) phát đúng `vn_tender_love` (`vn_tender_love_02.wav`).
  4. **Ngữ cảnh 3 — Lái xe `575 Broadway` + Va chạm + Tới đích + Ảnh kỷ niệm + Xe cháy `< 250 HP`:**
     - Bắt đầu hẹn hò trên `575 Broadway` cùng 3D Hu Tao (`2000.0 HP`): phát `outing_cruise_02.wav` (`play_count = 6`).
     - Va chạm xe (`CVehicle +0x4C0` tụt `-65 HP`, hạng `S-RANK -> A-RANK (+20)`): ghi đè ngay bằng `outing_bump_rescue_01.wav` (`play_count = 7`).
     - Tới đích Pier 69 (`Affection = 135 >= 120` mốc `M02`): phát `outing_arrive_photo_02.wav` (`play_count = 8`).
     - Rời xa `> 100m` sau `~11s`: tự động nổ banner `WAIFULINK PHOTO: HU TAO (M02)` kèm phát `outing_arrive_photo_01.wav` (`play_count = 9`).
     - Thử thách xe bốc cháy (`220 HP < 250 HP`): `EagleWaifuBridge.cs` sơ tán 3D Hu Tao an toàn ở `2000.0 HP` và phát `outing_bump_rescue_03.wav` (`play_count = 10`).
  5. **Ngữ cảnh 4 — Chat App 13 + Đủ `6/6` Nhân vật + Cờ Pause Menu `0x00BA67A4`:**
     - Nhắn tin trực tiếp cho `furina` phát `vn_sweet_happy_02.wav` (`Inori Minase`); mở thoại lần lượt cho `citlali`, `columbina`, `kirara`, `vesna` xác nhận `per_char_counts = {'hutao': 11, 'furina': 1, 'citlali': 1, 'columbina': 1, 'kirara': 1, 'vesna': 1}` (`mci_ok = True` 100%).
     - Khi Pause Menu bật (`0x00BA67A4 = 1`), câu thoại mới bị chặn sạch (`play_count` giữ ở `16`); khi bỏ Pause (`0x00BA67A4 = 0`), phát lại bình thường (`play_count = 17`).
  6. **Độ ổn định & Sức khỏe hệ thống:**
     - `cleo/EagleLuaErrors.log`: `0` byte (`0` lỗi Lua).
     - `gta_pe.exe`: `0` crash xuyên suốt toàn bộ bài test.
     - `eagle_doctor.py`: **`11/11 PASS`** (`Exit Code 0`).
     - Khối `finally:` đã tắt sạch `gta_pe.exe` + `EagleCompanion.py`, xóa DB tạm của ca test, khôi phục `voice_settings.json` (`voice_enabled=True, voice_volume=80`) và đặt `cleo/EaglePhoneHUD.dat` về `open=0, ev_active=0`.

---

## 3. Danh Mục File & Mã Băm SHA-256 Bàn Giao

| Đường dẫn tương đối từ `C:\Users\LENOVO\Desktop\GTA\` | Vai trò | SHA-256 |
|---|---|---|
| `Project Eagle\gta sa gameplay-lab\eagle_waifulink_voice.py` | Engine lồng tiếng Nhật bất đồng bộ (`winmm.dll` MCI) | `E1128D055B6BCB5DC9E3D5102AD84B4EBE5A79E9EDE4D28FA8C409083ECF5F21` |
| `Project Eagle\gta sa gameplay-lab\eagle_dating_sim.py` | Gắn hook phát thoại an toàn (`_play_voice_safe`) + telemetry | `900F7DACF1432B2754761A115D358135D72A989307A5FD0B8DB47642B8B54DE8` |
| `Project Eagle\gta sa gameplay-lab\EagleCompanion.py` | Endpoint `GET/POST /api/dating/voice_settings` & action `dating_voice_settings` | `1D95F1D3A78C545689E0244F788FF6A122A45CF64025047CDF8170C478E13B61` |
| `data\project-eagle\dating-sim\voices\manifest.json` | Manifest 144 câu thoại JP + SHA-256 + Seiyuu + transcript | `2E52D5CD8D793A6BDC1E57C8C74EB0137816AC999CE740FA298E4ADCBC90F388` |
| `data\project-eagle\dating-sim\voice_settings.json` | Cấu hình mặc định (`voice_enabled: true`, `voice_volume: 80`) | `18EC22AC5C172CDC369267B78338590B7BD329B344AAAC6DC09A79392BC18E9E` |

---

## 4. Hướng Dẫn Bật/Tắt & Phục Hồi (Rollback)

- **Tắt nhanh giọng nói trong lúc chơi (không cần sửa code):**
  - Gửi `POST http://127.0.0.1:8765/api/dating/voice_settings` với body `{"voice_enabled": false}` hoặc chỉnh `data/project-eagle/dating-sim/voice_settings.json`.
- **Rollback an toàn (nếu cần gỡ riêng tính năng JP Voice mà không ảnh hưởng nhân vật mới được hội thoại khác tích hợp sau đó):**
  - Vì `eagle_dating_sim.py` có thể đã được hội thoại song song (như `Columbina`) bổ sung thêm dòng sau thời điểm gắn hook, **không chép đè mù file `.before`** nếu file đã có thay đổi mới; chỉ cần đặt `"voice_enabled": false` hoặc xóa `eagle_waifulink_voice.py` (mọi điểm gọi trong `eagle_dating_sim.py` đều bọc `try/except` và kiểm tra `if self.voice_engine is None: return` nên game tự chạy êm 100% không phụ thuộc file âm thanh). Bản sao trước khi gắn hook vẫn được lưu đối chiếu tại `staging/project-eagle/waifulink-jp-voice-20261104/backups/`.
