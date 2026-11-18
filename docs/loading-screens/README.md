# Loading artwork — Project Wibu / Wibu World

**03/11 — Presentation DONE / user runtime PASS:** người dùng xác nhận toàn bộ thay đổi hoạt động hoàn hảo. [Project state / điểm vào cho agent](../presentation-current-state.md).178ảnh đã duyệt/cài, loading2s/menu4s, nhạc random+tự đổi bài, true intro bypass. Đã dọn40file build/QA/cache tạm; giữ nguồn/artwork/TXD/ASI/backup. Không còn việc chờ trong task này.

**03/11 — Đã cài menu tự đổi bài / true intro skip:** [Bàn giao và rollback](menu-autonext-no-intros-2026-11-03.md). Hết bài chọn ngẫu nhiên bài khác, không ghi default; bỏ qua hai trạng thái movie trước decoder. Chỉ đổi WibuMenu+state;178TXD, timer2s/4s, playlist/INI, PECore/exe/movie giữ nguyên. Build/native probes/hash/rollback-preflight đạt; chưa mở game, chờ user test. Nguồn hiện tại `staging/project-eagle/menu-autonext-no-intros-20261103`.

**03/11 — Đã cài178ảnh / loading2s / menu4s:** [Bàn giao và rollback](library-install-2026-11-03.md). User đã duyệt nốt M15/LS03, thư viện178/178duyệt (89loading+89menu). Cài180payload+state vào gameplay-lab,178texture decode/native timer/config/hash checks đạt;92file được bảo vệ và đoạn audio INI giữ nguyên. Đã nhả khóa, chưa mở game; chờ user test. Nguồn update hiện tại: `staging/project-eagle/art-library-install-20261103`.

**03/11 — EXC06 đã duyệt đầy đủ:** [Danica/Vodyanitsa V2](batch-EXC06-outfits-v2-2026-11-03.md) được user duyệt, Odette/Jean giữ bản gốc. Gói extra24/24đã duyệt; thư viện178 =173duyệt+5chờ (M15four/LS03one). Expansion133/133đã tạo,128/133duyệt. Chỉ cập nhật metadata, mọi ảnh giữ nguyên hash; chưa cài game.

**03/11 — EXC06 sửa trang phục V2:** [Danica / Vodyanitsa](batch-EXC06-outfits-v2-2026-11-03.md) đã sửa theo note mới, chờ duyệt; Odette/Jean đã duyệt, giữ nguyên file/hash. Danica đen–ivory–teal với chi tiết maid/váy ngắn/nối tất đùi; Vodyanitsa one-piece cổ/hông mở như Odette. Thư viện178 =171duyệt+7chờ; extra22/24duyệt, expansion126/133duyệt và133/133đã tạo. Chưa cài game.

**03/11 — EXC06 / tạo ảnh hoàn tất:** [Odette / Danica / Vodyanitsa / Jean](batch-EXC06-2026-11-03.md) có bốn loading đơn chờ duyệt theo note mới; EXC05 đã duyệt. **Extra24/24 và toàn expansion133/133 đã tạo đủ**, thư viện178 =169duyệt+9chờ (EXC06four/M15four/LS03one). Giữ mọi asset cũ/selected revisions, chưa cài game. Hết batch gen theo kế hoạch; tiếp theo chốt review/tổng hợp và chuẩn bị tích hợp theo yêu cầu.

**03/11 — Extra EXC05:** [Mona / Chiori / Navia / Lumine](batch-EXC05-2026-11-03.md) có bốn loading đơn chờ duyệt: Mona bộ một mảnh khoét hông cao, Chiori gravure/editorial, Navia lingerie satin/ren quý tộc Pháp, Lumine phiêu lưu hoang dã. Fischl V4/EXC04 đã duyệt. Extra20/24tạo,16duyệt; thư viện174 =165duyệt+9chờ. Chưa cài; batch cuối EXC06 Odette/Danica/Vodyanitsa/Jean.

**02/11 — Fischl fitted/fine lace:** [Áo ôm ren + váy gothic nhiều tầng, ren mảnh hơn](batch-EXC04-fischl-lace-refinements-2026-11-02.md) theo hai reference mới, V4 chờ duyệt. Hoa văn thưa/mảnh và màu vải nhẹ hơn ở áo/tất, thân áo có lót kín. V1/V2/V3 và ba ảnh duyệt giữ nguyên. Extra16tạo/15duyệt; thư viện170 =164duyệt+6chờ. Chưa cài; EXC05 Mona/Chiori/Navia/Lumine giữ kế hoạch.

**02/11 — Fischl streetwear revision:** [Cropped tee + miniskirt gothic](batch-EXC04-fischl-streetwear-v2-2026-11-02.md) đã xuất, chờ duyệt; khác rõ phom váy liền/corset cũ. Columbina/Citlali/Lisa đã duyệt và giữ nguyên file/hash. Chỉ thay selection Fischl, bản cũ giữ riêng. Extra16tạo/15duyệt; thư viện170 =164duyệt+6chờ. Chưa cài; kế tiếp vẫn EXC05 Mona/Chiori/Navia/Lumine.

**02/11 — Capella extras EXC04:** [Columbina / Citlali / Lisa / Fischl](batch-EXC04-2026-11-02.md) có bốn loading đơn chờ duyệt: Columbina mềm mại/ren/nơ, Citlali đồ ngủ hồng theo ảnh user, Lisa trưởng thành trêu ghẹo giữ tỷ lệ gốc, Fischl gothic lưới/ren kín và nét trẻ. Giữ Columbina đã tạo trước ngắt, không gen lại. EXC03 đã duyệt. Extra16/24tạo,12duyệt; thư viện170 =161duyệt+9chờ. Chưa cài; kế tiếp EXC05 Mona/Chiori/Navia/Lumine.

**02/11 — Capella extras EXC03:** [Arlecchino / Hu Tao / Furina / Kirara](batch-EXC03-2026-11-02.md) có bốn loading đơn chờ duyệt. Arlecchino cape/boots góc cạnh đinh bạc, thần thái áp đảo; Kirara hai găng tay mèo, hai đuôi và streetwear nữ miêu. Clorinde crop-v2 và toàn EXC02 đã duyệt. Extra12/24tạo,8duyệt; thư viện166 =157duyệt+9chờ. Chưa cài; kế tiếp EXC04 Columbina/Citlali/Lisa/Fischl.

**02/11 — Clorinde cropped revision:** [Áo/shorts ngắn hơn, lộ eo và bụng](batch-EXC02-clorinde-crop-v2-2026-11-02.md) đã xuất, chờ duyệt. Yelan/Nefer/Nicole đã duyệt, giữ nguyên file/hash. Old Clorinde giữ riêng, chỉ thay selection. Extra8tạo/7duyệt; thư viện162 =156duyệt+6chờ. Chưa cài; kế tiếp vẫn EXC03 Arlecchino/Hu Tao/Furina/Kirara.

**02/11 — Capella extras EXC02:** [Clorinde / Yelan / Nefer / Nicole](batch-EXC02-2026-11-02.md) có bốn loading đơn chờ duyệt. Clorinde dùng cropped cổ V +shorts cạp cao tím–đen theo lựa chọn mới sau lượt đầu bị ImageGen chặn; ba người còn lại giữ phom Capella, Nicole giữ mũ signature. EXC01 đã duyệt. Extra8/24tạo,4duyệt; thư viện162 =153duyệt +9chờ. Chưa cài. Kế tiếp EXC03 Arlecchino/Hu Tao/Furina/Kirara.

**02/11 — Capella extras EXC01:** [Lauma / Ronova / Tsaritsa / Raiden](batch-EXC01-2026-11-02.md) có bốn loading đơn chờ duyệt, cùng phom đồ Capella của Alice LS03, màu riêng và pose/cảnh riêng. [Kế hoạch24ảnh /6batch](capella-extra-batch-plan-2026-11-02.md) đã lưu. Extra4/24đã tạo; bộ trước109/109 giữ nguyên. Thư viện158 =149duyệt +9chờ; mục tiêu mới178. Không cài game. Kế tiếp EXC02 Clorinde/Yelan/Nefer/Nicole, giữ mũ Nicole.

**02/11 — LS03 Alice + Istaroth:** [Loading đôi Re:Zero light-novel couture](batch-LS03-2026-11-02.md) đã tạo: Alice lấy đồ Capella LN, Istaroth lấy đồ Liliana LN cách tân, giữ nhận diện Genshin trưởng thành. LS02 đã duyệt. **109/109 ảnh mở rộng đã tạo**,104 duyệt; thư viện154 =149 duyệt +5 chờ (M15 bốn +LS03 một),33/35 batch duyệt. Chưa cài. Hết batch tạo ảnh theo kế hoạch; tiếp theo duyệt phần còn lại và tổng hợp.

**02/11 — Loading đôi LS02:** [Asmoday+Lumine và Signora+Raiden Shogun](batch-LS02-2026-11-02.md) có hai ảnh chờ duyệt; đổi outfit ba người, Raiden trưởng thành khiêu gợi uy quyền theo user. LS01 đã duyệt.102/109 duyệt,108 tạo; thư viện147 duyệt +6 chờ. Chưa cài; kế tiếp LS03 Alice+Istaroth, một loading đôi cuối.

**02/11 — Loading đôi LS01:** [Rhinedottir+Tsaritsa và Ronova+Lumine](batch-LS01-2026-11-02.md) có hai ảnh chờ duyệt; Lumine quý phái quyến rũ theo user, mỗi cặp khác pose đứng–ngồi. LSS03 đã duyệt.100/109 duyệt,106 tạo; thư viện145 duyệt +6 chờ. Chưa cài; kế tiếp LS02 Asmoday+Lumine và Signora+Raiden Shogun.

**02/11 — Loading LSS03:** [Asmoday mini dress và Signora đầm burgundy xẻ bên](batch-LSS03-2026-11-02.md) có hai ảnh đơn chờ duyệt; giữ hai output đầu, không rescale. MS03 đã duyệt; Alice LSS01 bản gốc giữ nguyên.98/109 duyệt,104 tạo; thư viện143 duyệt +6 chờ. Chưa cài; kế tiếp LS01 Rhinedottir+Tsaritsa và Ronova+Lumine loading đôi.

**02/11 — Menu MS03:** [Alice playsuit và Istaroth halter dress](batch-MS03-2026-11-02.md) có hai ảnh chờ duyệt; giữ hai output đầu, không rescale. LSS02 đã duyệt; Alice LSS01 bản gốc giữ nguyên.96/109 duyệt,102 tạo; thư viện141 duyệt +6 chờ. Chưa cài; kế tiếp LSS03 Asmoday/Signora loading đơn.

**02/11 — Loading LSS02:** [Ronova evening separates và Istaroth draped couture](batch-LSS02-2026-11-02.md) có hai ảnh đơn chờ duyệt; giữ hai output đầu, không rescale. MS02 đã duyệt, Alice LSS01 vẫn bản gốc.94/109 duyệt,100 tạo; thư viện139 duyệt +6 chờ. Chưa cài; kế tiếp MS03 Alice/Istaroth menu đơn.

**02/11 — Menu MS02:** [Asmoday jumpsuit và Signora cocktail couture](batch-MS02-2026-11-02.md) có hai ảnh chờ duyệt; giữ hai output gốc. LSS01 đã duyệt, Alice chọn bản gốc trước rescale để thấy đùi; bản chỉnh mũ lưu lịch sử.92/109 duyệt,98 tạo; thư viện137 duyệt +6 chờ. Chưa cài; kế tiếp LSS02 Ronova/Istaroth loading đơn.

**02/11 — Loading LSS01:** [Hai ảnh đơn Rhinedottir đầm cúp ngực/xẻ bên và Alice thành thị](batch-LSS01-2026-11-02.md) chờ duyệt; đã sửa riêng khung mũ Alice bị cắt đáng kể. MS01 đã duyệt.90/109 duyệt,96 tạo; thư viện135 duyệt +6 chờ (M15+LSS01). Chưa cài; kế tiếp MS02 Asmoday/Signora menu đơn.

**02/11 — Menu MS01:** [Rhinedottir phóng khoáng và Ronova thờ ơ](batch-MS01-2026-11-02.md) có hai ảnh menu chờ duyệt, đúng reference bổ sung; hai output gốc giữ nguyên. 88/109 duyệt, 94/109 tạo; M15 vẫn chờ pass, thư viện133 duyệt +6 chờ. Chưa cài; kế tiếp LSS01 Rhinedottir/Alice loading đơn.

**02/11 — Mở rộng sáu quý bà:** [17 artwork đặc biệt /9 batch](special-six-batch-plan-2026-11-02.md): mỗi người menu đơn +loading đơn +tham gia loading đôi; thêm Alice/Istaroth, giữ bốn cặp cũ. Nhận 10 reference bổ sung và personality notes. Tổng mới 109 ảnh; 88 duyệt/92 tạo, M15 chờ pass. Chưa gen hoặc cài thêm; kế tiếp MS01.

**02/11 — Reference đặc biệt:** [Sáu ảnh Rhinedottir, Ronova, Signora, Asmoday, Istaroth, Alice](special-character-reference-review-2026-11-02.md) chờ xác nhận nhận diện; đã sửa nhãn nguồn Ronova trong audit cũ. Chưa tạo artwork mới; M15 vẫn chờ duyệt.

**02/11 — Menu M15:** [Sigewinne, Linnea cropped/mini skirt, Vodyanitsa quý phái và Yanfei tự tin](batch-M15-2026-11-02.md) có bốn ảnh đơn chờ duyệt; M13/M14 đã duyệt. 88% duyệt /92% đã tạo; thư viện 133 duyệt +4 chờ. Chưa cài bộ mới; kế tiếp MS01 Rhinedottir/Ronova.

**02/11 — M13 + M14:** [Tám menu công viên/picnic và phố pastel](batch-M13-M14-2026-11-02.md) chờ duyệt, giữ tạo hình nhỏ dễ thương; đã sửa riêng đoạn chân/giày thừa Yaoyao. Nicole/Zibai sửa chân đã duyệt. 80% duyệt /88% đã tạo; thư viện 125 duyệt +8 chờ. Chưa cài bộ mới; kế tiếp M15.

**02/11 — Chân Zibai v3 + Nicole:** [Zibai sửa dáng hai chân, giữ hai tay đã sửa; Nicole giữ bản hai chân hiện tại](zibai-legs-v3-and-nicole-review-2026-11-02.md). Chờ duyệt hai bản sửa; mở lại approval Zibai do lỗi mới được phát hiện. 78% duyệt /80% đã tạo. Chưa cài game; kế tiếp M13.

**02/11 — M12 sửa chân Nicole:** [Hai chân rõ, giữ mũ/mặt/outfit](batch-M12-nicole-legs-v2-2026-11-02.md). Charlotte/Sandrone/Prune đã duyệt, giữ nguyên đúng hash. 79% duyệt /80% đã tạo; thư viện 124 duyệt +1 chờ. Chưa cài bộ mới; kế tiếp M13.

**02/11 — Menu M12:** [Charlotte, Nicole, Sandrone, Prune](batch-M12-2026-11-02.md) có bốn ảnh đơn chờ duyệt; Nicole quyến rũ/mũ signature, Sandrone sắc sảo kiêu ngạo theo user. M11 sửa tay đã duyệt; 76% duyệt /80% đã tạo, thư viện 121 duyệt +4 chờ. Chưa cài bộ mới; kế tiếp M13.

**02/11 — M11 sửa tay Zibai:** [Hai tay rõ: một ở hông, một tựa lan can](batch-M11-zibai-arms-v2-2026-11-02.md). Lauma/Nefer/Lan Yan đã duyệt, giữ nguyên đúng hash. 75% duyệt /76% đã tạo; thư viện 120 duyệt +1 chờ. Chưa cài bộ mới; kế tiếp M12.

**02/11 — Menu M11:** [Lauma, Nefer, Lan Yan, Zibai](batch-M11-2026-11-02.md) có bốn ảnh đơn chờ duyệt, theo gợi ý vóc dáng/queen couture/đầm tà mở. L11 v2 đã duyệt; 72% duyệt /76% đã tạo, thư viện 117 duyệt +4 chờ. Chưa cài bộ mới; kế tiếp M12.

**02/11 — L11 sườn xám v2:** [Danica/Arlecchino liền thân, xẻ giữa đùi và chân trần](batch-L11-cheongsam-v2-2026-11-02.md) theo hướng giảm độ hở user đã chấp thuận; một ảnh sửa chờ duyệt. Linnea/Sigewinne giữ nguyên đúng hash. 71% đã duyệt /72% đã tạo; chưa cài game, kế tiếp M11.

**02/11 — L11 review:** Linnea/Sigewinne đã duyệt. Danica/Arlecchino bị user loại vì quá kín; giữ bản đó để đối chiếu, không tính đã duyệt. Hướng xẻ sâu đã bị công cụ chặn, không thử lại. 71% đã duyệt; M11 chưa tạo. [Chi tiết](batch-L11-2026-11-02.md).

**02/11 — Loading L11:** [Linnea/Sigewinne mùa hè; Danica/Arlecchino sườn xám thành thị](batch-L11-2026-11-02.md) có hai ảnh đôi chờ duyệt. Cặp sườn xám dùng bản kín đáo hơn sau khi mức xẻ sâu bị công cụ từ chối. M10 đã duyệt; 70% duyệt /72% đã tạo, thư viện 115 duyệt +2 chờ. Chưa cài bộ mới; kế tiếp M11.

**02/11 — Menu M10:** [Mualani beach-city, Varesa chubby/crop/váy ren bèo, Aino workshop, Ineffa solo đen–trắng](batch-M10-2026-11-02.md) có bốn ảnh đơn chờ duyệt. L10 v2 đã duyệt; 66% duyệt /70% đã tạo, thư viện 111 duyệt +4 chờ. Chưa cài bộ mới; kế tiếp L11 hai cặp.

**02/11 — L10 sửa v2:** [Đầu Odette tự nhiên hơn; tóc, nét mặt và móng Nefer theo reference mới](batch-L10-corrections-v2-2026-11-02.md). Ineffa/Aino đã duyệt, giữ nguyên file. 64% duyệt /66% đã tạo; thư viện 109 duyệt +2 chờ. Chưa cài bộ mới; kế tiếp M10.

**02/11 — Loading L10:** [Skirk/Odette băng giá, Ineffa/Aino cyberpunk, Nefer/Prune boutique Ai Cập](batch-L10-2026-11-02.md) có ba ảnh đôi chờ duyệt. M09 đã duyệt; 63% duyệt /66% đã tạo, thư viện 108 duyệt +3 chờ. Chưa cài bộ mới; kế tiếp M10.

**02/11 — Menu M09:** [Shinobu nữ tính, Xilonen disco, Iansan/Jahoda sporty vui tươi](batch-M09-2026-11-02.md) có bốn ảnh đơn chờ duyệt. L09 v2 đã duyệt; 59% duyệt /63% đã tạo, thư viện 104 duyệt +4 chờ. Chưa cài bộ mới; kế tiếp L10.

**02/11 — L09 sửa v2:** [Sửa chân Lynette/Sandrone, tăng nét sắc sảo/quyến rũ Sandrone và thêm mũ Nicole](batch-L09-corrections-v2-2026-11-02.md). Lan Yan/Zibai đã duyệt, giữ nguyên. 57% duyệt /59% đã tạo; gallery 102 duyệt +2 chờ. Bộ mới vẫn staging; kế tiếp M09.

**02/11 — Loading L09:** [Lan Yan/Zibai, Lynette/Sandrone, Charlotte/Nicole và preview M09](batch-L09-2026-11-02.md) có ba ảnh đôi chờ duyệt, bám gợi ý riêng. 56% duyệt /59% đã tạo; gallery chung 101 duyệt +3 chờ. Chưa cài bộ mới.

**01/11 — M08 sửa anatomy:** [Nilou hai chân và Faruzan trục thân/tay](batch-M08-anatomy-v2-2026-11-01.md) chờ duyệt; Candace/Xianyun giữ nguyên đã duyệt. Gợi ý riêng Zibai/Sandrone/Nicole đã lưu cho L09. Chưa cài bộ mới.

**01/11 — Menu M08:** [Candace, Nilou, Faruzan, Xianyun và preview L09](batch-M08-2026-11-01.md) có bốn ảnh đơn chờ duyệt. 52% duyệt /56% đã tạo; gallery chung 97 duyệt +4 chờ. Chưa cài bộ mới.

**01/11 — Loading L08:** [Sayu/Dori, Mualani/Varesa, Xilonen/Jahoda](batch-L08-2026-11-01.md) có ba ảnh đôi chờ duyệt, outfit đa dạng theo nhân vật. Tiến độ 49% duyệt /52% đã tạo, gallery chung 94 duyệt +3 chờ. Chưa cài bộ mới.

**01/11 — Menu M07:** [Sara, Chevreuse, Chasca, Aloy](batch-M07-2026-11-01.md) có bốn ảnh đơn chờ duyệt; 45% duyệt /49% đã tạo. Gallery chung 90 duyệt +4 chờ; chưa cài bộ mới.

**01/11 — Đã duyệt L07 + Arlecchino v2:** 45/100 ảnh mở rộng đã duyệt, 13/30 batch; thư viện chọn 90 ảnh, không còn ảnh chờ. [Rule thời trang nữ trưởng thành](wibu-world-art-direction.md) ưu tiên quyến rũ, tự tin, thanh lịch. Bộ mới vẫn staging; batch kế tiếp M07.

**01/11 — L07 và Arlecchino v2:** [Ba loading đôi + Arlecchino đầm cocktail, sửa hai chân](batch-L07-and-Arlecchino-v2-2026-11-01.md) chờ duyệt. Gallery chung 86 duyệt +4 chờ; 45/100 slot mở rộng đã tạo. Chưa cài bộ mới.

**01/11 — Menu M06:** [Dehya, Xinyan, Arlecchino, Danica](batch-M06-2026-11-01.md) có bốn ảnh đơn chờ duyệt. L06 v3 đã duyệt; roster 38% duyệt /42% đã tạo. Gallery chung 83 ảnh duyệt +4 chờ; chưa cài bộ mới.

**01/11 — L06 v3:** [Collei đứng ngửi hoa, đồ bám thiết kế gốc; Candace sửa hai chân](batch-L06-pose-anatomy-v3-2026-11-01.md) chờ duyệt. P18 Faruzan/Xianyun giữ nguyên; không tăng số poster hoặc cài vào game.

**01/11 — L06 đổi trang phục:** [Collei váy botanical; Candace/Nilou đầm cocktail](batch-L06-outfits-v2-2026-11-01.md) chờ duyệt; Faruzan/Xianyun đã duyệt, giữ nguyên file. Gallery chung 81 duyệt +2 chờ; chưa cài bộ mới.

**01/11 — Loading L06:** [Collei/Emilie, Candace/Nilou, Faruzan/Xianyun](batch-L06-2026-11-01.md) có ba ảnh đôi chờ duyệt. M05 đã duyệt; mở rộng đạt 35% duyệt /38% đã tạo. Gallery chung 80 ảnh duyệt +3 chờ; chưa cài bộ mới.

**01/11 — Menu M05:** [Yae Miko, Yun Jin, Mizuki, Lynette](batch-M05-2026-11-01.md) có bốn ảnh đơn chờ duyệt. L05 đã duyệt; roster đạt 31% duyệt /35% đã tạo. Gallery chung có 76 ảnh duyệt +4 chờ; chưa cài bộ mới.

**01/11 — Artwork:** [Tổng hợp thư viện và L05](art-library-progress-and-L05-2026-11-01.md): 73 ảnh đã duyệt, 3 L05 chờ duyệt; kế hoạch gen thêm 100 ảnh đạt 28% duyệt /31% đã tạo. Chưa cài bộ mới.

**01/11 — M04 sửa Odette:** Ba ảnh Eula/Escoffier/Skirk đã duyệt. [Gallery tóc Odette v2](../../../staging/project-eagle/menu-batches/M04-odette-hair-v2-20261101/gallery.html) dùng reference mới của user, búi tóc xanh băng gọn; chờ duyệt, chưa cài.

**01/11 — L04 v2 đã duyệt:** [ba cặp với pose khác rõ](batch-L04-v2-poses-2026-11-01.md), giữ nguyên bản đầu, chưa cài. [M04 — Eula, Escoffier, Skirk, Odette](batch-M04-2026-11-01.md) đã có bốn ảnh đơn chờ duyệt.

**01/11/2026 — L04 chờ duyệt, M03 đã pass:** Xinyan–Dehya, Xiangling–Yanfei, Yun Jin–Yae Miko có [gallery L04](../../../staging/project-eagle/loading-batches/L04-20261101/gallery.html) và [báo cáo](batch-L04-2026-11-01.md). Cả ba dùng bản đầu, không gọi chỉnh sửa thêm. Chưa cài, M04 chưa bắt đầu.

**01/11/2026 — M03 chờ duyệt, L03 đã pass:** Lisa, Rosaria, Fischl, Layla có [gallery M03](../../../staging/project-eagle/menu-batches/M03-20261101/gallery.html) và [báo cáo](batch-M03-2026-11-01.md). Giữ nhân vật lớn, chỉ sửa mũ/trâm thực sự bị cắt. Chưa cài, L04 chưa bắt đầu.

**01/11/2026 — L03 chờ duyệt, M02 đã pass:** Noelle–Sucrose, Lisa–Rosaria, Fischl–Layla có [gallery L03](../../../staging/project-eagle/loading-batches/L03-20261101/gallery.html) và [báo cáo](batch-L03-2026-11-01.md). Nhân vật lớn; chỉ chỉnh chi tiết bị cắt. Chưa cài, M03 chưa bắt đầu.

**01/11/2026 — M02 chờ duyệt, L02 đã pass:** Noelle, Sucrose, Collei, Emilie đã có [gallery M02](../../../staging/project-eagle/menu-batches/M02-20261101/gallery.html) và [báo cáo](batch-M02-2026-11-01.md). Giữ bốn bản đầu, không gọi chỉnh sửa thêm. Chưa cài, chưa bắt đầu L03.

**01/11/2026 — L02 chờ duyệt:** Amber–Yoimiya, Ningguang–Navia, Eula–Escoffier đã có [gallery L02](../../../staging/project-eagle/loading-batches/L02-20261101/gallery.html) và [báo cáo](batch-L02-2026-11-01.md). Giữ nhân vật lớn; chỉ sửa chi tiết phụ kiện thực sự bị cắt. Chưa cài, chưa bắt đầu M02.

**01/11/2026 — L01 và M01 đã user pass, chưa cài:** [gallery M01](../../../staging/project-eagle/menu-batches/M01-20261101/gallery.html), [báo cáo M01 và quy tắc framing](batch-M01-2026-11-01.md). Giữ nhân vật lớn như bản đầu; chỉ sửa khung khi thật sự bị cắt, không tạo thêm biến thể sau khi đã duyệt.

**01/11/2026 — kế hoạch roster đã pass, L01 chờ duyệt ảnh:** hoàn tất Tsaritsa–Vodyanitsa, Columbina–Yumemizuki Mizuki, Vesna–Lauma. [Gallery L01](../../../staging/project-eagle/loading-batches/L01-20261101/gallery.html), [báo cáo và điều phối](batch-L01-2026-11-01.md). Ba ảnh mới giữ ở staging; chưa cài hoặc bắt đầu M01.

**01/11/2026 — bộ 9 ảnh và kế hoạch roster đã user pass:** [kế hoạch 83 + 4 nhân vật / 30 batch nhỏ](female-roster-batch-plan-2026-11-01.md), [coverage từng người](../../../staging/project-eagle/female-roster-art-plan-20261101/coverage-plan.json), [audit reference đặc biệt](special-character-reference-audit-2026-11-01.md). Giữ ảnh đã duyệt; đề xuất gen thêm 32 loading đôi + 60 menu đơn cơ sở và 8 ảnh đặc biệt. Chưa gen hoặc cài phần roster mở rộng.

**01/11/2026 — startup và bộ 9 artwork đã user pass, artwork chưa cài:** user xác nhận intro hoạt động, crash do mở nhiều cửa sổ game. Đã chuẩn bị Barbara sửa tay + 6 ảnh đơn + bộ ba + bộ đôi, **chưa cài**: [gallery](../../../staging/project-eagle/loading-art-refresh-20261101/gallery.html), [báo cáo artwork](barbara-and-eight-artworks-2026-11-01.md). Hai video gốc đã thay bằng Project Wibu khoảng 0,2 giây mỗi clip: [kết quả/backup/phục hồi](startup-project-wibu-2026-11-01.md), [audit](intro-skip-audit-2026-11-01.md), [hàng đợi từng hạng mục](../work-items/2026-11-01-codex-wibu-startup-intros.md). Target hiện tại là gameplay-lab. Phần dưới giữ khảo sát/production history ngày 14/10, không dùng đường clean lịch sử để cài lại vào bản lưu trữ.

Khảo sát ngày **14/10/2026**, giờ Asia/Saigon. Game mục tiêu: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa clean\gta sa clean`.



Snapshot khảo sát ban đầu: `data\Changelog.txt` ghi **v1.3 / June 2026**; `PECore.log` khi khảo sát lưu build **Jun 15 2026** và **GTA SA v1.0 HOODLUM**, phiên 13/10/2026. Log live đã cập nhật sau lần thử pilot ngày 14/10; xem biên bản triển khai bên dưới.



**Bản đầy đủ đã cài ngày 14/10/2026:** 14 artwork anime 2D phẳng, đủ 23 nhân vật nữ Genshin, outfit đô thị, logo Wibu World trắng/đen và Project Wibu với silhouette Hu Tao. Người dùng sẽ tự test trong game. Xem [kết quả, bằng chứng và rollback](wibu-world-implementation.md), [gallery ảnh decode cuối](../../../staging/project-eagle/loading-screens/implementation/qa/LOADSCS-wibu-world/gallery.html), [art direction](wibu-world-art-direction.md) và [mapping 23 nhân vật](wibu-world-screen-map.json). Các phần inventory bên dưới mô tả snapshot gốc.



## Kết luận cần dùng khi chọn artwork



- Đường loading trong executable hiện tại mở **`models\txd\LOADSCS.txd`**, chọn texture `title_pc_US` và các tên `loadsc1`…`loadsc14` **bên trong dictionary này**. Đây là bộ widescreen Stars & Stripes/Eagle, không phải 14 file SA vuông cùng tên bên cạnh. Kết luận dựa trên disassembly cục bộ; chưa đo file access hoặc hình cuối cùng sau mọi ASI hook trong runtime.

- **`New Official Loading Themes` là theme nhạc:** các file được log cài là WAV `GENRL\Bank_076\sound_001…008.wav`; không có TXD artwork trong thư mục này. Không chọn thư mục này làm đường cài ảnh.

- `gta3.std.stream` bị tắt nhưng **`gta3.std.sprites` vẫn được log nạp**. Vì thế phải kiểm tra đường thay ảnh qua sprites riêng; không bật lại streaming để thử loading.

- Hướng nghệ thuật đã chốt: **anime/cel shading, bố cục GTA, chỉ nữ Genshin và outfit đô thị**. 9 khung đôi + 5 khung đơn phủ đủ 23 tên; vẽ toàn cảnh thống nhất. Wordmark mới là **Grand Theft Auto Wibu World**, lettering gợi Genshin.

- Pilot mới: **Hu Tao + Citlali / LOADSC8**, 1920×1080 DXT1. Title đổi thành **Project Wibu** với silhouette Hu Tao; PNG startup PECore và caption là các đích riêng. Xem [research branding](project-wibu-branding-research.md).

## Bộ ảnh và dữ liệu đối chiếu

- [Gallery toàn bộ texture đã decode](../../../staging/project-eagle/loading-screens/gallery.html) — mỗi ảnh có ID, source và thông số; các texture menu được tách để không nhầm phạm vi.
- [Manifest JSON](manifest.json) — đường nguồn, SHA-256 nguồn/bản trích, member/texture, codec, kích thước, mip và alpha.
- [Contact sheet bộ LOADSCS](../../../staging/project-eagle/loading-screens/previews/loadscs-posters.jpg) — 14 poster chính, đối chiếu texture ID và tên.
- [Trace loading/render và bằng chứng](loading-trace.md).
- [PNG startup nhúng trong PECore](../../../staging/project-eagle/loading-screens/source/pe-resources/PECore-RCDATA-200.png) — resource `E0001`, tách khỏi poster loading.
- [Staging index](../../../staging/project-eagle/loading-screens/README.md) — raw TXD, PNG và script chỉ đọc.

Đã trích **25 dictionary TXD, 75 texture/75 PNG**, tổng raw **43.162.812 byte**, không có gap decode trong các texture được chọn. Codec gặp: **71 DXT1, 3 DXT3, 1 X8R8G8B8**, native **D3D9**; tất cả texture trong inventory này có **một mip**. PNG là preview decode; native chunk, encoded raster và file TXD là những loại hash khác nhau. Raw source được copy nguyên byte, không phải TXD tái dựng. Decoder DXT1/DXT3 được đối chiếu với Pillow DDS: RGB lệch tối đa một mức do lượng tử RGB565, alpha khớp; uncompressed X8R8G8B8 khớp qua kiểm tra channel order độc lập. Xem [biên bản kiểm decoder](../../../staging/project-eagle/loading-screens/decode-validation.json).

Ngoài TXD có **một PNG nhúng** `PECore.asi::RCDATA/200/1033`, đã trích nguyên 166.605 byte: **640×640, RGBA 8-bit, có alpha**, không có mip theo nghĩa TXD. Manifest có mục `embedded_resources` riêng, không cộng nó thành texture thứ 76 trong TXD. Log/changelog mô tả splash khởi động PECore 5 giây; việc resource này được chính window đó vẽ vẫn chưa được chứng minh bằng call flow/runtime.

| Nhóm trên đĩa | Nội dung trích thực tế | Vai trò/độ xác minh |
| --- | --- | --- |
| `models\txd\LOADSCS.txd` | 17 texture: NVIDIA, EAX, `LOADSC1`…`LOADSC14`, `title_pc_US` | Dictionary được hàm loading cục bộ mở; poster và title là mục tiêu kỹ thuật chính. Hai vendor logo chưa được chứng minh hiển thị trong luồng đã trace. |
| `models\txd\loadsc0.txd`…`loadsc14.txd` | 15 ảnh 512×512, bộ GTA SA, logo/text bake trong tranh | Có file; luồng `LoadSplashes` đã trace không mở chúng riêng. Tham khảo bố cục; không tự cài từng file này. |
| `models\txd\LOADSUK.txd` | 15 texture SA 512×512, nhiều variant pose/background khác bộ loose | Variant có mặt; chưa xác minh đường chọn trong Eagle hiện tại. Không đồng nhất theo tên. |
| `models\txd\load0uk.txd` | Logo SA và legal, 512×512 | Candidate title variant, chưa chứng minh active. |
| `models\txd\splash1.txd`, `splash2.txd`, `splash3.txd` | Hai postcard “Greetings from Vice City”, 512×256; dictionary splash3 rỗng | Có file; chưa chứng minh là startup splash thực tế. Không gọi số 1/2/3 là trình tự. |
| `models\fronten1/2/3.txd`, `fronten_pc.txd` | 25 texture: logo radio/arrow, atlas nền menu/map, mảnh viền, cursor | `LoadAllTextures` có đường nạp riêng. Không phải 25 loading screen, ngoài phạm vi artwork. |
| `plugins\CustomStartScreenByDarkP1xel.asi` + INI XYZ | Plugin và thông số camera/điểm trong thế giới | Candidate scene 3D; không có bằng chứng nó là pack ảnh loading. Chi tiết static và gap trong trace. |
| `PECore.asi::RCDATA/200/1033` | PNG Project Eagle 640×640, nền trong suốt | Resource startup candidate tách riêng; PECore splash 5 giây có log/changelog, resource-to-window use chưa nghiệm thu. |

Inventory giới hạn ở candidate loading/menu được yêu cầu và lookup basename nhẹ trong `models`/`modloader`; không phải scan toàn bộ archive thế giới. `archive_member=null` nghĩa là source TXD loose, không phải member IMG. Trong TXD, tên texture được ghi ở từng entry `textures`; chữ hoa/thường phải được bảo toàn khi đóng gói lại.

## Những gì nhìn thấy trong ảnh trích

### Bộ chính: LOADSCS

Đây là poster đã ghép hoàn chỉnh, **một raster cho mỗi khung**, không có lớp nhân vật/background/logo riêng trong TXD. Ba khung đầu 3840×2160 thiên về phố, pickup và xe thể thao. Các khung sau chủ yếu 1920×1080 dùng nền gradient tím/xanh/đỏ, silhouette thành phố hoặc đồi và nhân vật lớn ở nửa phải. `LOADSC11` là 2000×1124; `title_pc_US` là 3800×2048. Không chuẩn hóa chúng về một kích thước chung chỉ vì gọi là widescreen.

Nhân vật có contour đen rõ, mảng shadow ít cấp, màu áo tách mạnh khỏi nền; background giảm chi tiết để đọc được silhouette. Logo **Grand Theft Auto / Stars and Stripes** đã bake vào phần trái dưới của poster. Title có biểu tượng **Project Eagle**, legal và các logo nhỏ bake trong raster khác. Không coi chúng là text được game vẽ động.

`LOADSC7` (`T0050`) và `LOADSC14` (`T0056`) có **encoded raster payload SHA-256 giống hệt nhau**, tức cùng pixel payload; native chunk hash khác vì metadata/tên member khác. Không tự xóa một texture hoặc coi hai số là hai cảnh khác nhau. Thứ tự member trong archive cũng không phải thứ tự hiển thị.

### Bộ SA và các phần ngoài mục tiêu

Bộ SA vuông dùng nền khói beige/green/teal, nhân vật lớn, đường phố/xe/nhà ít màu và logo góc trái dưới. `loadsc0` là collage với logo giữa và legal ở đáy. LOADSUK có những variant khác thực sự, ví dụ hai người/cảnh xe khác; không xem chúng là bản sao chỉ qua basename.

Các `back*` trong fronten2 là atlas/mảnh menu: preview có vùng nhiễu màu lớn và dải ảnh phong cảnh nhỏ phía dưới. Đây là nội dung raster đã decode, **chưa phải bằng chứng lỗi file hoặc vùng sẽ xuất hiện trên màn hình**; cần biết UV/rect của menu. Không dùng chúng làm tranh loading full screen. Hai postcard Vice City có chữ bake, còn sprite cursor/radio/arrow có chức năng UI riêng.

## Render và vùng cần giữ

Disassembly `CLoadingScreen::LoadSplashes` tại `0x5900B0` xác nhận directory `MODELS\TXD\`, slot `loadscs`, file `loadscs.txd`, title và tên `loadsc%d`. Hàm tạo permutation và gán **7 sprite: một title và sáu poster chọn trong các index 1…14**. Vì vậy bộ có 14 poster không có nghĩa mỗi lượt sẽ thấy cả 14 hay lần nào cũng bắt đầu ở `LOADSC1`.

PECore có module `[Splash]` khởi động riêng và log bản vá loading bar: expected file count tăng từ 100 lên 402. Cấu hình bật `TransparentMenu`, log ghi patch frontend background/scaling. Scan hẹp PECore/Modloader_Patch chưa thấy string hoặc direct reference thay `LOADSCS`/hàm loading cơ sở; kết quả âm tính này **không loại trừ hook gián tiếp/signature scanning**. REA provider không sẵn; phân tích dùng pefile/Capstone có sẵn, không setup thêm. Vì vậy source trên là đường cơ sở đã trace, không phải lời cam kết toàn bộ render sau hook đã được quan sát.

`CLoadingScreen::RenderSplash` tại `0x58FF60` vẽ rect phủ viewport `(-5,-5,width+5,height+5)`, clamp và có fade. Đường cơ sở này không có tile/layer cho từng nhân vật. **Kết quả aspect cuối cùng sau WidescreenFix và các ASI hook vẫn cần runtime**: INI `FrontendAspectRatio=16:9` là cấu hình, chưa đủ để kết luận mọi ảnh được center-crop, letterbox hay stretch. Không thiết kế artwork dựa trên một quy tắc crop chưa đo.

Loading bar, progress/status text và fade là phần renderer/UI riêng; **không bake chúng vào tranh mới**. Trước khi runtime xác định rect thật, có thể dùng vùng ít chi tiết ở dải đáy khoảng 12–15% như một *dự phòng thiết kế*, không gọi đó là safe area đã đo. Mặt, bàn tay và chi tiết nhận diện không chạm mép ngoài. Giữ khoảng trống logo ở trái dưới theo đúng raster đích, không mặc định vị trí giống nhau giữa SA và LOADSCS.

Logo đang bake nên khi vẽ lại cần tách thành lớp compositing được kiểm tra; chưa có sẵn alpha logo độc lập trong archive này. Bước artwork giữ nhận diện/logo gốc theo phạm vi hiện tại; thay logo hay title là lựa chọn riêng, chưa được duyệt. Không yêu cầu công cụ sinh ảnh tự viết lại các chữ trong logo.

## Hướng nghệ thuật ưu tiên

Giữ tóc, màu mắt, silhouette và chi tiết nhận diện của Genshin. Chuyển trang phục thành biến thể phố có chủ ý: áo khoác, bomber, vest, kính, dây chuyền hoặc trim gợi màu nhân vật; không bỏ mọi chi tiết đến mức thành nhân vật anime chung. Aether dùng tóc vàng, bím tóc và palette đen/trắng/vàng; trang phục có thể thích nghi để ngồi xe/đi phố nhưng vẫn nhận ra ngay.

Mỗi poster được vẽ như **một cảnh thống nhất**: nhân vật, xe, đường, ánh sáng và bóng cùng phối cảnh. Dùng pose đọc rõ ở thumbnail, contour đậm và 2–3 cấp cel shadow; background là hình khối đô thị có biển hiệu, đèn, palm trees, đường ven biển hoặc garage, không bê UI/screenshot gameplay vào tranh. Ưu tiên không khí lái xe dạo phố/nghe radio; vũ khí là lựa chọn props riêng nếu sau này muốn giữ mức action của khung gốc.

| Cách làm | Kết quả | Đánh đổi |
| --- | --- | --- |
| Giữ nguyên background/raster gốc, chỉ vẽ lại nhân vật vào đúng pose | Rất gần bộ hiện có, kiểm tra mapping nhanh | Dễ tạo cảm giác ghép lớp nếu style/ánh sáng khác; nền và trang phục ít đổi; logo vẫn bake. |
| **Vẽ lại toàn bộ khung, giữ nhịp bố cục GTA** — ưu tiên | Nhân vật/cảnh/xe thống nhất theo anime; mỗi khung có câu chuyện Genshin sống trong Eagle | Cần duyệt sketch/composition, kiểm tra nhận diện nhân vật và logo layer; khối lượng art cao hơn. |

Phương án ưu tiên giữ **vị trí trọng tâm, khoảng trống và palette tương phản** của khung cũ, nhưng cho phép đổi pose/phụ kiện đủ để nhân vật hòa vào cảnh. Không phải tracing từng nét, cũng không phải chèn render nhân vật lên một nền có sẵn.

## Mapping đề xuất cho bộ poster thực sự được đường loading tham chiếu

Tất cả nhân vật trừ trọng tâm Aether là **đề xuất chưa duyệt**, không lấy rating/ped roster làm artwork roster. Các bảng `npc-rosters` hiện để trống Char dự kiến nên không cung cấp một danh sách artwork đã chốt. Số `LOADSCn` là tên texture, không phải thứ tự slideshow.

Thông số trong cột cuối là **đích đóng gói giữ nguyên của texture hiện tại**, chưa phải yêu cầu sinh ảnh mới trong lượt khảo sát. Mỗi hàng dùng một PNG master RGB không bake bar/status/fade; bản TXD D3D9 giữ đúng name, dimensions, codec và mip count theo manifest. Với mục tiêu DXT1, không tự thêm alpha. `LOADSC6` đang là X8R8G8B8 nên không đổi sang DXT1 chỉ để đồng nhất.

| Texture / khung hiện tại | Nhân vật và cảnh đề xuất | Pose / màu / bố cục | Export và đóng gói |
| --- | --- | --- | --- |
| `T0044 / LOADSC1`: nữ ngoái vai, phố olive | **Yelan** đi qua phố thương mại sau chuyến lái xe | Ngoái vai nửa phải, jacket navy/trim xanh, nền olive/cream và cao ốc nhạt; logo trái dưới | 3840×2160, DXT1; member của LOADSCS |
| `T0045 / LOADSC2`: cowboy và pickup, palm sunset | **Dehya** cạnh pickup ở garage ven đường | Góc 3/4 phải, jacket đỏ/đen, chìa khóa hoặc radio; cam cát, palm/power line; logo trái dưới | 3840×2160, DXT1; cùng dictionary |
| **`T0046 / LOADSC3`: convoy xe thể thao, phố/bridge xanh** | **Aether**, xe coupe vàng/đen và xe bạn đồng hành — pilot ưu tiên | Aether ở ghế lái nhìn qua cửa hoặc đứng nửa phải cạnh xe; góc xe chéo giữ motion, nền cobalt/indigo, vàng làm accent, logo trái dưới | **3840×2160, DXT1; thay đúng một member trong bản copy LOADSCS** |
| `T0047 / LOADSC4`: người vest trắng, đồi tím/đỏ | **Kaeya** trước club trên sườn đồi | Vest trắng/trim xanh, cầm chìa khóa/điện thoại, trọng tâm phải; gradient tím/đỏ giữ nhịp gốc | 1920×1080, DXT1 |
| `T0048 / LOADSC5`: người vest sát mép phải | **Diluc** rời lounge, xe đỗ ở rìa phố | Nửa thân 3/4, tóc đỏ/tux đen, tay sửa cổ tay áo; mận đỏ/indigo, nhiều khoảng trống trái | 1920×1080, DXT1 |
| `T0049 / LOADSC6`: nữ với cocktail, skyline magenta | **Beidou** ở rooftop bar ven cảng | Ngoái vai, jacket khoác vai, ly nước/đồ uống tùy duyệt; magenta/violet và silhouette cảng | 1920×1080, **X8R8G8B8** |
| `T0050 / LOADSC7`: người áo khoác, prop chéo tiền cảnh | **Zhongli** bên sedan tại đường ven biển | Coat charcoal, tay cầm chìa khóa/điện thoại tạo đường chéo, mắt nhìn ngoài khung; violet/crimson | 1920×1080, DXT1 |
| `T0051 / LOADSC8`: nam vest đang chỉnh áo | **Diluc** trước garage đêm | Pose kéo/chỉnh jacket nửa phải, xe và biển hiệu silhouette; đỏ sâu/violet; không đổi thành wallpaper centered | 1920×1080, DXT1 |
| `T0052 / LOADSC9`: nhân vật cúi người, nền cây/đồi | **Kazuha** tựa xe thể thao ở overlook | Lean nghiêng thấp, jacket trắng/đỏ, radio portable; đường chân trời thấp, indigo/cam hoàng hôn | 1920×1080, DXT1 |
| `T0053 / LOADSC10`: hai người, nhân vật chính phía phải | **Keqing + Yelan** ở phố neon | Một người trước, một người nhỏ hơn phía sau trái, bất đối xứng giữ depth; lilac/blue, biển hiệu ít chi tiết | 1920×1080, DXT1 |
| `T0054 / LOADSC11`: ba sedan/limousine nhìn chéo | **Ningguang** và đoàn xe đón khách | Xe vẫn là chủ thể, nhân vật nhỏ cạnh xe ngoài cùng phải; pearl/cream, teal, đỏ/tím ở nền | **2000×1124**, DXT1; giữ kích thước riêng |
| `T0055 / LOADSC12`: nam vest chắp tay | **Zhongli** trước khách sạn/casino | Trọng tâm phải, tay chỉnh găng/khuy áo, vàng trim trên charcoal; burgundy/indigo, background rất giản lược | 1920×1080, DXT1 |
| `T0057 / LOADSC13`: nam mở vali, background xe | **Aether** mở vali đồ du lịch/đĩa nhạc trên xe | Nửa thân phải, vật dụng kể chuyện roadtrip; đen/vàng và neon xanh/tím, giữ silhouette vali | 1920×1080, DXT1 |
| `T0056 / LOADSC14`: pixel payload trùng khung 7 | **Zhongli** hoặc **Aether**, biến thể coastal dusk chỉ nếu muốn khung riêng | Dùng cùng brief của 7 để đồng nhất; hoặc duyệt biến thể mới; chưa mặc định tăng roster | 1920×1080, DXT1; vẫn giữ member riêng |

Để bộ không quá loãng, có thể chọn **Aether + 4–6 nhân vật** rồi tái sử dụng với outfit/cảnh khác. Không cần 14 nhân vật khác nhau cho 14 texture.

### Mapping phần được giữ làm tham khảo/ngoài đợt thay chính

| Screen/texture | Hướng dùng hoặc ý tưởng nếu người dùng mở rộng phạm vi | Thông số và route |
| --- | --- | --- |
| `loadsc1…14.txd` loose + `LOADSUK/loadsc1…14` | Tham khảo nhịp SA: bandana/nhân vật → Aether street jacket; người dựa xe → Aether roadtrip; officer/detective → Yelan/Keqing; BMX → Kazuha; portrait phố/beach → Dehya/Beidou; nhóm bên lowrider → Aether + Kazuha; vest/Chinatown → Zhongli + Ningguang. Chỉ lập mapping riêng nếu route này được chọn thực sự. | 512×512 DXT1 theo từng entry; **không cài vào route chính chỉ vì tên giống nhau**. Các variant phải đối chiếu từng preview. |
| `LOADSCS/title_pc_US` | Title Eagle hiện tại giữ nguyên. Collage Aether và các chuyến đi chỉ là hướng cho một yêu cầu title riêng. | 3800×2048 DXT1; title và legal cần approval phạm vi riêng. |
| `loadsc0`, `LOADSUK/loadscUK`, `load0uk` | Collage/logo/legal SA, giữ như source reference. | 512×512; activation chưa xác minh. |
| `LOADSCS/nvidia`, `eax` | Vendor startup logos; giữ nguyên. | 2048×1024 DXT1; route hiển thị chưa chứng minh. |
| `E0001 / PECore RCDATA/200/1033` | Logo startup Project Eagle nhúng; giữ nguyên, ngoài artwork batch. | 640×640 PNG/RGBA; không thay ASI/resource. |
| `splash1`, `splash2`, dictionary rỗng `splash3` | Postcard Vice City xanh/cam, giữ nguyên. Nếu được chọn sau này: silhouette Aether/xe ven biển với palm theo postcard. | 512×256 DXT1; không giả định thứ tự/active. |
| `fronten*` / scene CustomStartScreen | Menu atlas, radio icons, cursor hoặc scene 3D; không đưa vào artwork batch. | Cần tác vụ khác nếu người dùng muốn đổi. |

## Phép thử một screen sau yêu cầu triển khai

1. **Chốt artwork pilot và môi trường test:** duyệt brief Aether/LOADSC3, logo policy, một ảnh proof đúng ratio. Chọn bản thử riêng có save path đã xác minh và không bị agent gameplay/radio dùng; không chạy trên một lab đang được chỉnh đồng thời. Ghi resolution/aspect/settings đầu vào.
2. **Backup và build ngoài game:** dùng raw source có hash trong manifest; copy dictionary ra staging mới. Thay đúng texture `LOADSC3` trong bản copy, giữ name/case, native D3D9, 3840×2160, DXT1, mip count và opaque semantics. Giữ 16 member còn lại nguyên chunk nếu công cụ hỗ trợ; nếu tool tái serialize, phải so sánh pixel + metadata và báo khác biệt, không gọi là nguyên byte. Parse/decode lại output, so poster, mip/alpha và file size.
3. **Route ưu tiên cần nghiệm thu:** thư mục overlay riêng dạng `modloader\Genshin Loading Pilot\txd\loadscs.txd` qua `std.sprites`, dựa trên plugin docs/config/log đã trace. Đây là **whole dictionary replacement**, không phải đặt `LOADSC3.png` hay `loadsc3.txd` loose. Không sửa thư mục New Official Loading Themes, không bật std.stream, không ghi trực tiếp models\txd khi chưa thử overlay.
4. **Chứng minh đúng nguồn:** đọc log install của sprites và file-access trace nếu công cụ runtime có sẵn; chụp khi LOADSC3 thật sự được chọn. Sáu poster được chọn nên một lượt không xuất hiện pilot chưa chứng minh thất bại. Phân biệt overlay được nhận, file được mở, texture được chọn và hình đã render đúng. Nếu sprites route không hoạt động trên build này, dừng để review trace; fallback trực tiếp thay dictionary chỉ cân nhắc sau backup/approval triển khai, không tự bật plugin hoặc patch core.
5. **Visual/runtime test:** cold start/title, new game và load save thử riêng không ghi đè save; ghi nhận frame đang render và frame fade. Kiểm đúng nhân vật/logo, không méo mặt/bánh xe, không cắt đầu/tay, mép clamp, flash/đen, alpha halo, bar/status đọc được. Đo 16:9 trước; nếu dùng 4:3/ultrawide thì thử chúng riêng, không suy từ INI. So ít nhất một baseline với pilot về thời gian loading, peak RAM/VRAM nếu đo được và lỗi/crash; giữ dimensions/codec tránh tăng tài nguyên không cần thiết.
6. **Rollback:** gỡ/di chuyển đúng thư mục pilot ra ngoài modloader trong môi trường thử, cold start lại và xác minh trở về source gốc. Nếu đã dùng fallback direct replacement có duyệt, phục hồi TXD từ backup có hash. Hash config/exe/save phải giữ nguyên trong phạm vi phép thử. Chỉ nhân rộng sau một pilot đạt.

## Bằng chứng, giới hạn và quyết định còn lại

Local source/config/log/disassembly là nguồn quyết định; [loading-trace.md](loading-trace.md) ghi địa chỉ, path và nguồn tham khảo code. Community reverse-engineered source chỉ dùng để hỗ trợ tên/ý nghĩa hàm, không gọi là tài liệu chính thức Rockstar hoặc bằng chứng runtime Eagle.

[Audit đầu ra](evidence/root-audit.json) đối chiếu source/raw hash, dimensions 75 PNG, link local và hai vùng code loading của `gta_sa.exe`/`gta_pe.exe`. Snapshot hash của exe/config/plugin được giữ trong evidence; snapshot sau khảo sát không tự chứng minh chúng chưa từng đổi trước snapshot. Trong lượt này công cụ chỉ đọc game và ghi staging/docs.

**Đã trả lời:** inventory và decode candidate; phân biệt theme nhạc/ảnh; dictionary và tên texture của đường loading cơ sở; menu khác loading; bố cục/logo bake; kế hoạch art, packaging và rollback có phạm vi một member.

**Còn cần runtime:** hook/plugin cuối cùng và CustomStartScreen có active/scene gì; startup/movie/title ordering; ảnh từng lượt new/load save thật sự thấy; aspect/crop sau mọi hook; tọa độ UI safe area; hoạt động overlay std.sprites, thời gian/fade và chi phí tài nguyên. Khảo sát này không đưa ảnh tái tạo thay cho gap runtime.

**Người dùng chọn ở bước sau:** hướng vẽ lại toàn cảnh hoặc giữ nền; pilot Aether/LOADSC3; roster và outfit; giữ logo nào nếu mở rộng title/branding. Báo cáo dừng tại kế hoạch này.
