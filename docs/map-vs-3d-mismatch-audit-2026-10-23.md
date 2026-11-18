# Báo Cáo Đối Chiếu Mismatch Giữa Bản Đồ 2D / Đồ Thị GPS Và Thế Giới 3D Thực Tế (`gta sa gameplay-lab`)

- **Ngày thực hiện**: `2026-10-23 02:15 (+07:00)`
- **Phạm vi quét**:
  - **Thế giới 3D thực tế (`.IPL` / `.IDE` / `.COL`)**: `146,723` vật thể đặt trên bản đồ (`83,884` Text IPL + `62,839` Binary Stream IPL), `59,491` model IDE, `41,815` model va chạm `.COL`.
  - **Đồ thị đường bộ GPS (`data/pecore_gps_graph.pegg`)**: `147,175` node giao thông, `253,962` cạnh có hướng (`directed edges`), `151,470` car-links.
  - **Phân vùng bản đồ (`S&S/zon/map.zon` & `info.zon`)**: `1,640` vùng (`zones`).
  - **Danh bạ địa điểm `GG Map` (`eagle_gg_map_pois.py`)**: `631` địa điểm (POI).

---

## 1. Giải Mã Hiện Tượng Tại `BUG-006` (Đèo Keystone) & Hành Trình Tới `Sears Tower` (Chicago)

Phát hiện thực địa của bạn hoàn toàn chính xác: **Bản đồ 2D trong Pause Map được vẽ trước cho toàn bộ quy hoạch nước Mỹ của Project Eagle, nhưng thế giới 3D (`.IPL`/`.COL`) và mạng lưới đường GPS (`pecore_gps_graph.pegg`) mới chỉ xây dựng từng cụm và còn những khoảng trống hoàn toàn chưa dựng 3D (`trống lổng`)**.

### 1.1. Mật độ vật thể 3D dọc hành lang từ Carcer / Keystone (`X = 11500`) sang Chicago (`X = 5000`)
Quét toàn bộ dải vĩ độ `Y = 7800 .. 10800` từ Đông sang Tây:

| Dải tọa độ `X` | Số vật thể 3D (`.IPL`) | Trạng thái thực tế trong game |
|---|---|---|
| `11250 .. 11750` | `282` | Rìa Đông Keystone / đường nối sang Liberty City (phía Bắc `Y > 8300` của dải này là vực trống `0` vật thể). |
| `10750 .. 11250` | **`2,645`** | **Đông Carcer City & Đèo Keystone** (nơi có `BUG-006` tại `11092.8, 8207.6`). |
| `10250 .. 10750` | **`2,359`** | Trung tâm Carcer City. |
| `9750 .. 10250` | **`2,886`** | Tây Carcer City & Khu công nghiệp. |
| `9250 .. 9750` | **`1,228`** | Rìa Tây Carcer / Keystone. |
| `8750 .. 9250` | `104` | Đường bắt đầu cụt dần, chỉ còn lác đác địa hình biên. |
| `8250 .. 8750` | `83` | Vùng biên chưa hoàn thiện. |
| `7750 .. 8250` | `32` | Gần như trống rỗng. |
| **`7250 .. 7750`** | **`1`** | **Khoảng trống hoàn toàn (`trống lổng` — rộng ~`1.7 km` từ `X = 7118` đến `X = 8800`)**, không có mặt đất hay đường 3D, bắt buộc phải bay (`ROCKETMAN`/máy bay) qua. |
| `6750 .. 7250` | `102` | Bắt đầu vào bờ Đông của cụm đảo **Chicago / Windy Bay (`Comp #97`)**. |
| `6250 .. 6750` | `237` | Khu vực Windy Bay & ngoại ô Chicago. |
| `5750 .. 6250` | `192` | **Trung tâm Downtown Chicago & Tháp `Sears Tower` (`6127, 9477`)**. |

### 1.2. Tại sao GPS lúc chỉ đường được (đi vòng qua hầm `BUG-007`), lúc lại mất hẳn khi chọn `Sears Tower`?
- Mạng lưới GPS trong `data/pecore_gps_graph.pegg` gồm `147,175` node nhưng **không nối liền thành 1 khối duy nhất**, mà bị chia cắt thành **Lục địa chính (`Comp #0`: `131,181` node — chiếm `89.1%`)** và các **Ốc đảo đường bộ tách rời (`Comp #1..#104`)**:
  1. Khi bạn chấm điểm đến nằm trên **Lục địa chính (`Comp #0`)** (ví dụ từ Carcer City đi sang các vùng phía Đông/Nam nối qua hầm Porter Tunnel Liberty City ở `BUG-007`), cả điểm đầu và điểm cuối đều thuộc `Comp #0` nên GPS tìm được đường (dù phải đi vòng rất xa qua hầm `BUG-007`).
  2. Ngược lại, **Chicago & Sears Tower (`6127, 9477`)** nằm trên **Ốc đảo đường bộ `Comp #97` (`1,548` node, `X = 5199..7118, Y = 8980..10303`)**, cách Lục địa chính `Comp #0` **`1,703.4 mét`** qua vùng trống `X = 7118..8800` chưa có cầu hay đường nối.
  3. Do đó, khi bạn đang đứng ở Carcer City / Keystone (`Comp #0`) mà chọn đích là `Sears Tower` (`Comp #97`), thuật toán tìm đường của `PECore.asi` không có bất kỳ cạnh nối nào băng qua khoảng trống `1.7 km` đó $\rightarrow$ trả về `route not found` và **không vẽ vạch GPS**. Chỉ khi bạn bay (`ROCKETMAN`) sang tận đất Chicago (`Comp #97`), lúc này cả vị trí của bạn và `Sears Tower` đều cùng nằm trong `Comp #97` nên GPS nội khu mới hoạt động trở lại!
  4. Còn tại tọa độ `BUG-006` (`11092.8, 8207.6`), ngay phía Đông-Bắc của hàng cây `dlkytree125` (`X = 11300..11800, Y = 8400..9000`) cũng là một mảng biên bản đồ có **`0` vật thể 3D** trên lưới `100m x 100m`.

---

## 2. Toàn Cảnh Mismatch Giữa Bản Đồ 2D / Đồ Thị GPS Và Thế Giới 3D

### 2.1. Các "Ốc Đảo Đường Bộ" & "Thành Phố Ma" Trong Đồ Thị GPS (`pecore_gps_graph.pegg`)

| Hạng | Mã Cụm (`Comp`) | Số Node GPS | Tỷ lệ có 3D (`.IPL`) | Phạm vi tọa độ `X` / `Y` | Khu vực & Trạng thái Mismatch |
|---|---|---|---|---|---|
| **#0** | **`Comp #0`** | **`131,181`** | **`98%`** (`128,898`) | `X=[-3342..16021]`, `Y=[-10726..11248]` | **Lục địa chính (Mainland)**: Kết nối thông suốt SA, Carcer, Keystone, Liberty City, Vice City, Cottonmouth, Cheyenne, Jackalope, Independence, Rose. *(Lưu ý: vẫn có `2,283` node GPS rìa biên chưa có mặt đường 3D bên dưới)*. |
| **#1** | **`Comp #103`** | `2,248` | `100%` (`2,248`) | `X=[15338..17410]`, `Y=[10736..13248]` | **Đông Bắc Upstate (`DBZNS`)**: Đã có 3D hoàn chỉnh nhưng **bị đứt đoạn `1.14 km`** chưa nối đường với Liberty City (`Comp #0`). |
| **#2** | **`Comp #11`** | **`2,106`** | **`0%` (`0`)** | `X=[-2523..96]`, `Y=[-6108..-4533]` | **⚠️ "Thành phố ma" `MKLAS` (Tây Nam LS)**: Có sẵn `2,106` node đường bộ trong file GPS nhưng **hoàn toàn chưa có bất kỳ vật thể 3D nào (`0` `.IPL`)** ngoài biển! |
| **#3** | **`Comp #97`** | `1,548` | `100%` (`1,548`) | `X=[5199..7118]`, `Y=[8980..10303]` | **⚠️ Ốc đảo Chicago & Windy Bay (`Sears Tower`)**: Đã có `617` model 3D và đường nội khu, nhưng **cách Keystone/Carcer `1.70 km` khoảng trống chưa làm (`X=7118..8800`)** $\rightarrow$ Phải bay/teleport mới tới được. |
| **#4** | **`Comp #21`** | `1,507` | `92%` (`1,391`) | `X=[-2955..2931]`, `Y=[-2870..2302]` | Mạng đường sắt / nhánh ven biển SA (cầu sắt Kincaid, Bayside, Gaviota, ngọn hải đăng LS) — cách mạng đường bộ chính `Comp #0` chỉ `1.0m`..`13.6m` nhưng không nối node trong file `.pegg`. |
| **#5** | **`Comp #104`** | `1,497` | `100%` (`1,497`) | `X=[13371..14166]`, `Y=[11432..12596]` | **⚠️ Ốc đảo Thị trấn Bullworth (`BWMAIN`)**: Có 3D phần thị trấn (`X < 14166`), nhưng **cách Liberty City `1.58 km` khoảng trống phía Nam** VÀ phần Học viện phía Đông (`X > 14200`) **trống 3D hoàn toàn**. |
| **#6** | **`Comp #2`** | `456` | `96%` (`440`) | `X=[13666..16381]`, `Y=[-9351..-6033]` | Nhánh đường Vice City Beach (`TOUR1`) bị hở node `6.4m` so với `Comp #0`. |
| **#7** | **`Comp #51`** | `328` | `100%` (`328`) | `X=[4076..6991]`, `Y=[1651..2756]` | **Hẻm núi Abyssal Canyon (`Jackalope JP06`)**: Bị hở node `4.4m` tại điểm tiếp giáp `(5052, 2224)` với `Comp #0`. |
| **#8** | **`Comp #1`** | `281` | `91%` (`256`) | `X=[10503..13969]`, `Y=[-11037..-9325]` | **Quần đảo Gator Keys (`Nam Vice City`)**: Đảo biệt lập phía Nam Vice City. |

---

### 2.2. Các Phân Vùng Bản Đồ (`MAP.ZON` / `INFO.ZON`) Trống Rỗng 100% Trong 3D
Trong tổng số `1,640` phân vùng tên địa danh (`zones`) được khai báo trong game, có **`97` phân vùng có `0` vật thể 3D (`.IPL`)**, nổi bật gồm 4 đại phân vùng (`MAP.ZON`):
1. **`BLW01` (Bullworth Bắc)**: `X = [8059 .. 9025]`, `Y = [13586 .. 14888]` $\rightarrow$ **`0` vật thể 3D**.
2. **`UPS02` (Upstate Liberty Tây)**: `X = [12634 .. 12907]`, `Y = [10600 .. 10837]` $\rightarrow$ **`0` vật thể 3D**.
3. **`UPS04` (Upstate Liberty Trung)**: `X = [14615 .. 15402]`, `Y = [11131 .. 11327]` $\rightarrow$ **`0` vật thể 3D** (chính là dải đất trống cắt rời Bullworth/Upstate khỏi Liberty City).
4. **`CM01` (Cottonmouth Ngoại Ô)**: `X = [8452 .. 9570]`, `Y = [-7102 .. -6844]` $\rightarrow$ **`0` vật thể 3D**.

---

### 2.3. Kiểm Toán Toàn Bộ `631` Địa Điểm (`POI`) Trong App `GG Map`
Đối chiếu từng tọa độ trong `631` POI của `GG Map` với lưới 3D `.IPL` và đồ thị đường bộ `pecore_gps_graph.pegg`:
- **✅ `608 / 631` địa điểm (`96.4%`)**: Đã có đầy đủ công trình/mặt đất 3D **VÀ** nằm trên Lục địa chính (`Comp #0`) — chỉ đường GPS và lái xe tới bình thường.
- **🏝️ `21 / 631` địa điểm (`3.3%`) — Có 3D nhưng nằm trên Ốc đảo GPS tách rời (không có đường bộ nối từ lục địa chính)**:
  - **Cụm Chicago & Windy Bay (`Comp #97`)**:
    - `[S&S] Tháp Sears Tower & Downtown Chicago` `(6127, 9477)`
    - `[Photo Spot] Sân Thượng Tháp Sears Chicago` `(6127, 9477)`
    - `[Secret Map] Vùng Vịnh Gió Windy Bay (Inokia)` `(6488, 9344)`
  - **Cụm Thị trấn Bullworth (`Comp #104`)**:
    - `[S&S] Học Viện & Thị Trấn Bullworth [BW]` `(14029, 12064)`
    - `[Bullworth] Viện Điều Dưỡng Happy Volts` `(14162, 11839)`
  - **Cụm Đảo Pera Loca (`Comp #19`) & Anneland (`Comp #88`) & Gator Keys (`Comp #1`)**:
    - `[S&S] Đảo Nam Pera Loca` `(1606, -3867)` & `Quán Rượu Pera Loca Bar` `(1593, -3855)`
    - `[S&S] Thị Trấn Đồi Elham (Anneland)` `(7732, 5748)`
    - `[Sân Bay S&S] Sân Bay Đảo Gator Keys (Vice City)` `(11152, -10173)`
  - **Cụm bị hở node nhỏ trong `.pegg` (`Comp #51`, `Comp #21`, `Comp #33`)**:
    - `[S&S] Hẻm Núi Hùng Vĩ Abyssal Canyon` `(5149, 2244)` (hở `4.4m` tại đầu đường nối)
    - Một số điểm sát đường tàu / cầu cảng (`Ngọn Hải Đăng LS`, `Bến Câu Cá Hồ Fisher's Lagoon`, `Cầu Sắt Kincaid`, `Bờ Biển Gaviota`, `Bờ Vịnh Bayside`) bị snap nhầm vào node đường tàu/nhánh cụt `Comp #21`.
- **❌ `2 / 631` địa điểm (`0.3%`) — Khu vực chưa dựng 3D (`0` vật thể `.IPL` trong bán kính `150m`)**:
  - `[Bullworth] Tòa Nhà Chính Học Viện Bullworth` `(14456, 12162)`
  - `[Bullworth] Ký Túc Xá Nam Sinh Bullworth` `(14542, 12082)`
