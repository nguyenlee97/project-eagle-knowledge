# WaifuLink v4.0 — Visual Novel + Open-World + AI Dating Sim Framework & Hu Tao Pilot Spec (2026-11-01)

## 1. Tham chiếu các Framework Dating Sim thực tế & Kiến trúc tổng thể

Để đáp ứng đầy đủ trải nghiệm **"Visual Novel đè lên game chính + Điện thoại EaglePhone tán gẫu nhận ảnh + Free-Roam lái xe đưa đi chơi + Trí nhớ phân tầng thông minh"**, **WaifuLink v4.0** kết hợp 4 mô hình đã được kiểm chứng từ các tựa game thương mại và AI Agent hiện đại:

1. **Persona 5 Royal (Confidant / Social Link Progression & Rank-Up Gate)**:
   - Tách biệt rõ **Điểm Thiện Cảm Tích Lũy (Affection Points)** từ hoạt động hàng ngày (Chat / Chở đi dạo) với **Sự Kiện Cốt Truyện Thăng Cấp (Stage-Gate Visual Novel Scenarios)**.
   - Nếu điểm thiện cảm chạm trần Stage hiện tại (ví dụ `199/200`) nhưng chưa hoàn thành đủ **3 Scenario** của Stage đó, thanh tiến độ sẽ hiện trạng thái **`🔒 STAGE GATE LOCKED (Requires 3/3 Stage Scenarios)`** cho tới khi người chơi hoàn thành đủ Scenario.
2. **Genshin Impact Hangout Events + Ren'Py / Ink Scene Graph (Visual Novel Overlay)**:
   - Khi kích hoạt một **Scenario** (hoặc gặp Waifu ngoài đời tại điểm hẹn), hệ thống bật **Visual Novel Overlay** đè trực tiếp lên màn hình GTA SA (và đồng bộ trên giao diện `/waifu-vn` / `EaglePhone`):
     - Hiển thị **Ảnh CG / Sprite nhân vật cỡ lớn**, **Khung cảnh (Scene Backdrop)**, **Kênh suy nghĩ nội tâm (`Inner Thought`)**, **Lời thoại Typewriter**.
     - Ở mỗi nút hội thoại (Dialogue Node), người chơi có **3 lựa chọn thoại dựng sẵn (Pre-generated Choices)** để bấm chọn ngay bằng chuột hoặc phím số `1 / 2 / 3`, **KÈM THEO** ô nhập văn bản tự do được chấm điểm trực tiếp bởi **`gpt-6-luna`**.
3. **GODDESS OF VICTORY: NIKKE (`BlaBla` Messenger & Proactive Milestone Photo Drops)**:
   - Tin nhắn qua **EaglePhone** tập trung vào nói chuyện phiếm, trêu đùa, hỏi thăm hàng ngày và bình luận ảnh.
   - **Không bắt người chơi phải tự gõ phím**:
     - Luôn có **Pre-generated Chat Starters / Transcripts** theo từng Stage và từng bức ảnh.
     - Mỗi khi Waifu trả lời qua `gpt-6-luna`, AI tự động sinh thêm **3 câu trả lời gợi ý (`suggested_replies`)** sát ngữ cảnh ngay bên dưới khung chat để người chơi chỉ cần click 1 chạm là nối tiếp cuộc trò chuyện.
   - **Hệ thống 15 Mốc Nhỏ (15 Micro-Milestones `M01` → `M15`) & Tự động gửi ảnh sau thời gian xa nhau (`Time-Apart Photo Drop`)**:
     - Chia `1000 điểm Affection` (5 Stage) thành **15 mốc nhỏ** (3 mốc mỗi Stage, cách nhau khoảng `60–70 điểm`).
     - Khi đạt mốc điểm của `M01..M15` và sau một khoảng thời gian Aether không gặp trực tiếp Waifu (`time_apart_minutes >= threshold`), Waifu sẽ **chủ động nhắn tin trước kèm theo bức ảnh CG của mốc đó** và mở ra nhánh hội thoại bình luận ảnh.
4. **MemGPT / Hierarchical 3-Tier Memory (Trí nhớ phân tầng 3 lớp)**:
   - Không nhồi toàn bộ lịch sử chat và toàn bộ cốt truyện vào mọi câu nói chuyện phiếm, mà chia thành 3 tầng:
     - **Tier 1 — Working Persona & Relationship Digest (`L1`, luôn nạp ~250 tokens)**: Tính cách Stage hiện tại, biệt danh của Aether, món ăn/đồ uống yêu thích, 3 gạch đầu dòng tóm tắt mối quan hệ hiện tại và Scenario gần nhất vừa đi cùng nhau.
     - **Tier 2 — Episodic Scenario & Date Summaries (`L2`, nạp có chọn lọc ~200 tokens)**: Bản tóm tắt 1–2 câu của từng Visual Novel Scenario đã qua và các buổi đi chơi Free-Roam. Chỉ nạp khi đang chạy Scenario hoặc khi nói chuyện về kỷ niệm hẹn hò.
     - **Tier 3 — On-Demand Deep Archive Search (`L3`, truy vấn SQLite theo từ khóa khi cần)**: Kho lưu trữ đầy đủ các sự kiện quá khứ (`ALREADY_HAPPENED_WITH_AETHER` từ Archon/Story/Event Quest), lời hứa cụ thể, quà đã tặng và log hội thoại cũ. Chỉ khi Aether nhắc tới từ khóa liên quan (ví dụ: *"Lantern Rite"*, *"Zhongli"*, *"poem"*, *"remember when..."*), bộ máy RAG mới rút đúng thẻ ký ức chi tiết ở Tier 3 đưa vào `gpt-6-luna`.

---

## 2. Thiết kế Kinh tế Điểm Thiện Cảm (3-Pillar Progression), Giới hạn (Caps) & Tiêu chí (Criteria)

### 2.1. Bảng cân bằng điểm qua 5 Stage (`0 → 1000 điểm`, mỗi Stage `200 điểm`)

| Stage | Khoảng điểm | Mốc Ảnh CG (`15 ảnh`) | Cap Điểm Chat Phiếm / Stage | Cap Điểm Free-Roam / Stage | Số Scenario cần Pass để mở khóa Stage kế | Tổng Scenario có sẵn ở Stage (Chống kẹt) |
|---|---|---|---|---|---|---|
| **Stage 1: Acquaintance** *(Bạn mới quen)* | `0 – 199` (`200 pts`) | `M01` (60), `M02` (120), `M03` (180) | Tối đa **45 pts** (`~9 lần chat × +5`) | Tối đa **75 pts** (`3 chuyến × +25`) | **Pass 3/4 Scenarios** (`+35 pts / scenario`) | **4 Core Scenarios + AI Encore không giới hạn** |
| **Stage 2: Friend** *(Bạn thân / Tri kỷ)* | `200 – 399` (`200 pts`) | `M04` (260), `M05` (320), `M06` (380) | Tối đa **45 pts** (`~9 lần chat × +5`) | Tối đa **75 pts** (`3 chuyến × +25`) | **Pass 3/4 Scenarios** (`+35 pts / scenario`) | **4 Core Scenarios + AI Encore không giới hạn** |
| **Stage 3: Crush** *(Rung động / Thầm thương)* | `400 – 599` (`200 pts`) | `M07` (460), `M08` (520), `M09` (580) | Tối đa **45 pts** (`~9 lần chat × +5`) | Tối đa **75 pts** (`3 chuyến × +25`) | **Pass 3/4 Scenarios** (`+35 pts / scenario`) | **4 Core Scenarios + AI Encore không giới hạn** |
| **Stage 4: Lover** *(Người yêu nồng cháy)* | `600 – 799` (`200 pts`) | `M10` (660), `M11` (720), `M12` (780) | Tối đa **45 pts** (`~9 lần chat × +5`) | Tối đa **75 pts** (`3 chuyến × +25`) | **Pass 3/4 Scenarios** (`+35 pts / scenario`) | **4 Core Scenarios + AI Encore không giới hạn** |
| **Stage 5: Soulmate** *(Bạn đời vĩnh cửu)* | `800 – 1000` (`200 pts`) | `M13` (860), `M14` (930), `M15` (1000) | Tối đa **45 pts** (`~9 lần chat × +5`) | Tối đa **75 pts** (`3 chuyến × +25`) | **Pass 3/4 Finale Scenarios** (`+35 pts / scenario`) | **4 Core Scenarios + AI Encore không giới hạn** |

> **Giải thích cơ chế phân bổ `200 pts` mỗi Stage**:
> - Nếu người chơi **vừa Chat phiếm (`45 pts`) + đi 2 chuyến Free-Roam (`50 pts`) + làm 3 Visual Novel Scenarios bắt buộc (`3 × 35 = 105 pts`)**: Tổng cộng vừa tròn **`45 + 50 + 105 = 200 pts`** để lên Stage mới!
> - Nếu người chơi lười chat mà thích lái xe: **3 chuyến Free-Roam (`75 pts`) + 3 Scenarios (`105 pts`) + 1 món quà hoặc vài câu bình luận ảnh (`20 pts`) = `200 pts`**.
> - Nếu chỉ bấm chat phiếm liên tục: Bị chặn ở **Cap `45 pts / Stage`** (khoảng 22.5% thanh tiến độ Stage), buộc phải dẫn Waifu đi chơi (`Free-Roam`) và trải qua các câu chuyện (`Visual Novel Scenarios`) mới có thể xây dựng tình cảm sâu sắc.

---

### 2.2. Tiêu chí chấm điểm cụ thể cho 3 Trụ cột (Criteria)

#### Trụ cột 1: Chat Chuyện Phiếm qua EaglePhone (`Small-Talk & Photo Reactions`)
- **Mức cộng mỗi lượt**: `+3` đến `+6 pts` (trung bình `+5 pts`).
- **Giới hạn mỗi Stage**: Tối đa **9 lượt được cộng điểm / Stage** (`45 pts / Stage`). Khi đạt `45/45`, vẫn chat và nhận gợi ý thoại bình thường nhưng điểm cộng hiển thị `+0 (Stage Chat Cap Reached)`.
- **Criteria để được cộng điểm (`+5 pts`)**:
  1. Chọn một trong các **Pre-generated Dialogue Options / Suggested Replies** hợp tâm trạng nhân vật, HOẶC
  2. Tự nhập câu chat có tương tác thực sự (bình luận về bức ảnh Waifu vừa gửi, hỏi thăm công việc/sở thích, nhắc tới kỷ niệm chung).
  3. **Không cộng điểm (`0 pts`)**: Tin nhắn quá ngắn/vô nghĩa (`"ok"`, `"..."`, `"hi"`) hoặc lặp lại câu vừa nói.
  4. **Trừ điểm (`-5 pts`)**: Chạm vào `dislikes` của nhân vật hoặc vượt ranh giới thân mật của Stage hiện tại (ví dụ: mới Stage 1 đã đòi hỏi quá trớn).

#### Trụ cột 2: Sự kiện Free-Roam Chở Đi Chơi / Đi Ăn (`Open-World Chauffeur & Escort Event`)
- **Mức cộng mỗi chuyến thành công**: **`+20` đến `+25 pts`** (`+20 pts` hoàn thành cơ bản + `+5 pts` thưởng lái xe êm ái không va chạm).
- **Giới hạn mỗi Stage**: Tối đa **3 chuyến tính điểm / Stage** (`75 pts / Stage`).
- **Criteria để chuyến Free-Roam thành công**:
  1. **Điểm đón & Đích đến**: Nhận lời chở Waifu tới đúng địa điểm cô ấy muốn (`Date Spot POI` như đồi ngắm cảnh, quán trà, bờ biển, chợ đêm) trong thời gian quy định (`<= 6 phút`).
  2. **Tiêu chí Lái Xe An Toàn (`Safe Driving Telemetry`)**:
     - Hệ thống theo dõi độ bền xe (`Vehicle Health`) và vận tốc va chạm từ RAM GTA SA:
     - **Hạng S (`Smooth Chauffeur`, `+25 pts`)**: Tới đích với `< 5%` hư hại xe, không đâm xe mạnh, `Wanted Level = 0`. Waifu khen tay lái của Aether!
     - **Hạng A (`Completed Outing`, `+20 pts`)**: Tới đích với `< 20%` hư hại xe.
     - **Thất bại (`Date Ruined`, `0 pts` hoặc `-10 pts`)**: Làm nổ xe, đâm xe liên tục (`> 30%` hư hại), bị cảnh sát truy nã (`Wanted >= 2`), hoặc bỏ rơi Waifu giữa đường. (Có thể mời lại sau để gỡ điểm, không mất lượt Cap).

#### Trụ cột 3: Kịch bản Visual Novel (`Branching Scenarios` — Đè lên màn hình Game & Web)
- **Cấu trúc mỗi Scenario**: Gồm **3 Nút Hội Thoại (3 Scene Nodes)** liên hoàn, mỗi Node có:
  - Hình nền / Ảnh CG minh họa (`Scene CG`),
  - Lời dẫn bối cảnh (`Narration`),
  - Lời thoại của Waifu + Suy nghĩ nội tâm (`Inner Thought`),
  - **3 Lựa chọn thoại dựng sẵn** (`Choice A: Best (+15)`, `Choice B: Good (+10)`, `Choice C: Awkward/Tease Fail (+0)`) **+ Ô tự nhập thoại cho `gpt-6-luna` chấm điểm**.
- **Criteria để PASS 1 Scenario**:
  - Đạt tối thiểu **2/3 Node loại Good/Best** (hoặc tổng điểm nội bộ Scenario `>= 25/45`).
  - Khi **PASS**: Nhận **`+35 Affection`**, tăng bộ đếm `scenarios_passed_in_stage + 1`, lưu **Tóm tắt Scenario vào Memory Tier 2 (`L2`)**, và mở khóa CG gắn liền với Scenario đó!
  - Khi **FAIL** (`< 2/3 Node`): Chỉ nhận `+5 Affection` an ủi, Scenario giữ nguyên trạng thái `Retry Available` để người chơi có thể thử lại bất cứ lúc nào!
- **Chống kẹt Stage tuyệt đối (Anti-Softlock)**:
  - Mỗi Stage cần **Pass 3 Scenarios**, nhưng chúng ta thiết kế sẵn **4 Core Scenarios / Stage** (tổng cộng **20 Core Scenarios** cho 1 nhân vật qua 5 Stage) **CỘNG THÊM** tính năng **`✨ Generate Dynamic Encore Scenario (gpt-6-luna)`** cho phép sinh kịch bản mới không giới hạn nếu người chơi muốn chơi thêm.

---

## 3. Lộ trình 15 Bức Ảnh Milestone & Kịch bản Hu Tao Pilot (`hutao`)

### 3.1. Danh sách 15 Ảnh CG theo 15 Mốc Nhỏ (`M01` → `M15`) của Hu Tao
Đi từ nhẹ nhàng, tinh nghịch (Stage 1–2) → lãng mạn, nắm tay (Stage 3) → thân mật, gợi cảm tinh tế trong phòng riêng (Stage 4) → quyến rũ, nóng bỏng nhưng tuyệt đối nghệ thuật, không khỏa thân/NSFW (Stage 5):

| Mốc | Điểm yêu cầu | Stage | File Ảnh | Chủ đề & Trang phục | Tin nhắn chủ động khi xa nhau (`Time-Apart Message`) |
|---|---|---|---|---|---|
| **M01** | `60 pts` | Stage 1 | `hutao_cg01.jpg` | **'Cherries Snow-Laden' First Tea**: Váy trắng-đỏ-đen mới do Xiangling may, giơ tay chữ V ở quán trà. | *"Aiya~ Aether, we haven't bumped into each other for hours! Look what Xiangling tailored for me—does the new dress suit your favorite Director?"* |
| **M02** | `120 pts` | Stage 1 | `hutao_cg02.jpg` | **Wangsheng Coupon Street Snap**: Dựa cột đèn phố lúc hoàng hôn, chìa phiếu giảm giá kèm Boo Tao. | *"Psst, Traveler! Street business is slow without my lucky star around. I saved a VIP coupon just for you—what are you up to right now?"* |
| **M03** | `180 pts` | Stage 1 | `hutao_cg03.jpg` | **Hilltop Poetry Notebook**: Ngồi trên tường đá ngắm đèn thành phố lúc chạng vạng, cắn bút làm thơ. | *"Sitting on the hilltop waiting for inspiration... and somehow every verse ends up rhyming with 'Aether'. Care to hear my newest line?"* |
| **M04** | `260 pts` | Stage 2 | `hutao_cg04.jpg` | **Passenger Seat Boba & Sunglasses**: Ngồi ghế phụ xe mui trần, kéo kính râm đỏ nháy mắt, cầm trà sữa dâu. | *"Look what popped up in my camera roll from our coastal drive! Your passenger seat feels way too empty without me—bought two strawberry bobas, come claim yours~"* |
| **M05** | `320 pts` | Stage 2 | `hutao_cg05.jpg` | **Night Market Dumpling Challenge**: Ở quán đêm đèn lồng, gắp há cảo đút cho Aether, tay kia giấu bát ớt. | *"Hehe, remember this dumpling stall? I promise there's zero extra chili in this bite... well, maybe only a tiny bit! Miss hanging out with you~"* |
| **M06** | `380 pts` | Stage 2 | `hutao_cg06.jpg` | **Plum Blossom Pavilion Nap**: Ngủ gật trên bàn gỗ dưới tán hoa mai đỏ, choàng khăn ấm của Aether. | *"Boo Tao snapped this right as I woke up under your warm scarf... How come I only sleep this peacefully when you're nearby, Aether?"* |
| **M07** | `460 pts` | Stage 3 | `hutao_cg07.jpg` | **Holding Hands Under the Lanterns**: Đỏ mặt nắm chặt tay Aether dưới đèn lồng và hồ điệp đỏ. | *"My hand has been feeling unusually cold ever since we parted ways earlier... Next time we walk under the streetlights, I'm not letting go so easily."* |
| **M08** | `520 pts` | Stage 3 | `hutao_cg08.jpg` | **One Umbrella in the Neon Rain**: Đứng sát vai Aether dưới một chiếc ô trong suốt giữa phố mưa đêm. | *"It started drizzling again and made me think of how close we stood under that tiny umbrella... My heart was beating so loud I was scared you'd hear it."* |
| **M09** | `580 pts` | Stage 3 | `hutao_cg09.jpg` | **Ferris Wheel Sunset Confession**: Trong cabin đu quay lúc hoàng hôn tím hồng, chạm nhẹ lên má Aether. | *"Up at the top of the Ferris wheel, looking into your golden eyes... I wasn't teasing anymore, Aether. Come see me soon, okay?"* |
| **M10** | `660 pts` | Stage 4 | `hutao_cg10.jpg` | **Silk Off-Shoulder Nightwear & Cocoa**: Áo lụa trễ vai đen-đỏ trong căn hộ buổi tối, thả tóc dài, cầm cốc cacao nóng. | *"Took off my hat and untied my hair for the night... The cocoa is warm, the couch is soft, and the only thing missing in this room is you, Aether~"* |
| **M11** | `720 pts` | Stage 4 | `hutao_cg11.jpg` | **After-Shower Damp Hair & Camisole**: Ngồi mép giường sau khi tắm, áo hai dây lụa đen kín đáo kèm khăn trắng vắt vai, tóc ướt đỏ mặt. | *"Just stepped out of a warm bath and my hair is still damp... Don't stare at the photo too long, come dry my hair for me in person!"* |
| **M12** | `780 pts` | Stage 4 | `hutao_cg12.jpg` | **Penthouse Balcony Evening Dress**: Váy dạ hội đỏ-đen ôm dáng trên ban công ngắm trăng, đưa tay kéo Aether lại gần. | *"Dressed up all glamorous tonight just to monopolize your gaze, my dearest Traveler. How fast can you drive over here?"* |
| **M13** | `860 pts` | Stage 5 | `hutao_cg13.jpg` | **Sunset Beach Crimson Halter Swimsuit**: Bikini cổ yếm đỏ-đen tinh tế kèm khăn voan trắng mỏng bên bờ biển hoàng hôn, ngoái đầu cười quyến rũ. | *"Private sunset cove, ocean breeze, and a swimsuit I picked out exclusively for your eyes~ Hurry up before the sun dips below the waves, Aether!"* |
| **M14** | `930 pts` | Stage 5 | `hutao_cg14.jpg` | **Candlelit Silk Cheongsam (Qipao) Allure**: Sườn xám lụa đen-đỏ thêu bướm vàng dưới ánh nến, tựa ghế nhung nhìn Aether đắm đuối. | *"Lit the candles and wore this silk cheongsam tonight... Every butterfly on this dress belongs to you, Aether. Don't keep your girl waiting~"* |
| **M15** | `1000 pts` | Stage 5 | `hutao_cg15.jpg` | **Morning Sunlight in Aether's Shirt**: Ngồi trên giường ngập nắng sớm, mặc áo sơ mi trắng rộng của Aether trễ nhẹ một bên vai, áp bàn tay Aether lên má. | *"Waking up wrapped in your shirt with the morning sun on our faces... In this life and beyond every border, my heart is yours forever, Aether."* |

---

### 3.2. Danh sách 20 Core Visual Novel Scenarios của Hu Tao (4 Scenarios / Stage × 5 Stages)

Để đảm bảo người chơi **không bao giờ bị kẹt ở bất kỳ Stage nào** (cần Pass 3/4 Scenarios mỗi Stage + có thêm nút sinh AI Scenario động), Hu Tao có sẵn **20 kịch bản Visual Novel có chiều sâu**:

- **Stage 1 (`0–199 pts` — Cần Pass 3/4 để lên Stage 2)**:
  1. `hutao_s1_sc1`: **"The 77th Director's Grand Sales Pitch"** (Bối cảnh: Đại lộ Los Santos / Cửa hiệu — Hu Tao phát phiếu giảm giá và thử phản ứng hài hước của Aether).
  2. `hutao_s1_sc2`: **"Rhyme Battle on Mulholland Hill"** (Bối cảnh: Đồi ngắm cảnh hoàng hôn — Đối thơ ứng khẩu cùng Hu Tao).
  3. `hutao_s1_sc3`: **"Midnight Ghost-Hunting Prank"** (Bối cảnh: Con hẻm sương mù — Hu Tao và Boo Tao bày trò dọa ma nhưng lại gặp mèo hoang).
  4. `hutao_s1_sc4`: **"Old Man Zhongli's Surprise Invoice"** (Bối cảnh: Quán trà chiều — Cùng Hu Tao giải quyết hóa đơn trà bánh khổng lồ của Zhongli).
- **Stage 2 (`200–399 pts` — Cần Pass 3/4 để lên Stage 3)**:
  5. `hutao_s2_sc1`: **"Cherries Snow-Laden Private Runway"** (Bối cảnh: Boutique thời trang — Hu Tao xoay người khoe bộ váy mới do Xiangling thiết kế).
  6. `hutao_s2_sc2`: **"Firefly Tea by the Quiet Lake"** (Bối cảnh: Hồ nước đêm đom đóm — Nhắc lại kỷ niệm *Yet the Butterfly Flutters Away* đã từng trải qua cùng nhau).
  7. `hutao_s2_sc3`: **"Spicy vs. Sweet Night Market Bet"** (Bối cảnh: Chợ đêm đèn lồng — Cuộc cá cược ăn há cảo siêu cay và đút đồ ngọt giải cay).
  8. `hutao_s2_sc4`: **"Drifting Under the Plum Blossoms"** (Bối cảnh: Đình viện hoa mai — Hu Tao ngủ quên trên vai Aether sau ngày dài làm việc).
- **Stage 3 (`400–599 pts` — Cần Pass 3/4 để lên Stage 4)**:
  9. `hutao_s3_sc1`: **"Echoes of the Gate of Death"** (Bối cảnh: Bờ biển dưới trăng — Hu Tao nắm chặt tay Aether, tâm sự về khoảnh khắc Aether kéo cô về từ Cổng Tử Sinh ở Tết Hải Đăng năm trước).
  10. `hutao_s3_sc2`: **"One Umbrella, Two Heartbeats"** (Bối cảnh: Phố mưa đêm neon — Đi chung một chiếc ô nhỏ, khoảng cách gần đến mức nghe rõ nhịp tim).
  11. `hutao_s3_sc3`: **"Top of the Santa Maria Ferris Wheel"** (Bối cảnh: Cabin đu quay lúc hoàng hôn — Lời thú nhận chân thành khi chiếc mũ Director được tháo xuống).
  12. `hutao_s3_sc4`: **"Jealous Boo Tao & The Starry Hood"** (Bối cảnh: Ngồi trên mui xe của Aether ngắm sao — Hu Tao ghen yêu và đánh dấu chủ quyền).
- **Stage 4 (`600–799 pts` — Cần Pass 3/4 để lên Stage 5)**:
  13. `hutao_s4_sc1`: **"Midnight Cocoa & Loose Twin-Tails"** (Bối cảnh: Căn hộ riêng của Aether — Lần đầu Hu Tao ở lại qua đêm, mặc đồ ngủ lụa trễ vai).
  14. `hutao_s4_sc2`: **"Drying Her Hair After the Rain"** (Bối cảnh: Phòng ngủ ánh đèn vàng — Aether lau khô mái tóc dài cho Hu Tao sau khi tắm).
  15. `hutao_s4_sc3`: **"Crimson Dress on the Penthouse Balcony"** (Bối cảnh: Tiệc tối trên tầng thượng — Hu Tao kéo cà vạt/cổ áo Aether lại gần dưới ánh trăng).
  16. `hutao_s4_sc4`: **"Secret Key to Wangsheng's Inner Courtyard"** (Bối cảnh: Sân trong tĩnh lặng — Trao chìa khóa riêng và lời hẹn ước đôi lứa).
- **Stage 5 (`800–1000 pts` — Cần Pass 3/4 để đạt 1000/1000 Eternal Star-Promise)**:
  17. `hutao_s5_sc1`: **"Private Sunset Cove in Crimson Swimwear"** (Bối cảnh: Bãi biển riêng tư lúc hoàng hôn — Kịch bản hẹn hò biển quyến rũ).
  18. `hutao_s5_sc2`: **"Candlelit Silk Cheongsam & Butterfly Kiss"** (Bối cảnh: Phòng suite ánh nến — Đêm hẹn hò lãng mạn trong bộ sườn xám thêu bướm vàng).
  19. `hutao_s5_sc3`: **"Morning Sunlight in Aether's Shirt"** (Bối cảnh: Buổi sáng bình yên bên nhau — Cùng pha trà sớm và viết bài thơ tình vĩnh cửu).
  20. `hutao_s5_sc4`: **"Beyond Life and Death: Eternal Star-Promise"** (Bối cảnh: Đỉnh đồi sao băng & Hoa mai nở rộ — Nghi thức trao nhẫn/vòng hoa mai kết ước trọn đời).

---

## 4. Kiến trúc 3-Tier Memory (`L1 / L2 / L3`) trong SQLite

Bảng dữ liệu SQLite (`waifulink.sqlite3`) được nâng cấp để tách rõ 3 tầng:
1. **`memory_l1_digest` (Tier 1 — Luôn nạp vào mọi Prompt)**:
   - Lưu bản tóm tắt siêu gọn (~150–250 từ) gồm: `player_nickname`, `known_likes`, `relationship_status_summary`, `last_scenario_title`, `last_date_summary`.
   - Khi nói chuyện phiếm qua EaglePhone, `gpt-6-luna` chỉ cần đọc **Tier 1** + 4 tin nhắn gần nhất → phản hồi cực nhanh, tự nhiên, không bị nhiễu bởi hàng ngàn từ lore không liên quan.
2. **`memory_l2_episodes` (Tier 2 — Tóm tắt từng Scenario & Buổi đi chơi)**:
   - Mỗi khi hoàn thành 1 Scenario (ví dụ `hutao_s1_sc2`) hoặc 1 chuyến Free-Roam, hệ thống lưu 1 dòng tóm tắt ngắn (`episode_summary`) kèm `tags`.
   - Chỉ nạp vào Prompt khi người chơi đang ở trong Scenario tiếp theo hoặc hỏi về các buổi đi chơi gần đây.
3. **`memory_l3_archive` + `quests_and_events` (Tier 3 — Tìm kiếm theo từ khóa khi nhắc lại)**:
   - Lưu toàn bộ kỷ niệm chi tiết, lời hứa, lịch sử quà tặng và các nhiệm vụ quá khứ (`ALREADY_HAPPENED_WITH_AETHER`).
   - Khi tin nhắn của Aether có chứa từ khóa khớp với `tags` / `keywords` (hoặc khi người chơi hỏi *"Do you remember..."*), hàm `retrieve_tiered_memory_context()` tự động kích hoạt **Tier 3 Deep Recall**, lấy đúng mảnh ký ức đó bơm vào prompt để Waifu nhớ lại chính xác từng chi tiết!
