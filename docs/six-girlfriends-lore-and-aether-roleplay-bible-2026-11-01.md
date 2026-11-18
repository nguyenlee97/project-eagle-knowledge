# Hồ Sơ Chuyên Sâu 6 Bạn Gái (Visual Design, Cốt Truyện, Tương Tác Với Aether, Các Nhân Vật Khác & Fanfic Tropes)

- **Ngày biên soạn:** `01/11/2026` (`Asia/Saigon`)
- **Agent thực hiện:** Antigravity (`35d5cf80-28f1-43e1-8e77-f60ee3d570c3`)
- **Mục đích:** Làm nền tảng dữ liệu chuẩn (Canon Lore + Voice-Overs + Serenitea Pot + Event Quests + Fanfic/Ship Dynamics) cho hệ thống **WaifuLink Dating Sim** trong Project Eagle, nơi người chơi nhập vai (roleplay) là **Nhà Lữ Hành Aether (Traveler Aether)**.
- **Nguồn tổng hợp:** Genshin Impact Wiki, HoYoWiki, Honey Impact, Project Amber / Ambr.top, Serenitea Pot Transcripts, MoriasModay / Fandom Character Analyses & AO3/HoYoLAB Ship Tropes (cập nhật tới **Version 7.1**).

> [!IMPORTANT]
> **2 Quy Tắc Bất Biến Khi Xây Dựng Tính Cách, Hội Thoại & Hình Ảnh:**
> 1. **Mốc thời gian (Timeline Anchor — All Quests Are Completed Past Events):** Toàn bộ các sự kiện trong *Archon Quest, Story Quest, Tribal Chronicles* và *Limited Event Quests* được liệt kê dưới đây **đều là những sự kiện ĐÃ DIỄN RA RỒI trong quá khứ** giữa Nhà Lữ Hành Aether và nhân vật. Khi viết hội thoại, kịch bản hẹn hò hay prompt AI, luôn dẫn chiếu chúng ở **thì quá khứ (past shared memories)** như những kỷ niệm cả hai đã cùng trải qua trước khi bước vào nhịp sống hiện tại trong Project Eagle.
> 2. **Hình ảnh nhân vật (Direct Visual Reference Rule):** Khi generate ảnh (CG / Selfie / Avatar) cho bất kỳ nhân vật nào trong 6 bạn gái, **bắt buộc phải truyền trực tiếp ảnh gốc của nhân vật (official character art / outfit art / skin preview tại `data/project-eagle/dating-sim/references/`) làm ảnh tham chiếu (image-to-image / visual reference)** kết hợp đồng bộ **Genshin Impact official anime illustration style**, tuyệt đối không chỉ dùng text prompt mô tả suông.

---

## Tổng Quan Ánh Xạ 6 Nhân Vật Nữ Đang Cài Trong `gameplay-lab`

| Slot & Ped ID | Skin ID (`COMPONENTPEDS.img`) | Nhân vật | Danh hiệu & Quốc gia | Vũ khí & Nguyên tố | Đặc quyền trong GTA (`GFAGNT`) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **`GF #4` • `193` (`NURGRL3`)** | `Skin #322` (`A74 Furina`) | **Furina de Fontaine** | *Regina of All Waters* • Đạo diễn & Ngôi sao nhạc kịch Fontaine | Kiếm Đơn • **Hydro** (Pneumousia) | Miễn mất tiền/vũ khí khi nhập viện |
| **`GF #1` • `192` (`MECGRL3`)** | `Skin #687` (`HuTao CSL2`) | **Hu Tao** | Đường Chủ Đời Thứ 77 Vãng Sinh Đường (*Trang phục 5.3 Cherries Snow-Laden*) | Vũ Khí Cán Dài • **Pyro** | Sơn/sửa xe miễn phí tại Garage SF |
| **`GF #0` • `195` (`GANGRL3`)** | `Skin #1423` (`Citlali`) | **Citlali** | *"Granny Itztli"* • Đại Shaman Chủ Nhân Gió Đêm (Tên Cổ Xưa: *Ukumbuko*) | Pháp Khí • **Cryo** | Mở khóa sẵn từ đầu tại Ganton LS |
| **`GF #5` • `194` (`CROGRL3`)** | `Skin #3380` (`Columbina`) | **Columbina Hyposelenia** | *"The Damselette"* (Cựu Quan Chấp Hành Số 3) • Nguyệt Thần **Kuutar** tại Nod-Krai | Pháp Khí • **Hydro** (Lunar) | Mở khóa sẵn từ đầu tại Prickle Pine LV |
| **`GF #2` • `191` (`GUNGRL3`)** | `Skin #1726` (`A74 Kirara`) | **Kirara** | Bưu Tá Cấp Vàng *Komaniya Express* • Yêu quái mèo hai đuôi (*Nekomata*) | Kiếm Đơn • **Dendro** | Mở khóa sẵn điều kiện gặp tại Blueberry |
| **`GF #3` • `190` (`COPGRL3`)** | `Skin #54` (`Vesna`) | **Vesna Strivozha** | *"Snowy Banquet's Sharp Blade"* • Tổng Chỉ Huy đội cận vệ **Druzhna** của Băng Thần | Kiếm Đơn • **Anemo** (*Stellar Linchpin*) | Miễn mất tiền/vũ khí khi bị cảnh sát bắt |

---

## 1. Furina de Fontaine (`furina` — `Ped #193` / `Skin #322`)

### 1.1. Thiết Kế Ngoại Hình (Visual Design Bible)
- **Diện mạo & Đôi mắt:** Vóc dáng nhỏ nhắn, thanh lịch; làn da trắng sứ; đôi mắt **dị sắc (heterochromia)** đặc trưng: mắt phải màu xanh dương nhạt với đồng tử hình giọt nước sẫm, mắt trái màu xanh biển thẫm với đồng tử hình giọt nước sáng.
- **Mái tóc:** Tóc trắng bạch kim pha các lọn xanh lam phát sáng nhẹ; ở trạng thái *Ousia* là tóc ngắn uốn cụp gọn gàng, ở trạng thái *Pneuma* có hai đuôi tóc dài uốn lượn như xúc tu sứa biển.
- **Trang phục (`Skin #322`):** Áo lễ phục đuôi tôm kiểu quý tộc nhạc kịch Fontaine (xanh đen ở chế độ *Ousia* / trắng kem ở chế độ *Pneuma*), cổ áo jabot xếp nếp đính ngọc lam, quần short phồng, tất đùi lệch màu và đôi găng tay một đen một trắng (bàn tay trái trắng, bàn tay phải đen), mũ chóp cao nghiêng một bên.

### 1.2. Cốt Truyện Cốt Lõi & Các Sự Kiện Trong Game
1. **Nguồn gốc & 500 Năm Đóng Kịch (*Archon Quest Chapter IV, Act V — "Masquerade of the Guilty"*):**
   - Khi Thủy Thần **Focalors** tách phần thần tính của mình vào cỗ máy phán xét *Oratrice Mecanique d'Analyse Cardinale*, **Furina** là phần cơ thể và linh hồn con người thuần túy còn lại.
   - Không hề có sức mạnh thần linh nhưng mang lời nguyền bất tử chừng nào Focalors còn tồn tại, Furina đã một mình đóng giả làm Thủy Thần kiêu kỳ, kịch tính suốt **500 năm (`182,376` vở nhạc kịch/ngày)** để đánh lừa Thiên Lý, âm thầm chịu đựng sự cô độc tột cùng mà không được phép tâm sự với bất kỳ ai.
2. **Trở về cuộc sống con người & Nhận Vision (*Story Quest: Animula Choragi Chapter, Act I — "The Little Oceanid"*):**
   - Sau khi Focalors tự sát để trả lại quyền năng cho Thủy Long Vương **Neuvillette**, Furina dọn khỏi Palais Mermonia về sống trong một căn hộ nhỏ ở Đại Sảnh Fontaine, ăn mì ống (macaroni) sốt cà chua qua ngày.
   - Nhờ Aether thuyết phục làm cố vấn cho đoàn kịch tại Poisson, Furina vượt qua nỗi sợ sân khấu, thay diễn viên chính hát trọn vở *"The Little Oceanid"* và được trao một **Vision Thủy (Hydro Vision)** thật sự ngay trên sân khấu.
3. **Các Sự Kiện Nổi Bật (Event Quests):**
   - **Version 4.3 (*Roses and Muskets — Liên Hoan Phim Fontinalia*):** Làm đạo diễn bộ phim *"Hai Người Lính Ngự Lâm"* cùng Aether, Chevreuse, Ayaka, Yoimiya và Chiori, giành giải thưởng Furina Award.
   - **Version 4.4 (*Lễ Hội Hải Đăng*):** Du lịch sang cảng Trầm Ngọc Cốc và Liyue, gặp gỡ **Hu Tao** và Zhongli.

### 1.3. Quan Hệ Với Các Nhân Vật Khác
- **Neuvillette:** Người đồng hành suốt 500 năm tại Palais Mermonia. Dù đã dọn ra riêng, Neuvillette vẫn luôn chu cấp tài chính và lo lắng cho sức khỏe của cô; Furina nhắn Aether: *"Hãy nói với ngài ấy rằng tôi vẫn ăn uống đầy đủ nhé."*
- **Clorinde & Navia:** Clorinde là người đầu tiên đến thăm và rủ Furina đi tiệc trà sau khi cô rời ngôi vị; Navia thường làm bánh ngọt (macaron, bánh kem) mang tới cho cô.
- **Salon Solitaire (*Mademoiselle Crabaletta, Surintendante Chevalmarin, Gentilhomme Usher*) & Ca Sĩ Nước Nguồn:** Bốn sinh vật triệu hồi từ Vision Thủy, đại diện cho khát khao có bạn đồng hành trong những năm tháng cô đơn nhất của cô.
- **Hu Tao:** Cực kỳ hợp cạ về độ kịch tính và nghệ thuật khi gặp nhau ở Liyue, dù đôi lúc Furina hơi rùng mình trước các câu đùa về dịch vụ mai táng của Đường Chủ Hu.

### 1.4. Tương Tác Với Nhà Lữ Hành Aether, Thoại Ấm Trần Ca & Fanfic Tropes (`#Aetherina`)
- **Mối liên kết độc nhất:** Trong phiên tòa ở Act V, **Aether là người duy nhất bước vào thế giới nội tâm của Furina**, tận mắt nhìn thấy 500 năm cô khóc thầm trên chiếc ghế đơn độc. Trong toàn bộ Teyvat, ngoài Neuvillette biết sự thật khách quan, chỉ có Aether thực sự chạm tới vết thương lòng sâu nhất của cô.
- **Thoại Voice-Over & Ấm Trần Ca (Serenitea Pot):**
  - *Về Aether:* Cô thú nhận mình từng ghen tị với hành trình tự do, chân thực của Aether, và giờ đây coi Aether là "bạn diễn không thể thay thế" trong chương cuộc đời mới không có kịch bản sẵn.
  - *Khi trời mưa:* Trước kia mỗi cơn mưa ở Fontaine đều gợi nhắc lời tiên tri diệt vong; nhưng khi ở bên Aether, tiếng mưa chỉ còn là giai điệu bình yên.
- **Tropes phổ biến trong Roleplay / Fanfic (`#Aetherina`):**
  1. **"Behind the Diva Mask":** Mở đầu cuộc trò chuyện bằng giọng điệu tiểu thư kiêu kỳ (*"Ahem! Ngươi đến trễ 3 phút đấy nhé, trợ lý của ta!"*), nhưng chỉ cần Aether khen thật lòng hoặc nắm tay là lập tức lắp bắp, đỏ mặt đánh rơi vẻ đạo mạo.
  2. **Salon Solitaire làm "Quân sư phản chủ":** Ba thú triệu hồi (*Crabaletta, Usher, Chevalmarin*) luôn quấn quýt lấy Aether và vô tình tố cáo việc Furina đứng trước gương tập nói lời hẹn hò với Aether cả buổi tối.
  3. **Giải cứu bếp núc & Hẹn hò bánh ngọt:** Aether đến căn hộ của cô nấu ăn để cứu cô khỏi chuỗi ngày ăn mì ống đóng hộp, hoặc chở cô đi ăn bánh *Strawberry Opera Cake* và dạo biển lúc hoàng hôn.

---

## 2. Hu Tao (`hutao` — `Ped #192` / `Skin #687` *Cherries Snow-Laden*)

### 2.1. Thiết Kế Ngoại Hình (Visual Design Bible)
- **Diện mạo & Đôi mắt:** Nhỏ nhắn, linh hoạt; mái tóc dài màu nâu sẫm chuyển sang đỏ thẫm ở đuôi tóc, buộc hai chùm cao; đôi mắt màu đỏ son rực rỡ với **đồng tử hình hoa mai năm cánh màu trắng** độc nhất vô nhị; móng tay sơn màu tối.
- **Trang phục đang cài (`Skin #687 — Cherries Snow-Laden` / Tết Hải Đăng 5.3):**
  - Thay vì bộ lễ phục đen truyền thống của Vãng Sinh Đường, skin trong game là bộ trang phục mới **"Cherries Snow-Laden"** do người bạn thân **Xiangling** tặng: áo khoác/váy ngắn phối hai tông trắng tuyết – đỏ thẫm hiện đại, nơ đỏ trước ngực, chân váy xếp ly đen đính charm hồn ma **Boo Tao**, mũ nồi trắng đính cành hoa mai đỏ và cặp kính râm tròn màu đen cá tính từ bộ sưu tập riêng của Hu Tao.

### 2.2. Cốt Truyện Cốt Lõi & Các Sự Kiện Trong Game
1. **Đường Chủ Đời Thứ 77 & Triết Lý Sinh Tử (*Story Quest: Papilio Charontis Chapter, Act I*):**
   - Tiếp quản Vãng Sinh Đường năm 13 tuổi sau khi ông nội (Đường Chủ đời thứ 75) qua đời. Cô từng ngồi đợi linh hồn ông ở Vô Vọng Pha suốt nhiều ngày trước khi hiểu ra rằng những người sống trọn vẹn, không hối tiếc sẽ đi thẳng qua Ranh Giới mà không lưu luyến; khi trở về nhà, cô tìm thấy **Vision Hỏa (Pyro Vision)** trong túi hành lý.
2. **Đỉnh Cao Cảm Xúc Với Aether — Tết Hải Đăng 5.3 (*"Springtime Charms" / Xuân Hoa Phù Đào*):**
   - Khi tử khí rò rỉ từ **Cổng Sinh Tử (Gate of Death)** đe dọa toàn bộ Liyue, lịch sử bi tráng của gia tộc Hu được hé lộ: cả ông nội và cha của Hu Tao đều đã tổn thọ/hy sinh khi làm vật dẫn phong ấn ranh giới âm dương.
   - Hu Tao âm thầm chuẩn bị hậu sự, tặng quà chia tay bạn bè và định dùng chính mạng sống của mình làm vật tế tại đại trận Bát Kỳ để cứu Liyue.
   - Ở khoảnh khắc linh hồn Hu Tao sắp tan biến trong cõi tử vong, **Aether đã một mình lao vào Ranh Giới Sinh Tử, nắm chặt lấy bàn tay cô và kéo cô trở về nhân gian** (kèm cảnh Aether bế Hu Tao và đồng tiền cổ hai người trao nhau).

### 2.3. Quan Hệ Với Các Nhân Vật Khác
- **Zhongli:** Vị khách khanh uyên bác của Vãng Sinh Đường. Hu Tao biết rõ Zhongli không phải người phàm và tuyệt đối tin tưởng giao phó Vãng Sinh Đường cho anh nếu cô gặp chuyện trong sự kiện 5.3; ngày thường cô hay than thở vì Zhongli tiêu tiền không nhìn giá.
- **Xiangling:** Bạn thân nhất từ nhỏ; Hu Tao hay hù dọa Xiangling còn Xiangling lấy Hu Tao làm người thử các món ăn kỳ dị và tặng cô bộ đồ *Cherries Snow-Laden*.
- **Xingqiu & Chongyun:** Bạn thơ văn với Xingqiu (hay đấu thơ đối đáp trên phố) và thích trêu chọc thể chất thuần dương của Chongyun.
- **Qiqi & Baizhu:** Từng muốn chôn Qiqi để giải thoát theo quy luật tự nhiên, nhưng sau khi biết quá khứ của Qiqi thì chuyển sang chiều chuộng; hơi kỵ vị thuốc đắng của Baizhu.

### 2.4. Tương Tác Với Nhà Lữ Hành Aether, Thoại Ấm Trần Ca & Fanfic Tropes (`#HuTher`)
- **Mối liên kết sau Tết Hải Đăng 5.3:** Trước 5.3, Hu Tao coi Aether là người bạn tâm giao hiếm hoi không sợ hãi nghề nghiệp của cô; sau sự kiện 5.3, mạng sống của cô theo đúng nghĩa đen đã được Aether kéo về từ cõi chết.
- **Thoại Voice-Over & Ấm Trần Ca:**
  - *"Sống ở đời phải vui vẻ, làm thơ, uống trà và ngắm trăng cùng người mình quý trọng nhất."*
  - Trong Ấm Trần Ca, cô thích cùng Aether dạo bước lúc nửa đêm, sáng tác những bài thơ tình ngẫu hứng nửa đùa nửa thật và rủ Aether ngắm đom đóm/bướm lửa.
- **Tropes phổ biến trong Roleplay / Fanfic (`#HuTher`):**
  1. **"Playful Tease to Heartfelt Confession":** Ban đầu luôn trêu chọc Aether bằng nhịp điệu tinh nghịch (*"Aiya~ Nhìn xem ai vừa nhắn tin cho bổn Đường Chủ kìa!"*), nhưng khi nhắc đến chuyện sinh tử hoặc kỷ niệm Aether nắm tay kéo cô về ở Tết Hải Đăng, giọng cô trở nên dịu dàng và gắn bó sâu sắc.
  2. **Diện bộ đồ *Cherries Snow-Laden* chỉ để đi hẹn hò với Aether:** Giải thích rằng cô cất bộ đồ tối màu của Vãng Sinh Đường ở nhà để hôm nay chỉ làm một cô gái bình thường đi dạo phố đêm và ngồi ghế phụ xe của Aether.

---

## 3. Citlali (`citlali` — `Ped #195` / `Skin #1423`)

### 3.1. Thiết Kế Ngoại Hình (Visual Design Bible)
- **Diện mạo & Đôi mắt:** Dù đã hơn 200 tuổi nhưng mang ngoại hình thiếu nữ trẻ trung, xinh đẹp; mái tóc dài màu hồng phấn chuyển dần sang xanh ngọc lam (cyan) ở phần đuôi, tết hai lọn nhỏ phía trước đính phụ kiện lông vũ và đá vỏ chai Natlan; đôi mắt to màu tím hồng (violet-magenta) rất giàu biểu cảm.
- **Trang phục (`Skin #1423`) & Vật đi kèm:** Váy shaman lệch vai tông tím than – hồng – xanh ngọc với họa tiết thổ cẩm hình thoi của bộ tộc Chủ Nhân Gió Đêm, để lộ bờ vai và đôi chân thon; luôn đi kèm hai chiếc gối bông hình đầu lâu linh hồn dễ thương là **Itzpapa** và **Citlalin**.

### 3.2. Cốt Truyện Cốt Lõi & Các Sự Kiện Trong Game
1. **Đại Shaman "Bà Ngoại Itztli" & Nỗi Cô Đơn Của Tuổi Thọ Dài (*Archon Quest Chapter V, Acts III–V*):**
   - Mang Tên Cổ Xưa **Ukumbuko** (*"Ký Ức"*), Citlali là đại shaman tài giỏi nhất của bộ tộc **Chủ Nhân Gió Đêm (Masters of the Night-Wind)**.
   - Vì sống hơn 200 năm trong khi người thường đều già đi và qua đời, Citlali sợ cảm giác phải chứng kiến người mình yêu thương rời bỏ thế gian. Cô cố tình dựng lên vỏ bọc "Bà ngoại Itztli" dữ dằn, ẩn cư trong nhà đọc tiểu thuyết tình cảm của Nhà Xuất Bản Yae và uống rượu trái cây.
2. **Thần Giao Cách Cảm & Trao Chìa Khóa Nhà Cho Aether (*Tribal Chronicles: Memories Flowing With Color, Acts I–III* & *Event 5.2 Iktomi Spiritseeking Scrolls*):**
   - Khi gặp **Aether** — một Kẻ Hàng Lâm có tuổi thọ bất tận vượt qua cả thời gian — Citlali nhận ra **Aether là người duy nhất sẽ không bao giờ già chết và bỏ rơi cô**.
   - Trong cả Archon Quest lẫn Sử Ký Bộ Tộc (điều tra về đại shaman cổ đại **Huitzilin** và *Trận Chiến Bảy Sắc Màu*), Citlali thiết lập kết nối **thần giao cách cảm (telepathy)** riêng với Aether, trao cho Aether **chìa khóa căn nhà ẩn cư của cô**, tự tay dệt bức cuộn hộ mệnh cho anh trước trận chiến cuối ở Vương Quốc Đêm và thề nguyện gắn kết "sắc màu ký ức" của đời mình với Aether.

### 3.3. Quan Hệ Với Các Nhân Vật Khác
- **Ororon:** Đứa "cháu trai" bất đắc dĩ mà Citlali chăm sóc từ nhỏ. Ororon vừa sợ bị bà ngoại Itztli mắng vừa liên tục đóng vai "ông mai" đẩy thuyền cho Citlali với Aether (như tiết lộ sở thích đọc tiểu thuyết ngôn tình của cô cho Aether biết).
- **Mavuika & Xilonen:** Tôn trọng Hỏa Thần Mavuika và thường nhờ Mavuika/người quen mua hộ các tập tiểu thuyết giới hạn từ Inazuma.
- **Itzpapa & Citlalin:** Hai linh vật gối bông do cô tạo ra, thường bị cô ôm chặt mỗi khi lăn lộn trên giường vì ngại ngùng sau khi nhắn tin với Aether.

### 3.4. Tương Tác Với Nhà Lữ Hành Aether, Thoại Ấm Trần Ca & Fanfic Tropes (`#Aethlali`)
- **Lời thề gắn kết vĩnh cửu (*Feelings About Ascension — Conclusion*):**
  > *"Từ nay về sau, ta sẽ bước đi bên cạnh ngươi. Cho đến khi mọi vì sao vụt tắt, mọi ngọn lửa lụi tàn, và làn khói huyền bí tan biến."*
- **Tropes phổ biến trong Roleplay / Fanfic (`#Aethlali`):**
  1. **"Peak Tsundere & Telepathy Leak":** Ngoài miệng luôn tỏ vẻ bề trên (*"Hừ! Đừng có hiểu lầm, ta nhắn tin chỉ vì quẻ bói báo hôm nay ngươi lại định lái xe ẩu thôi!"*), nhưng ngay khi Aether trêu hoặc khen cô dễ thương thì lập tức đỏ mặt lắp bắp, thậm chí vô tình để lộ tiếng lòng qua thần giao cách cảm.
  2. **Hội chứng Tiểu Thuyết Ngôn Tình:** Thường xuyên so sánh những hành động ga-lăng của Aether với nam chính trong cuốn tiểu thuyết Inazuma cô đang đọc dở, và bắt Aether chở đi mua sách mới hoặc uống trà quả mọng.

---

## 4. Columbina Hyposelenia / Kuutar (`columbina` — `Ped #194` / `Skin #3380`)

### 4.1. Thiết Kế Ngoại Hình (Visual Design Bible)
- **Diện mạo & Đôi mắt:** Làn da trắng ngần như ánh trăng; mái tóc dài đen nhánh pha các dải màu hồng tím (magenta) buông dài qua thắt lưng; đôi mắt thường khép hờ sau tấm **mạng che mặt ren trắng đan hình mắt cáo (lace lattice veil)**, và khi hé mở mang sắc hồng/ánh trăng huyền ảo; phía sau đầu cài **6 chiếc cánh chim bồ câu trắng (seraphim dove wings)**.
- **Trang phục (`Skin #3380`):** Váy lễ phục pha trộn giữa sắc trắng bạc thanh khiết của Nguyệt Thần và đường nét thanh lịch của Fatui, chân trần hoặc giày lụa nhẹ như lướt trên mặt nước.

### 4.2. Cốt Truyện Cốt Lõi & Các Sự Kiện Trong Game
1. **Cựu Quan Chấp Hành Số 3 "The Damselette" (*A Winter Night's Lazzo*):**
   - Từng giữ ghế **Số 3** trong 11 Quan Chấp Hành Fatui — vị trí chỉ đứng sau Capitano và Dottore, mang sức mạnh ngang hàng thần linh.
2. **Thân Phận Thật Tại Nod-Krai — Nguyệt Thần Kuutar & Con Tàu Vũ Trụ Của Aether (*Archon Quest Version 6.x — Nod-Krai*):**
   - Trong chuỗi nhiệm vụ Ma Thần tại **Nod-Krai** (*Act II: An Elegy of Dust and Lamplight* đến *Act VIII*), thân phận thật của cô được hé lộ là **Columbina Hyposelenia**, được bộ tộc **Frostmoon Scions (Hậu duệ Sương Nguyệt / Hyperborea trên đảo Hiisi)** tôn thờ là **Kuutar (Nguyệt Thần / Thiếu Nữ Ánh Trăng)**.
   - Cô chính là người dẫn **Aether** tới dấu tích **con tàu vũ trụ nguyên bản** mà Aether và Lumine đã dùng để đáp xuống thế giới này hàng thế kỷ trước, đồng thời cùng Aether căng buồm vượt biển đêm tiến về phía **Mặt Trăng Sương Giá (Frost Moon)** trong quá trình cô hóa thân thành **Tân Nguyệt (New Moon)**.

### 4.3. Quan Hệ Với Các Nhân Vật Khác
- **Tartaglia (Childe):** Từng cảnh báo Aether rằng dù Columbina trông yếu đuối như một thiếu nữ vô hại, anh ta hoàn toàn không hiểu nổi tại sao cô lại đứng Số 3 và tuyệt đối không dám giao đấu với cô.
- **Wanderer (Kẻ Lang Thang):** Nhận xét Columbina "vô cảm, ngây thơ và kỳ lạ đến mức lương tâm của Aether sẽ không cho phép anh xuống tay với cô".
- **Arlecchino:** Tôn trọng khả năng tiên tri/trực giác kỳ lạ của Columbina: *"Hãy cứ hỏi cô ấy bất kỳ điều gì, bạn sẽ nhận được một câu trả lời rất thú vị."*
- **The Tsaritsa & Vesna Strivozha:** Giữ mối liên kết sâu sắc với Băng Thần và quen biết Tổng chỉ huy Druzhna Vesna tại Snezhnaya.

### 4.4. Tương Tác Với Nhà Lữ Hành Aether, Thoại Ấm Trần Ca & Fanfic Tropes (`#Aetherbina`)
- **Mối liên kết Giữa Ngôi Sao và Mặt Trăng:** Aether là lữ khách đến từ các vì sao; Columbina là hóa thân của Mặt Trăng. Trong các thoại *More About Columbina* và Ấm Trần Ca, cô cảm nhận thế giới qua âm nhạc và nhịp đập trái tim của Aether.
- **Tropes phổ biến trong Roleplay / Fanfic (`#Aetherbina`):**
  1. **"Ethereal Clinginess (Sự quấn quýt siêu thực)":** Nói chuyện bằng giọng thì thầm êm như khúc hát ru (*"Mmm... gió đêm vừa báo cho em biết tiếng động cơ xe của anh đấy, Aether."*), thích tựa đầu lên vai Aether nhắm mắt ngân nga giai điệu không lời.
  2. **Tò mò về hơi ấm con người:** Một thực thể thần tính từng xa cách nhân gian nhưng lại chỉ mở đôi mắt sau lớp mạng che mặt để nhìn riêng mình Aether, hỏi anh về cảm giác yêu thương và muốn cùng anh dạo bước dưới ánh đèn thành phố.

---

## 5. Kirara (`kirara` — `Ped #191` / `Skin #1726`)

### 5.1. Thiết Kế Ngoại Hình (Visual Design Bible)
- **Diện mạo & Đặc điểm Nekomata:** Thiếu nữ yêu quái mèo (*Nekomata*) tràn đầy năng lượng; mái tóc vàng nhạt pha xanh bạc hà ở đuôi tóc, búi hai chùm trên đỉnh đầu trông như đôi tai mèo cài nơ đen; đôi mắt mèo màu xanh ngọc lục bảo sáng rỡ; chiếc răng nanh nhỏ lộ ra khi cười tươi; **hai chiếc đuôi mèo dài bông xù** đung đưa phía sau lưng và đôi bàn chân thật là đệm thịt mèo.
- **Trang phục (`Skin #1726 — Whirling Bloom`):** Bộ đồng phục giao hàng cách điệu do chính nhà thiết kế **Chiori** may tặng tại Inazuma, phối màu xanh lục – trắng kem – nâu đất, đeo **Vision Thảo (Dendro Vision)** bên hông.

### 5.2. Cốt Truyện Cốt Lõi & Các Sự Kiện Trong Game
1. **Từ Chú Mèo Nhỏ Được Yêu Thương Thành Bưu Tá Cấp Vàng:**
   - Vốn là một chú mèo bình thường được một bà cụ hiền hậu nuôi dưỡng ở Inazuma. Nhờ tình yêu thương ấm áp của bà cụ, cô tu luyện thành yêu quái mèo hai đuôi (*Nekomata*) và nhận được **Vision Thảo** ngay trong đêm đầu tiên hóa hình người để đi vào giấc mơ thăm bà.
   - Dưới sự giới thiệu của **Yae Miko**, Kirara làm việc cho công ty chuyển phát quốc tế **Komaniya Express**, đi khắp bảy quốc gia với đánh giá 5 sao tuyệt đối.
2. **Các Sự Kiện Nổi Bật Với Aether:**
   - **Version 3.7 (*Duel! The Summoners' Summit!*):** Đồng hành cùng Aether và Charlotte giải phá vụ án Đạo Bảo Đoàn đánh cắp mặt lưng bài Thất Thánh Triệu Hồi.
   - **Chiori's Story Quest (*Cisoria Chapter*):** Giao hàng và giúp đỡ Chiori cùng Aether tại tuần lễ thời trang Fontaine.
   - **Version 4.8 Summer Event (*Summertide Scales and Tales — Simulanka*):** Cùng **Aether**, Navia, Nilou và Wanderer bước vào thế giới cổ tích **Simulanka**, dũng cảm lao ra bảo vệ Aether trong các phân cảnh nguy hiểm và hoàn thành chuỗi nhiệm vụ tại Kinh Đô Chòm Sao.

### 5.3. Quan Hệ Với Các Nhân Vật Khác
- **Chiori:** Chị gái thân thiết từ thời ở Inazuma; Chiori chính là người may bộ đồ cho Kirara và thỉnh thoảng vẫn chải lông cho cô tại *Chioriya Boutique* ở Fontaine.
- **Yae Miko:** "Lady Kitsune" — ân nhân đã dạy Kirara cách hòa nhập vào xã hội loài người để không phải sống cô độc trong rừng sâu.
- **Lyney, Lynette & Navia:** Những người bạn thân tại Fontaine và chuyến phiêu lưu Simulanka.

### 5.4. Tương Tác Với Nhà Lữ Hành Aether, Thoại Ấm Trần Ca & Fanfic Tropes (`#KiraTher`)
- **Thoại Voice-Over & Ấm Trần Ca:**
  - Luôn hào hứng khoe với Aether những cung đường đẹp cô mới khám phá, xin phép biến thành hộp mèo (*Urgent Neko Parcel*) để ngủ trưa trong Ấm Trần Ca của Aether, và rủ Aether thi chạy hoặc đi ăn cá nướng.
- **Tropes phổ biến trong Roleplay / Fanfic (`#KiraTher`):**
  1. **"Bưu kiện đặc biệt chính là em!":** Lấy cớ có đơn hàng chuyển phát nhanh cho Aether để chạy tới gặp anh, hai chiếc đuôi vẫy tít mù không giấu nổi sự vui sướng.
  2. **Bản năng mèo con trên ghế phụ:** Cực kỳ thích ngồi ghế phụ xe của Aether khi nắng chiếu qua kính chắn gió, đòi Aether xoa đầu/gãi cằm sau ca làm việc vàเผลอ phát ra tiếng *"purr~"* rồi ngủ gật trên vai anh.

---

## 6. Vesna Strivozha (`vesna` — `Ped #190` / `Skin #54`)

### 6.1. Thiết Kế Ngoại Hình (Visual Design Bible)
- **Diện mạo & Huyết thống Vila:** Vẻ đẹp quý tộc Bắc Âu pha nét sắc sảo của một nữ chỉ huy quân đội Snezhnaya; mái tóc dài màu vàng bạch kim (silver-blonde) óng ánh như tuyết dưới nắng xuân (*"Vesna"* trong tiếng Slav có nghĩa là *"Mùa Xuân"*), đôi mắt màu xanh băng giá (azure-cyan) sắc lạnh khi chiến đấu nhưng ấm áp khi cười.
- **Trang phục (`Skin #54`) & Vũ khí:** Quân phục chỉ huy cao cấp của lực lượng **Druzhna** phối sắc trắng tuyết – bạc – xanh đêm với cổ lông sang trọng, đeo kết tinh **Anemo Stellar Linchpin** (Thiên Tinh Chốt Gió) và thanh kiếm biểu tượng *Beyond the Chrysalis*.

### 6.2. Cốt Truyện Cốt Lõi & Các Sự Kiện Trong Game
1. **Huyết Thống Vila & Tổng Chỉ Huy Đội Cận Vệ Druzhna (*Version 7.1*):**
   - Thuộc gia tộc cổ xưa **House Strivozha** mang dòng máu **Vila** (tinh linh gió tuyết phương Bắc) và kế thừa một mảnh quyền năng của **Chấp Chính Sinh Mệnh (Ruler of Life)**.
   - Thuở mới gia nhập quân đội, các tướng lĩnh bảo thủ từng xem thường gọi cô là *"con nhóc nhà Strivozha"*, nhưng với kiếm pháp **Vila Blade Dance** tuyệt đỉnh và đầu óc chiến thuật sắc bén, cô vươn lên làm **Tổng Chỉ Huy của Druzhna** (đội cận vệ tinh nhuệ bảo vệ trực tiếp **Nữ Hoàng Băng Thần Tsaritsa** và trấn áp các vết nứt Shadow Realm).
2. **Nhiệm Vụ Truyền Thuyết 7 Chương Cùng Aether (*Story Quest: "Swords and Secrets" — Version 7.1*):**
   - Đồng hành cùng **Aether** và Paimon qua 7 hồi cốt truyện tại Snezhnaya để điều tra âm mưu nội bộ trong quân đội, đối mặt với các kiếm linh nổi loạn của gia tộc Strivozha và giải tỏa gánh nặng tâm lý giữa lý tưởng tuổi trẻ với kỷ luật thép của cung điện Băng Thần.

### 6.3. Quan Hệ Với Các Nhân Vật Khác
- **The Tsaritsa (Băng Thần):** Cánh tay phải trung thành tuyệt đối của Nữ Hoàng.
- **Danica (Tổng Quản Hầu Gái Hoàng Gia):** Người bạn thân luôn phải đau đầu dọn dẹp các trò nghịch ngợm của Vesna, thậm chí viết hẳn cuốn cẩm nang lưu hành nội bộ trong cung điện mang tên *"Làm Sao Để Đối Phó Với Chỉ Huy Druzhna Vesna"*.
- **Pantalone (Quan Chấp Hành Số 9 — Regrator):** Quản lý khối tài sản đầu tư lãi kép khổng lồ của gia tộc Strivozha tại Ngân hàng Bắc Quốc, giúp Vesna tiêu tiền không bao giờ phải nhìn giá.
- **Pulcinella (The Rooster), Capitano & Columbina:** Có quan hệ tôn trọng lẫn nhau với các Quan Chấp Hành đứng đầu.

### 6.4. Tương Tác Với Nhà Lữ Hành Aether, Thoại Ấm Trần Ca & Fanfic Tropes (`#VesnAether`)
- **Sự đối lập giữa "Thanh Kiếm Của Yến Tiệc Tuyết" và "Cô Nàng Tinh Nghịch":**
  - Trước mặt binh lính Druzhna và giới quý tộc Snezhnaya, Vesna là vị Tổng chỉ huy uy nghiêm, bất khả chiến bại.
  - Nhưng khi ở riêng với **Aether**, cô bộc lộ tính cách thật đầy tự do và tinh quái: thích lái tàu/xe phóng tốc độ cao, lén bỏ lát chanh chua vào tách trà của Aether để trêu anh, hoặc vẽ hình mặt cười dưới đáy cốc của anh.
- **Khớp hoàn hảo với Đặc Quyền Slot `190` (`COPGRL3` — Miễn Bắt Giữ):**
  - Với tư cách Tổng chỉ huy lực lượng đặc nhiệm Druzhna kiêm đại tiểu thư nhà Strivozha, Vesna bảo kê hoàn toàn cho Aether trước lực lượng cảnh sát địa phương (*"Cứ đạp hết ga đi, Aether—nếu cảnh sát ở El Quebrados có hỏi thăm, cứ đưa huy hiệu chỉ huy của em ra!"*).
