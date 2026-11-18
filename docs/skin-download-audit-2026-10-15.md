# Tải và kiểm tra skin — 15/10/2026

Snapshot cập nhật UTC: 2026-10-17T18:27:43.449120+00:00. Đây là kiểm tra file trong staging; chưa cài game.

Final FAD-27–31 local reconciliation: 44/45 canonical source rows have a local archive candidate. All 47 completed archive candidates matched their staged copies by size/SHA-256 and passed 7-Zip plus trusted inspector archive-integrity checks. Seven rows have internal DFF/TXD naming review notes that do not establish wrong-character identity. March 7th Hunt is a separate incomplete-resource review (no TXD); Promeia has no local completed archive after bounded matching and was not classified as VIP. No visual identity or in-game behavior was tested; no game files were changed. Frozen FAD groups end at FAD-31; no new groups are open.

| Nhóm nguồn | Nguồn cần tải hiện tại | Đã tải + mở archive | Trạng thái còn lại |
| --- | ---: | ---: | --- |
| catalogs | 317 | 310 | downloaded_inspection_issue: 7 |
| libertycity | 464 | 450 | downloaded_inspection_issue: 10; blocked_public_age_verification_gate: 3; metadata_only_policy_hold_source_identity_matched: 1 |
| creators | 290 | 253 | downloaded_inspection_issue: 35; replaced_by_user_selected_alternative: 1; handoff_no_archive: 1 |
| User-skipped theo yêu cầu | 28 | 0 | Đã loại khỏi hàng đợi; giữ quyết định và trạng thái trước khi bỏ trong evidence/user-skipped-sources-2026-10-16.json, user-skipped-sources-2026-10-17.json, user-skipped-sources-2026-10-18.json |

Manifest gốc: **977** job canonical; sau **28** nguồn người dùng bỏ, còn **953** job gốc. Bổ sung **67** nguồn Genshin Fad và **55** nguồn HSR/ZZZ Fad; tổng hiện cần xử lý là **1071** (gốc + hai phần bổ sung). Trạng thái và lịch sử gốc của nguồn bị bỏ được giữ lại; điểm đánh giá gốc không bị ghi đè.
Genshin Fad: **73** nguồn có rating theo yêu cầu nữ=Thích/nam=Hơi thích; **6** nguồn còn cần xác minh danh tính/giới tính; **1** nguồn đã được thay bằng lựa chọn người dùng, không tính là tải đúng source gốc.
HSR/ZZZ Fad: **55** HSR card (37 mới, 17 đã có trong FAD; 1 weapons pack loại khỏi skin) và **25** ZZZ card (18 mới, 6 đã có trong FAD, 1 đã tải/kiểm tra). Có **55** nguồn mới chờ đánh giá; trang nguồn không đồng nghĩa link archive. Danh sách 80 card và coverage nằm tại creators/manual-downloads/hsr-zzz-fad-status.html.

Archive có file và báo cáo mở: **1050 hash riêng**, tổng **4.897 GB**.
Trong archive tải về có **2755 lượt cặp**, gộp hash còn **2560 cặp DFF+TXD**. Trùng 98 cặp cũ. Cộng 236 cặp cũ được kiểm tra lại, inventory có **2698 cặp hash riêng**.
Hash archive khớp hash công khai trên trang nguồn: 456 nguồn; 0 trường hợp không khớp cần xem lại. Đây là đối chiếu đúng file, không phải kết quả quét virus.

## Liên kết đánh giá và tài nguyên

Có 2165 cặp vừa liên kết được đánh giá vừa có Skin plugin được bộ đọc nhận diện. 459 cặp còn cần xác định member/biến thể. 51 cặp được xác định là vũ khí/phụ kiện, không cộng vào NPC. Không mặc định mọi member trong pack yêu thích đều được duyệt.
Nhóm Thích có **57 cặp <2.000.000 byte DFF+TXD** đã liên kết đánh giá; 54 cặp không có cảnh báo từ bộ đọc cấu trúc. Chưa thử rig hoặc game.
Pool Bình thường hoặc member archive nhẹ đã duyệt có 1608 cặp hash riêng. Các nguồn trùng Thích vẫn giữ provenance dùng ở vùng còn lại theo yêu cầu.

## Những trường hợp cần kiểm tra tiếp

1065 cặp có cảnh báo cấu trúc/texture; 129 DFF chưa xác định được TXD. Cảnh báo chưa phải kết luận skin hỏng và không tự đổi đánh giá.
Cảnh báo: {"missing_material_textures": 722, "geometry_without_normals": 287, "no_skin_plugin_found": 61, "pairing_requires_review": 14, "no_native_textures": 1, "target_game_requires_review": 2, "metadata_requires_review": 5}.

Chi tiết nguồn lỗi, archive, member, hash và tài nguyên nằm trong evidence/skin-download-audit-2026-10-15.json. Quy tắc phân vùng mới được ghi ở skin-fill-rule-2026-10-15.md. Chưa chốt phép phủ 403/1.235 ID khi vòng tải và xác định member chưa xong.

## Dung lượng thực tế để cân nhắc

MB trong bảng = 1.000.000 byte. Size cặp là toàn bộ DFF + TXD, không lấy trung bình archive cho từng nhân vật; TXD dùng chung vẫn tính cả dictionary cho mỗi lựa chọn.

| Tập dữ liệu | Số cặp | Trung vị DFF+TXD | P95 | Lớn nhất |
| --- | ---: | ---: | ---: | ---: |
| NPC Eagle, snapshot 14/10 | 1638 | 0.148 MB | 0.458 MB | 5.355 MB |
| Ứng viên đã có file và Skin plugin, lượt này | 2165 | 2.359 MB | 23.454 MB | 120.530 MB |

Phân bố ứng viên: {"<2 MB": 591, "2–5 MB": 1005, "≥10 MB": 312, "5–10 MB": 257}.
Snapshot Eagle giữ nguyên hash roster và chỉ mục COMPONENTPEDS tại lần kiểm tra này; không quét lại toàn bộ payload game. So sánh dung lượng không dự đoán FPS hoặc mức RAM/VRAM trong game.

## Các cặp NPC lớn nhất đã có file

| Nhân vật / nguồn | Đánh giá | DFF | TXD | DFF+TXD | Triangle | Texture lớn nhất |
| --- | --- | ---: | ---: | ---: | ---: | ---: |
| KAITO | somewhat | 3.722 MB | 116.807 MB | 120.530 MB | 59,720 | 2048 px |
| Maki Zenin | neutral | 1.770 MB | 93.587 MB | 95.356 MB | 27,770 | 4096 px |
| Maki Zenin | neutral | 1.596 MB | 93.587 MB | 95.182 MB | 24,766 | 4096 px |
| Maki Zenin | neutral | 1.573 MB | 93.587 MB | 95.160 MB | 24,523 | 4096 px |
| Maki Zenin | neutral | 1.438 MB | 93.587 MB | 95.025 MB | 24,860 | 4096 px |
| Ikuyo Kita | like | 1.940 MB | 92.904 MB | 94.844 MB | 27,762 | 2048 px |
| Citlali | like | 2.654 MB | 50.334 MB | 52.988 MB | 35,175 | 2048 px |
| Citlali | like | 2.554 MB | 50.332 MB | 52.886 MB | 33,966 | 2048 px |
| Ororon | somewhat | 2.405 MB | 50.332 MB | 52.737 MB | 30,801 | 2048 px |
| Kinich | somewhat | 2.320 MB | 50.332 MB | 52.652 MB | 31,049 | 2048 px |
| Koleda | like | 1.861 MB | 50.332 MB | 52.194 MB | 25,092 | 2048 px |
| Noa | somewhat | 1.609 MB | 50.332 MB | 51.941 MB | 28,022 | 2048 px |
| Noa | somewhat | 1.446 MB | 50.332 MB | 51.778 MB | 31,418 | 2048 px |
| Usada Pekora | like | 4.492 MB | 45.091 MB | 49.583 MB | 85,146 | 4096 px |
| Narita Brian | somewhat | 4.583 MB | 42.992 MB | 47.575 MB | 82,153 | 2048 px |
| Satoru Gojo | neutral | 1.468 MB | 39.060 MB | 40.528 MB | 27,159 | 4096 px |
| Fuuka Yamagishi | somewhat | 0.990 MB | 34.626 MB | 35.616 MB | 17,561 | 2048 px |
| Vesna | like | 4.334 MB | 29.710 MB | 34.043 MB | 70,702 | 1024 px |
| Vesna | like | 4.334 MB | 29.710 MB | 34.043 MB | 70,702 | 1024 px |
| Vesna | like | 4.334 MB | 29.710 MB | 34.043 MB | 70,702 | 1024 px |
