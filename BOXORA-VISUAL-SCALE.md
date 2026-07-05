# BOXORA-VISUAL-SCALE.md

## 0. Vai trò file này (đã thu hẹp lại)

File này **không** định nghĩa Typography scale, Radius scale, Shadow/Elevation, Focus ring — các mục đó có sẵn trong HeroUI Figma Kit V3, xem `HEROUI-FIGMA-KIT-V3-SPECS.md`.

File này **chỉ** chứa những gì HeroUI (component library) không định nghĩa, vì nó thuộc về nghiệp vụ và layout riêng của Boxora:

1. Screen Inventory (bản đồ toàn bộ use case → screen cần dựng)
2. Dashboard/Admin layout (bố cục màn hình cho Locker Operator & Administrator)
3. UI nghiệp vụ locker (locker/compartment, parcel status, incident, audit log...)
4. Responsive riêng theo từng role (Resident/Shipper/Operator/Administrator có platform khác nhau)
5. Quy tắc copy tiếng Việt (thuật ngữ, tone)
6. Empty state / Error state đặc thù theo use case của SDLMS

**Nguyên tắc bắt buộc:** File này KHÔNG tự quyết định số liệu layout cụ thể (ví dụ sidebar rộng bao nhiêu px). Bảng số liệu là **khung trống** để bạn điền, kèm 1 ví dụ minh hoạ cách điền (đánh dấu rõ "VÍ DỤ", không phải giá trị thật). Agent đọc file này không được tự bịa số vào các dòng còn trống — nếu thiếu, tạo Figma note `Needs design decision` theo mục 7.

**Lưu ý về thông tin lấy từ ghi nhớ dự án trước đây:** Một số assumption từng được chốt ở các buổi làm việc trước (ví dụ Resident dùng Flutter + Material 3, hệ 7 màu semantic riêng) được giữ lại có trích dẫn rõ nguồn, nhưng đánh dấu **cần xác nhận lại** vì dự án đã pivot sang HeroUI làm design system chính — có thể một số quyết định cũ không còn khớp với `theme.css`/HeroUI hiện tại. Xem mục 4.1 và mục 3.1.

## Source Priority (đồng bộ với CLAUDE.md)

1. `theme.css` — màu, radius base, font family.
2. `HEROUI-FIGMA-KIT-V3-SPECS.md` — typography, radius scale, shadow, blur, focus ring, spacing.
3. `docs/heroui/react/llms-components.txt` — props/variant/anatomy component.
4. `docs/heroui/react/llms-patterns.txt` — layout/composition pattern của HeroUI.
5. `BOXORA-VISUAL-SCALE.md` (file này) — chỉ 6 mục nêu ở mục 0, không lặp lại token đã có ở trên.
6. HeroUI Figma Kit V3 (nếu đã attach vào file Figma) — đối chiếu pixel-perfect.

---

## VÍ DỤ MINH HOẠ CÁCH ĐIỀN (không phải giá trị thật của Boxora)

> Mục đích: chỉ để bạn thấy format điền, KHÔNG dùng số này cho dự án thật.

| Element | Giá trị | Lý do / Ghi chú |
|---|---|---|
| Sidebar width desktop | 280px | Đủ chứa label menu dài nhất ("Quản lý hạ tầng tủ khóa") không bị wrap, đã test ở Figma frame `Dashboard - Admin / Sidebar Expanded` |

Các bảng thật từ mục 1 trở xuống để trống hoàn toàn (hoặc chỉ điền phần lấy thẳng từ SRS) — bạn điền phần còn thiếu theo đúng format này (Element / Giá trị / Lý do).

---

# 1. Screen Inventory

Bản đồ toàn bộ 29 use case trong SRS → screen cần dựng trong Figma. Cột "Frame name gợi ý" theo naming convention ở `CLAUDE.md` mục 4. Cột "HeroUI component gợi ý sơ bộ" **chỉ là điểm khởi đầu, không phải quyết định cuối** — luôn tra `llms-components.txt` trước khi thực sự dựng.

| UC | Actor | Use case (theo SRS) | Frame name gợi ý | HeroUI component gợi ý sơ bộ (cần xác nhận lại) | Trạng thái dựng |
|---|---|---|---|---|---|
| UC-01 | Resident | Register Resident Account | `Auth / Register - Default` | Card, Input, Button, OTP input (tra `llms-components.txt`) | ☐ |
| UC-02 | Resident, Locker Operator, Administrator | Access Account | `Auth / Login - Default` | Card, Input, Button, Link, Alert | ☐ |
| UC-03 | Resident | Manage Personal Profile | `Resident App / Profile - Default` | Card, Avatar, Input, Button, Switch | ☐ |
| UC-04 | Resident | Configure Delivery Approval Mode | `Resident App / Approval Mode - Default` | Switch hoặc RadioGroup (tra component nào HeroUI hỗ trợ đúng) | ☐ |
| UC-05 | Resident | Process Delivery Request | `Resident App / Delivery Request - Pending` | Card, Button, Alert | ☐ |
| UC-06 | Resident | View Notifications | `Resident App / Notifications - List` | List, Badge, Tabs | ☐ |
| UC-07 | Resident | Track Parcels and Retrieval History | `Resident App / Parcel Tracking - Loaded` | Table/List, Badge, Tabs | ☐ |
| UC-08 | Resident | Retrieve Parcel | `Resident App / Retrieve Parcel - Default` | Card, Button, QR/OTP component | ☐ |
| UC-09 | Resident | Pay Overdue Fees | `Resident App / Overdue Fees - Default` | Card, Alert, Button | ☐ |
| UC-10 | Resident | Submit Incident Report | `Resident App / Report Incident - Default` | Form, Select, TextArea, Button | ☐ |
| UC-11 | Shipper | Drop Off Parcel via Guest Session | `Shipper Guest / Drop-off - Default` | Card, Input, Button, Stepper (tra component), Alert | ☐ |
| UC-12 | Shipper | Process Waybill with OCR | `Shipper Guest / Waybill OCR - Review` | Card, Image upload, Input, Button | ☐ |
| UC-13 | Shipper | Report Drop-off Incident | `Shipper Guest / Report Incident - Default` | Form, Select, Button | ☐ |
| UC-14 | Locker Operator | Monitor Assigned Locker Systems | `Dashboard - Operator / Monitoring - Default` | Card, Table/Grid, Badge, Alert | ☐ |
| UC-15 | Locker Operator | Search Operational Data | `Dashboard - Operator / Search - Default` | Table, Filter, Input | ☐ |
| UC-16 | Locker Operator | Handle Operational Incident | `Dashboard - Operator / Incident Detail - Default` | Card, Timeline/List, Badge, Form | ☐ |
| UC-17 | Locker Operator | Perform Emergency Locker Unlock | `Dashboard - Operator / Emergency Unlock - Confirm` | Modal/AlertDialog, Input, Button | ☐ |
| UC-18 | Locker Operator | Manage Locker and Compartment Operational Status | `Dashboard - Operator / Compartment Status - Edit` | Modal, Select, TextArea, Button | ☐ |
| UC-19 | Locker Operator | Manage Maintenance Requests | `Dashboard - Operator / Maintenance - List` | Table, Modal, Form, Badge | ☐ |
| UC-20 | Locker Operator | Clear Parcels Exceeding Maximum Storage Period | `Dashboard - Operator / Clear Overdue Parcel - Default` | Table, Modal, Button | ☐ |
| UC-21 | Locker Operator | View Operational History | `Dashboard - Operator / History - Default` | Table, Filter, Tabs | ☐ |
| UC-22 | Administrator | Manage User Accounts | `Dashboard - Admin / Users - List` | Table, Modal, Form, Button | ☐ |
| UC-23 | Administrator | Manage Roles and Access Permissions | `Dashboard - Admin / Roles - List` | Table, Modal, Checkbox group | ☐ |
| UC-24 | Administrator | Manage Buildings | `Dashboard - Admin / Buildings - List` | Table, Modal, Form | ☐ |
| UC-25 | Administrator | Manage Locker Infrastructure | `Dashboard - Admin / Locker Infrastructure - List` | Table, Modal, Form | ☐ |
| UC-26 | Administrator | Assign Locker Operators | `Dashboard - Admin / Operator Assignment - Default` | Table, Select, Modal | ☐ |
| UC-27 | Administrator | Manage System Policies | `Dashboard - Admin / System Policies - Default` | Form, Input, Select, Button | ☐ |
| UC-28 | Administrator | View and Export System Reports | `Dashboard - Admin / Reports - Default` | Table, Chart (tra pattern), Button (export) | ☐ |
| UC-29 | Administrator | View Audit Logs | `Dashboard - Admin / Audit Logs - List` | Table, Filter, Badge | ☐ |

Nếu phát sinh screen không map thẳng 1:1 với 1 UC (ví dụ 1 UC tách thành nhiều screen, hoặc 1 screen gộp nhiều UC) → thêm dòng mới, giữ nguyên format 6 cột trên.

---

# 2. Dashboard / Admin Layout

Áp dụng cho: **Locker Operator** (web dashboard) và **Administrator** (web).

## 2.1 Dashboard Shell

| Element | Giá trị | Lý do / Ghi chú |
|---|---|---|
| Sidebar width desktop | ☐ | |
| Sidebar width compact/tablet | ☐ | |
| Sidebar width collapsed | ☐ | |
| Top header height | ☐ | |
| Content max width | ☐ | |
| Main content padding desktop | ☐ | |
| Main content padding tablet | ☐ | |
| Main content padding mobile | ☐ | Operator có thể cần dùng dashboard trên mobile ngoài field — xem mục 4.3 |

## 2.2 Dashboard Grid Pattern

| Loại màn hình | Rule bố cục | Ghi chú |
|---|---|---|
| KPI cards (UC-14 monitoring) | ☐ | Số cột desktop/tablet/mobile |
| Management cards (UC-24/25/26) | ☐ | |
| Table page (UC-15 Search Operational Data, UC-28 Reports, UC-29 Audit Logs) | ☐ | Toolbar vị trí, filter vị trí |
| Detail page (UC-16 Incident detail, UC-19 Maintenance request detail) | ☐ | Panel phụ bên phải có/không |
| Form page (UC-24/25/26/27 config forms) | ☐ | 1 cột hay 2 cột |

## 2.3 Component nội bộ dashboard chưa có trong HeroUI generic

| Element | Giá trị | Ghi chú |
|---|---|---|
| Emergency Unlock confirmation modal (UC-17) — kích thước, warning style | ☐ | Cần nhấn mạnh vì có ghi audit log |
| Audit log table density (UC-29) | ☐ | Row height, có expand chi tiết hay không |
| Assignment picker cho Locker Operator (UC-26) | ☐ | Dạng multi-select building/cluster hay drag-drop |

---

# 3. UI Nghiệp vụ Locker (Locker Business UI)

Các thành phần này gắn với SRS, không phải component generic của HeroUI. Toàn bộ màu ở mục này map theo **semantic token trong `theme.css`** (`--danger`, `--warning`, `--success`, `--default`...) — đây là nguồn màu duy nhất theo `CLAUDE.md`, không dùng lại một hệ màu riêng tách biệt song song với `theme.css`.

## 3.1 Locker / Compartment Visualization

| Trạng thái ngăn tủ | Màu (map theo `theme.css` semantic token) | Icon | Ghi chú |
|---|---|---|---|
| Available (khả dụng) | ☐ | ☐ | |
| Occupied (đang chứa bưu kiện) | ☐ | ☐ | |
| Reserved (đã phân bổ, chờ Shipper đặt vào — UC-11) | ☐ | ☐ | |
| Out of Service (Ngừng Hoạt động — UC-18) | ☐ | ☐ | |
| Maintenance (đang bảo trì — UC-19) | ☐ | ☐ | |
| Overdue parcel inside (vượt thời hạn lưu trữ — UC-20) | ☐ | ☐ | Gợi ý: dùng `--danger` vì mang tính cảnh báo mạnh nhất trong nhóm |

| Element | Giá trị | Ghi chú |
|---|---|---|
| Kích thước 1 ô compartment trong grid view | ☐ | Cho màn hình UC-14 Monitor Assigned Locker Systems |
| Số cột grid theo breakpoint | ☐ | |

## 3.2 Parcel Status Badge (UC-07)

| Trạng thái bưu kiện | Màu (map theo `theme.css` semantic token) | Label tiếng Việt | Ghi chú |
|---|---|---|---|
| Đang lưu trữ | ☐ | ☐ | |
| Quá hạn | ☐ | ☐ | Gợi ý: `--danger` |
| Đã nhận | ☐ | ☐ | Gợi ý: `--success` |
| Đã bị xử lý (Clear — UC-20) | ☐ | ☐ | |

## 3.3 Approval Mode Toggle (UC-04)

| Element | Giá trị | Ghi chú |
|---|---|---|
| Component dùng (Switch/Segmented control/Radio) | ☐ | Kiểm tra `llms-components.txt` trước khi chọn |
| Vị trí đặt trong Resident profile screen | ☐ | |

## 3.4 Incident Report (UC-10/UC-13/UC-16)

| Element | Giá trị | Ghi chú |
|---|---|---|
| Layout report card | ☐ | |
| Timeline trạng thái xử lý sự cố | ☐ | Reported → Investigating → Resolved/Escalated → Closed |
| Phân biệt incident theo actor (Resident report vs Shipper report vs Operator handle) | ☐ | |

## 3.5 Fee / Payment Status (UC-09)

| Element | Giá trị | Ghi chú |
|---|---|---|
| Banner cảnh báo phí quá hạn (chặn mở khóa) | ☐ | UC-08 nói rõ: không cho mở khóa khi còn phí tồn đọng |
| Trạng thái thanh toán (Pending/Success/Failed) | ☐ | Payment API bên thứ ba |

---

# 4. Responsive theo Role (Boxora-specific, không phải breakpoint generic)

Theo kiến trúc đã chốt: 3 loại trải nghiệm khác nhau cho 4 role.

## 4.1 Resident — Mobile app

| Element | Giá trị | Ghi chú |
|---|---|---|
| Platform (tech stack thực tế) | ☐ **cần xác nhận lại** | Ghi nhớ dự án trước đây ghi Resident dùng Flutter + Material 3 native. Nhưng dự án hiện đã pivot sang **HeroUI (React)** làm design system chính, và repo có `docs/heroui/native/` — gợi ý có thể đang cân nhắc HeroUI Native/React Native cho mobile thay vì Flutter. Cần xác nhận rõ Resident app hiện tại dùng công nghệ gì trước khi dựng UI Figma cho Resident, không lấy assumption cũ làm chắc. |
| Breakpoint cần quan tâm | ☐ | Chủ yếu 1 kích thước mobile, có cần hỗ trợ tablet không? |
| Tối thiểu hỗ trợ | ☐ | Kích thước màn hình nhỏ nhất |

## 4.2 Shipper — Mobile-responsive web, guest session (UC-11/UC-12), không cài app

| Element | Giá trị | Ghi chú |
|---|---|---|
| Breakpoint | ☐ | Chỉ cần mobile web, có cần layout desktop dự phòng không (trường hợp Shipper dùng máy tính)? |
| Luồng OCR waybill (UC-12) trên mobile web | ☐ | Camera access, review/edit sau OCR |
| Single-column hay có thể multi-step | ☐ | |

## 4.3 Locker Operator — Web dashboard + field mobile

| Element | Giá trị | Ghi chú |
|---|---|---|
| Web dashboard breakpoint | ☐ | Dùng chung Dashboard Shell ở mục 2.1 |
| Field mobile — có phải app riêng hay responsive web? | ☐ | Ảnh hưởng tới UC-17 Emergency Unlock ngoài field |
| Quick action ưu tiên trên mobile (khác desktop) | ☐ | Ví dụ: Emergency Unlock, Report Incident cần nổi bật hơn trên mobile |

## 4.4 Administrator — Chủ yếu web

| Element | Giá trị | Ghi chú |
|---|---|---|
| Có cần responsive mobile không, hay chỉ desktop? | ☐ | SRS ghi "chủ yếu web-based" — cần xác nhận rõ có bắt buộc mobile hay không |

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

## 5.2 Tone / Voice (chưa quyết định — điền)

| Ngữ cảnh | Tone | Ví dụ | Ghi chú |
|---|---|---|---|
| Error message cho Resident | ☐ | ☐ | Thân thiện hay trung lập? |
| Error message cho Operator/Admin (dashboard) | ☐ | ☐ | Có thể ngắn gọn/kỹ thuật hơn Resident |
| Cách xưng hô (có dùng "bạn" không, hay chỉ mô tả trung lập) | ☐ | ☐ | |
| Định dạng ngày/giờ | ☐ | ☐ | dd/mm/yyyy? có giờ theo 24h? |
| Định dạng tiền tệ | ☐ | ☐ | VNĐ, phân cách hàng nghìn |
| Định dạng số điện thoại | ☐ | ☐ | |

---

# 6. Empty State / Error State đặc thù SDLMS

Trigger condition lấy trực tiếp từ SRS (đã có sẵn trong use case), phần message/icon/action để trống cho bạn quyết định.

| Use case | Trigger condition (theo SRS) | Message tiếng Việt | Icon/Illustration | Action chính | Action phụ |
|---|---|---|---|---|---|
| UC-01 | OTP không hợp lệ hoặc hết hạn | ☐ | ☐ | ☐ | ☐ |
| UC-08 | Còn phí quá hạn chưa thanh toán → chặn mở khóa | ☐ | ☐ | ☐ | ☐ |
| UC-11 | Không có ngăn tủ khả dụng cho phiên gửi hàng | ☐ | ☐ | ☐ | ☐ |
| UC-11 | Resident từ chối yêu cầu giao hàng | ☐ | ☐ | ☐ | ☐ |
| UC-11 | Yêu cầu hết hạn (Shipper không hoàn tất kịp) | ☐ | ☐ | ☐ | ☐ |
| UC-12 | OCR nhận dạng thất bại → chuyển nhập thủ công | ☐ | ☐ | ☐ | ☐ |
| UC-14 | Mất kết nối thiết bị (tủ/ngăn tủ) | ☐ | ☐ | ☐ | ☐ |
| UC-15 | Không tìm thấy kết quả tìm kiếm (bưu kiện/sự cố/bảo trì) | ☐ | ☐ | ☐ | ☐ |
| UC-20 | Bưu kiện đã vượt thời hạn lưu trữ tối đa | ☐ | ☐ | ☐ | ☐ |
| Chung | Danh sách trống (chưa có dữ liệu, khác với "không tìm thấy") | ☐ | ☐ | ☐ | ☐ |

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
- `Missing: Icon set cho locker compartment status chưa chốt`
- `Missing: Tone error message cho Resident chưa chốt`
- `Missing: Resident app tech stack (Flutter hay HeroUI Native) chưa xác nhận lại sau khi pivot sang HeroUI`