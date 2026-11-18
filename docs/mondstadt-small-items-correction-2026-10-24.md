# Mondstadt — sửa sáu cụm đồ vật theo ảnh, 24/10/2026

Trạng thái **handoff — candidate đã sửa và mở lại trình xem**. Chưa cài vào gameplay-lab. Nguồn M0 V2 và toàn bộ binary M1 giữ nguyên.

Người dùng xác nhận mũi tên là hướng chuyển từng cụm và bổ sung Hiệp Hội sang mặt tiền tòa nhà đối diện trong ảnh `codex-clipboard-88b9f15b-95db-4f2b-8dfd-c3137185335b.png`. Các tọa độ đích suy từ ảnh, được raycast xuống nền nguồn và chỉnh khoảng hở cho toàn bộ cụm. Đây là bố trí theo ảnh được duyệt, chưa phải tọa độ POI đo từ game Genshin.

## Bố trí cuối

Hệ ENU cục bộ; U tính bằng mét, giữ pivot/ID/IPL. Sáu cụm quay cứng 180°; không phản chiếu mesh, UV hay biển hiệu. Giữ đài phun nước và thùng gỗ.

| Cụm | Tâm chân trước (E, N, U) | Tâm chân sau (E, N, U) |
|---|---|---|
| Good Hunter / cụm bàn ăn | 86.400, -48.418, -46.840 | 141.142, 24.000, -48.959 |
| Bàn giả kim | 98.071, -31.823, -46.900 | 106.925, -7.548, -46.897 |
| Quầy hoa Flora | 133.670, -44.378, -50.960 | 146.226, -29.583, -52.850 |
| Lò rèn | 146.572, -27.704, -52.850 | 144.205, -71.879, -52.981 |
| Xe trái cây | 137.892, -51.575, -52.970 | 165.155, -33.483, -52.945 |
| Hiệp Hội Mạo Hiểm | 135.042, -31.744, -50.960 | 128.968, -41.499, -50.961 |

Đầu mũi tên chạm sát tường nên footprint lớn được kéo ra ngoài: bàn ăn 2,2 m, Hiệp Hội 1,3 m; lò rèn 3,3 m vào phía trong thành và trái cây 4,3 m ra khỏi gatehouse. Vẫn giữ đúng tòa nhà/khu cổng được đánh dấu. Không có giao cắt cạnh prop với tam giác tường/mái tĩnh trong phép kiểm offline; kiểm này không thay thế GTA physics.

![Bố trí sau sửa](mondstadt-small-items-captures-2026-10-24/after-overview.png)

![Hiệp Hội trước mặt tiền đối diện](mondstadt-small-items-captures-2026-10-24/guild-final.png)

## Artifact và kiểm chứng

- Candidate riêng: `D:\GTA Archive\Staging\mondstadt-small-items-correction-2026-10-24\candidate-m0`. Chỉ `md_city_gate_walls.dff`, `md_city_lower_plaza.dff` và `mondstadt_city.col` đổi payload trong IMG 17 member; 1.316 tam giác render + 1.316 COL chuyển đồng bộ; bảy vị trí đèn liên quan cập nhật.
- Bảy LOD giữ nguyên byte vì không chứa các prop được thêm này. Năm COL entry khác, hai TXD, ID/pivot/IDE/IPL/ownership và phần geometry ngoài sáu cụm giữ nguyên. 65 file nguồn M0 được kiểm hash không đổi; staging M1 theo receipt cũ không đổi.
- Binary QA PASS; max COL entry 46.720 B, max local component 203,602 m; sai số render/COL tối đa 11,85 mm. UV, material, day/night prelight giữ nguyên; normal quay cùng mesh.
- Browser đọc lại DFF/COL candidate: 43 Near, 36 LOD, 36.558 mặt COL; không có lỗi runtime. Cả sáu vị trí có mẫu nền lân cận không vướng thân va chạm. Nút **6 cụm đã sửa** đưa camera về góc đối chiếu.
- Đã chạy lại A* trên COL mới: 257.728 support samples, vùng tới được 22.313 mẫu; **0/3 mốc vẫn chưa đạt**, khoảng cách còn lại 19,023 / 477,367 / 297,452 m. Các mốc gần đúng, water cutoff −58 m và hạn chế offline của M1 giữ nguyên.
- NPC nodes/spawns/Lua giữ nguyên, **chưa retarget theo quầy mới**. Chưa kiểm GTA loader, streaming, FPS hay actor interaction. Candidate manifest ghi rõ các kết quả M0 trước sửa chỉ là lịch sử.

## Tái tạo và phục hồi

Nguồn tái tạo: `identified-groups.json`, `make_plan.py`, `relocation-plan.json`, `patch_binaries.py`, `placement_clearance.py`, `refresh_viewer.py`. Snapshot M1 trước sửa và HTML cũ ở `D:\GTA Archive\Staging\mondstadt-small-items-correction-2026-10-24\backup`; file kiểm chứng gồm `binary-qa.json`, `placement-clearance.json`, `browser-qa.json`, `walkability-after.json`, `delivery-manifest.json`.

Chạy lại candidate bằng `patch_binaries.py`; sau đó `refresh_viewer.py --walk` để đọc binary mới và dựng HTML. `refresh_viewer.py` sử dụng snapshot M1 đã sao lưu của tác vụ này; nếu M1 có build mới, cần nhập lại baseline trước khi dùng. `finish_report.py` của M1 dựng bản gốc và sẽ ghi đè trình xem sửa nếu chạy lại.

Khôi phục riêng HTML bằng `restore_viewer.py`; script chỉ ghi khi current hash khớp bản đã bàn giao và backup hash khớp bản trước sửa. Không phục hồi nguyên thư mục, không ghi game. Ghi chú bàn giao/README vẫn được giữ như lịch sử sau phục hồi.

IMG sau: `36c31f6070cfd4ae529ccd9bcd9f0efb1637de444099625cf7b8502d741d180e`. COL sau: `ccbda8e24277b427359bf70104a52f1dc80bca7b998681e7733220c8dc8be526`. Plan: `2fbe5d76b1addae0b053c7bffff6e7100a4ff68fd9faffd783ccc7015143ec7c`. Không nhận khóa game-write vì không ghi runtime hoặc deployment state.
