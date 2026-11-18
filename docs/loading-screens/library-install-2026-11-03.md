# Thư viện178 ảnh — cài gameplay-lab, loading2s / menu4s

**Nghiệm thu03/11:** người dùng báo “mọi thứ đã work hoàn hảo rồi”; task hoàn tất. [State/source/cleanup](../presentation-current-state.md). Các mục kiểm tra bên dưới là bằng chứng/kịch bản lưu lại.

**Cập nhật03/11:** Plugin đã được cập nhật tiếp cho EOF random-next và true intro bypass;178ảnh/2s/4s giữ nguyên. Muốn rollback thư viện phải rollback update plugin mới trước. [Bàn giao mới](menu-autonext-no-intros-2026-11-03.md).

Đã cài ngày03/11/2026 theo yêu cầu, vào duy nhất `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`. Người dùng đã duyệt nốt M15four và LS03one; tất cả178ảnh hiện được duyệt. **Người dùng đã test và chốt runtime PASS03/11/2026; agent không tự mở game.**

- Loading:89 ảnh, đổi mỗi2000ms theo đồng hồ thực ở lượt vẽ kế tiếp. Chọn điểm bắt đầu khác nhau mỗi phiên load, sau đó đi qua danh sách. Giữ Project Wibu/title/legal và thanh tiến độ gốc; không kéo dài thời gian load để xem hết ảnh.
- Main menu:89 ảnh, đổi mỗi4000ms trên các trang artwork trước khi vào game. Mở bảng F6 sẽ tạm dừng đổi để F7/F8 chọn ảnh; đóng bảng tiếp tục chu kỳ. Favorite/random vẫn là lựa chọn khởi đầu. Pause giữ portrait hiện tại, không có bộ đếm4s riêng.
- Giữ nguyên toàn bộ đoạn `[audio]` trong INI, bao gồm7 bài, random mỗi lần mở game, volume0.25 và bài mặc định. Radio Studio đọc được plugin mới, nhận đủ7bài và hai capability persistence/random.
- Flat2D, logo trắng–đen và mọi bản đã chọn được giữ. Alice LSS01 bản gốc, FischlV4, Clorinde cropV2 và Danica/Vodyanitsa EXC06V2 theo đúng selection; không dùng bản bị thay thế.

## Bản cài và ownership

Nguồn hiện tại cho lần update này là `staging/project-eagle/art-library-install-20261103`; không chạy lại installer/build của clean hoặc candidate menu cũ. [Pinned selection](../../../staging/project-eagle/art-library-install-20261103/selected-library.json) có89 loading +89 menu.

Thay đúng180 file nội dung: `WibuMenu.asi`, `plugins/wibu-menu/wibu-menu.ini`,178TXD mới dưới `plugins/wibu-menu/assets/library-20261103/{loading,menu}`. Cập nhật thêm `plugins/wibu-menu/.wibu-menu-install-state.json`, giữ owner/game_root/merge_origin/merge_transaction và lịch sử update. State hiện có217 file sở hữu; cover23 cũ và tài nguyên merge vẫn được giữ.

Transaction [transaction.json](../../../staging/project-eagle/art-library-install-20261103/transaction.json) ghi hash trước/sau, nguồn,92 tài nguyên được bảo vệ và thời điểm cài. ASI mới SHA256 `7a6fe712a42fa3ac579438faaa2f07da4f4a1c6b51a9bd74c62300b343999164`. PECore, hai executable, archive/loadscs cũ, radio, nhạc và mod khác giữ nguyên. Ghi runtime dưới khóa độc quyền `data/project-eagle/coordination/game-write.lock`, đã giải phóng sau khi cài.

## Kiểm chứng

- [Texture QA](../../../staging/project-eagle/art-library-install-20261103/package/qa/texture-package.json):178/178 qua encode/parse/decode, D3D9 DXT1, một texture `cover`,1920×1080,một mip. Mean RGB error2.49–4.37; input opaque và source hash khớp selection. Chỉ export/resample kỹ thuật, không tạo/sửa artwork.
- [Build QA](../../../staging/project-eagle/art-library-install-20261103/qa/plugin-build.json):x86 PE32, kernel32/user32 imports, module pin, private BASS và các hook/menu table khớp cả `gta_sa.exe`/`gta_pe.exe`. Giữ các guard của menu/audio hiện tại.
- Native tests dùng hàm timer thật kiểm mốc1999/2000 và3999/4000, vòng89ảnh, tick wrap, tạm dừng F6 và không fast-forward qua ảnh chưa vẽ; exit0. Probe gọi `LoadConfig()` thật trên INI fixture, xác nhận89+89,2s/4s,7bài/random/volume; exit0. Không gọi engine/game hooks trong probe.
- [Live install QA](../../../staging/project-eagle/art-library-install-20261103/qa/live-install.json):180 payload +state hash khớp, mọi đường dẫn INI tồn tại,178source hash giữ nguyên,92 protected file không đổi, `[audio]` byte-identical, merge ownership giữ nguyên, rollback preflight qua. [Radio Studio read-only](../../../staging/project-eagle/art-library-install-20261103/qa/radio-studio-read.json) nhận plugin mới và playlist hiện tại.
- Người dùng đã xác nhận trải nghiệm runtime PASS; agent không đo độc lập timing/fade/performance. Đổi ảnh theo2s/4s không thể vẽ trong lúc engine đang chặn giữa hai frame.

## Cách tích hợp loading

Clone từ bản WibuMenu random-music đang cài và thêm ba hook riêng: `RenderSplash`0x58FF60, `LoadSplashes`0x5900B0, `Shutdown`0x58FF10. Địa chỉ/cdecl và7sprite được đối chiếu với [Plugin-SDK CLoadingScreen](https://github.com/DK22Pac/plugin-sdk/blob/master/plugin_sa/game_sa/CLoadingScreen.cpp), [gta-reversed LoadingScreen](https://github.com/gta-reversed/gta-reversed/blob/master/source/game_sa/LoadingScreen.cpp), cùng disassembly trực tiếp của cả hai executable lab. REA MCP không có trong phiên; CLI help được kiểm tra, nhưng không có REA native evidence. Bằng chứng binary dùng pefile/Capstone thông thường và signature guards.

Texture loading nằm trong một CTxdStore slot riêng, tạo/hủy trên thread render. Khi vẽ, tạm mượn texture pointer cho native current/previous sprite, trả lại ngay sau hàm native; không chuyển ownership hoặc để engine shutdown xóa nhầm. Sprite/title/legal index0 được giữ. Cùng texture ở hai lớp làm native crossfade giữa các ảnh theo phần trăm load không còn đổi hình; ảnh mới cắt trực tiếp theo timer2s. Chỉ một ảnh loading resident; TXD đọc đồng bộ ở ranh giới đổi ảnh có thể tạo khựng ngắn cần người dùng quan sát. Không sửa PECore/executable hay dùng global D3D hook/MH_Uninitialize.

## Phục hồi riêng lần update này

Before-images plugin/INI/state tại `staging/project-eagle/art-library-install-20261103/runtime-before`. Phục hồi chỉ bản update03/11, giữ transaction merge và mod khác. Thoát game trước khi chạy:

```powershell
C:/Python310/python.exe -X utf8 staging/project-eagle/art-library-install-20261103/deploy_library.py rollback-preflight
C:/Python310/python.exe -X utf8 staging/project-eagle/art-library-install-20261103/deploy_library.py rollback
```

Hoặc dùng `Check_Rollback.cmd` / `Rollback_Library.cmd` tại cùng staging. Guard chặn rollback nếu plugin/config/state/asset đã đổi sau cài; không ghi đè chỉnh sửa mới. Không chạy rollback merge chỉ để gỡ update này. Transaction ghi trạng thái `installing` và candidate-state trước khi ghi runtime; nếu process bị ngắt ngang, cần kiểm tra owner/PID/manifest và hash trước khi phục hồi, không xóa khóa cũ tùy tiện. Rollback thực tế chưa chạy.

## Người dùng test

Mở bản gameplay-lab: kiểm Project Wibu startup; vào loading xem ảnh đổi khoảng2s, không lỗi tay/chân từ bản cũ; đứng main menu20–30s xem ảnh đổi khoảng4s và nghe nhạc; F6/F7/F8 rồi đóng panel; load save, pause/resume và thoát game. Nếu load xong nhanh sẽ không thấy hết89ảnh trong một lần vào. Đây là bước nghiệm thu runtime còn lại.
