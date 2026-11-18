# Tìm lại skin trên YouTube và tự thêm link

Ngày 14/10/2026. Gallery hiện có **671 thẻ**: thêm **12 lựa chọn có nguồn tải**, giữ nguyên 659 ID/URL/ảnh của bản trước. Hai subagent **GPT Luna** rà lại 176 nhãn đang thiếu bằng tên nhân vật + game/anime + `GTA San Andreas skin`, có thử alias. Có **36 video cho 22 tên**, trong đó **24 video còn chờ link tải hoặc bằng chứng PC**.

Đợt này tìm trực tiếp trên trang kết quả YouTube và đọc metadata/mô tả video, bên cạnh kết quả tìm web. Tìm web với `site:youtube.com` đã bỏ sót một số video; vì vậy kết luận “chưa tìm thấy” ở các lượt trước có giới hạn. Các roster đã rà vẫn chưa bao phủ toàn bộ cast/playable. Bình luận/ghim không lấy được trong phản hồi trang công khai của lượt này; người dùng có thể mở video để lấy link rồi dán vào gallery. Một video chưa đủ bằng chứng danh tính không được đưa vào 36 video.

## Cách thêm skin bạn tìm được

Mở [gallery](../../staging/project-eagle/skin-search-gallery-2026-10-14/gallery.html), tải lại trang để nhận bản mới.

1. Nhấn **+ Thêm skin / link tôi tìm được** trên thanh công cụ, **Nhập link tôi tìm được** dưới tên còn thiếu hoặc **Gắn link tải cho video này** trong mục YouTube.
2. Chọn tên và series. Chỉ có video/trang nguồn thì lưu trước: mục ở trạng thái **chờ link tải**.
3. Điền **Link tải skin** (trang có nút tải hoặc URL gói) và lưu: thẻ lên đúng series, có thể đánh giá Thích/Hơi thích/Bình thường/Không sử dụng. Trạng thái ban đầu là Chưa chọn. Với video đã gắn link, video rời danh sách chờ.
4. Có thể thêm ảnh, size công bố, phiên bản và ghi chú. Dùng **Sửa link đã thêm** để sửa mà giữ ID/đánh giá.
5. Xuất **new-skin-ratings.json** để lưu/gửi lại. File chứa cả thẻ tự thêm và nguồn/video đang chờ; nạp lại khôi phục link và đánh giá. File đánh giá cũ vẫn nạp được.

Tự lưu phụ thuộc trình duyệt và địa chỉ mở. Khóa rating cũ/schema cũ giữ nguyên; link tự thêm dùng khóa `project-eagle-new-skin-manual-sources-v1`. Trước khi chuyển trình duyệt/địa chỉ, xuất JSON để mang theo dữ liệu. Gallery skin nhẹ có thể nạp JSON này để đối chiếu nhân vật Thích/Hơi thích.

Thumbnail YouTube dùng để nhận diện video, không phải ảnh render riêng được kiểm tra. Link người dùng tự thêm được ghi rõ nguồn và chưa được kiểm tra gói/tương thích Eagle. Size mới chưa công bố thì để trống. Chưa tải archive, cài model hoặc nghiệm thu rig.

## Nguồn mới đã có trong gallery

| Nhân vật | Series | Video | Nguồn tải do tác giả liên kết |
| --- | --- | --- | --- |
| Mari | Blue Archive | [Video](https://www.youtube.com/watch?v=wKu9sYQ5nXI) | [GTAinside](https://www.gtainside.com/en/sanandreas/skins/210989-iochi-mari-blue-archive/) |
| David Martinez | Cyberpunk: Edgerunners | [Video](https://www.youtube.com/watch?v=KCHxKryr4x4) | [MediaFire](https://www.mediafire.com/file/g9jnb1ujmrxlkra/David_Martinez.rar/file) |
| Fischl | Genshin Impact | [Video](https://www.youtube.com/watch?v=RoTe4BLXG-k) | [LibertyCity](https://libertycity.net/files/gta-san-andreas/168864-fischl-from-genshin-impact.html) |
| Kazuma Satou | Konosuba | [Video](https://www.youtube.com/watch?v=_ZnK50yL_Fw) | [GTAinside](https://www.gtainside.com/en/sanandreas/skins/170314-kazuma-satou-konosuba-fixed) |
| Megumin | Konosuba | [Video](https://www.youtube.com/watch?v=j0kL_rI9ZPI) | [GTAall](https://www.gtaall.net/gta-san-andreas/skins/104324-superdimensional-megumin.html) |
| Megumin | Konosuba | [Video](https://www.youtube.com/watch?v=iEHQEL6LUKA) | [MediaFire](https://www.mediafire.com/file/2sckxygm7si2acn/Skin_Megumin.zip/file) |
| Rock Lee | Naruto | [Video](https://www.youtube.com/watch?v=HLrscUM3PCI) | [GTAinside](http://www.gtainside.com/download.php?do=comments&cat=124&id=35558) |
| Franky | One Piece | [Video](https://www.youtube.com/watch?v=k9Zxs10b0Dc) | [Trang tác giả](https://gtasaevolutionressubd.blogspot.com/2023/11/skin-de-franky.html) |
| Tony Tony Chopper | One Piece | [Video](https://www.youtube.com/watch?v=yJcRwvNbOqw) | [Trang tác giả](https://gtasaevolutionressubd.blogspot.com/2023/11/skin-de-chopper.html) |
| Kurisu Makise | Steins;Gate | [Video](https://www.youtube.com/watch?v=xosYcazlhdc) | [GTAall](https://www.gtaall.com/gta-san-andreas/skins/162625-makise-kurisu-from-steins-gate-v2-1.html) |
| Gawr Gura | VTuber | [Video](https://www.youtube.com/watch?v=MzAdPU-dmws) | [LibertyCity](https://libertycity.net/files/gta-san-andreas/169830-gawr-gura.html) |
| Usada Pekora | VTuber | [Video](https://www.youtube.com/watch?v=0_mqMD8scnU) | [GTAinside](https://www.gtainside.de/en/sanandreas/skins/211483-v-tuber-usada-pekora-from-valkyrie-connect/) |

Đây là nguồn tải được liên kết trong mô tả, chưa phải bằng chứng archive còn tải được hoặc chứa đúng DFF/TXD. Một nhân vật có nhiều video/variant có thể trỏ về cùng asset; bước tải sau cần kiểm tra trùng. Link MMD/Steam/DeviantArt làm nguyên liệu model, trang chủ tác giả chung, cosplay nhân vật khác và video chỉ ghi Android không được tự coi là skin GTA SA PC có link tải.

## Phạm vi và kiểm tra

- Roster: [176 nhãn được giao](evidence/skin-youtube-search-roster.json). [Nhóm game](evidence/new-skin-youtube-games.json) có 107 tên; [nhóm anime/khác](evidence/new-skin-youtube-anime.json) có 69 tên. File ghi truy vấn, video, bằng chứng và giới hạn nguồn; xem thêm [danh sách còn thiếu](skin-search-missing-characters.md).
- Form kiểm tra trên Chromium qua HTTP ở 1280px và 390px: nguồn chờ, reload, chuyển lên series, sửa link giữ rating, loại video đã gắn link khỏi mục chờ, xuất/nạp, 659 rating cũ và từ chối JSON lỗi trước khi đổi dữ liệu. [Kết quả](evidence/new-skin-manual-source-verification.json).
- 12 thumbnail mới tải được; 659 preview không đổi kế thừa kiểm tra trước đó. [Audit ảnh](../../staging/project-eagle/skin-search-gallery-2026-10-14/preview-audit.json).
- Lỗi giật cuộn không tái xuất hiện khi đổi rating; lọc/sắp xếp/lưu/xuất cũng qua trên hai kích thước. [Bằng chứng](evidence/skin-gallery-scroll-after.json).
- [Kiểm tra dữ liệu và hash](evidence/skin-search-additions-verification.json): đủ ID/URL/ảnh trước lượt YouTube; HTML inline khớp catalog và bản dist. Các context kiểm thử dùng dữ liệu giả riêng, không ghi vào đánh giá người dùng.

Bản trước lượt này lưu ở `catalog-before-youtube-search.json` và `gallery-before-youtube-search.html` trong thư mục gallery. Không thay đổi game trong tác vụ này.
