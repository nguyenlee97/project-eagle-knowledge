# Prompt Tách *Re:Zero Arc 7, Arc 8, Arc 9* Thành 18 Phim Chiếu Rạp Riêng Lẻ Theo Tập Light Novel (`Vol. 26` .. `Vol. 43`)

- **Mục tiêu:** Tách 3 đại tuyển tập Web Novel nguyên khối (`rezero_arc7_wn` `116` ch, `rezero_arc8_wn` `76` ch, `rezero_arc9_wn` `62` ch) thành **18 gói Phim Chiếu Rạp độc lập (`venue_type = "cinema"`)** theo đúng ranh giới **Light Novel Tập 26 đến Tập 43** của Shinichirou Otsuka, đồng thời giữ 3 gói nguyên khối `rezero_arc{7,8,9}_wn` làm **Sách Thư Viện độc quyền (`venue_type = "library"`)** trên kệ `LIB-01..15`.
- **Tái sử dụng tài nguyên `100%` (`0 MB` phình ổ đĩa):** Toàn bộ `254` chương Dual-Mode JSON, `1,250` bức CG `1376x768` (`cg_pending = 0`) và `35` bản nhạc nền `bgm/*.mp3` chuẩn Win32 MCI đã hoàn thiện sẵn 100% trong `D:\Eagle Literature Studio\packages\rezero_arc{7,8,9}_wn\`. Dùng NTFS Hardlink (`os.link`) trên ổ `D:` cho `cgs/*.jpg` & `bgm/*.mp3` và NTFS Directory Junction sang ổ `C:` để tốn **`0 MB` dung lượng trùng lặp**!
- **Tương thích tự động với Weekly Film Rollout (`v3.2`):** Ngay khi 18 gói phim Volume được cấp chứng chỉ `.cert.json` và gắn Junction vào `gameplay-lab\data\project-eagle\literature\packs\`, bộ xoay tua lịch chiếu tuần trong `eagle_literature_engine.py` (`10` phim/tuần ở Rạp Lớn, `6` phim/tuần ở Rạp Nhỏ, Shuffle-Bag chống trùng tuần trước) sẽ tự động nhận diện toàn bộ **25 bộ phim** (`6` phim *IF* + `18` phim *Arc 7–9 Volumes* + *Starlight*) mà không cần sửa code engine.

---

## Khối Prompt Sao Chép (Dán vào Hội thoại Mới tại `C:\Users\LENOVO\Desktop\GTA` hoặc `D:\Eagle Literature Studio`)

```markdown
Bạn là **Eagle Literature Volume-Film Splitter & Release Integrator**, phụ trách tách 3 bộ tiểu thuyết dài kỳ đã hoàn thiện tại `D:\Eagle Literature Studio\packages\` (`rezero_arc7_wn`, `rezero_arc8_wn`, `rezero_arc9_wn`) thành **18 bộ Phim Chiếu Rạp độc lập (`venue_type = "cinema"`)** dựa trên ranh giới từng tập Light Novel (`Volumes 26..43`), kiểm định chuẩn 7 cổng `EagleLit Pack v1.0`, cấp chứng chỉ Gatekeeper `.cert.json`, và tích hợp vào `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`.

### 1. TÀI LIỆU & LUẬT CỨNG BẮT BUỘC ĐỌC TRƯỚC KHI LÀM
1. Đọc kỹ:
   - `C:\Users\LENOVO\Desktop\GTA\AGENTS.md` và `docs\project-eagle\shared-agent-workflow.md`
   - `D:\Eagle Literature Studio\AGENTS.md` và `D:\Eagle Literature Studio\bootstrap\GTA_EAGLE_LIT_CONTRACT_V1.md`
   - `D:\Eagle Literature Studio\tools\validate_pack.py` và `C:\Users\LENOVO\Desktop\GTA\tools\deploy_literature_pack.py`
   - 3 file kế hoạch cụm chương gốc chứa ranh giới Volume chính xác:
     - `D:\Eagle Literature Studio\packages\rezero_arc7_wn\clusters\arc7_cluster_master_plan.json`
     - `D:\Eagle Literature Studio\packages\rezero_arc8_wn\clusters\arc8_cluster_master_plan.json`
     - `D:\Eagle Literature Studio\packages\rezero_arc9_wn\clusters\arc9_cluster_master_plan.json`
2. **LUẬT CỨNG AN TOÀN PHỐI HỢP & TẠO ẢNH (KHÔNG NGOẠI LỆ):**
   - **CẤM TUYỆT ĐỐI** gọi bất kỳ API tạo ảnh bên ngoài nào (OpenAI `gpt-image-*`, `dall-e-*`, v.v.) trừ khi tôi ra lệnh rõ ràng trong hội thoại này. Toàn bộ `1,250` CG cảnh phim của Arc 7, 8, 9 đã vẽ xong `100%` (`cg_pending = 0`) trên ổ `D:`, hãy tái sử dụng nguyên vẹn chúng! Nếu cần vẽ/biên tập mới bất kỳ bìa `poster.jpg` / `banner_16x9.jpg` nào, mặc định chỉ dùng `image-generator` nội bộ của Antigravity (dừng ngay nếu gặp `429`), hoặc trích xuất/chuyển thể chuẩn xác từ kho ảnh bìa & tranh màu Light Novel chính thức sẵn có tại `D:\Eagle Literature Studio\references\rezero_arc{7,8,9}\ln_volumes\vol26..vol43\` + các bức Key-Visual CG đỉnh cao của từng tập (lưu ý đảm bảo `poster.jpg` `832x1248` và `banner_16x9.jpg` `1376x768` là Baseline RGB JPEG và có **SHA-256 duy nhất không trùng byte** với bất kỳ file nào trong `cgs/*.jpg` để vượt qua Gate 5 của `validate_pack.py`!).
   - **Bảo vệ tiến trình đang chạy:** Trước khi ghi vào `gameplay-lab`, kiểm tra `Get-Process gta_pe -ErrorAction SilentlyContinue` và `python tools/eagle_coord_lock.py status`. **TUYỆT ĐỐI KHÔNG** tự ý kill `gta_pe.exe` hay `EagleCompanion.py`, và **KHÔNG** chạm vào `EagleCompanion.py` hay `hud.lua`.
   - **Bảo toàn 3 gói sách gốc cho Thư Viện (`LIB-01..15`):** Giữ nguyên vẹn 100% `rezero_arc7_wn`, `rezero_arc8_wn`, và `rezero_arc9_wn` với `venue_type = "library"` làm Sách Tuyển Tập Độc Quyền tại 15 Thư viện/Nhà sách (tuyệt đối không xóa gói gốc và không đưa 3 gói `_wn` nguyên khối này vào lịch chiếu Rạp Phim).

---

### 2. BẢNG ÁNH XẠ CHÍNH XÁC 18 BỘ PHIM THEO TẬP LIGHT NOVEL (`VOL. 26` .. `VOL. 43`)

Hãy viết script tự động hóa sạch sẽ tại `D:\Eagle Literature Studio\tools\build_rezero_volume_films.py` để sinh ra đúng **18 gói `EagleLit Pack v1.0`** dưới `D:\Eagle Literature Studio\packages\<work_id>\` theo bảng ranh giới chuẩn dưới đây:

#### A. Chuỗi Phim *Re:Zero Arc 7 — The Land of Wolves* (`8` Phim: `Vol. 26` .. `Vol. 33`, từ `packages/rezero_arc7_wn`)
1. **`rezero_arc7_vol26`** — `ch001..ch012` (`12` chương, `cluster_01`)
   - `title`: `"Re:Zero Arc 7 Film I (Vol. 26) - The Land of Wolves"`
   - `short_title`: `"Re:Zero Vol.26: Land of Wolves"`
   - Bối cảnh: Tỉnh dậy ở rừng Buddheim, Rem mất trí nhớ & Louis, trại quân Đế quốc, Abel & tộc Shudraq, săn đại xà Elgina.
2. **`rezero_arc7_vol27`** — `ch013..ch024` (`12` chương, `cluster_02`)
   - `title`: `"Re:Zero Arc 7 Film II (Vol. 27) - The Bloodless Siege of Guaral"`
   - `short_title`: `"Re:Zero Vol.27: Siege of Guaral"`
   - Bối cảnh: Flop & Medium, màn hóa trang vũ nữ Natsumi Schwartz - Bianca - Flora, hạ thành Guaral không đổ máu, Arakiya tập kích.
3. **`rezero_arc7_vol28`** — `ch025..ch039` (`15` chương, `cluster_03 + cluster_04`)
   - `title`: `"Re:Zero Arc 7 Film III (Vol. 28) - Demon City Chaosflame"`
   - `short_title`: `"Re:Zero Vol.28: Demon City Chaosflame"`
   - Bối cảnh: Đàm phán với Priscilla & Al, Quân sư Natsumi, tiến vào ma đô Chaosflame, Cửu Vĩ Hồ Yorna Mishigure & lời nguyền thu nhỏ của Olbart.
4. **`rezero_arc7_vol29`** — `ch040..ch054` (`15` chương, `cluster_05 + cluster_06`)
   - `title`: `"Re:Zero Arc 7 Film IV (Vol. 29) - Ten-Second Loop & Shadow Calamity"`
   - `short_title`: `"Re:Zero Vol.29: Shadow of Chaosflame"`
   - Bối cảnh: Shotabaru 10 tuổi, Hôn Nhân Linh Hồn của Yorna, vòng lặp 10 giây tử thần đấu Olbart, đại họa bóng tối nhấn chìm Chaosflame.
5. **`rezero_arc7_vol30`** — `ch055..ch066` (`12` chương, `cluster_07`)
   - `title`: `"Re:Zero Arc 7 Film V (Vol. 30) - Dragon General Madeline & Emilia Camp"`
   - `short_title`: `"Re:Zero Vol.30: Dragon General's Assault"`
   - Bối cảnh: Phi Long Tướng Madeline tấn công thành Guaral, nhóm Emilia - Beatrice - Ram - Garfiel vượt biên giới vào Vollachia.
6. **`rezero_arc7_vol31`** — `ch067..ch081` (`15` chương, `cluster_08 + cluster_09`)
   - `title`: `"Re:Zero Arc 7 Film VI (Vol. 31) - Gladiator Island Ginunhive"`
   - `short_title`: `"Re:Zero Vol.31: Gladiator Island"`
   - Bối cảnh: Đảo giác đấu Ginunhive, Weitz - Idra - Hiain, Cecilus 10 tuổi, cuộc thảm sát của Todd, thức tỉnh Cor Leonis & lập Quân đoàn Pleiades.
7. **`rezero_arc7_vol32`** — `ch082..ch102` (`21` chương, `cluster_10 + cluster_11`)
   - `title`: `"Re:Zero Arc 7 Film VII (Vol. 32) - Rebel March on Bastion Kugihari"`
   - `short_title`: `"Re:Zero Vol.32: March on Lupugana"`
   - Bối cảnh: Sự thật về hai Hoàng đế (Chisha Gold), giải cứu thành Kugihari, đoàn tụ với Beatrice, đại liên quân tiến về Đế đô.
8. **`rezero_arc7_vol33`** — `ch103..ch116` (`14` chương, `cluster_12`)
   - `title`: `"Re:Zero Arc 7 Film VIII (Vol. 33) - Siege of the Star-Shaped Capital"`
   - `short_title`: `"Re:Zero Vol.33: Siege of Lupugana"`
   - Bối cảnh: Đại chiến 5 pháo đài sao Đế đô Lupugana, Cecilus vs Arakiya, sự hy sinh của Chisha Gold & Đại Thảm Họa Sphinx trỗi dậy.

#### B. Chuỗi Phim *Re:Zero Arc 8 — Vincent Vollachia* (`5` Phim: `Vol. 34` .. `Vol. 38`, từ `packages/rezero_arc8_wn`)
9. **`rezero_arc8_vol34`** — `ch001..ch015` (`15` chương, `cluster_01 + cluster_02`)
   - `title`: `"Re:Zero Arc 8 Film I (Vol. 34) - The Undead Disaster & Empire Alliance"`
   - `short_title`: `"Re:Zero Vol.34: Undead Disaster"`
10. **`rezero_arc8_vol35`** — `ch016..ch028` (`13` chương, `cluster_03 + cluster_04`)
    - `title`: `"Re:Zero Arc 8 Film II (Vol. 35) - Coupled Dragon Carriages & Spica"`
    - `short_title`: `"Re:Zero Vol.35: Naming Spica"`
11. **`rezero_arc8_vol36`** — `ch029..ch044` (`16` chương, `cluster_05 + cluster_06`)
    - `title`: `"Re:Zero Arc 8 Film III (Vol. 36) - Iris and the King of Thorns"`
    - `short_title`: `"Re:Zero Vol.36: King of Thorns"`
12. **`rezero_arc8_vol37`** — `ch045..ch061` (`17` chương, `cluster_07 + cluster_08`)
    - `title`: `"Re:Zero Arc 8 Film IV (Vol. 37) - Battle of the Five Bastions"`
    - `short_title`: `"Re:Zero Vol.37: Five Bastions"`
13. **`rezero_arc8_vol38`** — `ch062..ch076` (`15` chương, `cluster_09 + cluster_10`)
    - `title`: `"Re:Zero Arc 8 Film V (Vol. 38) - Curtain's Close: Priscilla Barielle"`
    - `short_title`: `"Re:Zero Vol.38: Priscilla Barielle"`

#### C. Chuỗi Phim *Re:Zero Arc 9 — Light of the Nameless Star* (`5` Phim: `Vol. 39` .. `Vol. 43`, từ `packages/rezero_arc9_wn`)
14. **`rezero_arc9_vol39`** — `ch001..ch014` (`14` chương, `cluster_01 + cluster_02`)
    - `title`: `"Re:Zero Arc 9 Film I (Vol. 39) - Light of the Nameless Star & Ol Shamak"`
    - `short_title`: `"Re:Zero Vol.39: Ol Shamak Seal"`
15. **`rezero_arc9_vol40`** — `ch015..ch024` (`10` chương, `cluster_03 + cluster_04`)
    - `title`: `"Re:Zero Arc 9 Film II (Vol. 40) - Reinhard vs Al & Book of the Dead"`
    - `short_title`: `"Re:Zero Vol.40: Reinhard vs Al"`
16. **`rezero_arc9_vol41`** — `ch025..ch037` (`13` chương, `cluster_05 + cluster_06`)
    - `title`: `"Re:Zero Arc 9 Film III (Vol. 41) - Witch of Tristitia & Rem's Awakening"`
    - `short_title`: `"Re:Zero Vol.41: Rem's Awakening"`
17. **`rezero_arc9_vol42`** — `ch038..ch050` (`13` chương, `cluster_07 + cluster_08`)
    - `title`: `"Re:Zero Arc 9 Film IV (Vol. 42) - The Aldebusters & Volcanica"`
    - `short_title`: `"Re:Zero Vol.42: The Aldebusters"`
18. **`rezero_arc9_vol43`** — `ch051..ch062` (`12` chương, `cluster_09 + cluster_10`)
    - `title`: `"Re:Zero Arc 9 Film V (Vol. 43) - Ten Thousand Loops & The Great Reset"`
    - `short_title`: `"Re:Zero Vol.43: The Great Reset"`

---

### 3. QUY TRÌNH KỸ THUẬT CHI TIẾT (4 BƯỚC CHUẨN XÁC)

#### Bước 1: Kiểm định gói sách `rezero_arc9_wn` (`library`)
- Kiểm tra `D:\Eagle Literature Studio\packages\rezero_arc9_wn\` qua `tools\validate_pack.py` và `tools\build_preview_html.py` để đảm bảo cả 3 đại tuyển tập Sách Thư Viện (`rezero_arc7_wn`, `rezero_arc8_wn`, `rezero_arc9_wn`) đều đạt **`PASS` (`0` errors)** với `venue_type = "library"`.

#### Bước 2: Đóng gói tự động 18 Phim Volume (`D:\Eagle Literature Studio\packages\rezero_arc{7,8,9}_vol{26..43}\`)
Với mỗi gói Volume Film:
1. **`manifest.json`:**
   - Đặt `"schema_version": "eagle_lit_v1"`, `"work_id": "<vol_work_id>"`, **`"venue_type": "cinema"`**, **`"default_read_mode": "adv_cinema"`**, `"supported_read_modes": ["adv_cinema", "nvl_book"]`.
   - Đánh số lại danh sách `"chapters"` từ `index = 1..M` (`chapters/ch01.json` .. `chapters/chMM.json` hoặc giữ tên file sạch CFont ASCII), đồng thời sao chép tương ứng `sources/<vol_work_id>/raw_chapters/` từ `sources/rezero_arc{7,8,9}_wn/raw_chapters/` để Gate 2 (`Verbatim Coverage 99%–100%`) của `validate_pack.py` đối chiếu khớp tuyệt đối `100%`!
   - Lọc chính xác `"cast"`, `"cg_catalog"`, và `"bgm_catalog"` chỉ giữ các nhân vật, bức CG và bản BGM thực sự xuất hiện trong các chương thuộc Volume đó (`0` orphan CG/BGM!).
   - Tính chuẩn `"economy"` (`cinema_ticket_usd = 25`, `estimated_minutes` theo tổng từ / tốc độ đọc) và bảng màu `"theme_color_rgb"` đặc trưng cho từng Volume.
2. **Liên kết `cgs/` và `bgm/` Không Tốn Dung Lượng Ổ `D:`:**
   - Dùng **NTFS Hardlink (`os.link`)** từ `packages/rezero_arc{7,8,9}_wn/cgs/<file>.jpg` sang `packages/<vol_work_id>/cgs/<file>.jpg` và tương tự cho `bgm/*.mp3` -> tốn **`0 MB`** dung lượng thêm trên ổ `D:` mà mọi công cụ đọc file vẫn thấy file vật lý độc lập!
3. **Thiết lập `poster.jpg` (`832x1248` `2:3`) & `banner_16x9.jpg` (`1376x768` `16:9`) + `cg_generation_manifest.json`:**
   - Tận dụng ảnh bìa màu chính thức của đúng Tập Light Novel tương ứng (`references/rezero_arc{7,8,9}/ln_volumes/vol26..vol43/`, kiểm tra từng tấm bằng `read_file` để chọn tấm bìa không dính chữ/barcode xấu hoặc crop vùng nhân vật đẹp nhất) cho `poster.jpg` (`832x1248`, RGB Baseline JPEG), và tạo `banner_16x9.jpg` (`1376x768`, RGB Baseline JPEG) từ tranh spread màu đầu tập hoặc tinh chỉnh nhẹ độ tương phản/vignette điện ảnh từ bức Key-Visual CG tiêu biểu nhất của tập đó sao cho **SHA-256 của `banner_16x9.jpg` và `poster.jpg` là duy nhất (`0` trùng SHA-256 với `cgs/*.jpg`)** và mặt nhân vật nằm gọn trong dải `y = 0.08..0.75`.
   - Sinh `cg_generation_manifest.json` ghi nhận đầy đủ `"status": "done"` cho `poster`, `banner_16x9` và toàn bộ `cgs/*` của Volume.
4. **Chạy đủ 7 Cổng Kiểm Định Studio:**
   - Chạy `tools/cfont_sanitizer.py`, `tools/build_preview_html.py`, và `tools/validate_pack.py` trên toàn bộ **18 gói Volume** cho tới khi cả `18/18` file `validation_report.json` đều báo **`PASS` (`0` errors)**.

#### Bước 3: Cấp Chứng Chỉ Gatekeeper `.cert.json` & Viết `waifu_discussion_hooks`
- Chạy kiểm định sẵn sàng tích hợp GTA (4 cổng: Schema/Sync, CFont ASCII, Raster D3D9 Baseline JPEG, Win32 MCI Audio Probe) và xuất chứng chỉ `READY_FOR_INTEGRATION` tại `C:\Users\LENOVO\Desktop\GTA\data\project-eagle\literature\certifications\<work_id>.cert.json` cho:
  - `rezero_arc9_wn.cert.json` (`venue_type = "library"` — đưa lên kệ sách `LIB-01..15` cạnh `Arc 7` & `Arc 8`), và
  - Toàn bộ **18 gói phim Volume** (`rezero_arc7_vol26.cert.json` .. `rezero_arc9_vol43.cert.json`, `venue_type = "cinema"`).
- Bổ sung `waifu_discussion_hooks` (100% printable ASCII sạch `CFont`, không chứa `~ | *`) cho `rezero_arc9_wn` và 18 phim Volume vào `C:\Users\LENOVO\Desktop\GTA\tools\deploy_literature_pack.py` & `schedule_and_catalog.json`.

#### Bước 4: Gắn NTFS Junction & Tích Hợp Vào `gameplay-lab` Dưới Khóa `game-write.lock`
- Kiểm tra `Get-Process gta_pe` (không tự ý kill game!) và giữ `EagleCoordLock("game-write")`:
  - Tạo NTFS Directory Junction (`0 MB` trên ổ `C:`) trong `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\data\project-eagle\literature\packs\` cho `rezero_arc9_wn` và toàn bộ `18` gói `rezero_arc{7,8,9}_vol{26..43}`.
  - Cập nhật `schedule_and_catalog.json`:
    - Thêm `rezero_arc9_wn` + `18` gói Volume vào `certified_works`.
    - Đưa `rezero_arc9_wn` lên kệ sách `LIB-01..15` (cùng `rezero_arc7_wn` & `rezero_arc8_wn`), **giữ nguyên quy tắc 0 gói `_wn` nguyên khối trong `cinema_schedules`** và giữ nguyên cấu hình xoay tua tuần (`weekly_rollout_policy`: Rạp Lớn `10` phim/tuần, Rạp Nhỏ `6` phim/tuần).
- Chạy kiểm tra offline (`verify_m5_overhaul.py` + `eagle_doctor.py --doctor --json` `11/11 PASS`), tạo script rollback riêng cho đợt tích hợp Volume Films, giải phóng khóa và ghi phiếu bàn giao trong `docs/project-eagle/work-items/`.
```
