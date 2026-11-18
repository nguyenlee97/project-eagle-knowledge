# Khảo Sát & Thiết Kế Kiến Trúc Tính Năng `Story Quest` (Branching Visual Novel Từ Fanfic) — Pilot: Hu Tao

- **Ngày thực hiện:** `05/11/2026`
- **Agent thực hiện:** Antigravity (`35d5cf80-28f1-43e1-8e77-f60ee3d570c3`)
- **Phạm vi:** Chỉ khảo sát, thu thập kho tư liệu (`987,724 bytes` / `45 files`) trong staging và thiết kế sơ đồ bóc tách nhân quả (`DAG` + `Flag Combination Re-Convergence` + `5 Endings`) cho nhân vật thí điểm **Hu Tao (`char_id = "hutao"`)**. **Không chỉnh sửa bất kỳ file runtime nào** trong `Project Eagle\gta sa gameplay-lab` và không chiếm khóa `game-write.lock` / `ingame-runtime.lock`.
- **Thư mục kho tư liệu đã tải về máy:** [`staging/project-eagle/story-quest-hutao-research-20261105/`](../../staging/project-eagle/story-quest-hutao-research-20261105/) (danh mục kèm SHA-256 tại [`corpus_index.json`](../../staging/project-eagle/story-quest-hutao-research-20261105/corpus_index.json)).

---

## 1. Tổng Quan Kho Tư Liệu Đã Thu Thập & Đánh Giá Thực Tế

### 1.1. Nhóm Tư Liệu Fanfic & Fan Visual Novel `Hu Tao × Aether` (`AeTao`)

Qua rà soát trên Archive of Our Own (`Hu Tao/Kong | Aether` & `Hu Tao & Kong | Aether`), FanFiction.Net, Wattpad, itch.io, YouTube Fandub và các chủ đề đề cử trên `r/Aether_Mains` / `r/HuTao_Mains`:

1. **Dự án Fan Visual Novel có sẵn — *"Genshin Impact Visual Novels: Hu Tao Route"* của `@pai-pomlofi` (lồng tiếng bởi `Voxlumiii` & `TheSayuVA`)**:
   - **Cấu trúc & Cốt truyện:** Lấy bối cảnh dịp Tết Hải Đăng tại Cảng Liyue; Aether lạc khỏi Paimon ở khu quầy ẩm thực, tình cờ gặp Đường Chủ Hu Tao và cùng cô giải quyết tâm nguyện cuối đời của một vị khách đặc biệt tại Vãng Sinh Đường — một người cha từng mắc lỗi nặng với con gái, âm thầm làm việc kiệt sức gửi Mora ẩn danh nuôi con suốt năm cuối đời và chỉ xin thả một ngọn đèn trời duy nhất để linh hồn được dõi theo con.
   - **Đánh giá khi chuyển thể:** Rất hợp làm nhánh **Điều tra nhân gian / Chữa lành hối tiếc (`Harbor Regret Sub-Route`)**, nhưng bản gốc thiên về tuyến tính theo chương (chưa có cơ chế `Flag Combination` lật kèo phức tạp).

2. **Nhóm Fanfic Hurt/Comfort & Sinh Tử Bờ Cõi (`AeTao` Angst / Mortality):**
   - **Làn sóng Fanfic Canon-Divergence hậu `Version 5.3 — Swirling Butterflies` (`AO3` / `HoYoLAB` / `Reddit`)** kết hợp cùng trọn bộ **4 hồi kịch bản gốc `Springtime Charms` (`250,038 bytes` đã tải nguyên văn vào `transcripts/hutao_lr53_*.wiki.txt`)** và **4 màn `Papilio Charontis Act I` (`97,240 bytes` tại `transcripts/hutao_sq1..4_*.wiki.txt`)**:
     - Xoay quanh chuỗi tín hiệu chia tay thầm lặng của Hu Tao trước khi một mình bước vào Tử Môn (`Gate of Death`): tặng Aether **cành hoa mai (`Plum Branch`)** gỡ từ mũ của chính cô, nhờ Zhongli trả lại **đồng tiền Rex (`Rex Coin`)**, ngâm 5 tầng Cung Mệnh như bài thơ tuyệt mệnh trên cầu, và khoảnh khắc Aether lợi dụng thể chất Người Ngoại Giới không kết nối Địa Mạch để thò tay xuyên ranh giới sinh tử kéo cô về.
   - ***"Stars within the Afterlife"* của `Obsidian_Matriarch` (`Wattpad`)** & ***"Fall of the Great Traveller"* / tuyến truyện của `TheDrifterscoin`, `UnknownJester25` (`AO3` / `r/Aether_Mains`)**:
     - Khai thác xung đột cốt lõi giữa **Lữ Khách bất tử mang nỗi sợ sống lâu hơn người mình thương** và **Đường Chủ phàm nhân sống rực rỡ từng giây phút**. Aether bị thương nặng hoặc kiệt quệ tâm thần trốn vào Ấm Trần Ca / lạc trong sương mù Vô Vọng Pha; Hu Tao dùng triết lý sinh tử của Vãng Sinh Đường tổ chức một *"tang lễ chôn cất nỗi tiếc nuối"* để giữ anh lại với thực tại.

3. **Nhóm Fanfic Hài Lãng Mạn & Trò Đùa Quái Chiêu (`Chaotic Rom-Com`):**
   - ***"Look All I want to do is burn his house down!"* của `DRSM` (`FanFiction.Net ID: 14282210`, Hoàn thành, `~5,800` từ, Rated T)** & one-shot đồi Vô Vọng của `Bige1218` / chuỗi tag *"Hu Tao Being a Little Shit"* (`AO3`):
     - Hu Tao muốn Aether nhận ra tình cảm của mình nhưng thay vì tỏ tình bình thường lại kéo Yanfei (tư vấn lách luật) và Klee (thuốc nổ!) bày trò náo loạn ngay trước nhà của Aether trong Ấm Trần Ca.
   - **Nhận xét trung thực về nguồn AO3:** Trên `archiveofourown.org`, số lượng long-fic thuần `Hu Tao/Aether` độc lập ở mức `General/Teen` ít hơn đáng kể so với các fic đa nhân vật (*The Children of Aether* của `GodSlayer2468`) hoặc fic gắn nhãn `Explicit`, đồng thời domain chính của AO3 bật Cloudflare challenge với trình tải tự động. Do đó, phương án tối ưu nhất cho dự án là **tổng hợp chất liệu cốt truyện từ 4 tác phẩm/nhánh fanfic tiêu biểu trên + `347 KB` kịch bản thoại chuẩn giọng Hu Tao đã tải về**, rồi cấu trúc lại bằng **khuôn mẫu nhân quả – nhiều kết thúc chuyên nghiệp** ở Mục 1.2.

---

### 1.2. Nhóm Transcript & Mã Nguồn Visual Novel Nhân Quả – Đa Kết Thúc (`~575 KB` Đã Tải Về `vn_blueprints/`)

Để đảm bảo cơ chế rẽ nhánh và `Combination` hoạt động chặt chẽ như một game Visual Novel thực thụ, chúng ta đã thu thập nguyên văn 4 mẫu kiến trúc chuẩn:

| Nguồn tham chiếu | File trong `staging/.../vn_blueprints/` | Dung lượng | Cơ chế nhân quả rút ra cho Story Quest |
|---|---|---|---|
| **Inkle Studios — *The Intercept* (`ink`)** | `inkle_intercept_Assets_Ink_TheIntercept.ink` | `102,225 B` | **Gold Standard về Flag Combination & Re-Convergence**: theo dõi đồng thời biến đếm thái độ (`forceful`, `evasive`), biến vật chứng (`gotcomponent`, `teacup`, `hooperClueType`) và cờ sai lầm (`losttemper`, `longgrasshooperframe`). Dù người chơi rẽ sang nhánh bị nghi ngờ ở giữa truyện, tổ hợp `{ hooperClueType > NONE && not losttemper }` ở đêm cuối vẫn bẻ lái cốt truyện quay lại nhánh thoát tội, trong khi thiếu 1 vế sẽ trượt thẳng qua 3–4 cảnh dẫn tới kết cục bị bắt. |
| **Genshin Hangout 4.5 — *Lynette: Checks & Cats*** | `vn_lynette_1_decision.wiki.txt` + `2a_mask` + `2b_detectives` + `3a_break` + `3b_closure` | `249,180 B` | **Cây Rẽ Nhánh 5 Kết Thúc + Tích Lũy Suy Luận (`+5 Check Bonus`)**: chia 2 đại lộ lớn (`Mask/Break` vs `Detectives/Closure`), có nhánh kết thúc sớm hài hước ngay đầu truyện (`"Standby Mode"`) và cơ chế gom đúng các kết luận điều tra ở bước 19 để vượt ngưỡng sang True Ending của nhánh thám tử (`Adventurers, Investigators, and Cats`), nếu hụt sẽ rơi vào kết cục dở dang (`Save the Kitty!`). |
| **Genshin Hangout 3.5 — *Faruzan: A Confounding Conundrum*** | `vn_faruzan_1_senior.wiki.txt` + `2c_lonesome_shadow` | `96,220 B` | **Thiết kế Bittersweet / Emotional Ending (`5 Endings`)**: minh họa cách một lựa chọn rẽ nhánh ngay nút gốc dẫn người chơi sang hành trình hoàn toàn khác (từ hài hước học viện sang bi kịch lá thư 100 năm của Tamimi ở sa mạc). |
| **Fan Genshin Ren'Py VN — *The Bygone Days of Her and the Flowers* (`luern0313`) & Mẫu `Steins;Gate` / `Fate/stay night`** | `gh_nahida_game_*.rpy` (`17` file `.rpy` gồm `screen_choices_exhibit.rpy`, `turtle_soup.rpy`) | `75,621 B` | **Giao diện Trình Bằng Chứng (`Exhibit/Clue`) + Chuỗi Cờ True Ending (`Steins;Gate` 6-Flag Cascade) + Dead-End / Tiger Dojo (`Fate/stay night`)**: cho phép hiển thị vật phẩm/manh mối ngay trong khung lựa chọn và lưu `persistent` mở khóa sơ đồ Flowchart. |

---

## 2. Kiến Trúc Máy Trạng Thái Đồ Thị Có Hướng (`DAG`) Cho Tính Năng `Story Quest`

So với `WaifuLink Scenario` hiện tại trong [`eagle_waifulink_v4_pilot.py`](../../Project%20Eagle/gta%20sa%20gameplay-lab/eagle_waifulink_v4_pilot.py) (chỉ có 4 cảnh tuyến tính `Scene 1/4..4/4`, chấm điểm `BEST/GOOD/AWKWARD` để cộng tim), **Story Quest Engine (`eagle_story_quest.py`)** chuyển sang mô hình **Đồ thị nhân quả có hướng không chu trình (`DAG`)**:

1. **Tập biến trạng thái mỗi phiên chạy (`QuestState`)**:
   - `current_node_id`: mã nút hiện tại (ví dụ `"ht_sq1_n14_midnight_gate"`).
   - `beat_index`: trang thoại hiện tại trong nút đó (`1..K`, giúp mỗi cảnh kể chuyện sâu `12–20` câu thoại chia làm nhiều nhịp bấm thay vì ép cứng 3 dòng).
   - `flags`: tập cờ boolean nhân quả do các lựa chọn trước đó sinh ra (ví dụ `{"spotted_hat_plum", "kept_unlinked_rattan", "decoded_rex_coin"}`).
   - `meters`: các thanh chỉ số ẩn của câu chuyện (`bond`: gắn kết tình cảm, `insight`: thấu hiểu quy luật sinh tử/Địa Mạch, `regret_weight`: sức nặng chấp niệm).
   - `visited_checkpoints`: lưu snapshot `{node_id -> QuestState}` vào bảng SQLite mới `story_quest_checkpoints` để người chơi **nhảy tức thì về bất kỳ ngã rẽ nào trên sơ đồ Flowchart** sau khi mở 1 Ending.

2. **Ba kiểu cạnh chuyển tiếp (`Edge Types`) giải quyết trọn vẹn yêu cầu của người dùng**:
   - **Cạnh Rẽ Nhánh Thật (`Divergence Split`)**: tại nút ngã rẽ, Lựa chọn A nhảy tới chuỗi nút `Route A (N05 -> N06 -> N07)`, Lựa chọn B nhảy tới `Route B (N08 -> N09 -> N10)`, Lựa chọn C nhảy tới `Route C (N11 -> N12)`. Bối cảnh, nhân vật phụ và CG hoàn toàn khác nhau.
   - **Cạnh Tổ Hợp Quay Lại Hướng Chính (`Combination Re-Convergence Gate`)**:
     $$\text{Unlock\_Reconverge} \iff (\text{flag}_1 \land \text{flag}_2) \lor (\text{insight} \ge \theta \land \text{flag}_3)$$
     Khi người chơi đang đi ở một nhánh phụ tưởng như sắp thất bại (`Route B` hoặc `Route C`), nếu trước đó họ đã vô tình hoặc chủ động thu thập đủ **tổ hợp 2–3 mảnh ghép nhân quả**, một lựa chọn đặc biệt màu vàng kim **`[⚡ KẾT HỢP MANH MỐI]`** sẽ mở khóa, cho phép **bẻ lái cốt truyện từ nhánh phụ nhập trở lại Trục Chính (`Main Climax`)**! Ngược lại, nếu thiếu mảnh ghép, lựa chọn này hiện trạng thái khóa kèm gợi ý mơ hồ (`[🔒 Cần nhận ra vật kỷ niệm trên mũ & bí mật Địa Mạch]`) và nhánh phụ sẽ trôi thẳng về `Bad` hoặc `Neutral Ending`.
   - **Cạnh Đi Thẳng Tới Kết Thúc (`Multi-Scene Terminal Run-Out`)**: một số quyết định mang tính triết lý hoặc sai lầm nghiêm trọng không cắt cụt bằng bảng báo lỗi, mà dẫn người chơi đi tiếp `2–4` nút truyện riêng biệt có cao trào cảm xúc trọn vẹn rồi hạ màn tại `BAD ENDING`, `NEUTRAL ENDING`, `GOOD ENDING` hoặc `TRUE ENDING`.

---

## 3. Bản Bóc Tách Pilot Hoàn Chỉnh Cho Hu Tao (`Story Quest #1`: *"Hoa Đào Đôi Nơi Ranh Giới Sương Mù"*)

Kịch bản Pilot hợp nhất tinh hoa của **3 nguồn fanfic/kịch bản mạnh nhất**:
- Trục chính & cao trào sinh tử từ **5.3 *Swirling Butterflies* + Fanfic *AeTao* Hậu Hải Đăng** (`Cành Mai Trên Mũ` + `Đồng Tiền Rex` + `Tử Môn Đào Đô`);
- Nhánh sương mù tâm thức & nỗi sợ bất tử từ ***Stars within the Afterlife* (`Obsidian_Matriarch`) / *Where the Papilio Fluttered***;
- Nhánh náo loạn Ấm Trần Ca & tâm nguyện khách hàng từ ***Look All I want to do is burn his house down!* (`DRSM`) + `@pai-pomlofi` *Hu Tao Route***.

### 3.1. Hệ Thống 6 Cờ Nhân Quả (`Causal Flags`) & 2 Tổ Hợp Bẻ Lái (`Combinations`)

- `F1_PLUM_HAT`: Ở Hồi I (`N02`), khi Hu Tao xoay người khoe diện mạo mới, Aether không chỉ khen áo đẹp mà **nhận ra ngay nhánh hoa mai quen thuộc trên chiếc mũ Càn Khôn đã biến mất** -> Hu Tao sững người đỏ mặt, trao cành mai thật cho anh kèm lời dặn về cội rễ sự sống.
- `F2_FATHER_LANTERN`: Ở Hồi I (`N03`), Aether nán lại giúp Hu Tao hoàn tất hồ sơ ngọn Tiêu Đăng ẩn danh của người cha quá cố (`pai-pomlofi` motif) -> Hu Tao mở lòng kể về quy tắc *"không được cưỡng cầu người đã khuất nhưng phải giữ trọn lời hứa với người đang sống"*.
- `F3_FUNERAL_OF_REGRET`: Ở Nhánh A (`N06` — Đồi Vô Vọng), khi sương mù phản chiếu nỗi sợ sống trơ trọi ngàn năm của Aether, anh đồng ý cùng Hu Tao cử hành *"Tang lễ tiễn biệt nỗi sợ"* thay vì gồng mình chống cự một mình.
- `F4_LEYLINE_IMMUNITY`: Ở Nhánh B (`N09` — Cảng Liyue & Ngọc Kinh Đài), khi hình nhân mây của Lan Yan không thể kết nối Aether vào Địa Mạch, Aether xâu chuỗi sự kiện để suy ra **thể chất Người Ngoại Giới miễn nhiễm với quy luật xóa sổ của Bát Môn**.
- `F5_ZHONGLI_REX_COIN`: Ở Nhánh B (`N10` — Cầu Cảng Liyue) hoặc Nhánh C (`N13`), Aether kịp chất vấn Zhongli về đồng tiền Rex mà Hu Tao gửi trả -> giải mã bài thơ 5 Cung Mệnh là lời từ biệt.
- `F6_TEAPOT_TRUCE`: Ở Nhánh C (`N12` — Ấm Trần Ca cùng Yanfei & Klee), Aether bắt bài kế hoạch "đốt nhà gây chú ý" của Hu Tao nhưng dịu dàng giữ cô lại ăn bát chè trôi nước nóng, buộc cô hứa không tự gánh tai ương một mình.

#### Hai Tổ Hợp Bẻ Lái (`Combination Gates`):
1. **`COMBO_RECONVERGE_HARBOR_TO_MAIN` (`F1_PLUM_HAT` + `F4_LEYLINE_IMMUNITY` + `F5_ZHONGLI_REX_COIN`)**:
   - **Tác dụng:** Người chơi chọn **Nhánh B** (để Hu Tao đi một mình, ở lại Cảng Liyue điều tra) bình thường sẽ đến trễ và rơi thẳng vào **`BAD ENDING 2` (*Cánh Bướm Đỏ Mùa Đèn Năm Sau*)** hoặc **`NEUTRAL ENDING`**. Nhưng nếu gom đủ tổ hợp `F1 + F4 + F5`, tại `N14`, Aether dùng chính **cành hoa mai (`F1`)** kích hoạt **hình nhân mây chưa nối Địa Mạch (`F4`)** ngay khi vừa nhận **đồng tiền cảnh báo của Zhongli (`F5`)**, xé toạc vết nứt cây Đào Đô để **nhập ngược trở lại Trục Chính (`N16: Nắm Tay Xuyên Tử Môn`)** đúng khoảnh khắc quyết định!
2. **`COMBO_RECONVERGE_TEAPOT_TO_GOOD_OR_TRUE` (`F6_TEAPOT_TRUCE` + (`F1_PLUM_HAT` hoặc `F2_FATHER_LANTERN`))**:
   - **Tác dụng:** Người chơi rẽ sang **Nhánh C (Hài lãng mạn Ấm Trần Ca)** bình thường sẽ đi thẳng tới **`GOOD ENDING` (*Khế Ước Ấm Trần Ca Huyên Náo* — tránh được bi kịch nhờ gọi các Tiên Nhân/Zhongli can thiệp sớm nhưng không giải quyết tận gốc nỗi lòng sinh tử)**. Tuy nhiên, nếu có thêm **`F1_PLUM_HAT` + `F2_FATHER_LANTERN`**, Hu Tao tin tưởng tiết lộ bí mật Tử Môn ngay trong Ấm Trần Ca, cho phép hai người **quay lại hợp lưu vào `N15 -> N16` trên Trục Chính** với lợi thế chuẩn bị trước!

### 3.2. Danh Sách 5 Kết Thúc (`5 Distinct Endings`)

1. **`TRUE ENDING` — *"Song Hoa Đào Đôi Dưới Trời Nhân Gian"* (`Matching Plum Branches`)**:
   - **Điều kiện:** Đạt tới `N16` (qua Nhánh A có `F3_FUNERAL_OF_REGRET`, hoặc lật kèo từ Nhánh B/C nhờ `Combination`) **VÀ** có `F1_PLUM_HAT` + `bond >= 3`.
   - **Diễn biến (`N17 -> N22`):** Aether nắm chặt tay Hu Tao kéo qua cổng ranh giới, hút toàn bộ tử khí vào cơ thể ngoại giới. Hu Tao cõng Aether bất tỉnh suốt đêm về Nhà Thuốc Bubu, túc trực 2 ngày liền. Sáng sớm trên lan can nhìn xuống Cảng Liyue rực nắng, cô bịt mắt anh từ phía sau (*"Đoán xem ai nàooo~?"*), đọc tặng bài thơ về món quà sự sống mỗi ngày và gắn thêm nhánh mai thứ hai lên mũ để hai người mang hoa đào đôi suốt hành trình.
2. **`GOOD ENDING` — *"Khế Ước Ấm Trần Ca Huyên Náo"* (`Chaotic Serenitea Truce`)**:
   - **Điều kiện:** Đi trọn Nhánh C (`N11 -> N12 -> N19 -> N23`) với `F6_TEAPOT_TRUCE` (không kích hoạt cổng quay lại Tử Môn đơn độc).
   - **Diễn biến:** Nhờ Aether giữ chân Hu Tao trong Ấm Trần Ca và báo động sớm cho Zhongli cùng Lục Hợp Tiên Nhân chia tải trận pháp, tai họa được dập tắt an toàn từ xa. Cảnh kết là bữa tiệc lẩu hỗn loạn nhưng ấm áp cùng Yanfei, Xiangling và Klee bên hiên Ấm Trần Ca — ngọt ngào, vui nhộn chuẩn chất fanfic `DRSM`, dù bí mật sâu nhất nơi cội Đào Đô vẫn còn bỏ ngỏ.
3. **`NEUTRAL / BITTERSWEET ENDING` — *"Một Ngọn Tiêu Đăng Cho Lời Chưa Nói"* (`One Lantern for the Unspoken`)**:
   - **Điều kiện:** Vượt qua khủng hoảng ở `N16` nhưng thiếu `F1_PLUM_HAT` hoặc chỉ chọn các đáp án công việc khách sáo (`bond <= 1`).
   - **Diễn biến (`N20 -> N24`):** Liyue bình yên, Hu Tao sống sót trở về và cùng Aether thả ngọn đèn ước nguyện cuối cùng cho người cha quá cố (`pai-pomlofi` motif). Tuy nhiên, vì nghĩ rằng trái tim Lữ Khách chỉ hướng về bầu trời xa xôi, Hu Tao giấu nhẹm lời tỏ tình sau nụ cười tinh nghịch quen thuộc, dúi vào tay anh tấm phiếu giảm giá Vãng Sinh Đường 50% rồi quay lưng bước vào biển đèn lồng.
4. **`BAD ENDING 1 (Kết thúc sớm giữa truyện — Hồi II)` — *"Lạc Giữa Sương Trắng Vô Vọng"* (`Lost in Monochrome Mist`)**:
   - **Điều kiện:** Đi Nhánh A (`N05 -> N06`) nhưng từ chối nghi thức buông bỏ chấp niệm (`not F3_FUNERAL_OF_REGRET`) và cố lao sâu vào vùng sương mù đơn sắc (`N07 -> N25`).
   - **Diễn biến (3 cảnh riêng):** Sương mù ranh giới khuếch đại nỗi ám ảnh mất người thân ngàn năm của Aether thành xiềng xích chì kéo chìm cả hai. Zhongli buộc phải phóng thiên thạch phá sương cứu khẩn cấp hai người ra ngoài; trận pháp gián đoạn, Vãng Sinh Đường phải đóng cửa phong ấn và Hu Tao tự trách mình đã đẩy anh vào hiểm cảnh.
5. **`BAD ENDING 2 (Bi kịch cao trào — Hồi III)` — *"Cánh Bướm Đỏ Mùa Đèn Năm Sau"* (`Next Year's Crimson Butterfly`)**:
   - **Điều kiện:** Đi Nhánh B (`N08 -> N09 -> N10 -> N14`) mà **thiếu tổ hợp `F1 + F4 + F5`**, nên không mở được cổng bẻ lái quay lại Trục Chính (`N14 -> N21 -> N26`).
   - **Diễn biến (4 cảnh điện ảnh gây ám ảnh nhất):** Đèn Minh Tiêu bừng sáng trên bầu trời Liyue, những cánh bướm lửa chữa lành cho toàn thành phố nhưng hình nhân mây trong tay Aether vụt xám ngắt. Anh chạy bán sống bán chết lên Đồi Vô Vọng chỉ còn thấy **Trượng Hộ Ma cắm thẳng đứng giữa đống tro tàn**, cùng một con bướm đỏ phát sáng khẽ đậu lên đầu ngón tay anh kèm tiếng vọng dịu dàng: *"Tết Hải Đăng năm sau... nếu thấy bướm lửa bay qua, đó là ta về thăm người đấy..."* -> Mở khóa ngay gợi ý trên **Sơ Đồ Nhân Quả (`Flowchart`)** hướng dẫn người chơi nhảy lại `N02` và `N09` để tìm tổ hợp cứu cô!

---

## 4. Tích Hợp Kỹ Thuật Với `gta sa gameplay-lab` & Ngân Sách Ảnh CG

### 4.1. Khả Năng Tái Sử Dụng & Nâng Cấp Trên Hạ Tầng Sẵn Có

Qua đọc trực tiếp [`hud.lua`](../../Project%20Eagle/gta%20sa%20gameplay-lab/hud.lua) (`DrawWaifuLinkDatingHud()` dòng `1722–1900`), [`eagle_dating_sim.py`](../../Project%20Eagle/gta%20sa%20gameplay-lab/eagle_dating_sim.py) và [`eagle_waifulink_voice.py`](../../Project%20Eagle/gta%20sa%20gameplay-lab/eagle_waifulink_voice.py):

- **Có sẵn 100% (dùng lại ngay, không rủi ro crash):**
  - Cơ chế ping-pong `models/txd/WLCG0.TXD` & `WLCG1.TXD` hiển thị ảnh `16:9` fullscreen sắc nét, che kín HUD gốc của GTA SA.
  - Khung thoại kính mờ (`Sprite2d.DrawRect` alpha blending) + bảng tên nhân vật có avatar `ep_ms_hutao`.
  - Bộ `24` file voice tiếng Nhật Rie Takahashi của Hu Tao trong `eagle_waifulink_voice.py` (`vn_sweet_happy`, `vn_shy_blush`, `vn_playful_tease`, `vn_tender_love`).
  - Chuột cảm ứng `144Hz` và cuộn danh sách của `EaglePhone OS v6.3`.
- **4 Điểm Cần Nâng Cấp Khi Triển Khai Code (Giai Đoạn Sau Khi Chốt Thiết Kế):**
  1. **Module `eagle_story_quest.py` + Bảng SQLite `story_quest_state` / `story_quest_checkpoints`**: chạy trình thông dịch đồ thị `DAG`, đánh giá biểu thức `combination` (`all_flags`, `any_flags`, `min_bond`), và lưu snapshot tại mọi nút rẽ nhánh.
  2. **Nhịp Thoại Đa Trang (`Multi-Beat Paging`) trong `hud.lua`**: ở chế độ `wl_vn_mode == "story_quest"`, các trang dẫn chuyện bấm `[Space / Enter / Click]` để đọc tiếp từng đoạn văn giàu cảm xúc kiểu Visual Novel thực thụ; chỉ trang cuối của Node mới bật các hàng lựa chọn (`2–4` lựa chọn).
  3. **Thanh Trạng Thái Manh Mối & Huy Hiệu `[⚡ COMBO]`**: thay thanh cứng `1/4..4/4` ở đầu màn hình (dòng `1755` `hud.lua`) bằng thanh hiển thị `HỒI / NHÁNH HIỆN TẠI` + các icon vật chứng đã nhặt (`[Nhánh Mai]`, `[Hình Nhân Mây]`, `[Đồng Tiền Rex]`), đồng thời tô viền vàng kim cho lựa chọn `Combination` vừa được mở khóa.
  4. **Màn Hình Sơ Đồ Nhánh (`Interactive Flowchart & 5 Endings Gallery`)**: đặt trong `App #13 WaifuLink -> Tab Story Quest` (hoặc mục riêng tại menu `[F9]` trước cửa nhà nhân vật) để người chơi xem trực quan sơ đồ các nhánh đã mở, `Endings: X/5`, và bấm nhảy thẳng về nút ngã rẽ bất kỳ mà không phải chơi lại từ đầu.

### 4.2. Bài Toán Tối Ưu Số Lượng Ảnh CG Theo Luật Cứng `image-generator` (`100` hình / `5 tiếng`)

Thay vì vẽ `1` ảnh cho mỗi câu thoại (gây tốn quota vô ích), chuẩn Visual Novel thương mại sử dụng **CG Theo Cảnh Nút Thắt (`Scene/Bottleneck CG`) + CG Đặc Tả Kết Thúc (`Ending Splash CG`)**:
- `3` CG Hồi I (Cổng Vãng Sinh Đường đêm hội, Khoảnh khắc trao cành mai trên mũ, Ngọn đèn của người cha)
- `3` CG Nhánh A — Đồi Vô Vọng & Nghi thức tiễn biệt nỗi sợ
- `3` CG Nhánh B — Hình nhân mây Ngọc Kinh Đài, Zhongli trao đồng tiền Rex trên cầu, Đèn Minh Tiêu bùng cháy
- `3` CG Nhánh C — Kế hoạch náo loạn Ấm Trần Ca cùng Yanfei/Klee & bát chè trôi nước đêm khuya
- `3` CG Cao Trào Chung (`Combination Portal` xé vết nứt Đào Đô, Nắm tay xuyên Tử Môn, Hu Tao cõng Aether dưới ánh trăng)
- `5` CG Toàn Màn Hình Cho `5 Endings` (`True`, `Good`, `Neutral`, `Bad 1`, `Bad 2`)
- **Tổng cộng: đúng `20` ảnh CG `16:9` chất lượng cao cho toàn bộ `26` Nodes (`~75` trang thoại, `5` Endings) của Hu Tao!** Với mức `20` ảnh/nhân vật, chỉ riêng 1 chu kỳ `100` hình / `5 tiếng` của `image-generator` nội bộ đủ sức hoàn thiện tới **`4–5` Story Quest lớn** mà không bao giờ lo chạm trần quota.

---

## 5. Trạng Thái Bàn Giao

- **Trạng thái tác vụ khảo sát:** `done` (chờ người dùng duyệt hướng kịch bản và phạm vi UI để bước sang giai đoạn viết kịch bản chi tiết + code `Story Quest Engine`).
- **Tác động Runtime:** `0` file sửa đổi trong `Project Eagle\gta sa gameplay-lab`.
- **Trạng thái Khóa:** `game-write.lock` = `OPEN`, `ingame-runtime.lock` = `OPEN`.
