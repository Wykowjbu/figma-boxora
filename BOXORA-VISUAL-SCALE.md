# BOXORA-VISUAL-SCALE.md

## 0. Vai trò file này

File này là **nguồn Boxora-specific** khi dùng Claude Code + `figma-console-mcp` để dựng UI trong Figma.

File này **không** định nghĩa lại Typography scale, Radius scale, Shadow/Elevation, Blur/Backdrop, Focus Ring hoặc Spacing token nền. Các mục đó lấy từ `HEROUI-FIGMA-KIT-V3-SPECS.md`, vì đó là bản Markdown hoá token chính thức từ HeroUI Figma Kit V3.

File này **chỉ** chứa những quyết định mà HeroUI không thể tự định nghĩa vì thuộc về nghiệp vụ và layout riêng của Boxora / SDLMS:

1. Screen Inventory: bản đồ use case → screen cần dựng.
2. Dashboard/Admin layout: bố cục màn hình cho Locker Operator và Administrator.
3. UI nghiệp vụ locker: locker/compartment, parcel status, incident, audit log, fee/payment.
4. Responsive theo role: Resident, Shipper, Locker Operator, Administrator.
5. Copy tiếng Việt: thuật ngữ, tone, định dạng dữ liệu.
6. Empty state / Error state đặc thù SDLMS.

## 0.1 Decision status

Các giá trị đã điền trong file này là **decision chính thức của Boxora**, không phải ví dụ, trừ khi dòng đó ghi rõ `VÍ DỤ`, `Needs design decision`, hoặc để trống.

Agent phải hiểu theo bảng sau:

| Trạng thái trong file | Ý nghĩa | Agent được làm gì |
|---|---|---|
| Có giá trị cụ thể | Decision đã chốt | Dùng đúng giá trị đó |
| `☐` ở cột `Trạng thái dựng` | Tracker tiến độ dựng Figma | Không xem là thiếu design decision |
| `Needs design decision` | Chưa chốt | Không tự đoán, tạo Figma note cùng tên và ghi rõ thiếu gì |
| Component/pattern ghi “tra `llms-components.txt`/`llms-patterns.txt`” | Cần xác nhận với HeroUI React docs trước khi dựng | Tra docs trước; nếu không có component/pattern chính thức thì áp dụng mục 0.3 |
| Phát sinh giá trị không có trong source priority | Chưa có nguồn sự thật | Tạo note `Needs design decision` |

## 0.2 Source Priority

Dùng nguồn theo đúng thứ tự, không đảo:

1. `theme.css` — màu, radius base, field-radius, font family, light/dark mode.
2. `HEROUI-FIGMA-KIT-V3-SPECS.md` — typography, radius scale, shadow, blur, focus ring, spacing/token visual.
3. `docs/heroui/react/llms-components.txt` — props, variants, anatomy, states của HeroUI React component.
4. `docs/heroui/react/llms-patterns.txt` — layout/composition pattern khi ghép nhiều HeroUI component.
5. `BOXORA-VISUAL-SCALE.md` — chỉ các quyết định Boxora-specific trong 6 nhóm ở mục 0.
6. HeroUI Figma Kit V3 — chỉ dùng nếu đã attach vào file Figma, để đối chiếu pixel-perfect hoặc lấy component instance chính thức.

`theme.css` luôn thắng nếu có xung đột màu/radius/font. `HEROUI-FIGMA-KIT-V3-SPECS.md` luôn thắng nếu có xung đột typography/radius/shadow/blur/focus/spacing. File này không được dùng để ghi đè token nền của HeroUI.

## 0.3 Component Resolution Rule

Trong file này có một số từ như `Stepper`, `Timeline`, `Segmented control`, `Banner`, `Form`, `Filter`, `Chart`, `Grid`, `QR/OTP component`, `Image upload`. Đây là **gợi ý nghiệp vụ hoặc pattern**, không tự động được xem là component chính thức của HeroUI.

Khi dựng UI:

1. Tra `docs/heroui/react/llms-components.txt`.
2. Nếu component chính thức tồn tại trong HeroUI React → dùng đúng anatomy/props/variants/states từ docs.
3. Nếu không có component chính thức nhưng có composition pattern trong `llms-patterns.txt` → dùng pattern đó.
4. Nếu cả component và pattern đều không có → không tự invent component mới dưới tên HeroUI. Tạo Figma note `Needs design decision — component/pattern chưa chốt` và ghi rõ đang thiếu gì.
5. Nếu user đã chốt custom pattern riêng cho Boxora → đặt tên layer rõ là `Custom Pattern`, không đặt như component HeroUI chính thức.

Ví dụ: nếu `Stepper` không có trong HeroUI React docs, không được tự tạo component tên `Stepper` như HeroUI. Có thể dùng `Card + Progress + ordered steps` nếu được `llms-patterns.txt` hoặc user chốt; nếu không, tạo note.

## 0.4 Scope Lock

Hiện tại chỉ được dựng high-fidelity cho các phạm vi đã đủ decision:

| Phạm vi | Trạng thái | Rule |
|---|---|---|
| Shipper Guest mobile web | Được dựng | Mobile-responsive web, không cài app, target 375–430px |
| Locker Operator web dashboard + responsive field mobile | Được dựng | Dùng HeroUI React + Dashboard Shell trong mục 2 |
| Administrator desktop dashboard | Được dựng | Desktop first |
| Resident App | Chưa dựng high-fidelity | Platform còn `Needs design decision`; chỉ được làm screen planning/wireframe rất thấp nếu user yêu cầu rõ |
| Administrator mobile | Chưa dựng high-fidelity | Mobile còn `Needs design decision`; không tự dựng responsive mobile chi tiết |

---
# 1. Screen Inventory

Bản đồ toàn bộ 29 use case trong SRS → screen cần dựng trong Figma. Cột "Frame name gợi ý" theo naming convention ở `CLAUDE.md` mục 4. Cột "HeroUI component gợi ý sơ bộ" **chỉ là điểm khởi đầu, không phải quyết định cuối** — luôn tra `llms-components.txt` trước khi thực sự dựng.

| UC | Actor | Use case (theo SRS) | Frame name gợi ý | HeroUI component gợi ý sơ bộ (cần xác nhận lại) | Trạng thái dựng |
|---|---|---|---|---|---|
| UC-01 | Resident | Register Resident Account | `Auth / Register - Default` | Card, Input, Button, OTP input (chỉ dùng nếu có trong HeroUI React docs; nếu không có thì `Needs design decision`) | ☐ |
| UC-02 | Resident, Locker Operator, Administrator | Access Account | `Auth / Login - Default` | Card, Input, Button, Link, Alert | ☐ |
| UC-03 | Resident | Manage Personal Profile | `Resident App / Profile - Default` | Card, Avatar, Input, Button, Switch | ☐ |
| UC-04 | Resident | Configure Delivery Approval Mode | `Resident App / Approval Mode - Default` | RadioGroup ưu tiên; Switch chỉ dùng nếu HeroUI docs/pattern xác nhận phù hợp | ☐ |
| UC-05 | Resident | Process Delivery Request | `Resident App / Delivery Request - Pending` | Card, Button, Alert | ☐ |
| UC-06 | Resident | View Notifications | `Resident App / Notifications - List` | List, Badge, Tabs | ☐ |
| UC-07 | Resident | Track Parcels and Retrieval History | `Resident App / Parcel Tracking - Loaded` | Table hoặc List pattern, Badge, Tabs (tra HeroUI docs trước) | ☐ |
| UC-08 | Resident | Retrieve Parcel | `Resident App / Retrieve Parcel - Default` | Card, Button, QR/OTP pattern (tra HeroUI docs; không tự invent component) | ☐ |
| UC-09 | Resident | Pay Overdue Fees | `Resident App / Overdue Fees - Default` | Card, Alert, Button | ☐ |
| UC-10 | Resident | Submit Incident Report | `Resident App / Report Incident - Default` | Form pattern, Select, TextArea, Button (tra HeroUI docs) | ☐ |
| UC-11 | Shipper | Drop Off Parcel via Guest Session | `Shipper Guest / Drop-off - Default` | Card, Input, Button, multi-step pattern (tra HeroUI docs; nếu Stepper không có thì không tự tạo), Alert | ☐ |
| UC-12 | Shipper | Process Waybill with OCR | `Shipper Guest / Waybill OCR - Review` | Card, upload/chụp ảnh pattern, Input, Button (tra HeroUI docs) | ☐ |
| UC-13 | Shipper | Report Drop-off Incident | `Shipper Guest / Report Incident - Default` | Form pattern, Select, Button | ☐ |
| UC-14 | Locker Operator | Monitor Assigned Locker Systems | `Dashboard - Operator / Monitoring - Default` | Card, Table hoặc Grid pattern, Badge, Alert | ☐ |
| UC-15 | Locker Operator | Search Operational Data | `Dashboard - Operator / Search - Default` | Table, filter toolbar pattern, Input | ☐ |
| UC-16 | Locker Operator | Handle Operational Incident | `Dashboard - Operator / Incident Detail - Default` | Card, status history list pattern, Badge, Form pattern | ☐ |
| UC-17 | Locker Operator | Perform Emergency Locker Unlock | `Dashboard - Operator / Emergency Unlock - Confirm` | AlertDialog hoặc Modal (theo HeroUI docs), Input, Button | ☐ |
| UC-18 | Locker Operator | Manage Locker and Compartment Operational Status | `Dashboard - Operator / Compartment Status - Edit` | Modal, Select, TextArea, Button | ☐ |
| UC-19 | Locker Operator | Manage Maintenance Requests | `Dashboard - Operator / Maintenance - List` | Table, Modal, Form pattern pattern, Badge | ☐ |
| UC-20 | Locker Operator | Clear Parcels Exceeding Maximum Storage Period | `Dashboard - Operator / Clear Overdue Parcel - Default` | Table, Modal, Button | ☐ |
| UC-21 | Locker Operator | View Operational History | `Dashboard - Operator / History - Default` | Table, filter toolbar pattern, Tabs | ☐ |
| UC-22 | Administrator | Manage User Accounts | `Dashboard - Admin / Users - List` | Table, Modal, Form pattern pattern, Button | ☐ |
| UC-23 | Administrator | Manage Roles and Access Permissions | `Dashboard - Admin / Roles - List` | Table, Modal, Checkbox group/CheckboxGroup (tra HeroUI docs) | ☐ |
| UC-24 | Administrator | Manage Buildings | `Dashboard - Admin / Buildings - List` | Table, Modal, Form pattern | ☐ |
| UC-25 | Administrator | Manage Locker Infrastructure | `Dashboard - Admin / Locker Infrastructure - List` | Table, Modal, Form pattern | ☐ |
| UC-26 | Administrator | Assign Locker Operators | `Dashboard - Admin / Operator Assignment - Default` | Table, Select/Autocomplete + TagGroup nếu HeroUI docs hỗ trợ, Modal | ☐ |
| UC-27 | Administrator | Manage System Policies | `Dashboard - Admin / System Policies - Default` | Form pattern, Input, Select, Button | ☐ |
| UC-28 | Administrator | View and Export System Reports | `Dashboard - Admin / Reports - Default` | Table, chart placeholder/pattern (chỉ dùng nếu được user hoặc docs chốt), Button export | ☐ |
| UC-29 | Administrator | View Audit Logs | `Dashboard - Admin / Audit Logs - List` | Table, filter toolbar pattern, Badge | ☐ |

Nếu phát sinh screen không map thẳng 1:1 với 1 UC (ví dụ 1 UC tách thành nhiều screen, hoặc 1 screen gộp nhiều UC) → thêm dòng mới, giữ nguyên format 6 cột trên.

## 1.1 Use Case Icon Mapping

Icon set chính thức: `lucide-react`.

Bảng này định nghĩa icon chính thức cho từng use case trong Screen Inventory. Khi dựng navigation, quick action, card header, empty/error state hoặc screen title liên quan đến UC, dùng đúng icon dưới đây. Không tự chọn icon khác nếu chưa có decision mới.

| UC | Actor | Use case | Lucide icon | Kebab-case | Ghi chú |
|---|---|---|---|---|---|
| UC-01 | Resident | Register Resident Account | `UserPlus` | `user-plus` | Tạo tài khoản cư dân mới |
| UC-02 | Resident, Locker Operator, Administrator | Access Account | `LogIn` | `log-in` | Đăng nhập / truy cập tài khoản |
| UC-03 | Resident | Manage Personal Profile | `CircleUserRound` | `circle-user-round` | Hồ sơ cá nhân |
| UC-04 | Resident | Configure Delivery Approval Mode | `SlidersHorizontal` | `sliders-horizontal` | Cấu hình chế độ phê duyệt |
| UC-05 | Resident | Process Delivery Request | `MessageSquare` | `message-square` | Yêu cầu giao hàng cần phản hồi |
| UC-06 | Resident | View Notifications | `Bell` | `bell` | Thông báo |
| UC-07 | Resident | Track Parcels and Retrieval History | `Package` | `package` | Theo dõi bưu kiện |
| UC-08 | Resident | Retrieve Parcel | `QrCode` | `qr-code` | Nhận bưu kiện bằng QR/OTP/app unlock |
| UC-09 | Resident | Pay Overdue Fees | `HandCoins` | `hand-coins` | Thanh toán phí quá hạn |
| UC-10 | Resident | Submit Incident Report | `TriangleAlert` | `triangle-alert` | Báo cáo sự cố |
| UC-11 | Shipper | Drop Off Parcel via Guest Session | `CirclePlus` | `circle-plus` | Tạo phiên gửi bưu kiện |
| UC-12 | Shipper | Process Waybill with OCR | `ScanQrCode` | `scan-qr-code` | Quét/chụp vận đơn OCR |
| UC-13 | Shipper | Report Drop-off Incident | `ShieldAlert` | `shield-alert` | Báo cáo sự cố khi gửi hàng |
| UC-14 | Locker Operator | Monitor Assigned Locker Systems | `LayoutDashboard` | `layout-dashboard` | Dashboard giám sát |
| UC-15 | Locker Operator | Search Operational Data | `Search` | `search` | Tìm kiếm dữ liệu vận hành |
| UC-16 | Locker Operator | Handle Operational Incident | `Wrench` | `wrench` | Xử lý sự cố vận hành |
| UC-17 | Locker Operator | Perform Emergency Locker Unlock | `Flame` | `flame` | Mở khóa khẩn cấp, hành động rủi ro cao |
| UC-18 | Locker Operator | Manage Locker and Compartment Operational Status | `Layers` | `layers` | Quản lý trạng thái ngăn tủ |
| UC-19 | Locker Operator | Manage Maintenance Requests | `Wrench` | `wrench` | Yêu cầu bảo trì |
| UC-20 | Locker Operator | Clear Parcels Exceeding Maximum Storage Period | `Archive` | `archive` | Thu hồi/xử lý bưu kiện quá hạn lưu trữ |
| UC-21 | Locker Operator | View Operational History | `History` | `history` | Lịch sử vận hành |
| UC-22 | Administrator | Manage User Accounts | `UsersRound` | `users-round` | Quản lý người dùng |
| UC-23 | Administrator | Manage Roles and Access Permissions | `ShieldCheck` | `shield-check` | Vai trò và phân quyền |
| UC-24 | Administrator | Manage Buildings | `Building2` | `building-2` | Tòa nhà |
| UC-25 | Administrator | Manage Locker Infrastructure | `Database` | `database` | Hạ tầng tủ khóa |
| UC-26 | Administrator | Assign Locker Operators | `Handshake` | `handshake` | Phân công Operator |
| UC-27 | Administrator | Manage System Policies | `FileText` | `file-text` | Chính sách hệ thống |
| UC-28 | Administrator | View and Export System Reports | `ChartNoAxesCombined` | `chart-no-axes-combined` | Báo cáo / phân tích |
| UC-29 | Administrator | View Audit Logs | `ScrollText` | `scroll-text` | Nhật ký kiểm toán |

---

# 2. Dashboard / Admin Layout

Áp dụng cho: **Locker Operator** (web dashboard) và **Administrator** (web).

## 2.1 Dashboard Shell

| Element | Giá trị | Lý do / Ghi chú |
|---|---|---|
| Sidebar width desktop | 260px | Cân bằng giữa diện tích content và khả năng hiển thị icon + label tiếng Việt trong menu dashboard |
| Sidebar width compact/tablet | 72px | Icon-only sidebar |
| Sidebar width collapsed | Desktop/tablet collapsed: 64px, Mobile collapsed: 0px | Rule mobile: ẩn sidebar, dùng top menu / quick actions thay cho sidebar |
| Top header height | 64px | Đủ không gian cho breadcrumb, search, notification, avatar/profile |
| Content max width | Full width / không giới hạn max-width | Dashboard có nhiều màn hình table-heavy như Reports, Audit Logs, Search Operational Data |
| Main content padding desktop | 32px | Khoảng đệm rộng rãi cho giao diện máy tính |
| Main content padding tablet | 24px | Khoảng đệm trung bình cho máy tính bảng |
| Main content padding mobile | 16px | Operator có thể cần dùng dashboard trên mobile ngoài field — xem mục 4.3 |

## 2.2 Dashboard Grid Pattern

| Loại màn hình | Rule bố cục | Ghi chú |
|---|---|---|
| KPI cards (UC-14 monitoring) | Desktop: 4 cột, Tablet: 2 cột, Mobile: 1 cột | Áp dụng chính cho UC-14 Monitor Assigned Locker Systems |
| Management cards (UC-24/25/26) | Desktop: 3 cột, Tablet: 2 cột, Mobile: 1 cột | Áp dụng cho UC-24 Manage Buildings, UC-25 Manage Locker Infrastructure, UC-26 Assign Locker Operators |
| Table page (UC-15 Search Operational Data, UC-28 Reports, UC-29 Audit Logs) | Toolbar nằm trên cùng gồm search + filter + actions; Table nằm bên dưới toolbar | Mobile: filter có thể chuyển thành Drawer/Sheet. Áp dụng cho UC-15, UC-28, UC-29 |
| Detail page (UC-16 Incident detail, UC-19 Maintenance request detail) | Desktop: split view / right-side detail panel; Mobile: full-width detail page hoặc Drawer | Áp dụng cho UC-16 Incident Detail, UC-19 Maintenance Request Detail |
| Form page (UC-24/25/26/27 config forms) | Desktop: dùng 2 cột nếu form dài, dùng 1 cột nếu form ngắn; Tablet/mobile: dùng 1 cột | Áp dụng cho UC-24, UC-25, UC-26, UC-27 |

## 2.3 Component nội bộ dashboard chưa có trong HeroUI generic

| Element | Giá trị | Ghi chú |
|---|---|---|
| Emergency Unlock confirmation modal (UC-17) — kích thước, warning style | Pattern: AlertDialog. Width desktop: khoảng 520px. Warning style: dùng Alert với `--danger` | Bắt buộc Operator nhập lý do trước khi confirm. Có ghi chú rõ thao tác sẽ được ghi vào audit log. Áp dụng cho UC-17 Perform Emergency Locker Unlock |
| Audit log table density (UC-29) | Row height: compact, khoảng 36–40px. Mỗi row có thể expand để xem chi tiết | Áp dụng cho UC-29 View Audit Logs |
| Assignment picker cho Locker Operator (UC-26) | Pattern: multi-select bằng Select/Autocomplete + TagGroup | Không dùng drag-drop trong phase hiện tại vì phức tạp hơn. Áp dụng cho UC-26 Assign Locker Operators |

---

# 3. UI Nghiệp vụ Locker (Locker Business UI)

Các thành phần này gắn với SRS, không phải component generic của HeroUI. Toàn bộ màu ở mục này map theo **semantic token trong `theme.css`** (`--danger`, `--warning`, `--success`, `--default`...) — đây là nguồn màu duy nhất theo `CLAUDE.md`, không dùng lại một hệ màu riêng tách biệt song song với `theme.css`.

## 3.1 Locker / Compartment Visualization

| Trạng thái ngăn tủ | Màu (map theo `theme.css` semantic token) | Icon | Ghi chú |
|---|---|---|---|
| Available (khả dụng) | `--success` | `CircleCheck` | |
| Occupied (đang chứa bưu kiện) | `--accent` | `Lock` | |
| Reserved (đã phân bổ, chờ Shipper đặt vào — UC-11) | `--warning` | `Clock` | |
| Out of Service (Ngừng Hoạt động — UC-18) | `--danger` | `Ban` | |
| Maintenance (đang bảo trì — UC-19) | `--warning` | `Wrench` | |
| Overdue parcel inside (vượt thời hạn lưu trữ — UC-20) | `--danger` | `TriangleAlert` | Mang tính cảnh báo mạnh nhất trong nhóm |

| Element | Giá trị | Ghi chú |
|---|---|---|
| Kích thước 1 ô compartment trong grid view | 80x80px | Dùng tỷ lệ 1:1 để dễ scan trạng thái ngăn tủ. Cho màn hình UC-14 Monitor Assigned Locker Systems |
| Số cột grid theo breakpoint | Desktop: 8 cột, Tablet: 4 cột, Mobile: 2 cột | Tự động thích ứng layout sơ đồ tủ khóa trên các thiết bị |

## 3.2 Parcel Status Badge (UC-07)

| Trạng thái bưu kiện | Màu (map theo `theme.css` semantic token) | Label tiếng Việt | Icon | Ghi chú |
|---|---|---|---|---|
| Đang lưu trữ | `--accent` | Đang lưu trữ | `Package` | |
| Quá hạn | `--danger` | Quá hạn | `Timer` | |
| Đã nhận | `--success` | Đã nhận | `BadgeCheck` | |
| Đã bị xử lý (Clear — UC-20) | `--default` / neutral badge | Đã thu hồi | `ArchiveRestore` | |

## 3.3 Approval Mode Toggle (UC-04)

| Element | Giá trị | Ghi chú |
|---|---|---|
| Component dùng | Ưu tiên `RadioGroup` nếu HeroUI React docs xác nhận. Chỉ dùng `Segmented control` nếu có component/pattern chính thức trong `llms-components.txt` hoặc `llms-patterns.txt` | Không dùng `Switch` làm pattern chính vì 2 chế độ cần giải thích rõ: Phê duyệt Tự động và Phê duyệt Thủ công. Nếu không có component phù hợp, tạo note `Needs design decision — approval mode component chưa chốt`. |
| Vị trí đặt trong Resident profile screen | Đặt trong một `Card` cấu hình riêng trong Profile / Settings | |

- Phê duyệt Tự động: dùng icon `Zap`.
- Phê duyệt Thủ công: dùng icon `SlidersHorizontal`.

## 3.4 Incident Report (UC-10/UC-13/UC-16)

| Element | Giá trị | Ghi chú |
|---|---|---|
| Layout report card | Dùng `Card` có: header, status badge, severity badge, actor/source chip, metadata, mô tả, ảnh đính kèm nếu có | Đảm bảo hiển thị đầy đủ thông tin sự cố trực quan |
| Lịch sử/trạng thái xử lý sự cố | Dùng `status history list pattern`: danh sách dọc bằng Card/List item + Badge + timestamp + mô tả. Chỉ dùng component tên `Timeline` hoặc `Stepper` nếu HeroUI React docs có chính thức hoặc user chốt custom pattern riêng | Flow trạng thái: Reported → Investigating → Resolved / Escalated → Closed. Step đã hoàn tất dùng `--success`, step hiện tại dùng `--warning`. |
| Phân biệt incident theo actor (Resident report vs Shipper report vs Operator handle) | Dùng `Chip` theo actor/source: Resident, Shipper, Operator | Không tự gán màu actor riêng ngoài `theme.css` |

## 3.5 Fee / Payment Status (UC-09)

| Element | Giá trị | Ghi chú |
|---|---|---|
| Cảnh báo phí quá hạn (chặn mở khóa) | Dùng sticky `Alert`. Màu: `--danger`. Có nút action chính: `Thanh toán ngay` | Không dùng component tên `Banner` nếu HeroUI React docs không có. Đặt Alert trên cùng màn hình chi tiết bưu kiện / retrieve parcel khi còn phí quá hạn. Áp dụng cho UC-08 và UC-09 |
| Trạng thái thanh toán (Pending/Success/Failed) | Dùng `Badge` / `Chip`. Pending: `--warning`, Success: `--success`, Failed: `--danger` | Tương thích trực tiếp với phản hồi Payment API bên thứ ba |

---

# 4. Responsive theo Role (Boxora-specific, không phải breakpoint generic)

Theo kiến trúc đã chốt: 3 loại trải nghiệm khác nhau cho 4 role.

## 4.1 Resident — Mobile app

| Element | Giá trị | Ghi chú |
|---|---|---|
| Platform (tech stack thực tế) | `Needs design decision` | Chưa chốt Resident app dùng HeroUI React, HeroUI Native, Flutter hay platform khác. Không tự assume. |
| Breakpoint cần quan tâm | Mobile portrait + tablet portrait | Chỉ ghi responsive requirement ở mức role/screen planning, chưa map sang component/platform-specific pattern vì platform chưa chốt. |
| Tối thiểu hỗ trợ | 360px logical width | Áp dụng làm minimum supported width cho Resident experience. |

## 4.2 Shipper — Mobile-responsive web, guest session (UC-11/UC-12/UC-13), không cài app

| Element | Giá trị | Ghi chú |
|---|---|---|
| Breakpoint | Target width: 375–430px | Mobile web only. Không cần desktop fallback trong phase hiện tại. |
| Luồng OCR waybill (UC-12) trên mobile web | Dùng upload/chụp ảnh qua file input; sau OCR phải có bước review/edit thông tin trước khi tiếp tục | Không cho phép OCR xong đi tiếp ngay mà không có bước kiểm tra lại. |
| Single-column hay có thể multi-step | Dùng multi-step wizard pattern cho UC-11/UC-12/UC-13 | Không dùng single long form làm pattern chính. Chỉ đặt tên component là `Stepper` nếu HeroUI React docs có component này; nếu không, dùng Card + Progress/Steps copy + Button navigation theo pattern được xác nhận. |

## 4.3 Locker Operator — Web dashboard + field mobile

| Element | Giá trị | Ghi chú |
|---|---|---|
| Web dashboard breakpoint | Full responsive desktop/tablet/mobile | Phase hiện tại: responsive web. Dùng chung Dashboard Shell ở mục 2.1. |
| Field mobile — có phải app riêng hay responsive web? | Responsive web trong phase hiện tại | App riêng cho Operator có thể làm sau, nhưng không thuộc scope hiện tại vì sẽ làm dự án phình to. |
| Quick action ưu tiên trên mobile (khác desktop) | Primary: Emergency Unlock + Report/Handle Incident. Secondary: Compartment Status | Mobile field workflow ưu tiên quick actions, không tự thiết kế app native riêng ở section này. |

## 4.4 Administrator — Desktop first

| Element | Giá trị | Ghi chú |
|---|---|---|
| Có cần responsive mobile không, hay chỉ desktop? | Desktop first. Mobile: `Needs design decision` | Mobile để phase sau. Không tự dựng mobile requirement chi tiết cho Admin trong phase hiện tại. |

---

# 5. Quy tắc Copy Tiếng Việt

## 5.1 Thuật ngữ chính thức (lấy từ SRS — đã có sẵn, không tự đặt tên mới)

| Khái niệm (EN) | Thuật ngữ tiếng Việt chính thức (theo SRS) | Không dùng |
|---|---|---|
| Locker | Tủ khóa | (tránh lẫn với "tủ đồ") |
| Compartment | Ngăn tủ | "khoang tủ", "hộc tủ" |
| Parcel | Bưu kiện | "gói hàng", "đơn hàng" |
| Waybill | Vận đơn | |
| Guest session (Shipper) | Phiên gửi hàng dành cho khách | |
| OTP | Mật khẩu Dùng một lần | Có thể giữ "OTP" trong context kỹ thuật (label input), nhưng copy chính nên dùng đủ tiếng Việt |
| Personal QR Code | Mã QR Cá nhân | |
| Remote App Unlock | Mở khóa Từ xa qua Ứng dụng | |
| Face Recognition | Nhận diện Khuôn mặt | |
| Overdue fee | Phí quá hạn / Phí lưu trữ quá hạn | |
| Delivery Approval Mode | Chế độ Phê duyệt Giao hàng | Auto = "Phê duyệt Tự động", Manual = "Phê duyệt Thủ công" |
| Emergency Unlock | Mở khóa Khẩn cấp | |
| Audit log | Nhật ký kiểm toán | |
| Maintenance request | Yêu cầu bảo trì | |

Nếu cần thêm thuật ngữ không có trong SRS → điền thêm dòng vào bảng này, không tự dịch máy cứng.

## 5.2 Tone / Voice

| Ngữ cảnh | Tone | Ví dụ | Ghi chú |
|---|---|---|---|
| Error message cho Resident | Thân thiện, rõ ràng, không kỹ thuật, luôn có hướng dẫn bước tiếp theo | `Mã OTP không hợp lệ hoặc đã hết hạn. Vui lòng yêu cầu mã mới để tiếp tục.` | Dùng cho Resident app/mobile experience. Tránh thuật ngữ kỹ thuật như API, server, request timeout nếu không cần thiết. |
| Error message cho Operator/Admin (dashboard) | Trung lập, ngắn gọn, có thể kỹ thuật hơn Resident, ưu tiên nguyên nhân + hành động xử lý | `Không thể mở khóa ngăn tủ. Kiểm tra kết nối thiết bị hoặc thử lại.` | Có thể hiển thị mã lỗi hoặc trạng thái thiết bị nếu backend cung cấp, nhưng không tự bịa mã lỗi trong UI spec. |
| Cách xưng hô (có dùng "bạn" không, hay chỉ mô tả trung lập) | Resident/Shipper: dùng “bạn”. Operator/Admin dashboard: ưu tiên câu trung lập, hạn chế xưng hô | Resident: `Bưu kiện của bạn đã sẵn sàng để nhận.` Dashboard: `Không tìm thấy bản ghi phù hợp.` | Resident/Shipper cần dễ hiểu và gần gũi hơn; dashboard cần gọn, trực tiếp, nghiệp vụ. |
| Định dạng ngày/giờ | `dd/MM/yyyy HH:mm`, dùng giờ 24h, mặc định theo múi giờ Việt Nam | `06/07/2026 14:30` | Nếu chỉ cần ngày thì dùng `dd/MM/yyyy`. Nếu có deadline/hạn nhận bưu kiện thì hiển thị cả ngày và giờ. |
| Định dạng tiền tệ | Dùng `VNĐ`, phân cách hàng nghìn bằng dấu chấm, không dùng số thập phân | `12.000 VNĐ` | Áp dụng cho phí quá hạn, lịch sử thanh toán, payment result. |
| Định dạng số điện thoại | Dùng format Việt Nam 10 số, nhóm `4-3-3`; khi cần bảo mật thì mask một phần | Đầy đủ: `0912 345 678`; Mask: `0912 *** 678` | Dùng bản mask ở các màn hình không cần hiển thị toàn bộ số điện thoại, đặc biệt với Shipper hoặc dashboard operator. |

---

# 6. Empty State / Error State đặc thù SDLMS

Trigger condition lấy trực tiếp từ SRS/use case. Các message/icon/action bên dưới là decision đã chốt; nếu phát sinh case mới thì thêm dòng mới, không tự viết rời rạc ngoài file.

| Use case | Trigger condition (theo SRS) | Message tiếng Việt | Icon/Illustration | Action chính | Action phụ |
|---|---|---|---|---|---|
| UC-01 | OTP không hợp lệ hoặc hết hạn | `Mã OTP không hợp lệ hoặc đã hết hạn. Vui lòng yêu cầu mã mới để tiếp tục.` | `ShieldAlert` | `Gửi lại mã OTP` | `Đổi số điện thoại` |
| UC-08 | Còn phí quá hạn chưa thanh toán → chặn mở khóa | `Bạn cần thanh toán phí quá hạn trước khi mở ngăn tủ.` | `HandCoins` | `Thanh toán ngay` | `Xem chi tiết phí` |
| UC-11 | Không có ngăn tủ khả dụng cho phiên gửi hàng | `Hiện chưa có ngăn tủ phù hợp để gửi bưu kiện. Vui lòng thử lại sau hoặc báo sự cố nếu cần hỗ trợ.` | `ArchiveX` | `Thử lại` | `Báo sự cố` |
| UC-11 | Resident từ chối yêu cầu giao hàng | `Người nhận đã từ chối yêu cầu giao bưu kiện. Phiên gửi hàng hiện tại đã kết thúc.` | `CircleX` | `Kết thúc phiên` | `Gửi yêu cầu khác` |
| UC-11 | Yêu cầu hết hạn (Shipper không hoàn tất kịp) | `Phiên gửi hàng đã hết hạn vì chưa được hoàn tất trong thời gian quy định.` | `Clock` | `Bắt đầu phiên mới` | `Quay lại` |
| UC-12 | OCR nhận dạng thất bại → chuyển nhập thủ công | `Không thể nhận dạng thông tin từ vận đơn. Bạn có thể nhập số điện thoại người nhận thủ công.` | `ScanEye` | `Nhập thủ công` | `Chụp hoặc tải ảnh lại` |
| UC-14 | Mất kết nối thiết bị (tủ/ngăn tủ) | `Tủ khóa hoặc ngăn tủ đang mất kết nối. Kiểm tra trạng thái thiết bị hoặc tạo yêu cầu bảo trì nếu sự cố tiếp diễn.` | `WifiOff` | `Kiểm tra lại kết nối` | `Tạo yêu cầu bảo trì` |
| UC-15 | Không tìm thấy kết quả tìm kiếm (bưu kiện/sự cố/bảo trì) | `Không tìm thấy kết quả phù hợp với từ khóa hoặc bộ lọc hiện tại.` | `Search` | `Xóa bộ lọc` | `Thử từ khóa khác` |
| UC-20 | Bưu kiện đã vượt thời hạn lưu trữ tối đa | `Bưu kiện đã vượt thời hạn lưu trữ tối đa. Kiểm tra điều kiện xử lý trước khi thu hồi.` | `ArchiveX` | `Bắt đầu xử lý` | `Xem chi tiết bưu kiện` |
| Chung | Danh sách trống (chưa có dữ liệu, khác với "không tìm thấy") | `Chưa có dữ liệu để hiển thị.` | `Database` | `Không có action mặc định` | `Tải lại` |

Nếu phát sinh thêm case chưa liệt kê ở đây khi dựng UI → thêm dòng mới vào bảng, không tự bịa message rồi bỏ qua việc ghi vào file.

---

# 7. Missing Decision Rule

Áp dụng khi 1 giá trị cần dùng không có trong:

1. `theme.css`
2. `HEROUI-FIGMA-KIT-V3-SPECS.md`
3. `docs/heroui/react/llms-components.txt` / `llms-patterns.txt`
4. File này (`BOXORA-VISUAL-SCALE.md`)
5. HeroUI Figma Kit V3 (nếu đang attach)

→ Không tự bịa. Tạo Figma note tên `Needs design decision`, ghi rõ đang thiếu gì, ví dụ:

- `Missing: Sidebar width desktop chưa chốt`
- `Missing: Icon chi tiết cho trạng thái ngăn tủ chưa chốt`
- `Missing: Tone error message cho Resident chưa chốt`
- `Missing: Resident app tech stack (Flutter hay HeroUI Native) chưa xác nhận lại sau khi pivot sang HeroUI`

---

# 8. Agent Handoff Checklist

Trước khi agent coi một screen là hoàn tất trong Figma, phải kiểm tra đủ checklist sau:

| Nhóm kiểm tra | Bắt buộc |
|---|---|
| Scope | Screen thuộc phạm vi được dựng ở mục 0.4, không phải Resident App high-fidelity hoặc Admin mobile khi còn `Needs design decision` |
| Use case | Có UC/actor rõ ràng và map trong Screen Inventory |
| Icon | Đã tra mục 1.1 Use Case Icon Mapping nếu screen có navigation, quick action, card header, empty/error state hoặc title icon |
| Component | Đã tra `docs/heroui/react/llms-components.txt`; không dùng component giả mạo HeroUI |
| Pattern | Nếu là layout ghép nhiều component, đã tra `docs/heroui/react/llms-patterns.txt` |
| Token thị giác | Typography/radius/shadow/blur/focus/spacing lấy từ `HEROUI-FIGMA-KIT-V3-SPECS.md` |
| Màu | Chỉ dùng semantic token có trong `theme.css`; không dùng token không tồn tại như `--primary` hoặc `--secondary` nếu không có trong file |
| Copy | Copy UI dùng tiếng Việt theo mục 5; thuật ngữ đúng bảng 5.1 |
| Empty/error | Nếu screen có empty/error state đã tra mục 6 |
| Naming | Page/Frame/Layer đặt đúng convention trong `CLAUDE.md` |
| Missing | Mọi phần chưa có nguồn sự thật đã có note `Needs design decision` |

# 9. Build Order Khuyến nghị

Dựng theo thứ tự này để giảm rủi ro agent phải suy luận:

| Ưu tiên | Flow | Lý do |
|---|---|---|
| 1 | Shipper Guest mobile web: UC-11, UC-12, UC-13 | Platform rõ, scope hẹp, ít phụ thuộc dashboard |
| 2 | Locker Operator monitoring: UC-14, UC-15 | Dashboard shell và locker visualization đã có decision |
| 3 | Emergency / incident flow: UC-16, UC-17, UC-18, UC-19, UC-20 | Nghiệp vụ quan trọng, cần dùng đúng warning/danger/audit copy |
| 4 | Admin desktop dashboard: UC-22 đến UC-29 | Table/form-heavy, phù hợp HeroUI React |
| Tạm hoãn | Resident App | Platform chưa chốt |
| Tạm hoãn | Admin mobile | Mobile chưa chốt |

