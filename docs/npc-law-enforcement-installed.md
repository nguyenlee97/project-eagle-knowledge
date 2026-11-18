# Cài thử NPC cảnh sát, SWAT và quân đội trong Project Eagle

Ngày: **13/10/2026**. Trạng thái cuối: **đã cài**, đã kiểm tra archive và phục hồi/cài lại; **chưa nghiệm thu hình ảnh hoặc gameplay trong game**.

**Cập nhật 14/10/2026:** người dùng báo đã trigger được cảnh sát và SWAT Los Santos, skin hoạt động ổn. Ghi nhận này áp vào hai vai trò của bộ thử (lapd1 280, swat 285), không phải nghiệm thu riêng mọi animation/chức năng. Army 287 chưa có kết quả gameplay được báo. [Ghi nhận từ người dùng](evidence/user-runtime-observations.json).

Game đã xử lý: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa clean\gta sa clean`.

## Bộ thử và nơi quan sát

Theo yêu cầu mới của người dùng, lượt thử chuyển từ dân thường sang cảnh sát/quân đội để có thể gọi bằng mức truy nã. Ba target thực tế được đối chiếu với IDE và `data/variation.dat`:

| Vai trò | ID / model Eagle | Nhãn asset nguồn cũ | DFF + TXD | Tam giác | Mapping cấu hình |
| --- | --- | --- | ---: | ---: | --- |
| Cảnh sát thường Los Santos | **280 / lapd1** | `ReiAyanami2` | 136.298 B | 1.601 | LS COPPED, `variation.dat:57`; `peds.ide:321` |
| SWAT | **285 / swat** | `hanekawa` | 372.770 B | 3.622 | CS/LS/SF/LV SWPED; LS `variation.dat:64`; `peds.ide:330` |
| Quân đội | **287 / army** | `senjo` | 377.322 B | 3.696 | CS/LS/SF/LV ARPED; LS `variation.dat:69`; `peds.ide:332` |

**Hãy thử lượt đầu tại Los Santos.** Tăng truy nã để quan sát cảnh sát thường, rồi SWAT/quân đội khi gameplay gọi các vai trò đó. Nếu dùng trainer để chỉnh wanted level, dùng chức năng hiện có trong game; lượt này không sửa mức truy nã, spawn logic, vũ khí, pedtype hoặc AI. Không khẳng định ngưỡng sao riêng của Eagle đã được kiểm tra.

Người dùng hỏi điểm spawn đầu vì thường xuất hiện cùng một chỗ. **Changelog cục bộ `data/Changelog.txt:84` ghi đã chuyển điểm khởi đầu từ Rose City sang Carcer City**; dòng 85 đổi thời gian bắt đầu sang buổi sáng. Đây là tài liệu của bản cài, **chưa phải vị trí runtime được người dùng hay agent xác nhận**. Save/script có thể đặt vị trí khác. Nếu đang ở Carcer, cần đến Los Santos để kiểm tra bộ thử có mapping rõ này.

`variation.dat` liệt kê CC trong header nhưng không có dòng active CC COPPED/SWPED/ARPED. Các model `CC_CCPD1–6` và `CC_SWAT` có IDE/asset, nhưng chưa tìm được bằng chứng selector wanted dùng chúng; không có `CC_ARMY` trong danh mục. Vì vậy không gọi bộ này là thay toàn bộ cảnh sát/quân đội của Carcer hoặc mọi thành phố. Những model vùng khác và cảnh sát đi motorbike vẫn giữ tài nguyên của chúng. [Đối chiếu vùng và model](evidence/npc-law-enforcement-targets.md).

Tên `ReiAyanami2`, `hanekawa`, `senjo` là nhãn mapping lịch sử từ JSON audit workbook cũ. Chưa xác nhận nhân vật bằng render; đây là skin thử, chưa chốt danh sách anime/game cuối. Tài nguyên được lấy từ bộ sẵn có, không tải skin mới.

## Kiểm tra tĩnh trước cài

Đọc chính DFF/TXD gốc của ba target trong COMPONENTPEDS. Cả ba asset nguồn khớp **33 frame, 32 bone**, HAnim, bone IDs/index/flags, quan hệ bone cha gần nhất và các frame cánh tay/cẳng tay/bàn tay/ngón tay của target. Không báo lỗi bone indices, vertex không trọng số, NaN/Inf/trọng số âm, tổng trọng số lệch tolerance hoặc material thiếu texture.

Đây là bằng chứng rig cơ sở cho NPC, gồm cấu trúc tay cần khi cầm vũ khí; **chưa chứng minh pose bắn/reload, vào xe hoặc biến dạng mesh trong animation**. Rei dùng texture 128×128; hai mẫu còn lại 512×512. Chúng nhẹ trong tập mẫu đã đo, nhưng lượng geometry vẫn lớn hơn NPC gốc và chưa đo FPS.

Manifest source hash, file nguồn/RAR member, target gốc, rig contract và sáu file staging: [npc-law-enforcement-rig-audit.json](evidence/npc-law-enforcement-rig-audit.json), [rig summary](evidence/npc-law-enforcement-rig-summary.md).

## Cách cài và thay đổi thực tế

**File game duy nhất đã đổi:**

```text
S&S\Cdimages\default\COMPONENTPEDS.img
```

Thay đúng sáu member: `lapd1.dff/txd`, `swat.dff/txd`, `army.dff/txd`. Cặp nguồn giữ nguyên byte, chỉ đổi basename tại staging để khớp định nghĩa Eagle; các tên texture bên trong TXD vẫn khớp vật liệu DFF.

Plugin ModLoader stream hiện bị tắt (`plugins.ini:14`). Lượt này dùng archive gốc đã được manifest mount tại `gta.dat:25`, thay entry chính xác để tránh phụ thuộc vào custom IMG precedence chưa kiểm chứng. Không bật plugin stream, không mount thêm IMG và không đưa các skin này vào thư mục RZL-Skin.

Archive candidate được xây từ **backup byte-for-byte** của bản đang cài. Append sáu payload có sector padding rồi cập nhật đúng sáu record directory gốc để trỏ tới payload mới. Giữ nguyên tên/member count; các slot cũ còn là byte không được sáu entry này tham chiếu. Không rebuild hoặc đổi payload của NPC khác.

| Thuộc tính | Trước | Sau |
| --- | ---: | ---: |
| Archive bytes | 444.082.176 | 444.977.152 |
| Directory members | 4.224 | 4.224 |
| Entries thay đổi metadata | 0 | 6 |
| Entries khác giữ nguyên | 4.218 | 4.218 |

Builder kiểm tra header/directory, tên trùng, biên file, sector allocations và overlap. So sánh toàn bộ prefix archive gốc ngoài sáu trường metadata 8 byte: **khớp byte**; các filename bytes của cả sáu entry cũng giữ nguyên. Hash sáu payload mới khớp ready/source. Vì vậy phạm vi thay đổi gồm metadata của sáu entry và payload mới append, không phải toàn bộ nội dung ped khác.

SHA-256 archive gốc:

```text
9D1FCE78EC9B4D124A59C7312776D5F58973F7133C699289688BB787FE2A02A1
```

SHA-256 archive đang cài:

```text
082976033F74EF2FAB2AF39477E2DC61B23757C5607C0ED323F2A67F6A971437
```

Builder và candidate: `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\law-enforcement`; audit ở `archive-build-audit.json`. Directory offsets lịch sử trong ped-catalog của lượt khảo sát vẫn là snapshot trước cài; các offset mới cho sáu entry có trong manifest cài đặt.

## Phục hồi đã thử

Backup:

```text
C:\Users\LENOVO\Desktop\GTA\backups\project-eagle\npc-law-enforcement-20261013-211911
```

Có archive gốc, baseline/installed manifests, operation log, verification JSON và script kiểm tra game đã tắt/hash trước khi thay file. Chỉ nhận archive đúng hash gốc hoặc hash của bộ thử; nếu có mod khác đổi archive sau đó, script từ chối ghi đè để đối chiếu trước. Việc thay archive dùng file tạm đã kiểm hash và thao tác thay file nguyên khối.

Đã chạy **cài → phục hồi về hash gốc → cài lại**, thành công. Trạng thái cuối là bộ ba NPC **đang cài**. Trong lượt gọi đầu, lệnh .NET thay file nhận sai null-string argument và dừng trước khi đổi archive; đã sửa wrapper và hoàn tất các lượt nêu trên. Không có thay đổi dở dang trong game.

Để gỡ, tắt game rồi chạy PowerShell:

```powershell
& 'C:\Users\LENOVO\Desktop\GTA\backups\project-eagle\npc-law-enforcement-20261013-211911\Restore-NpcPilot.ps1'
```

[Restore-NpcPilot.ps1](../../backups/project-eagle/npc-law-enforcement-20261013-211911/Restore-NpcPilot.ps1) / [Install-NpcPilot.ps1](../../backups/project-eagle/npc-law-enforcement-20261013-211911/Install-NpcPilot.ps1). Reinstall dùng candidate giữ ngoài game.

## Phạm vi đã kiểm chứng và cần thử

**17/17 file hash theo dõi khớp trạng thái mong đợi:** COMPONENTPEDS khớp bản cài; 16 file còn lại giữ hash baseline, gồm executable, Aether DFF/TXD, modloader IMG, default/gta.dat, peds.ide, variation.dat, trainer, loader và PECore.ini. Metadata của 1.699 file game ngoài archive đích không thay đổi. Aether-Autoload vẫn vắng mặt. Không sửa audio, population config, script hoặc save; không mở game trong lượt này.

Kiểm tra thủ công ở Los Santos: nhận diện NPC mới khi wanted-response gọi đúng ID; xem gần/xa, ngày/đêm và mặt trước/sau; quan sát chạy, cầm/bắn/reload vũ khí, nhận hit/ngã, vào/ra xe; theo dõi stutter khi nhiều NPC xuất hiện và khi quay lại vùng. Bất kỳ lỗi texture/mesh/crash hoặc giảm performance rõ đều là lý do phục hồi hoặc thu hẹp mẫu. Đây là test NPC cơ bản, không phải checklist nhân vật chính Aether.

**Chưa xác minh:** ngoại hình đúng nhãn nhân vật, spawn và pose runtime, ngưỡng wanted của Eagle, FPS, nhiệm vụ/cutscene/multiplayer hoặc wanted selectors Carcer. Việc archive đã cài và hash đúng được xác nhận riêng với những phần runtime này.
