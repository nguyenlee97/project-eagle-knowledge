# Crash khi load save/New Game sau khi áp dụng NPC IMG

## Bằng chứng và nguyên nhân tương thích

Crash gốc `ProjectEagle_crashes/2026-10-22_04-06-47.log`: `0x00749B7B`, `RpClumpForAllAtomics`, đọc qua con trỏ clump NULL. Stack đi qua `GetFirstAtomic` và khởi tạo animation. FLA log nạp lặp `male01.txd` / `male01.dff` (NPC 7), rồi dừng. Log `04-06-56` người dùng dán có `std.data.dll` trong `LdrShutdownProcess/ExitProcess`; đó là lỗi sau trong lúc thoát, không phải vị trí lỗi đầu tiên.

Đọc tĩnh executable thực tế bằng pefile/capstone, không vá executable: `RpClumpStreamRead` tại `0x74B420` lấy phiên bản Struct, kiểm tra `0x34000..0x36003` tại `0x74B475..0x74B485`; ngoài khoảng thì nhảy `0x74BC92`, ghi lỗi rồi trả NULL tại `0x74BCB8`. Evelyn đang gán NPC 7 có phiên bản `0x33002`, nằm ngoài khoảng này. Đây là lỗi định dạng xác định được trong tài nguyên đã cài; việc hết crash hoàn toàn vẫn cần thử lại trong game.

Khảo sát nguồn của 1.638 mapping tìm được 4 DFF RW 3.3.0.2, dùng ở 7 NPC:

| Skin | NPC |
|---|---|
| Evelyn Chevalier | 7, 48897 |
| player4 | 165, 48574 |
| Tsukishiro Yanagi | 48105, 48570 |
| Grace Howard — GTA VC model | 49165 |

Ba TXD của Evelyn/Yanagi/Grace dùng native D3D8 DXT, tương ứng 5 member đích. Chi tiết scan chỉ đọc: [crash-ped-dff-audit-2026-10-22.md](evidence/crash-ped-dff-audit-2026-10-22.md).

## Bản sửa builder

`tools/skin-viewer/sa_assets.py`, được gọi sau ghép TXD chung và trước ghi IMG:

- Chuyển RW 3.3.0.2 → 3.6.0.3 trong bản build, không chỉ đổi version tag: bỏ 12 byte surface-properties geometry legacy; chuyển Skin plugin từ per-matrix marker sang used-bones/max-weights/split-data hiện đại; cập nhật độ dài chunk cha.
- Giữ nguyên byte tọa độ/UV/index/normal/weight/bone matrix, frame hierarchy, material và tên texture. Giữ dữ liệu ngoài root như nguồn. Nguồn/catalog/key/ranking/mapping không đổi.
- Native D3D8 DXT1/3/5 → header D3D9, giữ nguyên toàn bộ mip payload; kiểm từng kích thước mip và alpha. Không giải mã/nén lại ảnh trong builder. Layout không hỗ trợ bị từ chối thay vì đoán.
- Kiểm Clump Struct version khi lập kế hoạch để từ chối nguồn chưa có bộ chuyển an toàn. Hash nguồn gốc vẫn được giữ trong `sourceInputs`, hash tài nguyên chuyển được ghi riêng trong candidate.

Đối chiếu độc lập bằng reader/renderer trên cả 4 nguồn trước/sau: geometry, material, pixel RGBA, frame hierarchy, vertex bone indices/weights và inverse matrices bằng nhau. Test có thêm chuyển legacy ở hai slot, giữ source byte/mapping, idempotence và chặn file cắt/phiên bản không hỗ trợ; các test build/apply/restore vẫn qua.

Tài liệu cấu trúc đã đối chiếu: [librw Skin](https://github.com/aap/librw/blob/master/src/skin.cpp), [DragonFF DFF](https://github.com/Parik27/DragonFF/blob/master/gtaLib/dff.py). Đây là tham chiếu định dạng; bằng chứng giới hạn executable và crash lấy từ file cục bộ.

Snapshot metadata trước sửa: `evidence/crash-before-sa-compat-2026-10-22/`. Bản chuyển thử và danh sách đối chiếu: `D:/GTA Staging/Project Eagle Viewer Builds/compatibility-check-20261022/`. Không thay DLL/ASI, executable, loading, Aether, radio hoặc game lab.

## Kết quả cài bản sửa

Đã build lại và áp dụng bằng transaction của viewer, đủ 1.638 mapping. Sau cài kiểm trực tiếp 12 member đã chuyển trong IMG: 7 DFF có Clump Struct RW `0x36003`, 5 TXD đều dùng native platform 9; hash từng payload khớp candidate. Tool đã kiểm hash toàn IMG sau cài. Mapping và đánh giá khớp snapshot trước sửa; baseline đúng hash, không còn transaction/lock hoặc file tạm/rollback cạnh IMG. [Kết quả kiểm tra](evidence/crash-sa-compat-applied-2026-10-22.json).

**Chưa nghiệm thu trong game:** cần người dùng load lại save/New Game. Nếu còn lỗi, dùng log đầu tiên của lần chạy mới để tiếp tục; không lấy crash thứ hai trong lúc ExitProcess làm vị trí lỗi gốc.

Lần chạy tiếp theo đã qua lỗi NULL clump, nhưng dừng ở `CAnimBlendNode::Update` với con trỏ sequence không hợp lệ. Bốn model trên vẫn có rig VC 24 khớp sau bước chuyển wire format. Xem [phần điều tra và chuyển rig 32 khớp](crash-animation-rig-2026-10-22.md); không coi kết quả kiểm định dạng ở tài liệu này là xác nhận tương thích animation.
