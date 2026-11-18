# Tóm tắt toàn bộ skin FadXploit đã xử lý

Ảnh chụp: **18/10/2026**. Phạm vi là các nguồn FadXploit canonical; không tính nguồn từ host khác vào mẫu số. Có **306 nguồn**: 184 nguồn nền + 67 nguồn Genshin bổ sung + 55 nguồn HSR/ZZZ bổ sung. Trong đó 293 nguồn thuộc 31 nhóm FAD-01–31; 13 nguồn đã được kiểm tra trước khi lập nhóm.

## Trạng thái nguồn

| Kết quả chi tiết theo tiến độ nhóm | Số nguồn |
|---|---:|
| Đã có base archive và 4 cặp DFF/TXD; còn static review | 2 |
| Tải và kiểm tra tĩnh | 216 |
| Có mục kiểm tra | 10 |
| Archive integrity và inspector đã qua | 53 |
| Chưa tìm thấy archive sau khi quét | 1 |
| Resource dẫn xuất đã kiểm tra; archive gốc còn unverified | 2 |
| Thay bằng lựa chọn của người dùng | 1 |
| Bỏ vì ngoại hình | 2 |
| Bỏ qua archive mã hóa theo yêu cầu | 1 |
| Bỏ VIP/premium theo yêu cầu | 18 |

Có **284 source row** gắn với **301 archive records**; trong số đó một source bị bỏ qua vẫn có archive vật lý giữ nguyên. Mẫu số hiện cần xử lý là **285**, trong đó 283 source có archive; 300 archive records thuộc nguồn chưa bị loại khỏi hàng đợi. Cả 301 đường dẫn cục bộ còn tồn tại và kích thước khớp metadata đã lưu. Có 300 hash SHA-256 cục bộ đã lưu (1,564.19 MB sau khử trùng lặp; gồm archive vật lý của Rosaria đã bỏ). Hash cục bộ không được coi là SHA công bố từ publisher.

Bản audit tổng hợp cũ dùng nhãn rộng hơn (**248 downloaded_inspected, 35 downloaded_inspection_issue, 21 user_skipped, 1 replacement, 1 handoff_no_archive**). Nó gộp nhiều trạng thái `variant_review`/integrity vào nhãn rộng; bảng chi tiết theo nhóm ở báo cáo này giữ riêng các trạng thái đó.

Bảng chi tiết giữ 13 nguồn đã được manifest đóng băng liệt kê là đã kiểm tra trước khi lập nhóm; các nhãn audit cũ vẫn được giữ riêng theo từng nguồn để thấy sự khác biệt giữa hai bản ghi. Trong nhóm thủ công, 13 nguồn đang mang nhãn `downloaded_inspection_issue`. Các nguồn FAD-08 Len/KAITO có thêm tài nguyên dẫn xuất đã phục hồi và được kiểm tra; archive ZIP gốc vẫn được giữ trạng thái integrity chưa xác minh.

Có **21 nguồn bị người dùng bỏ qua**: 18 VIP/premium, 2 vì ngoại hình, và 1 archive mã hóa. Rosaria bị bỏ theo chỉ dẫn “Bỏ luôn”; archive 7z vật lý vẫn được giữ, integrity vẫn unverified, và dòng này đã rời mẫu số hiện cần xử lý. Hai source Fatui Cryogunner và Hydrogunner là các lựa chọn ngoại hình duy nhất; không áp dụng NoUse cho Fatui khác. Jean được thay bằng lựa chọn người dùng; archive thay thế không cộng vào kho Fad-only. Promeia vẫn chưa có archive sau bounded local scan và không bị gán VIP.

Người dùng chấp nhận **18 source association theo tên archive**: 17 dòng từng bị `variant_review` và một ghi chú tên nội bộ bổ sung của Fenny Lionheart. Quy tắc này chỉ bỏ hold về tên bên trong archive; member names vẫn được giữ làm metadata, không xác nhận ngoại hình hoặc danh tính model. Có **31 nguồn với tổng 78 DFF không ghép cặp**; 8 nguồn không có cặp xác nhận nào. Cảnh báo ghép cặp đó được giữ riêng.

Belle và March 7th Hunt hiện đều có full base archive cùng optional Breast Physics DFF add-on. Mỗi cặp source có 4 biến thể DFF/TXD, không còn DFF chưa ghép: Belle dùng TXD 4,217,292 bytes; March 7th Hunt dùng TXD 3,518,056 bytes. Hai cặp shadeless của mỗi source có cảnh báo geometry_without_normals; các archive đều qua integrity, còn tương thích trong game chưa thử.

## Tài nguyên DFF/TXD

Các archive liên kết **724 lần xuất hiện** và **659 liên kết source/hash riêng biệt**, gộp thành **657 cặp hash DFF/TXD duy nhất**. Có 653 cặp được parser đánh dấu ứng viên ped tĩnh; 4 cặp chưa được gắn nhãn ứng viên ped (cảnh báo chính là thiếu skin plugin); không có cặp nào được xác định là vũ khí/phụ kiện. Có 657 hash DFF và 295 hash TXD, tổng **4,580.91 MB** sau khử trùng lặp theo file hash.

Kích thước cặp DFF+TXD theo từng biến thể: trung vị 13.52 MB; nhỏ nhất 2.09 MB; lớn nhất 52.89 MB. Phân bố: <2 MB: 0, 2–5 MB: 140, 5–10 MB: 116, ≥10 MB: 401. Mỗi cặp tính đủ TXD cho biến thể đó; các biến thể có hash khác nhau được giữ riêng. Cặp dưới 2 MB: 0.

Những cặp lớn nhất:

| Nhân vật/nguồn | DFF+TXD |
|---|---:|
| Citlali (Genshin Impact) | 52.89 MB |
| Ellen Joe (Zenless Zone Zero) | 52.46 MB |
| Ellen Joe (Zenless Zone Zero) | 52.46 MB |
| Castorice (Honkai: Star Rail) | 37.14 MB |
| Castorice (Honkai: Star Rail) | 36.50 MB |

Cảnh báo parser trên các cặp hash duy nhất (các loại có thể chồng lấp): `geometry_without_normals` 225, `missing_material_textures` 4, `no_skin_plugin_found` 4, `pairing_requires_review` 6.

## Các điểm cần xem lại

- **DFF/TXD pairing warning — Jinhsi (Earlier inspected source (outside FAD-01–31), `0bd8e33530d9a3e2`):** The saved source inspection records 2 DFF variant(s) without a corresponding confirmed DFF/TXD pair. This is a resource-pairing review item; it does not by itself establish archive corruption or wrong character identity. [source page](https://fadxploit.my.id/gtasa/jinhsi-wuthering-waves/)
- **DFF/TXD pairing warning — Charolic (FAD-03, `1ec477c84f2d1d55`):** The saved source inspection records 2 DFF variant(s) without a corresponding confirmed DFF/TXD pair. This is a resource-pairing review item; it does not by itself establish archive corruption or wrong character identity. [source page](https://fadxploit.my.id/gtasa/charolic-girls-frontline-2-exilium/)
- **DFF/TXD pairing warning — Chasca (FAD-02, `2241e2fb66703e34`):** The saved source inspection records 3 DFF variant(s) without a corresponding confirmed DFF/TXD pair. This is a resource-pairing review item; it does not by itself establish archive corruption or wrong character identity. [source page](https://fadxploit.my.id/gtasa/chasca-genshin-impact/)
- **DFF/TXD pairing warning — Jingliu (FAD-05, `37294229ad27c448`):** The saved source inspection records 2 DFF variant(s) without a corresponding confirmed DFF/TXD pair. This is a resource-pairing review item; it does not by itself establish archive corruption or wrong character identity. [source page](https://fadxploit.my.id/gtasa/jingliu-honkai-star-rail/)
- **DFF/TXD pairing warning — Leva (UMP45) (Earlier inspected source (outside FAD-01–31), `399977046a5c2df8`):** The saved source inspection records 2 DFF variant(s) without a corresponding confirmed DFF/TXD pair. This is a resource-pairing review item; it does not by itself establish archive corruption or wrong character identity. [source page](https://fadxploit.my.id/gtasa/leva-ump45-girls-frontline-2-exilium/)
- **DFF/TXD pairing warning — Akeha (FAD-07, `491e995ab93e0f65`):** The saved source inspection records 2 DFF variant(s) without a corresponding confirmed DFF/TXD pair. This is a resource-pairing review item; it does not by itself establish archive corruption or wrong character identity. [source page](https://fadxploit.my.id/gtasa/akeha-summer-assassin-nier-reincarnation/)
- **DFF/TXD pairing warning — Klukai (FAD-03, `510fbc93e7128be4`):** The saved source inspection records 2 DFF variant(s) without a corresponding confirmed DFF/TXD pair. This is a resource-pairing review item; it does not by itself establish archive corruption or wrong character identity. [source page](https://fadxploit.my.id/gtasa/klukai-girls-frontline-2-exilium/)
- **DFF/TXD pairing warning — Zhu Yuan (Earlier inspected source (outside FAD-01–31), `564639fbd106a004`):** The saved source inspection records 2 DFF variant(s) without a corresponding confirmed DFF/TXD pair. This is a resource-pairing review item; it does not by itself establish archive corruption or wrong character identity. [source page](https://fadxploit.my.id/gtasa/zhu-yuan-zenless-zone-zero/)
- **DFF/TXD pairing warning — Sinon Bikini (FAD-11, `8cb0be46b9da5e8d`):** The saved source inspection records 4 DFF variant(s) without a corresponding confirmed DFF/TXD pair. This is a resource-pairing review item; it does not by itself establish archive corruption or wrong character identity. [source page](https://fadxploit.my.id/gtasa/sinon-bikini-sword-art-online-variant-showdown-sword-art-online/)
- **DFF/TXD pairing warning — Mavuika (FAD-02, `90a9423247e7786c`):** The saved source inspection records 1 DFF variant(s) without a corresponding confirmed DFF/TXD pair. This is a resource-pairing review item; it does not by itself establish archive corruption or wrong character identity. [source page](https://fadxploit.my.id/gtasa/mavuika-genshin-impact/)
- **DFF/TXD pairing warning — Fu Xuan (FAD-05, `9db85ebdbe3ca75a`):** The saved source inspection records 2 DFF variant(s) without a corresponding confirmed DFF/TXD pair. This is a resource-pairing review item; it does not by itself establish archive corruption or wrong character identity. [source page](https://fadxploit.my.id/gtasa/fu-xuan-honkai-star-rail/)
- **DFF/TXD pairing warning remains after source-name acceptance — Lan Yan (FAD-22, `GEN-FAD-1937d9fcbe38eee0`):** The user accepted the archive filename and frozen group membership as source association. 4 DFF variant(s) remain unpaired in the saved inspection; this technical warning remains separate from the removed member-name identity hold. [source page](https://fadxploit.my.id/gtasa/lan-yan-genshin-impact/)
- **DFF/TXD pairing warning remains after source-name acceptance — Kamisato Ayato (FAD-22, `GEN-FAD-292596f6910d8c17`):** The user accepted the archive filename and frozen group membership as source association. 4 DFF variant(s) remain unpaired in the saved inspection; this technical warning remains separate from the removed member-name identity hold. [source page](https://fadxploit.my.id/gtasa/kamisato-ayato-custom-tuxedo-genshin-impact/)
- **DFF/TXD pairing warning — Varesa (FAD-25, `GEN-FAD-41438d34ec3c0f1f`):** The saved source inspection records 1 DFF variant(s) without a corresponding confirmed DFF/TXD pair. This is a resource-pairing review item; it does not by itself establish archive corruption or wrong character identity. [source page](https://fadxploit.my.id/gtasa/varesa-genshin-impact/)
- **DFF/TXD pairing warning — Chevreuse (FAD-19, `GEN-FAD-4ccad8f5f39e72b7`):** The saved source inspection records 3 DFF variant(s) without a corresponding confirmed DFF/TXD pair. This is a resource-pairing review item; it does not by itself establish archive corruption or wrong character identity. [source page](https://fadxploit.my.id/gtasa/chevreuse-genshin-impact/)
- **DFF/TXD pairing warning — Nefer (FAD-23, `GEN-FAD-84be8950c5eb5812`):** The saved source inspection records 2 DFF variant(s) without a corresponding confirmed DFF/TXD pair. This is a resource-pairing review item; it does not by itself establish archive corruption or wrong character identity. [source page](https://fadxploit.my.id/gtasa/nefer-genshin-impact/)
- **DFF/TXD pairing warning remains after source-name acceptance — Kamisato Ayato (FAD-21, `GEN-FAD-e3afceeaf693aaf0`):** The user accepted the archive filename and frozen group membership as source association. 2 DFF variant(s) remain unpaired in the saved inspection; this technical warning remains separate from the removed member-name identity hold. [source page](https://fadxploit.my.id/gtasa/kamisato-ayato-genshin-impact/)
- **DFF/TXD pairing warning — Shenhe (FAD-24, `GEN-FAD-ebb421e6ca56a780`):** The saved source inspection records 2 DFF variant(s) without a corresponding confirmed DFF/TXD pair. This is a resource-pairing review item; it does not by itself establish archive corruption or wrong character identity. [source page](https://fadxploit.my.id/gtasa/shenhe-custom-bikini-genshin-impact/)
- **DFF/TXD pairing warning — Tsukishiro Yanagi (FAD-31, `HSR-ZZZ-FAD-17ddbc858e448907`):** The saved source inspection records 6 DFF variant(s) without a corresponding confirmed DFF/TXD pair. This is a resource-pairing review item; it does not by itself establish archive corruption or wrong character identity. [source page](https://fadxploit.my.id/gtasa/tsukishiro-yanagi-zenless-zone-zero/)
- **base package and shared-TXD pairs verified; static geometry review remains — March 7th Hunt (FAD-28, `HSR-ZZZ-FAD-64de4f95d36005c6`):** The full base archive and optional Breast Physics DFF archive both passed integrity. Combined source has 4 DFF variants, one base TXD and 4 verified DFF/TXD pairings, with no unpaired DFF. The add-on DFFs share the base TXD through exact material-texture-name matches. Remaining warning: geometry_without_normals on the shadeless variants; game compatibility is untested. [source page](https://fadxploit.my.id/gtasa/march-7th-hunt-honkai-star-rail/)
- **missing_after_bounded_filename_scan — Promeia (FAD-30, `HSR-ZZZ-FAD-71d91ac2be859d80`):** No complete archive matching the canonical source was found after the bounded local filename and identity scan; this source was not classified as VIP. [source page](https://fadxploit.my.id/gtasa/promeia-zenless-zone-zero/)
- **DFF/TXD pairing warning — Ellen Joe (FAD-30, `HSR-ZZZ-FAD-8b7aff890b7ee58f`):** The saved source inspection records 2 DFF variant(s) without a corresponding confirmed DFF/TXD pair. This is a resource-pairing review item; it does not by itself establish archive corruption or wrong character identity. [source page](https://fadxploit.my.id/gtasa/ellen-joe-zenless-zone-zero/)
- **DFF/TXD pairing warning — Ukinami Yuzuha (FAD-31, `HSR-ZZZ-FAD-8c79d987f5131c07`):** The saved source inspection records 2 DFF variant(s) without a corresponding confirmed DFF/TXD pair. This is a resource-pairing review item; it does not by itself establish archive corruption or wrong character identity. [source page](https://fadxploit.my.id/gtasa/ukinami-yuzuha-zenless-zone-zero/)
- **DFF/TXD pairing warning — Burnice White (FAD-30, `HSR-ZZZ-FAD-c8cc24595b474012`):** The saved source inspection records 2 DFF variant(s) without a corresponding confirmed DFF/TXD pair. This is a resource-pairing review item; it does not by itself establish archive corruption or wrong character identity. [source page](https://fadxploit.my.id/gtasa/burnice-white-zenless-zone-zero/)
- **DFF/TXD pairing warning — Tingyun (FAD-29, `HSR-ZZZ-FAD-e5cb09e10aee2eda`):** The saved source inspection records 2 DFF variant(s) without a corresponding confirmed DFF/TXD pair. This is a resource-pairing review item; it does not by itself establish archive corruption or wrong character identity. [source page](https://fadxploit.my.id/gtasa/tingyun-honkai-star-rail/)
- **DFF/TXD pairing warning — Lenna (UMP9) (FAD-03, `af879fe958b58003`):** The saved source inspection records 2 DFF variant(s) without a corresponding confirmed DFF/TXD pair. This is a resource-pairing review item; it does not by itself establish archive corruption or wrong character identity. [source page](https://fadxploit.my.id/gtasa/lenna-ump9-girls-frontline-2-exilium/)
- **DFF/TXD pairing warning — Cherno (FAD-10, `baa54cb0cd0fb6ea`):** The saved source inspection records 3 DFF variant(s) without a corresponding confirmed DFF/TXD pair. This is a resource-pairing review item; it does not by itself establish archive corruption or wrong character identity. [source page](https://fadxploit.my.id/gtasa/cherno-enigma-tidal-whispers-snowbreak-containment-zone/)
- **DFF/TXD pairing warning — Ken Kaneki (FAD-12, `bfe223aa04252f2a`):** The saved source inspection records 4 DFF variant(s) without a corresponding confirmed DFF/TXD pair. This is a resource-pairing review item; it does not by itself establish archive corruption or wrong character identity. [source page](https://fadxploit.my.id/gtasa/ken-kaneki-s1-tokyo-ghoul-re-birth/)
- **DFF/TXD pairing warning — Herta (FAD-05, `c5052633d5bef952`):** The saved source inspection records 1 DFF variant(s) without a corresponding confirmed DFF/TXD pair. This is a resource-pairing review item; it does not by itself establish archive corruption or wrong character identity. [source page](https://fadxploit.my.id/gtasa/herta-honkai-star-rail/)
- **base package and shared-TXD pairs verified; static geometry review remains — Belle (FAD-18, `d8b598d5893d70c2`):** The full base archive and optional Breast Physics DFF archive both passed integrity. Combined source has 4 DFF variants, one base TXD and 4 verified DFF/TXD pairings, with no unpaired DFF. The add-on DFFs share the base TXD through exact material-texture-name matches. Remaining warning: geometry_without_normals on the shadeless variants; game compatibility is untested. [source page](https://fadxploit.my.id/gtasa/belle-zenless-zone-zero/)
- **DFF/TXD pairing warning — Rover (female) (Earlier inspected source (outside FAD-01–31), `f085bf9b7a53cc0d`):** The saved source inspection records 2 DFF variant(s) without a corresponding confirmed DFF/TXD pair. This is a resource-pairing review item; it does not by itself establish archive corruption or wrong character identity. [source page](https://fadxploit.my.id/gtasa/rover-female-wuthering-waves/)
- **DFF/TXD pairing warning — Kurumi Tokisaki (FAD-01, `f3ae1818de80d3a4`):** The saved source inspection records 4 DFF variant(s) without a corresponding confirmed DFF/TXD pair. This is a resource-pairing review item; it does not by itself establish archive corruption or wrong character identity. [source page](https://fadxploit.my.id/gtasa/kurumi-tokisaki-date-a-live/)
- **DFF/TXD pairing warning — Zani (FAD-18, `f630e9556fe899a8`):** The saved source inspection records 2 DFF variant(s) without a corresponding confirmed DFF/TXD pair. This is a resource-pairing review item; it does not by itself establish archive corruption or wrong character identity. [source page](https://fadxploit.my.id/gtasa/zani-wuthering-waves/)
- **DFF/TXD pairing warning — Ken Kaneki (FAD-12, `ff44a7be3a09ae3b`):** The saved source inspection records 4 DFF variant(s) without a corresponding confirmed DFF/TXD pair. This is a resource-pairing review item; it does not by itself establish archive corruption or wrong character identity. [source page](https://fadxploit.my.id/gtasa/ken-kaneki-s2-tokyo-ghoul-re-birth/)

Các tên nội bộ của 17 dòng `variant_review` và Fenny Lionheart đã được ghi là chấp nhận tên archive làm source association theo quyết định người dùng ngày 18/10. Tên DFF/TXD thật vẫn được giữ trong validation evidence; không kết luận nhân vật ngoại hình đúng hay sai từ tên file. DFF không ghép cặp, cảnh báo geometry/texture và integrity flags vẫn còn nguyên.

Với FAD-08, không cần kiểm tra thêm cho sáu resource pairs dẫn xuất của Kagamine Len và KAITO; cả sáu đã qua CRC và trusted-inspector checks. Hai ZIP gốc vẫn giữ trạng thái integrity unverified do descriptor error, không sửa hoặc xóa; tương thích trong game vẫn chưa thử. Ganyu có một alternate với member path mang nhãn `Ganyu_NSFW`; đây chỉ là metadata, chưa được đánh giá hình ảnh và không được nâng thành skin được duyệt.

## Quyết định đã xử lý

- **Kagamine Len (FAD-08, `d0fa86c7cfde1b27`):** No additional inspection is needed for the recovered pairs at this stage. Preserve the original archive caveat and the not-tested-in-game status.
- **KAITO (FAD-08, `4e5f6d8064889336`):** No additional inspection is needed for the recovered pairs at this stage. Preserve the original archive caveat and the not-tested-in-game status.
- **Belle (FAD-18, `d8b598d5893d70c2`):** Full base archive provided; 4 DFF/TXD variants are paired and 0 remain unpaired. Static geometry warnings are retained.
- **March 7th Hunt (FAD-28, `HSR-ZZZ-FAD-64de4f95d36005c6`):** Full base archive provided; 4 DFF/TXD variants are paired and 0 remain unpaired. Static geometry warnings are retained.

## Ghi chú metadata

- **Ganyu (`GEN-FAD-02d162039c2f725a`):** One local-variant member path contains “Ganyu_NSFW”. This label alone was not treated as a visual/content assessment; the summary does not promote that alternate.

Không có skin nào được cài hoặc thử trong game. Tên source, cấu trúc DFF/TXD và parser tĩnh không chứng minh ngoại hình, rig, animation hay tương thích gameplay.

## Nhóm FAD-01–31

| Nhóm | Nguồn | Có archive | File archive | Cặp hash trong nhóm |
|---|---:|---:|---:|---:|
| FAD-01 | 10 | 10 | 10 | 23 |
| FAD-02 | 10 | 9 | 9 | 15 |
| FAD-03 | 10 | 9 | 9 | 18 |
| FAD-04 | 10 | 10 | 10 | 26 |
| FAD-05 | 10 | 10 | 10 | 29 |
| FAD-06 | 10 | 10 | 10 | 22 |
| FAD-07 | 10 | 8 | 8 | 20 |
| FAD-08 | 10 | 10 | 12 | 25 |
| FAD-09 | 10 | 10 | 10 | 27 |
| FAD-10 | 9 | 9 | 9 | 19 |
| FAD-11 | 9 | 9 | 9 | 22 |
| FAD-12 | 9 | 9 | 9 | 20 |
| FAD-13 | 9 | 9 | 9 | 19 |
| FAD-14 | 9 | 9 | 9 | 19 |
| FAD-15 | 9 | 9 | 10 | 22 |
| FAD-16 | 9 | 3 | 3 | 7 |
| FAD-17 | 9 | 5 | 5 | 20 |
| FAD-18 | 9 | 5 | 6 | 16 |
| FAD-19 | 10 | 10 | 10 | 20 |
| FAD-20 | 10 | 8 | 14 | 20 |
| FAD-21 | 10 | 10 | 10 | 15 |
| FAD-22 | 10 | 10 | 10 | 23 |
| FAD-23 | 9 | 8 | 11 | 16 |
| FAD-24 | 9 | 9 | 9 | 14 |
| FAD-25 | 9 | 9 | 9 | 19 |
| FAD-26 | 10 | 10 | 11 | 32 |
| FAD-27 | 9 | 9 | 9 | 26 |
| FAD-28 | 9 | 9 | 10 | 25 |
| FAD-29 | 9 | 9 | 9 | 18 |
| FAD-30 | 9 | 8 | 10 | 22 |
| FAD-31 | 9 | 9 | 9 | 17 |

## Franchise và rating labels

Các số dưới đây đếm source row; nhãn rating hiện có được giữ nguyên, không gán rating mới trong báo cáo này.

| Franchise | Nguồn |
|---|---:|
| Blue Archive | 8 |
| Chuunibyou demo Koi ga Shitai! | 1 |
| Cyberpunk: Edgerunners | 2 |
| Date A Live | 2 |
| Evangelion | 1 |
| Frieren / Sousou no Frieren | 1 |
| Genshin Impact | 79 |
| Girls' Frontline 2: Exilium | 10 |
| Goddess of Victory: NIKKE | 2 |
| Honkai Impact | 6 |
| Honkai: Star Rail | 54 |
| Jujutsu Kaisen | 1 |
| MiSide | 7 |
| Neverness to Everness | 4 |
| NieR Reincarnation | 7 |
| Project SEKAI COLORFUL STAGE! feat. Hatsune Miku | 10 |
| Punishing: Gray Raven | 6 |
| Re:Zero | 2 |
| Snowbreak: Containment Zone | 11 |
| Sword Art Online | 3 |
| Tokyo Ghoul | 5 |
| Umamusume | 24 |
| VTuber | 6 |
| Vocaloid / voicebanks | 7 |
| Wuthering Waves | 22 |
| Zenless Zone Zero | 25 |

| Rating label | Nguồn |
|---|---:|
| like | 91 |
| neutral | 8 |
| rating_pending | 61 |
| somewhat | 146 |

| Rating cao nhất đang có trên mỗi cặp hash DFF/TXD duy nhất | Cặp |
|---|---:|
| like | 193 |
| neutral | 14 |
| rating_pending | 143 |
| somewhat | 307 |

## Cách đọc và nguồn dữ liệu

- Số nguồn đếm theo canonical job ID, không theo số nhân vật, archive, hay model.
- Bảng trạng thái chi tiết dùng `group-progress.json`, per-group validation và skip evidence; trạng thái trong audit tổng hợp được giữ thêm riêng để thấy khác biệt phân loại.
- Archive bytes và SHA là metadata cục bộ đã ghi. Không có SHA publisher thì không kết luận thiếu hoặc lỗi hash công khai.
- Cặp DFF/TXD là ứng viên tài nguyên tĩnh; chưa có mapping NPC/ped và chưa đánh giá ngoại hình/rig trong game.

Nguồn chính: `download-manifest.json`, hai extension Genshin và HSR/ZZZ, `fad-manual-downloads.json`, `group-progress.json`, các báo cáo FAD theo nhóm, `skin-download-audit-2026-10-15.json` và hai danh sách user-skip 16–17/10/2026.
