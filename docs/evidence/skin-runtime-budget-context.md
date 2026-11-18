# Ngữ cảnh ngân sách tài nguyên skin cho Project Eagle

Ngày kiểm tra: 14-10-2026. Phạm vi chỉ đọc: cấu hình và log đã có, PE header, thông tin phần cứng Windows và các tệp asset hiện diện. Không mở game, benchmark, sửa game, cài hay tải asset. Đây là ngữ cảnh để lựa chọn skin; chưa phải ngân sách runtime đã đo.

## Kết luận

Máy có AMD Ryzen 7 4800H (8 nhân/16 luồng), 15,4 GiB RAM hệ thống Windows báo khả dụng và NVIDIA GeForce GTX 1650 với 4096 MiB VRAM theo nvidia-smi. gta_sa.exe là PE32 x86, cờ Large Address Aware đang bật; trên Windows 64-bit, Microsoft nêu ứng dụng 32-bit có cờ này có thể nhận 4 GiB **không gian địa chỉ ảo**. Những điều này cho thấy có cơ sở để thử skin chi tiết, nhưng không cho biết FPS, VRAM còn trống, hay số model an toàn. Chưa xác minh Eagle chọn GPU nào khi chạy.

Ngân sách phụ thuộc vào số **model khác nhau đang cư trú** trong streaming pool và số **ped đồng thời hiện/vẽ**, không chỉ số file skin đã cài. Con số 403 là **slot mục tiêu NPC dự kiến**, không phải 403 skin đã cài; hiện có ba skin NPC pilot và Aether. Dù số skin đã cài là bao nhiêu, không thể quy trực tiếp số đó thành số model cư trú đồng thời. Một model đã nạp có thể được dùng cho nhiều NPC: số instance tăng công việc vẽ/animation, còn model ID mới thường cần bộ tài nguyên riêng. Không giả định các ID khác nhau được gộp tài nguyên giống nhau.

Đối với NPC phụ, ưu tiên mesh vừa phải và texture đủ dùng. Giảm mesh có thể giúp khi nhiều NPC cùng hiện; giảm texture chủ yếu giảm payload texture và áp lực bộ nhớ/băng thông. Aether là nhân vật chính nên cần budget/đánh giá riêng về ngoại hình, rig và animation; kích thước file không nói lên các tiêu chí đó.

## Bằng chứng hiện tại

| Hạng mục | Quan sát | Giới hạn |
|---|---|---|
| CPU | AMD Ryzen 7 4800H with Radeon Graphics; 8 nhân, 16 luồng | Thông tin WMI, không phải benchmark. |
| RAM | 16,119,108 KiB visible, xấp xỉ 15,37 GiB | Không phải lượng RAM/commit còn trống khi chơi. |
| GPU | NVIDIA GeForce GTX 1650, 4096 MiB theo nvidia-smi; AMD Radeon tích hợp cũng được Windows liệt kê | WMI báo AdapterRAM NVIDIA gần trần 32-bit nên không dùng con số đó. GPU Eagle thực tế dùng chưa được xác nhận; VRAM trống chưa đo. |
| Hệ điều hành | Windows 10 Home Single Language, 64-bit | Đọc từ WMI. |
| PE | gta_sa.exe, 14,383,616 byte; Machine 0x014C x86; Optional Header 0x010B PE32; COFF 0x012F; bit 0x0020 Large Address Aware bật | Đây là header đọc trực tiếp. 4 GiB là virtual address space, không phải RAM vật lý hay quota skin. Không cần thay cờ/giới hạn hệ thống. |
| Thiết lập PECore | FPSlimit 80, RefreshRate 80; PedDensityExt 1.5, PedPopulationMult 1.5; VehicleDensity 1.5, VehPopulationMult 1.5; NumDesiredLoadedVeh 75; DistantTraffic tắt | Chỉ là cấu hình; không phải FPS hay số NPC đo được. Không nhân hai hệ số ped thành 2,25× vì tương tác chưa rõ. |
| Streaming | stream.ini: memory 13500, devkit_memory 13500, vehicles 12. Log ModLoader cũ ghi đã nạp stream.ini. | Đơn vị và ý nghĩa runtime của 13500 chưa xác minh; không gọi là MB, VRAM hoặc cache thực tế. |
| Kết quả runtime | Không thu FPS, frametime, working set, VRAM residency hoặc streaming churn | Log ghi cap 80 FPS là cấu hình, không phải FPS benchmark. |
| Aether | Trong modloader/RZL-Skin: AETHER.dff 1,080,110 byte; AETHER.txd 1,311,272 byte; cộng 2,391,382 byte (2,28 MiB) trên đĩa. Audit asset xác nhận mesh 17.706 tam giác. | Các tài liệu cj-aether.md và aether-autoload-rollback.md báo cáo người dùng xác nhận workflow F2 hoạt động; không phải phép đo GPU residency. Audit asset: biến thể shadeless có 4 texture DXT1 (2×1024² + 2×512²), 1 mip/texture, tổng mip payload 1.310.720 byte; biến thể standard có body 1024² không nén, 4.194.304 byte. Cả hai biến thể có cùng 17.706 tam giác. |

stream.ini chỉ cho biết cặp giá trị cấu hình đã được nạp trong log cũ; vẫn chưa có bằng chứng cho đơn vị/ý nghĩa hữu hiệu. FPSlimit=80 cũng có thể che chênh lệch khi đo FPS vượt mức giới hạn.

## Mô hình ước lượng có điều kiện

### Payload texture theo số model cư trú

Các mức 0,5 / 2 / 8 MiB là **giả định tổng texture nén cho mỗi model, đã gồm mip**; không phải số đo skin trong Eagle. Phép tính chỉ nhân mức giả định với số model riêng biệt cùng cư trú. Không gồm mesh, texture thế giới/xe, buffer, metadata, alignment hay overhead; không phải tổng VRAM/RAM và không dự đoán FPS.

| Model riêng đang cư trú | 0,5 MiB/model | 2 MiB/model | 8 MiB/model |
|---:|---:|---:|---:|
| 10 | 5 MiB | 20 MiB | 80 MiB |
| 25 | 12,5 MiB | 50 MiB | 200 MiB |
| 50 | 25 MiB | 100 MiB | 400 MiB |

Ví dụ Direct3D 9 có điều kiện: texture vuông 512² DXT1 có payload cơ sở 128 KiB, DXT5 là 256 KiB; đầy đủ mip xấp xỉ 171/341 KiB. 1024² lần lượt là 512 KiB/1 MiB ở mức cơ sở, xấp xỉ 683 KiB/1,33 MiB có mip. Căn cứ block 4×4: DXT1 dùng 64 bit/16 texel (4 bit/texel), DXT2–5 dùng 128 bit/16 texel. Audit của biến thể shadeless xác nhận 4 texture DXT1, đúng 1 mip mỗi texture; tổng 1.310.720 byte là tổng mip payload, không phải toàn bộ VRAM runtime. Biến thể standard có body 1024² không nén chiếm 4.194.304 byte; chưa cộng thêm các texture khác trong standard nếu audit không nêu tổng.

Microsoft mô tả D3D9 managed resources có bản system-memory và được đưa vào video memory khi cần; runtime có thể quản lý/loại bỏ residency. Đây là mô tả API chung, không chứng minh Eagle dùng pool nào cho TXD skin. Vì vậy không cộng đôi mọi payload hoặc coi file TXD là toàn bộ VRAM của game.

### Công việc hình học theo số instance

| Ped đồng thời hiện | 1.000 tam giác/model | 4.000 tam giác/model | 20.000 tam giác/model |
|---:|---:|---:|---:|
| 20 | 20.000 tam giác/scene | 80.000 tam giác/scene | 400.000 tam giác/scene |
| 40 | 40.000 tam giác/scene | 160.000 tam giác/scene | 800.000 tam giác/scene |

Đây là phép nhân so sánh cấp scene, không phải FPS, lượng mesh memory hay chi phí skinning thực tế. LOD, bone count, alpha, số draw call, số pass và kích thước trên màn hình ảnh hưởng kết quả. Bảng chỉ minh họa vì sao mesh rất nặng có thể hợp lý cho nhân vật chính nhưng kém phù hợp khi nhân cho nhiều NPC.

Audit cho biết mesh Aether có 17.706 tam giác ở cả hai biến thể: nếu cùng mesh đó xuất hiện ở 20/40 NPC nhìn thấy, phép nhân thô là 354.120/708.240 tam giác mỗi scene trước LOD/culling. Đây là phép so sánh hình học, không phải benchmark.

## Cách chốt ngưỡng sau này

Chưa có số liệu để đặt ngưỡng cuối theo MiB, độ phân giải hay tam giác. Khi roster/asset đã chốt, đo trong cùng một cảnh trước/sau khi thêm từng nhóm skin: số model ID riêng của vùng, số ped thấy được, frametime/FPS, VRAM dedicated/shared, working set và hiện tượng khựng/lỗi khi lái qua vùng đổi model. Ghi cấu hình/resolution và lưu ý cap 80 FPS.

Nếu sàng lọc asset trước runtime, ghi riêng cho từng DFF/TXD: byte trên đĩa, số mesh/material, vertex/triangle/LOD, số texture, kích thước/format/mip của từng texture. Không đổi dung lượng file thành VRAM/FPS bằng một tỉ lệ chung. Chốt tier NPC từ phân bố asset và phép đo thật; đánh giá Aether riêng theo độ đẹp, rig và animation nhân vật chính.

## Nguồn kỹ thuật

- [Microsoft: Performance and Memory Consumption Under WOW64](https://learn.microsoft.com/en-us/windows/win32/winprog64/performance-and-memory-consumption) — giới hạn địa chỉ ảo PE32 LAA trên WOW64.
- [Microsoft: Managing Resources (Direct3D 9)](https://learn.microsoft.com/en-us/windows/win32/direct3d9/managing-resources) — managed resource và residency system/video memory.
- [Microsoft: Compressed Texture Formats (Direct3D 9)](https://learn.microsoft.com/en-us/windows/win32/direct3d9/compressed-texture-formats) — block DXT 4×4 và số bit lưu trữ.
- [Microsoft: Opaque and 1-Bit Alpha Textures (Direct3D 9)](https://learn.microsoft.com/en-us/windows/win32/direct3d9/opaque-and-1-bit-alpha-textures) — DXT1 4 bit/texel.

Tệp local đối chiếu: gta_sa.exe, PECore.ini, stream.ini, PECore.log, modloader/modloader.log, modloader/RZL-Skin/AETHER.dff, modloader/RZL-Skin/AETHER.txd, staging/project-eagle/aether/asset-audit.json (metadata DFF/TXD), cj-aether.md, aether-autoload-rollback.md, skins.md. Census skin-size-census.json là dung lượng trên đĩa, không phải runtime.
