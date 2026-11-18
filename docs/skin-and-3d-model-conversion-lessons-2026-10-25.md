# Sổ Tay Kinh Nghiệm Convert Skin & Model 3D (Genshin / Anime → GTA SA `.DFF` + `.TXD`) — Chuẩn Bề Mặt Kín 100% (`0` Lỗ Thủng)

- **Ngày cập nhật**: `2026-10-25`
- **Hội thoại đúc kết**: [`327d7afd-8da6-4eec-ac19-02d7dfebb8b1`](conversation://327d7afd-8da6-4eec-ac19-02d7dfebb8b1)
- **Script chuẩn hóa thực tế**: [`parse_collada_dae.py`](file:///C:/Users/LENOVO/.gemini/antigravity/brain/327d7afd-8da6-4eec-ac19-02d7dfebb8b1/scratch/parse_collada_dae.py) & [`build_m1_multiverse_landmarks.py`](file:///D:/GTA%20Archive/Staging/mondstadt-m1-multiverse-landmarks-2026-10-24/build_m1_multiverse_landmarks.py)
- **Báo cáo kiểm định 3D WebGL trực quan (97 Model & Nội thất)**: [`mondstadt-models-resource-conversion-audit-2026-10-24.html`](mondstadt-models-resource-conversion-audit-2026-10-24.html)

---

## 1. Quy Tắc #1 (Bắt Buộc): Ưu Tiên Tuyệt Đối Dùng Skin `.DFF` + `.TXD` Có Sẵn Trong `Skin Library` Trước Khi Convert Model Trên Mạng

- **Nguyên tắc**:
  - Trước khi convert bất kỳ nhân vật Playable hay NPC nào từ file `.dae` / `.fbx` / `.pmx` tải trên mạng (`The Models Resource`, `Aplaybox`), **bắt buộc phải tra cứu trong kho `D:\GTA Archive\Skin Library\Project Eagle\numbered-skins\raw`** (và các thư mục con của `D:\GTA Archive\Skin Library`).
  - Nếu nhân vật đã có sẵn bản skin GTA SA (`.dff` + `.txd`), **phải dùng trực tiếp cặp `.dff` + `.txd` đó**; chỉ những nhân vật/NPC/quái vật/đồ vật chưa có trong `Skin Library` mới dùng model `.dae` / `.fbx` / `.pmx` convert về.
- **Lý do kỹ thuật**:
  - Các bản skin `.dff` + `.txd` trong `Skin Library` đã được xử lý sẵn bảng tách vật liệu `BinMesh PLG` (`mat_split`), gộp chuẩn 3–4 texture Diffuse và khớp sẵn UV mắt/mặt/trang phục cho RenderWare GTA SA.
- **Cách trích xuất Mesh & Texture từ Skin `.DFF` + `.TXD` có sẵn**:
  1. Dùng `DragonFF/gtaLib/dff.py` (`dff.load_memory(dff_bytes)`) để đọc `geometry_list[0]`, lấy danh sách mặt tam giác theo từng vật liệu từ `g.extensions.get("mat_split")` (`split.indices` cho từng `split.mat_index`), kết hợp với `g.vertices` và `g.uv_layers[0]`.
  2. Dùng `tools/world-texture-studio/core/rw_txd.py` (`parse_txd_bytes`, `decode_raster_to_pil`) để giải mã toàn bộ raster trong file `.txd` đi kèm sang ảnh PIL `RGBA`.
  3. **Chuẩn hóa tư thế trục đứng (`Z_UP` / `Y_UP` / `X_UP`)**: Các skin `.dff` trong `Skin Library` có 3 kiểu hướng trục xương gốc (Bind-Pose) khác nhau tùy công cụ xuất (`3ds Max Kam's Script` vs `Blender DragonFF`):
     - **`Z_UP` (`(vx, vy, vz)`)**: Nhân vật đứng dọc trục `Z`, chân ở `-Z`, đầu ở `+Z` (ví dụ: `Diluc #328746`, `Kaeya #328743`, `Jean #328744`).
     - **`Y_UP` (`(vx, -vz, vy)`)**: Nhân vật đứng dọc trục `Y` (ví dụ: `Barbara #328747`, `Rosaria #514444`, `Albedo #525577`, `Sucrose #538867`).
     - **`X_UP` (`(-vz, -vy, vx)`)**: Nhân vật nằm dọc theo trục xương `Root/Pelvis` `X` của GTA SA, chân ở `-X`, đầu ở `+X` (ví dụ: `Venti #328741`, `Lisa #328745`, `Diona #539022`, `Klee #536287`).
  4. **Lọc bỏ lớp vật liệu phủ mắt trong suốt (`alpha_mean < 80`)**:
     - Một số skin GTA SA (như `Venti`, `Lisa`) có thêm 1 sub-material phụ đè lên trước mắt với kênh Alpha gần như trong suốt (`alpha_mean ≈ 24.8`, ví dụ `tex='4'`). Nếu ép sang ảnh RGB/DXT1 đặc mà không lọc, lớp phủ này sẽ biến thành miếng băng đen che mắt nhân vật.
     - **Giải pháp**: Kiểm tra `np.array(pil_rgba)[:, :, 3].mean() < 80.0` — nếu một material có độ đục trung bình `< 80/255`, tự động bỏ qua `mat_split` đó khi xuất sang mesh tĩnh DXT1.

---

## 2. Quy Tắc #2 (Bắt Buộc): Tuyệt Đối Cấm Giảm Đa Giác Bằng Cách Xóa Tam Giác Rời Rạc (`max_tris` Subsampling)

- **Triệu chứng lỗi từng gặp ("nổi da gà / thủng lỗ chỗ như tổ ong")**:
  - Các NPC (`Katheryne`, `Wagner`, `Timmie`, `Cyrus`) chỉ có `4,025 – 6,725` mặt tam giác (`< 8,500`) nên không bị cắt giảm và hiển thị kín 100%.
  - Trong khi đó, toàn bộ **11 nhân vật Playable** (`18,138 – 44,985` mặt), **`Statue of Marble and Brass (#604549)`** (`34,482` mặt), **`Lupus Boreas / Andrius (#540934)`** (`31,548` mặt) và **`Stormterror Dvalin (#328740)`** (`76,525` mặt) vượt ngưỡng `max_tris = 8,500` (hoặc `2,800` trong nội thất).
  - Việc dùng bước nhảy `conv_tris[::step]` để ép xuống `max_tris` mà không khâu lại lưới (`retriangulation`) đã xóa bỏ **55% – 89% số tam giác** rải rác khắp bề mặt, đục hàng nghìn lỗ thủng xuyên qua mặt, ngực, tay chân và thân model!
- **Quy tắc bắt buộc**:
  - **Cấm tuyệt đối** dùng `conv_tris[::step]` hoặc xóa ngẫu nhiên tam giác trên bất kỳ nhân vật, NPC, quái vật, boss, tượng hay đồ nội thất nào.
  - **Giữ nguyên 100% mặt tam giác bề mặt (`0` tam giác bị cắt)** để mọi model đều kín khít tuyệt đối (`100% watertight`).

---

## 3. Quy Tắc #3 (Bắt Buộc): Hàn Đỉnh Ở Độ Chính Xác `0.1 mm` (`round(p, 4)`) & Không Tách Đỉnh Theo Pháp Tuyến Mặt (`Face Normal`)

- **Bẫy làm tròn tọa độ đỉnh `round(p, 2)` (`1 cm`)**:
  - Trên khuôn mặt, con ngươi mắt, lông mi, trang sức và ngón tay của nhân vật anime/Genshin, kích thước cạnh tam giác chỉ từ **`1 mm – 8 mm` (`0.001m – 0.008m`)**.
  - Nếu làm tròn tọa độ đỉnh ở mức `round(p, 2)` (`0.01m = 1 cm`) khi hàn đỉnh (`vertex welding`), hai đỉnh gần nhau `< 1 cm` sẽ bị chập làm một (`itri[0] == itri[1]`), làm suy biến và xóa mất **`6,200 – 11,200` tam giác nhỏ trên mắt/mặt/tay** của mỗi nhân vật!
  - **Giải pháp**: Bắt buộc dùng độ chính xác **`round(p, 4)` (`0.0001m = 0.1 mm`)** và **`round(uv, 4)`** — giữ nguyên `100%` tam giác chi tiết (`0` tam giác bị suy biến).
- **Cách giữ tổng số đỉnh `.DFF` dưới trần `65,535` (`uint16`) mà không xóa tam giác nào**:
  - Khi đóng gói `.DFF`, nếu đưa cả vector pháp tuyến mặt phẳng `round(face_normal, 1)` vào khóa hàn đỉnh `v_map`, mỗi đỉnh trên bề mặt cong sẽ bị tách thành 5–6 đỉnh riêng biệt, làm tổng số đỉnh tăng gấp 3 lần và vượt quá giới hạn `65,535` đỉnh `uint16` của RenderWare `.DFF`.
  - **Giải pháp**: Chỉ dùng khóa hàn đỉnh **`key = (round(px, 4), round(py, 4), round(pz, 4), round(u, 4), round(v, 4))`** (chia sẻ đỉnh mượt qua các mặt cùng UV). Nhờ đó:
    * **`Stormterror Dvalin (#328740)`**: Giữ đủ **`76,525 / 76,525` mặt tam giác** nhưng chỉ dùng **`51,253` đỉnh** (`< 65,535`).
    * **`Statue of Marble and Brass (#604549)`**: Giữ đủ **`34,482 / 34,482` mặt tam giác** với **`24,242` đỉnh**.
    * **`Lupus Boreas / Andrius (#540934)`**: Giữ đủ **`31,548 / 31,548` mặt tam giác** với **`21,507` đỉnh**.
    * **Cả 6 Phòng Nội Thất Hợp Nhất (`INT-01 .. INT-06`)**: Dù chứa sẵn 2–3 nhân vật + toàn bộ bàn ghế/tượng chi tiết cao (`39,343 – 79,323` mặt tam giác/phòng), số đỉnh mỗi phòng chỉ từ **`29,718 – 53,937` đỉnh** (`< 65,535`), nằm gọn trong 1 file `.DFF` duy nhất!

---

## 4. Quy Tắc #4 (Bắt Buộc): Bộ Lọc Sạch 7 Loại Lưới/Vật Liệu Phụ Gây Lỗi Khi Convert `.DAE` Từ `The Models Resource`

Khi convert các model chưa có trong `Skin Library` từ file `.dae` (`The Models Resource`) hoặc `.fbx`/`.pmx` (`Aplaybox`), bắt buộc áp dụng đầy đủ 7 bộ lọc sau trong [`parse_collada_dae.py`](file:///C:/Users/LENOVO/.gemini/antigravity/brain/327d7afd-8da6-4eec-ac19-02d7dfebb8b1/scratch/parse_collada_dae.py):

| STT | Loại Lưới / Vật Liệu Phụ Trong File Gốc | Hậu Quả Nếu Không Lọc Bỏ | Quy Tắc Xử Lý Chuẩn Đã Áp Dụng |
| :-: | :--- | :--- | :--- |
| **1** | **Lớp lưới ánh sao mắt `EyeStar-mesh` (`*eyestar*`)** | Tạo mảng đen che kín con ngươi mắt nhân vật khi convert sang vật liệu thường. | Bỏ qua mọi `<geometry>` hoặc `<node>` có tên chứa `eyestar`. |
| **2** | **Vũ khí rời & mặt nước hiệu ứng đặt ở `(0, 0, 0)` (`MonEquip_*`, `EffectWater`)** | Trong `#604549 StatueOfMarbleAndBrass.dae`, kiếm/khiên rời (`MonEquip_Golem_Centaur_SwordShield_01/02`) và `EffectWater` nằm chồng đống dưới chân tượng. | Bỏ qua các geometry/material chứa `monequip`, `mon_equip`, `effectwater`, `weapon_`. |
| **3** | **Lớp vỏ VFX bao ngoài Boss (`*Evil_Eff_Mat*`, `*Purified_Eff_Mat*`, `*EffectMesh*`, `*Tornado_Eff_Mat*`)** | Làm `#328740 Dvalin`, `#540934 Andrius` và `#601779 Eye of the Storm` bị bọc trong lớp vỏ đen/tím che mất thân thật. | Bỏ qua mọi material chứa `eff_`, `_eff`, `evil_eff`, `purified_eff`, `tornado_eff`, `effectmesh`, `meshpillar`. |
| **4** | **Thư mục con `Objects/` chứa vũ khí rời trong các pack nhiều file `.dae` (`#584572`, `#584645`, `#585038`)** | Nếu chọn `.dae` theo độ dài tên ngắn nhất (`len(p.name)`), script sẽ lấy nhầm `Objects/Torch/Torch.dae` thay vì `Hilichurl.dae`, hoặc `Objects/Axe/Axe.dae` thay vì `Mitachurl.dae`. | Khi duyệt `folder.rglob("*.dae")`, bắt buộc đẩy mọi đường dẫn có chứa thư mục `Objects/` xuống cuối danh sách ưu tiên (`1 if "objects" in parts else 0`). |
| **5** | **Lưới trùng lặp kênh Lightmap `*_UV1.._UV4`, `*_LOD1.._LOD3` & Morph Targets mặt** | Đè lên lưới `UV0` chính gây sọc/rác texture (`Z-fighting`) trên mặt NPC (`Timmie`, `Katheryne`, `Cyrus`, `Wagner`) và chim bồ câu (`#606466`). | Chỉ nhận `<geometry>` được gắn vào `<visual_scene><node>`, loại bỏ toàn bộ `_uv1.._uv4`, `_lod1.._lod3`, `.001/.002` và các morph biểu cảm (`eye_angry`, `mouth_`). |
| **6** | **Hộp chắn sáng `*_Ocl` (Occluder) & vỏ rương `CreateTreasureBox*`** | Tạo khối hộp xám không có texture xuyên qua tường nhà Mondstadt hoặc bọc kín bên ngoài 5 loại Rương Báu (`#543920..#543924`). | Loại bỏ mọi node/geometry chứa `_ocl`, `occluder`, `createtreasurebox`, `_shadowmesh`, ` bounds`. |
| **7** | **Dải bờm/đuôi dựng đứng ở tư thế Bind-Pose (`#540934 Andrius.dae`)** | Trong `#540934 Andrius.dae`, dải bờm trên vai (`z = 4.2m .. 8.87m`) dựng thẳng đứng lên trời theo xương vật lý lúc chưa chạy animation. | Uốn mượt các đỉnh có `z > 4.2m` xuôi về phía lưng/đuôi (`py += (pz - 4.2) * 0.88`, `pz = 4.2 + (pz - 4.2) * 0.15`) — giữ nguyên 100% tam giác mà dáng đứng tự nhiên. |
