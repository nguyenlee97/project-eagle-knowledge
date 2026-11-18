# Dryxio GTA AI Modding Toolkit — Tài liệu Tham chiếu & Tích hợp cho Project Eagle (23/10/2026)

- **Nguồn gốc**: Hệ sinh thái mã nguồn mở của **Dryxio** (`https://github.com/dryxio`, `dryx.io/projects/`)
- **Mục đích**: Cung cấp bộ công cụ chuyên biệt cho **AI Coding Agents (Antigravity / Codex)** để xem/chỉnh sửa bản đồ 3D ngoài game, chụp ảnh render 3D tự động (`capture-views`), kiểm tra địa hình/va chạm, tạo model 3D qua Blender, thiết kế luồng giao thông (`traffic routes`), viết script CLEO chuẩn hóa và dịch ngược binary.
- **Đích áp dụng**: `C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab`

---

## 1. Danh mục 7 Công cụ Trọng tâm trong Kho `github.com/dryxio`

| STT | Repository | Stars | Vai trò & Ứng dụng trực tiếp cho Project Eagle |
| :-: | :--- | :-: | :--- |
| **1** | **[`Dryxio/ariane`](https://github.com/Dryxio/ariane)** | ★140 | **Trình Xem & Sửa Bản Đồ 3D Hiện Đại (`librw` / `euryopa`)**:<br>- Có nhánh build riêng **`PE / FLA`** (`v1.40.11-PE-920b8e9`) dành riêng cho **Project Eagle (`PE`) / Fastman92 Limit Adjuster (`FLA`)**.<br>- Có bản **`Agent Alpha` (`v1.40.9-agent-alpha.1`)** đi kèm **`arianectl` (Python CLI)** và **MCP Server (`ariane-mcp`)** để AI Agent điều khiển camera, chụp ảnh 3D đa góc độ (`capture-views`), kiểm tra va chạm/độ phẳng địa hình (`analyze-placement`, `fit-terrain`), chỉnh sửa `.IPL` có hoàn tác (`session begin/rollback/commit`) và Hot-Reload vào game qua `ariane.asi`. |
| **2** | **[`Dryxio/gta-scout`](https://github.com/Dryxio/gta-scout)** | ★87 | **AI + Blender 3D Asset & Scene Builder**:<br>- Cho phép AI Agent tìm kiếm, trích xuất `.DFF`, `.TXD` từ các kho `.IMG` của GTA SA và điều khiển **Blender** để lắp ghép, chỉnh sửa model 3D, tạo khu phố mới, cửa hàng hoặc đạo cụ theo đúng phong cách đồ họa gốc của game. |
| **3** | **[`Dryxio/gta-flow`](https://github.com/Dryxio/gta-flow)** | ★24 | **AI + Blender Traffic Route Authoring**:<br>- Công cụ thiết kế đồ thị đường đi cho xe cộ (`traffic routes` / `path nodes`) bằng AI và Blender: đọc mặt đường 3D, đề xuất đường tâm (`centerlines`), phân làn, kiểm tra tính hợp lệ của mạng lưới giao thông và xuất file path cho GTA SA. |
| **4** | **[`Dryxio/plugin-sdk-sa`](https://github.com/Dryxio/plugin-sdk-sa)** & **[`gta-reversed`](https://github.com/Dryxio/gta-reversed)** | ★35 / ★17 | **Plugin-SDK C++ Đã Chuẩn Hóa 100% Cho GTA SA 1.0 US (`gta_pe.exe`)**:<br>- Sửa toàn bộ struct layouts, field offsets, class sizes, chữ ký hàm và địa chỉ bộ nhớ dựa trên mã nguồn dịch ngược byte-for-byte của GTA SA 1.0 US.<br>- Tài liệu tham chiếu chuẩn khi viết/nâng cấp `.asi` (`EagleStreamingFix.asi`, `WibuMenu.asi`, `EagleMapInspector.asi`) và đọc bộ nhớ trong `eagle_debug_system.py`. |
| **5** | **[`Dryxio/cleo-ai`](https://github.com/Dryxio/cleo-ai)** & **[`library`](https://github.com/Dryxio/library)** | ★29 | **AI-Native CLEO Modding Workflow**:<br>- Bộ từ điển Opcode tự động kèm quy trình biên dịch & kiểm chứng bằng Sanny Builder CLI để AI viết script `.cs` chính xác 100%, không đoán mò opcode. |
| **6** | **[`Dryxio/reagent`](https://github.com/Dryxio/reagent)** & **[`ghidra-bridge`](https://github.com/Dryxio/ghidra-bridge)** | ★2155 / ★111 | **AI Reverse Engineering & Ghidra Bridge**:<br>- Cho phép AI truy cập phân tích của Ghidra qua CLI/Python API và tái tạo mã C/C++ có kiểm chứng từ các binary đóng (như `PECore.asi`, `std.data.dll`, `fastman92limitAdjuster.asi`). |
| **7** | **[`Dryxio/mtasa-neon`](https://github.com/Dryxio/mtasa-neon)** | ★123 | **Engine Fork Mở Rộng Giới Hạn Thế Giới Lớn**:<br>- Nguồn tham khảo kiến trúc mở rộng giới hạn thế giới (`world bounds`, `streaming limits`) cho bản đồ đại lục đa thành phố. |

---

## 2. Chi tiết Kênh Phát Hành & Cách Dùng `Dryxio/ariane` cho Project Eagle

### 2.1. Hai bản phát hành quan trọng của `Ariane`
1. **Bản `PE / FLA` (`v1.40.11-PE-920b8e9`)**:
   - URL Release: `https://github.com/Dryxio/ariane/releases/tag/v1.40.11-PE-920b8e9`
   - Binary: `ariane.exe` (được biên dịch với cờ `--channel=PE`, hỗ trợ giới hạn mở rộng của Project Eagle / Fastman92 Limit Adjuster, tháo rời panel đa màn hình, sửa FOV và hướng làn xe).
2. **Bản `Agent Alpha 1 - CLI and MCP` (`v1.40.9-agent-alpha.1`)**:
   - URL Release: `https://github.com/Dryxio/ariane/releases/tag/v1.40.9-agent-alpha.1`
   - Assets cho Windows:
     - `ariane-agent-windows-x64.zip` (`~2.01 MB`: bao gồm `ariane.exe` hỗ trợ Agent TCP IPC, thư mục `fonts`, wheel Python và `AGENT_README.md`)
     - `ariane_agent-0.1.0a1-py3-none-any.whl` (`~110 KB`: cài đặt CLI `arianectl` và MCP server `ariane-mcp`)
   - Lưu ý kỹ thuật khi dùng với **Project Eagle (`gta sa gameplay-lab`)**:
     - Nếu cần vừa có **expanded limits của nhánh `PE`** vừa có **giao thức điều khiển AI (`arianectl` / TCP loopback)**, có thể chạy thử `ariane.exe` trong gói `ariane-agent-windows-x64.zip`, hoặc merge/cherry-pick nhánh `PE` + `codex/agent-public-release` của `Dryxio/ariane`, hoặc kết hợp `Ariane (PE)` với pipeline render 3D trực tiếp để chụp ảnh thực tế cảnh 3D.

### 2.2. Quy trình Kết nối & Chụp Ảnh Cảnh 3D (`capture-views`) bằng `arianectl` trên Windows
```powershell
# 1. Cài đặt môi trường Python cho arianectl
py -3 -m venv .venv-agent
.venv-agent\Scripts\python.exe -m pip install "./ariane_agent-0.1.0a1-py3-none-any.whl[mcp]"

# 2. Đánh chỉ mục tài nguyên IDE của game
.venv-agent\Scripts\arianectl.exe assets index --gta-dir "C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab"

# 3. Khởi chạy Ariane kết nối qua TCP Loopback (chạy cùng phiên PowerShell)
$env:ARIANE_ENGINE_TCP_PORT = '48731'
$env:ARIANE_ENGINE_TOKEN = [guid]::NewGuid().ToString('N') + [guid]::NewGuid().ToString('N')
Start-Process "C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab\ariane.exe" -WorkingDirectory "C:\Users\LENOVO\Desktop\GTA\Project Eagle\gta sa gameplay-lab"

# 4. Kiểm tra kết nối và chụp ảnh 3D tại bất kỳ tọa độ nào trên bản đồ
.venv-agent\Scripts\arianectl.exe ping
.venv-agent\Scripts\arianectl.exe capture-views "C:\path\to\output_dir" --center 8786.8 9625.4 41.9 --span 120
```

### 2.3. Các lệnh `arianectl` hữu ích nhất cho Map & Tester Agent
- **Chụp ảnh khảo sát 3D quanh tọa độ `(X, Y, Z)`**:
  `arianectl capture-views <output_dir> --center <X> <Y> <Z> --span <bán_kính>`
- **Render ảnh preview model 3D đơn lẻ hoặc bảng tổng hợp (`contact-sheet`)**:
  `arianectl assets preview <MODEL_ID> --output preview.png`
  `arianectl assets contact-sheet <ID1> <ID2> ... --output sheet.png`
- **Kiểm tra vùng 3D & va chạm địa hình**:
  `arianectl inspect-zone <X> <Y> <RADIUS>`
  `arianectl validate-zone <X> <Y> <RADIUS>`
- **Chuyển đổi tọa độ pixel trên ảnh chụp màn hình sang tọa độ thế giới 3D**:
  `arianectl screen-to-world <PIXEL_X> <PIXEL_Y> <WIDTH> <HEIGHT>`

---

## 3. Quy ước Sử dụng trong Project Eagle

1. **Cách ly & Không làm bẩn thư mục game**:
   - Mọi công cụ biên dịch, môi trường `.venv-agent`, database SQLite chỉ mục của `arianectl` hoặc staging render 3D phải đặt trong `C:\Users\LENOVO\Desktop\GTA\staging\project-eagle\` hoặc thư mục công cụ riêng.
   - Nếu đặt `ariane.exe` vào `gta sa gameplay-lab` để đọc `gta.dat` và render/chụp cảnh 3D, chỉ đọc dữ liệu (read-only) trừ khi giữ khóa `game-write.lock` để lưu thay đổi `.IPL`.
2. **Ứng dụng cho Interactive Map 2D/3D & Automated Tester**:
   - Dùng `Ariane (PE)` / `arianectl` hoặc bộ render 3D dựa trên `librw` / `.DFF+.TXD+.IPL` để chụp hình thực tế (3D Scene Captures) tại các địa danh, 6 cây cầu cao tốc mới, và các vùng đảo rồi nhúng trực tiếp vào **Interactive Atlas HTML** (`docs/project-eagle/map-mismatch-interactive-atlas-2026-10-23.html`).
