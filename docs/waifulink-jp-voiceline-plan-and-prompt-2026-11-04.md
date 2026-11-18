# Kế Hoạch Kiến Trúc & Master Prompt: Hệ Thống Voiceline Tiếng Nhật (`WaifuLink JP Voice Engine v1.0`)

## Phần 1 — Kế Hoạch Kỹ Thuật (Dành Cho Người Dùng Nắm Tổng Quan)

### 1. Mục tiêu trải nghiệm
- Mang giọng lồng tiếng **tiếng Nhật (JP Seiyuu)** dễ thương, truyền cảm, chuẩn chất anime/Genshin vào **cả 4 ngữ cảnh** trong `gta sa gameplay-lab`:
  1. **Gặp Waifu ngoài map (`Ambient Proximity` & `House Visit Menu [F9]`)**: Khi Aether chạy xe/đi bộ lại gần cửa nhà bạn gái (`<= 22m`), cô ấy cất tiếng chào tiếng Nhật dễ thương (*"Oya? Aether~!"*, *"Yahhoo~!"*); khi mở menu trước cửa nhà (`[F9]`) phát câu mời đi chơi.
  2. **Chế độ Dạo Phố (`Free-Roam Chauffeur Outing` trên xe mui trần `575 Broadway`)**:
     - Lúc bắt đầu lên ghế phụ: câu hào hứng lên đường.
     - Lúc lái êm ái giữ hạng `S-Rank` (mỗi `40s`): câu ngân nga / khen ngợi dễ thương.
     - Lúc tông xe tụt máu `CVehicle` hoặc xe cháy `< 250 HP` phải sơ tán khẩn cấp (`EagleWaifuBridge.cs`): câu giật mình / nhắc nhở đáng yêu (*"Kyaa! Abunai!"*, *"Chotto matte!"*).
     - Lúc cán đích thành công (`S-Rank` / `A-Rank`): câu khen thưởng ngọt ngào.
  3. **Trong Kịch Bản Visual Novel (`Scenario Scene 1/4 .. 4/4` & `Extra Cameo`)**:
     - Mỗi khi mở Scene 1/4 hoặc chuyển sang Scene 2/4, 3/4, 4/4, hệ thống đọc nhãn cảm xúc (`mood` / `grade`) của cảnh đó để phát ngay 1 câu thoại tiếng Nhật khớp tông cảm xúc (vui vẻ, ngại ngùng đỏ mặt, trêu chọc tinh nghịch, hoặc dịu dàng lãng mạn ở kết cảnh 4/4), tự ngắt câu cũ khi người chơi bấm qua cảnh mới để không bao giờ chồng tiếng.
  4. **Tin nhắn Chat App 13 & Rơi Ảnh Kỷ Niệm (`Time-Apart Milestone Photo Drop`)**:
     - Phát tiếng chuông thông báo ngắn + câu nhắn giọng Nhật ngọt ngào khi bạn gái gửi ảnh kỷ niệm `M01..M15` lúc hai người ở xa nhau.

### 2. Nguồn tải Audio Tiếng Nhật & Phân loại Cảm Xúc (`8 Voice Buckets`)
- **Nguồn chính thống chất lượng phòng thu**: Tải trực tiếp các file `.ogg` Voice-Overs tiếng Nhật công khai từ **Genshin Impact Wiki (`genshin-impact.fandom.com/wiki/<Character>/Voice-Overs/Japanese` thông qua MediaWiki API)** — đúng 100% Seiyuu thật của từng nhân vật:
  - **Hu Tao**: CV *Takahashi Rie* (高橋李依)
  - **Furina**: CV *Minase Inori* (水瀬いのり)
  - **Citlali**: CV *Tago Natsumi* (田子夏美)
  - **Columbina**: CV *Lynn* (リン — kết hợp voice lines của Columbina / Damselette)
  - **Kirara**: CV *Suzushiro Sayumi* (鈴代紗弓)
  - **Vesna**: Ghép bộ giọng JP quý tộc kiêu kỳ ấm áp chuẩn anime (*Uesaka Sumire* / *Hayami Saori* / *Ishikawa Yui* từ Genshin Wiki) để đồng nhất chất lượng âm thanh.
- **Chuẩn hóa độ dài & âm lượng**: Chọn các câu ngắn gọn tự nhiên (`1.2s – 5.5s`), chuyển sang `.wav` PCM 16-bit `44.1kHz` (hoặc `.mp3`) lưu tại `data/project-eagle/dating-sim/voices/<char_id>/<bucket>_01.wav`, gồm **8 nhóm cảm xúc (`2–3` file/nhóm = `18–24` câu/nhân vật)** xoay vòng chống lặp (`round-robin` tránh phát trùng 2 lần liên tiếp):
  1. `greet_doorstep` — Gặp ngoài map (`<= 22m`) & mở menu `[F9]`.
  2. `vn_sweet_happy` — Cảnh VN / Chat vui vẻ, khen ngợi (`Delighted`, `Warm Playful`, `Cheerful`, `BEST`).
  3. `vn_shy_blush` — Cảnh VN / Chat bối rối, tsundere, đỏ mặt (`Blushing`, `Flustered`, `Tsundere`).
  4. `vn_playful_tease` — Cảnh VN / Chat tinh nghịch, cà khịa đáng yêu (`Playful`, `Mischievous`, `Sassy`).
  5. `vn_tender_love` — Cảnh kết `Scene 4/4` lãng mạn / Stage 4–5 sâu lắng (`Tender`, `Touched`, `Serene`, `Soulmate`).
  6. `outing_cruise` — Lên xe `575 Broadway` & câu thoại dạo phố êm ái.
  7. `outing_bump_rescue` — Xe va chạm hoặc sơ tán khỏi xe cháy `< 250 HP`.
  8. `outing_arrive_photo` — Tới điểm hẹn thành công & khi nhận ảnh kỷ niệm `Milestone Photo Drop`.

### 3. Kiến trúc phát âm thanh an toàn 100% (Không đụng Engine SFX cũ của GTA SA)
- Xây dựng module độc lập `Project Eagle/gta sa gameplay-lab/eagle_waifulink_voice.py` chạy trong tiến trình Sidecar `EagleCompanion.py`, sử dụng **Windows Multimedia API (`winmm.dll` -> `mciSendStringW` / `PlaySoundW`)**:
  - Không cài đặt plugin `.asi` rủi ro vào `gta_pe.exe`, không sửa `GENRL`/`SFX` của GTA SA -> **0% nguy cơ gây crash game**.
  - Hỗ trợ điều chỉnh âm lượng độc lập (`0..100%`, mặc định `80%`), tự động tắt tiếng khi `gta_pe.exe` mở Pause Menu (`0x00BA67A4 != 0`) hoặc thoát game, và tự ngắt câu trước (`stop wl_voice`) trước khi phát câu mới.
  - Cô lập hoàn toàn code trong `eagle_waifulink_voice.py`; khi đấu nối vào `EagleCompanion.py` và `eagle_dating_sim.py` chỉ cần giữ `game-write.lock` trong vài giây để thêm 4 lời gọi hook không xâm lấn.

---

## Phần 2 — Copy-Paste Prompt Cho Hội Thoại Mới (Triển Khai Voiceline Tiếng Nhật)

> Sao chép toàn bộ khối dưới đây và dán vào một hội thoại mới:

```markdown
# NHIỆM VỤ: Triển Khai Hệ Thống Voiceline Tiếng Nhật (`WaifuLink JP Voice Engine v1.0`) Cho Project Eagle (`gta sa gameplay-lab`)

Bạn phụ trách xây dựng trọn gói tính năng **Lồng Tiếng Nhật (JP Voice Pack)** cho dàn nhân vật bạn gái của **WaifuLink v4.0** (`hutao`, `furina`, `citlali`, `columbina`, `kirara`, `vesna`) trong `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`.
Người dùng không cần câu tiếng Nhật phải dịch sát từng chữ tiếng Anh trên màn hình; mục tiêu là **tải audio giọng Nhật thật sự dễ thương, đúng Seiyuu / đúng tính cách từng nhân vật, cắt/chọn câu ngắn gọn tự nhiên (1.2s–5.5s) và phát khớp mượt mà theo đúng ngữ cảnh cảm xúc** ở cả ngoài map (Ambient Doorstep), khi lái xe hẹn hò (Free-Roam Outing), khi xem kịch bản Visual Novel (Scenario Scene 1/4..4/4), và khi nhận tin nhắn/ảnh kỷ niệm!

Luôn giao tiếp với người dùng bằng **tiếng Việt**.

---

## 1. QUY TẮC BẮT BUỘC VỀ PHỐI HỢP ĐA HỘI THOẠI & KHÓA AN TOÀN (ĐỌC KỸ TRƯỚC KHI LÀM!)

Hiện đang có **3–4 hội thoại Antigravity chạy song song** trên cùng repo (tích hợp Furina, tích hợp Citlali, triển khai Columbina, và hội thoại Voiceline của bạn). Để KHÔNG BAO GIỜ ghi đè code của nhau hoặc giết nhầm `gta_pe.exe` khi hội thoại khác đang test:

1. Đọc ngay từ đầu:
   - `C:\Users\LENOVO\Desktop\GTA\AGENTS.md`
   - `C:\Users\LENOVO\Desktop\GTA\docs\project-eagle\shared-agent-workflow.md`
   - `C:\Users\LENOVO\Desktop\GTA\docs\project-eagle\waifulink-hutao-e2e-qa-and-app13-2026-11-03.md`
   - `C:\Users\LENOVO\Desktop\GTA\tools\eagle_coord_lock.py`
2. Tạo phiếu công việc riêng tại `docs/project-eagle/work-items/2026-11-04-antigravity-waifulink-jp-voicelines.md`.
3. **Làm việc nặng 100% NGOÀI KHÓA**:
   - Việc tìm/tải file âm thanh tiếng Nhật, chuẩn hóa `.wav`/`.mp3` vào `C:\Users\LENOVO\Desktop\GTA\data\project-eagle\dating-sim\voices\<char_id>\`, viết file module mới `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\eagle_waifulink_voice.py`, và viết unit test âm thanh độc lập phải làm hoàn toàn **NGOÀI KHÓA**!
   - Không chạm vào các file `eagle_waifulink_v4_furina.py`, `eagle_waifulink_v4_citlali.py`, `eagle_waifulink_v4_columbina.py`, `models/hud.txd`, `data/peds.ide`, hay các gói presentation `03/11`.
4. **Khi gắn hook vào `EagleCompanion.py` / `eagle_dating_sim.py`**:
   - Bắt buộc chiếm `game-write.lock` trước:
     `python "C:\Users\LENOVO\Desktop\GTA\tools\eagle_coord_lock.py" acquire game-write --chat "<CONVERSATION_ID>" --task "Wire JP Voice hooks" --wait 600`
   - **Đọc lại nội dung mới nhất trên đĩa** của `EagleCompanion.py` / `eagle_dating_sim.py` ngay sau khi chiếm khóa (vì hội thoại khác có thể vừa cập nhật thêm nhân vật!), chỉ thêm các lời gọi hook gọn sạch (`try/except` an toàn để nếu thiếu file audio không bao giờ văng lỗi), kiểm tra `py_compile`, rồi **release `game-write.lock` ngay lập tức**!
5. **Khi chạy kiểm thử In-Game (`gta_pe.exe` + `EagleCompanion.py` trên `:8765`)**:
   - **CẤM TUYỆT ĐỐI** chạy `taskkill /IM gta_pe.exe` hoặc xóa `data/eagle_companion.db` trước khi chiếm được `ingame-runtime.lock`!
   - Bắt buộc bọc toàn bộ script QA In-Game trong `with EagleCoordLock("ingame-runtime", chat="<CONVERSATION_ID>", task="JP Voice Live QA", wait_sec=900):` (từ `tools/eagle_coord_lock.py`). Trong khối `finally:` phải tắt sạch `gta_pe.exe` + `EagleCompanion.py` và reset sạch `data/eagle_companion.db` + `cleo/EaglePhoneHUD.dat` (`open=0`, `ev_active=0`).

---

## 2. YÊU CẦU CHI TIẾT VỀ DỮ LIỆU & TÍNH NĂNG

1. **Tải & Chuẩn Hóa Bộ Giọng Tiếng Nhật (`data/project-eagle/dating-sim/voices/<char_id>/`)**:
   - Tải các câu thoại tiếng Nhật thật (ưu tiên từ MediaWiki API của `genshin-impact.fandom.com/wiki/<Character>/Voice-Overs/Japanese` hoặc nguồn anime/Genshin voice-over công khai chất lượng cao) cho cả 6 nhân vật:
     - `hutao` (CV: Rie Takahashi), `furina` (CV: Inori Minase), `citlali` (CV: Natsumi Tago), `columbina` (CV: Lynn — nếu ít file thì bổ sung từ kho giọng JP dịu dàng cùng chất giọng), `kirara` (CV: Sayumi Suzushiro), `vesna` (chọn 1 giọng Seiyuu nữ quý tộc tinh nghịch cố định từ kho Genshin JP chưa dùng như Yelan/Jean/Eula/Navia để đồng bộ chất lượng studio).
   - Mỗi nhân vật cần tối thiểu **16–24 file audio thật** (`> 10 KB/file`, độ dài `1.0s – 6.0s`, tuyệt đối không tạo file sine-wave/beep giả!), chia đều vào **8 nhóm cảm xúc (`Voice Buckets`)**:
     - `greet_doorstep` (lại gần nhà `<= 22m` hoặc mở menu `[F9]`)
     - `vn_sweet_happy` (cảnh VN / chat vui vẻ, ngọt ngào, chọn đáp án `BEST`)
     - `vn_shy_blush` (cảnh VN / chat đỏ mặt, ngại ngùng, tsundere)
     - `vn_playful_tease` (cảnh VN / chat trêu chọc, tinh nghịch)
     - `vn_tender_love` (cảnh kết `Scene 4/4` lãng mạn / tâm sự sâu lắng)
     - `outing_cruise` (bắt đầu lên ghế phụ xe `575 Broadway` & câu thoại dạo phố êm ái mỗi `40s` có cooldown)
     - `outing_bump_rescue` (khi xe đụng tụt HP trong Free-Roam hoặc khi `EagleWaifuBridge` sơ tán khỏi xe cháy `< 250 HP`)
     - `outing_arrive_photo` (khi tới đích hẹn hò S/A-Rank hoặc khi nhận ảnh kỷ niệm `Time-Apart Milestone Photo Drop`)
   - Tạo `voices/manifest.json` lưu danh sách file, thời lượng (giây), SHA-256, Seiyuu và mô tả câu thoại.

2. **Xây dựng `eagle_waifulink_voice.py` (Phát qua Windows `winmm.dll` `mciSendStringW` / `PlaySoundW`)**:
   - Phát bất đồng bộ trên luồng nền nhẹ, có hàm `play_event(char_id, bucket, mood="", interrupt=True)`:
     - Khi chuyển cảnh VN (`Scene 1/4 -> 2/4 -> 3/4 -> 4/4`), `interrupt=True` ngắt ngay câu cũ để phát câu mới khớp với `mood` của cảnh hiện tại!
     - Khi đi dạo ngoài map (`greet_doorstep` cooldown `25s`, `outing_cruise` cooldown `40s`, `outing_bump_rescue` cooldown `3.5s`), không đè lên câu đang nói dở trừ trường hợp khẩn cấp (`outing_bump_rescue`).
     - Tự động kiểm tra nếu `gta_pe.exe` đang mở Pause Menu (`0x00BA67A4 != 0`) thì tạm ngưng phát.
     - Hỗ trợ bật/tắt & chỉnh âm lượng (`voice_enabled`, `voice_volume = 80`) qua API `/api/dating/voice_settings` và lưu cấu hình JSON.
     - Ghi telemetry `last_voice_played` (`char_id`, `bucket`, `file`, `timestamp`, `play_count`) vào `/api/state` (`dating_sim.voice_telemetry`) để kiểm tra tự động dễ dàng!

3. **Kiểm Thử Thực Tế & Bàn Giao**:
   - Kiểm tra 100% file audio của cả 6 nhân vật đọc được header hợp lệ, thời lượng thực `1.0s–7.0s`, độ lệch chuẩn biên độ âm thanh thực (không phải file câm hay sóng sin đơn điệu), và phát thành công qua `mciSendStringW`.
   - Dưới khóa `ingame-runtime.lock`, chạy kiểm thử thực tế với `gta_pe.exe` + `EagleCompanion.py` xác nhận telemetry `play_count` tăng đúng ở cả 4 ngữ cảnh: (1) lại gần cửa nhà waifu, (2) mở & đi qua 4 cảnh Scenario VN, (3) lên xe `575 Broadway` + va chạm + tới đích + nhận ảnh kỷ niệm, (4) `0` lỗi Lua (`cleo/EagleLuaErrors.log`), `0` crash, `eagle_doctor.py` `11/11 PASS`.
   - Cập nhật phiếu công việc & báo cáo tại `docs/project-eagle/waifulink-jp-voiceline-report-2026-11-04.md`, và đảm bảo đã nhả sạch cả `game-write.lock` lẫn `ingame-runtime.lock`!
```
