# Bàn giao sau merge: chuyển dữ liệu sang D và chỉ build gameplay-lab

> **Quy ước dùng tiếp:** người dùng xác nhận mọi feature mới xây dựng cho gameplay-lab; Codex và Antigravity dùng cùng [knowledge, phiếu công việc và khóa ghi chung](shared-agent-workflow.md). Đọc và đăng ký phạm vi trước khi sửa để tránh conflict.

Cập nhật: **07:02 22/10/2026 (Asia/Saigon)**. Yêu cầu người dùng: lưu trữ clean và kho skin trên D; từ giờ chỉ chơi và build tiếp trên gameplay-lab. Báo cáo này nối tiếp [báo cáo merge 37 file](merge-clean-to-gameplay-lab-2026-10-22.md).

Trước lượt chuyển ổ này đã merge loading/splash, main menu 32 file và archive NPC mới nhất từ clean vào lab; Aether/radio đã khớp nên được giữ. Lần merge gồm **36 file nội dung + 1 state menu tạo riêng cho lab**; tại thời điểm kiểm sau merge, **2.789 file khác và 10 junction lab giữ nguyên**. PECore giữ nguyên `.text`/`.data`, tương thích patch GPS của Sidecar; bảy DFF từng có lỗi đã được đọc kiểm hash và rig 32/32 trong archive. Backup và transaction merge vẫn ở D, không bị lượt chuyển ổ này thay thế.

## Trạng thái dùng tiếp

- **Game chơi/build duy nhất:** `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`.
- **Launcher:** `Start_Eagle_Lab_With_Sidecar.bat` ngay trong thư mục lab.
- **Game clean lưu trữ:** `D:\GTA Archive\Project Eagle\gta sa clean\gta sa clean`. Đây là bản nguồn đã mod trước merge, không phải GTA SA vanilla và không còn là đích cài mod.
- **Kho skin vật lý:** `D:\GTA Archive\Skin Library`; Skin Viewer vẫn truy cập được đường dẫn C cũ qua junction.
- **Thư mục build IMG:** `D:\GTA Staging\Project Eagle Viewer Builds` (đã có từ trước, giữ nguyên).
- **Staging/backup skin:** các vị trí D trong bảng dưới. D cần sẵn khi xem kho skin hoặc build. Code công cụ đang dùng, tài liệu và fixture QA khoảng 35 MB của Skin Viewer giữ trên C; runtime skin/radio/menu của lab giữ trên C.

## Dữ liệu đã chuyển

Đủ **19 cây thư mục**, **29,133 đường dẫn file**, **74.666 GiB dung lượng logic**. Có **22,568 file ID nguồn duy nhất**, tương ứng **53.433 GiB payload duy nhất**; giữ hardlink nội bộ và hardlink giữa Library với staging. Không nhân bản các alias tải skin vốn đã là junction.

| Đường dẫn cũ tương đối workspace | Vị trí vật lý trên D | File | GiB logic |
| --- | --- | ---: | ---: |
| `Project Eagle\gta sa clean` | `D:\GTA Archive\Project Eagle\gta sa clean` | 1,759 | 23.466 |
| `Skin Library` | `D:\GTA Archive\Skin Library` | 21,040 | 41.894 |
| `staging\project-eagle\skin-gallery-2026-10-14` | `D:\GTA Archive\Skin Staging\project-eagle\skin-gallery-2026-10-14` | 4,375 | 7.268 |
| `staging\project-eagle\texture-optimization-2026-10-22` | `D:\GTA Archive\Skin Staging\project-eagle\texture-optimization-2026-10-22` | 869 | 0.901 |
| `staging\project-eagle\prostitute-role-pool-2026-10-17` | `D:\GTA Archive\Skin Staging\project-eagle\prostitute-role-pool-2026-10-17` | 42 | 0.113 |
| `staging\project-eagle\heavy-skin-test-2026-10-21` | `D:\GTA Archive\Skin Staging\project-eagle\heavy-skin-test-2026-10-21` | 33 | 0.084 |
| `staging\project-eagle\skin-light-gallery-2026-10-14` | `D:\GTA Archive\Skin Staging\project-eagle\skin-light-gallery-2026-10-14` | 35 | 0.016 |
| `staging\project-eagle\skin-search-gallery-2026-10-14` | `D:\GTA Archive\Skin Staging\project-eagle\skin-search-gallery-2026-10-14` | 46 | 0.025 |
| `staging\project-eagle\skin-viewer-qa-import-deploy-20261018` | `D:\GTA Archive\Skin Staging\project-eagle\skin-viewer-qa-import-deploy-20261018` | 22 | 0.001 |
| `staging\project-eagle\skin-budget` | `D:\GTA Archive\Skin Staging\project-eagle\skin-budget` | 8 | 0.000 |
| `staging\project-eagle\aether` | `D:\GTA Archive\Skin Staging\project-eagle\aether` | 22 | 0.015 |
| `staging\project-eagle\aether-autoload` | `D:\GTA Archive\Skin Staging\project-eagle\aether-autoload` | 756 | 0.036 |
| `staging\project-eagle\law-enforcement` | `D:\GTA Archive\Skin Staging\project-eagle\law-enforcement` | 37 | 0.417 |
| `staging\project-eagle\npc-reuse-survey` | `D:\GTA Archive\Skin Staging\project-eagle\npc-reuse-survey` | 58 | 0.015 |
| `staging\project-eagle\optimized-representatives-2026-10-21T18-04-28-449Z-dcd7dc` | `D:\GTA Archive\Skin Staging\project-eagle\optimized-representatives-2026-10-21T18-04-28-449Z-dcd7dc` | 3 | 0.000 |
| `staging\project-eagle\mapping-reset-2026-10-21T18-08-50-514Z` | `D:\GTA Archive\Skin Staging\project-eagle\mapping-reset-2026-10-21T18-08-50-514Z` | 2 | 0.001 |
| `backups\project-eagle\aether-autoload-20261013` | `D:\GTA Archive\Skin Backups\project-eagle\aether-autoload-20261013` | 9 | 0.000 |
| `backups\project-eagle\cj-aether-20261013` | `D:\GTA Archive\Skin Backups\project-eagle\cj-aether-20261013` | 8 | 0.000 |
| `backups\project-eagle\npc-law-enforcement-20261013-211911` | `D:\GTA Archive\Skin Backups\project-eagle\npc-law-enforcement-20261013-211911` | 9 | 0.414 |

Mỗi root cũ trên C hiện là **NTFS junction** tới đúng root D, không còn bản dữ liệu vật lý thứ hai tại C. Điều này giữ được gallery, sourceInputs, metadata, đường dẫn backup cũ và alias Downloads. Các junction runtime riêng của lab không được đổi.

Quy trình: kiểm đúng root tuyệt đối và không đi theo reparse; chép đồng thời tính SHA-256; đọc lại toàn bộ file duy nhất trên D để đối chiếu SHA-256; kiểm inventory nguồn không đổi; sau đó mới gỡ từng file nguồn đã ghi trong manifest và thư mục rỗng, rồi tạo/kiểm junction. Kiểm file ID toàn bộ các root xác nhận hardlink chéo vẫn dùng chung file trên D. Có journal/checkpoint; không thực hiện xóa cây mù.

Dung lượng C tại đầu/cuối journal: **2.89 → 56.38 GiB trống**. Số liệu là hai thời điểm thực đo, gồm hoạt động thông thường khác trên máy.

## Skin Viewer và ownership mới

`tools/skin-viewer/import_npcs.py` mặc định đọc gameplay-lab. `deploy_skins.py` chặn plan/build, apply và recover nếu catalog hoặc biến môi trường chọn target khác lab; các kiểm tra currentHash/baseline/game đang chạy vẫn giữ.

Đã xác minh baseline `082976033f74ef2fab2af39477e2dc61b23757c5607c0ed323f2a67f6a971437` chính là archive lab **trước merge**. Archive đang cài ở lab được đọc toàn bộ và khớp `9bf8f76c59167c3664f187083d2b951213bf69ce7dc6f242c7706dbdefbf37e2`, cũng là hash build sửa RW/rig và hash merge. Vì vậy có cơ sở chuyển ownership hiện tại, không cần reset hoặc thay baseline.

Đã cập nhật `numbered-skins/npcs.json:gameRoot` và `deployment/state.json:gameRoot` sang lab; thêm provenance chuyển đích. Giữ `appliedAt`, baseline/currentHash, **1.638 appliedMappings**, catalog skin và toàn bộ reviews/mappings. `generatedFrom` của catalog NPC vẫn là bằng chứng lịch sử nguồn, không bị thay đường dẫn hàng loạt. Có backup JSON trước sửa.

Build cũ có target clean và expectedCurrentHash cũ được lưu tại `D:\GTA Archive\Skin Library\Project Eagle\numbered-skins\deployment\history\build-before-lab-migration-20261022.json`; không sửa hash để tái dùng candidate đó. Lần build tiếp theo phải tạo plan/build mới. Đã chạy plan thật chỉ đọc với kho đã chuyển: **1638 mapping, 1638 slot, 0 lỗi**; target là lab. Không build/apply archive mới trong lượt chuyển dữ liệu này.

Khi thử plan lab lần đầu, builder phát hiện **11 member trùng tên giữa `custom/GROUP_A_MODS.IMG` và `S&S/Cdimages/default/COMPONENTPEDS.img`**. Chúng là `bmypol1.txd` và các cặp DFF/TXD `wmypizz`, `wmybell`, `wmyammo`, `bmytatt`, `wfyburg`; `GROUP_B1_TEXTURES.IMG` không chứa các mục này. Đây là đặc điểm archive gameplay cần tính đến khi build trên lab. Đã thêm policy giới hạn đúng 11 tên và đúng hai archive: dùng payload cuối sau ghép shared TXD và chuyển RW/rig cho cả hai bản sao. Baseline, currentHash và rollback được quản lý riêng cho từng archive. Trùng tên ngoài policy vẫn là lỗi. Không suy đoán thứ tự ưu tiên loader và không chỉ bỏ qua thông báo trùng; thay đổi này chỉ áp dụng cho lần build tiếp theo.

**Trạng thái đang cài:** `GROUP_A_MODS.IMG` vẫn giữ nguyên bản gameplay trước lượt này. Hash vùng member (gồm padding IMG) của 11 mục trên hiện khác archive NPC chính. Chưa xác minh trong game archive nào thắng ở sáu slot NPC 66/155/167/179/180/205; không coi plan thành công là bằng chứng sáu slot đang hiển thị đúng skin. Build/apply mới trên lab sẽ đồng bộ các bản sao theo policy vừa bổ sung; lượt này chưa thực hiện thao tác đó.

## Menu, loading và radio

- Radio Studio chỉ còn target lab trong UI/API, fallback dự án cũ cũng chọn lab. Deploy/restore/uninstall kiểm đúng đường dẫn và hash hai exe lab; từ chối clean ở cả đường C cũ, D và alias. Lịch sử backup/manifest clean giữ nguyên để tham khảo.
- Wibu menu installer và manifest generator nhắm lab, kiểm hai exe, dùng history lab riêng. Khi update giữ `merge_origin` và `merge_transaction`; standalone rollback không được xóa file do transaction merge sở hữu.
- Loading installer/preparer và live verifier nhắm lab, dùng state/history lab riêng. Việc nhận ownership chỉ được thực hiện dựa trên hash transaction merge và PECore before-image đã kiểm trên D; không dùng state clean cho lab. PECore preparer đọc baseline từ backup transaction trên D.
- Rollback độc lập của menu/loading đối với tài nguyên merge-owned bị chặn có chủ đích. Muốn phục hồi lần merge, dùng transaction 37 file và hướng dẫn ở báo cáo merge; không đưa lịch sử clean sang lab.
- Các script thử nghiệm Aether/autoload/NPC pilot cũ được lưu làm tài liệu lịch sử qua đường dẫn junction; không phải luồng build mới và không được chạy lại chỉ vì còn tồn tại.

## Kiểm tra và giới hạn

- Skin Viewer: **10/10 unittest đạt**, gồm guard từ chối clean, shared TXD, chuyển tương thích, dữ liệu mirror cuối giống nhau, phục hồi cả hai archive và chặn trùng tên ngoài policy. Kiểm thử dùng game giả trong thư mục tạm.
- Radio Studio: **7 kiểm tra đạt**; lifecycle trên game giả trong thư mục tạm bao phủ prepare/apply, lỗi giữa chừng và tự rollback, restore theo hash, uninstall. Hai kiểm tra cũ ghi vào lab thật đã không được chạy.
- Python compile và parser PowerShell của 6 script đạt; manifest Wibu đủ **32/32 file**, target và hai hash exe lab đúng.
- [Kiểm tra phục hồi merge sau khi chuyển ổ](../../staging/project-eagle/storage-migration-2026-10-22/rollback-preflight-after-move.json) đạt: **37 đường dẫn chính xác, hash backup hợp lệ** (`rollback-preflight`); chưa chạy rollback.
- File baseline, kho đã chuyển, metadata và plan thật đã kiểm như trên. Lượt kiểm plan dùng cache hash từ snapshot D vừa được đọc kiểm toàn bộ, chỉ tái dùng khi size/mtime còn khớp; metadata đã đổi và file ngoài snapshot được hash lại. Không thêm cơ chế cache này vào builder production. Phiên game lúc bắt đầu đang chạy từ lab; không dừng game và không ghi asset runtime của game trong lượt này. Đây không phải một lượt nghiệm thu gameplay hoặc đo FPS.
- Các ghi chú còn chờ nghiệm thu Waypoint/ENEX và kiểm thử dài hạn B3 ở hồ sơ lab trước merge vẫn giữ nguyên; việc chuyển ổ không được dùng để đánh dấu các mục đó hoàn tất.

## Chỗ agent tiếp theo cần đọc

- Báo cáo này và `AGENTS.md` là điểm vào cho policy target mới.
- [Journal đầy đủ](../../staging/project-eagle/storage-migration-2026-10-22/migration.json), [allowlist](../../staging/project-eagle/storage-migration-2026-10-22/roots.json), [script di chuyển](../../staging/project-eagle/storage-migration-2026-10-22/move_storage.py).
- [Lineage baseline/archive](../../staging/project-eagle/storage-migration-2026-10-22/skin-target-preflight.json), [kết quả chuyển metadata](../../staging/project-eagle/storage-migration-2026-10-22/skin-target-migration.json), [plan lab sau di chuyển](../../staging/project-eagle/storage-migration-2026-10-22/lab-plan-verification.json).
- [Plan lỗi trước sửa policy mirror](../../staging/project-eagle/storage-migration-2026-10-22/before-lab-mirror-fix/lab-plan-verification.json) được giữ để agent sau đối chiếu.
- [Kiểm tra cuối](../../staging/project-eagle/storage-migration-2026-10-22/final-handover-verification.json): 19 junction đúng đích, catalog/reviews giữ hash, 1.638 mapping giữ nguyên, 11 mirror không nén và đối chiếu vùng member đang cài.
- Backup trước sửa code: `staging/project-eagle/storage-migration-2026-10-22/tool-code-backup` và `workflow-code-backup`.
- Backup metadata trước rebind: `staging/project-eagle/storage-migration-2026-10-22/skin-target-metadata-backup`.
- Backup lần merge: `D:\GTA Archive\Project Eagle Merges\clean-to-lab-2026-10-22`. Báo cáo merge trước đó giữ giá trị bằng chứng ở thời điểm merge; đường nguồn C hiện đi qua junction tới D.

