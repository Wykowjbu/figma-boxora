# CLAUDE.md — Boxora UI Design

## 0. Scope

- Mục đích DUY NHẤT của repo này: dùng Claude Code + `figma-console-mcp` để tạo/chỉnh sửa UI trong Figma.
- KHÔNG viết code production.
- KHÔNG tạo/chỉnh sửa file `.tsx`, `.jsx`, `.ts`, `.js`, `.css` trong app code nếu user không yêu cầu rõ.
- Nếu user yêu cầu "implement" UI, luôn hiểu là "dựng trong Figma qua MCP", không phải viết code.
- Không tự ý gọi MCP khác ngoài Figma trong flow design (kể cả khi có sẵn MCP khác trong session).

## 1. Platform Lock

- Platform target: `docs/heroui/react/**` (Next.js web) — DUY NHẤT.
- KHÔNG đọc, KHÔNG tham chiếu `docs/heroui/native/` hoặc `docs/heroui/all/` trừ khi user yêu cầu rõ bằng chữ.
- Nếu search HeroUI docs trả về kết quả từ `native/` hoặc `all/`, bỏ qua, chỉ dùng `react/`.

## 1.1 Scope Readiness Lock

Chỉ dựng high-fidelity UI cho các phạm vi đã đủ decision:

| Phạm vi | Trạng thái | Rule |
|---|---|---|
| Shipper Guest mobile web | Được dựng | Mobile-responsive web, không cài app, target 375–430px |
| Locker Operator web dashboard + responsive field mobile | Được dựng | Dùng HeroUI React + Dashboard Shell trong `BOXORA-VISUAL-SCALE.md` |
| Administrator desktop dashboard | Được dựng | Desktop first |
| Resident App | Chưa dựng high-fidelity | Platform còn `Needs design decision`; không tự assume HeroUI React/HeroUI Native/Flutter |
| Administrator mobile | Chưa dựng high-fidelity | Mobile còn `Needs design decision`; không tự dựng responsive mobile chi tiết |

Nếu user yêu cầu dựng Resident App hoặc Admin mobile khi decision còn thiếu, tạo note `Needs design decision` và hỏi/chờ user chốt platform/scope trước. Không tự mở rộng phạm vi để “hoàn thành task”.

## 2. Source Priority — BẮT BUỘC đọc trước khi design

Thứ tự nguồn sự thật, không đảo:

1. **`theme.css`** — màu, radius, field-radius, font family, light/dark. Đã chốt, không đổi.
2. **`HEROUI-FIGMA-KIT-V3-SPECS.md`** — Typography (Heading 1–4, Body, Link, Text field, Button), Radius scale, Effect Styles (Shadow, Blur, Focus Ring), Spacing/Token theo đúng token gốc của HeroUI Figma Kit V3. File này tồn tại độc lập với việc Figma Kit V3 có đang attach hay không — luôn đọc file này trước khi cần bất kỳ giá trị typography/radius/shadow/focus ring/spacing nào, không đợi mở Figma Kit.
3. **`docs/heroui/react/llms-components.txt`** — props/variants/anatomy component HeroUI (Button, Input, Card, Modal, Table...).
4. **`docs/heroui/react/llms-patterns.txt`** — layout/composition pattern khi ghép nhiều component.
5. **`BOXORA-VISUAL-SCALE.md`** — CHỈ 6 mục sau, không lặp lại bất kỳ token nào đã có ở nguồn 1–4: Screen Inventory, dashboard/admin layout, UI nghiệp vụ locker (locker/compartment/parcel status/incident/audit log), responsive riêng theo role, quy tắc copy tiếng Việt, empty/error state đặc thù SDLMS.
6. **HeroUI Figma Kit V3** — chỉ dùng nếu đã attach vào file Figma đang làm việc. Nếu chưa chắc kit này có trong file, hỏi user trước, không tự giả định có. Khi có attach, dùng để đối chiếu pixel-perfect với `HEROUI-FIGMA-KIT-V3-SPECS.md`, không dùng thay thế file đó.

Đọc `docs/heroui/react/llms.txt` khi không chắc component nào phù hợp (tra nhanh). Chỉ đọc `llms-full.txt` khi nguồn 1–5 không đủ — file này rất nặng context, tránh load nếu không cần.

Nếu giá trị cần dùng không có trong bất kỳ nguồn nào ở trên → áp dụng "Missing Decision Rule" ở mục 7 của `BOXORA-VISUAL-SCALE.md`: KHÔNG tự bịa số, tạo Figma note tên `Needs design decision` ghi rõ đang thiếu gì.

## 2.1 Component Resolution Rule

Không được giả định mọi tên trong `BOXORA-VISUAL-SCALE.md` đều là component chính thức của HeroUI.

Áp dụng khi gặp các từ như `Stepper`, `Timeline`, `Segmented control`, `Banner`, `Form`, `Filter`, `Chart`, `Grid`, `QR/OTP component`, `Image upload`:

1. Tra `docs/heroui/react/llms-components.txt`.
2. Nếu component chính thức tồn tại → dùng đúng anatomy/props/variants/states từ docs.
3. Nếu không có component chính thức nhưng có composition pattern trong `docs/heroui/react/llms-patterns.txt` → dùng pattern đó.
4. Nếu cả component và pattern đều không có → không tự invent component mới dưới tên HeroUI. Tạo note `Needs design decision — component/pattern chưa chốt`.
5. Nếu user chốt custom pattern riêng cho Boxora → đặt tên layer rõ là `Custom Pattern`, không đặt như component HeroUI chính thức.

## 2.2 Token / Color Lock

- Màu chỉ lấy từ `theme.css`.
- Không dùng token không tồn tại trong `theme.css`, ví dụ `--primary`, `--secondary`, `--info`, nếu file không định nghĩa.
- Không tự tạo palette riêng cho trạng thái locker/parcel/incident.
- Không hard-code màu Hex trong Figma trừ khi đang map chính xác từ token đã có trong `theme.css` hoặc `HEROUI-FIGMA-KIT-V3-SPECS.md`.
- Typography/radius/shadow/blur/focus/spacing chỉ lấy từ `HEROUI-FIGMA-KIT-V3-SPECS.md` hoặc HeroUI Figma Kit V3 đã attach để đối chiếu.
- Nếu cần token mới → `Needs design decision`, không tự tạo.

## 3. Quy trình dựng 1 màn hình mới (Workflow)

Theo đúng thứ tự, không bỏ bước:

1. Xác định actor và use case (mã UC theo SRS nếu có) đang dựng.
2. Kiểm tra scope readiness ở mục 1.1. Nếu screen thuộc Resident App high-fidelity hoặc Admin mobile khi còn `Needs design decision`, không dựng tiếp.
3. Tra `BOXORA-VISUAL-SCALE.md` mục 1 (Screen Inventory). Nếu use case đã có dòng, dùng đúng frame name làm điểm khởi đầu. Nếu chưa có, thêm dòng mới vào bảng đó trước khi dựng.
4. Tra `BOXORA-VISUAL-SCALE.md` mục 1.1 (Use Case Icon Mapping) nếu screen có navigation, quick action, card header, title icon, empty state hoặc error state liên quan đến UC.
5. Tra `docs/heroui/react/llms-components.txt` để chọn component HeroUI phù hợp và xem đúng props/variant/state component đó hỗ trợ.
6. Áp dụng Component Resolution Rule ở mục 2.1 với mọi tên component/pattern chưa chắc là HeroUI chính thức. Không tự tạo component giả mạo HeroUI.
7. Nếu có nhiều component ghép lại, tra `docs/heroui/react/llms-patterns.txt` để lấy đúng pattern composition.
8. Áp token Typography/Radius/Shadow/Blur/Focus/Spacing từ `HEROUI-FIGMA-KIT-V3-SPECS.md`.
9. Áp màu từ `theme.css` theo Token / Color Lock ở mục 2.2.
10. Nếu màn hình có nghiệp vụ locker riêng (trạng thái ngăn tủ, parcel, incident, fee...) hoặc cần copy tiếng Việt/empty-error state → tra đúng mục tương ứng trong `BOXORA-VISUAL-SCALE.md` (mục 3–6).
11. Nếu bất kỳ bước trên thiếu giá trị → tạo Figma note `Needs design decision`, không tự đoán, không bỏ qua bước để “xong việc”.
12. Đặt tên Page/Frame/Layer theo mục 4 (Figma Naming Convention) trước khi coi màn hình là hoàn tất.
13. Chạy checklist ở mục 10 (Completion Gate).
14. Cập nhật cột `Trạng thái dựng` trong Screen Inventory (`BOXORA-VISUAL-SCALE.md` mục 1) sau khi hoàn tất.


## 4. Figma Naming Convention

- Component/layer đặt tên đúng theo tên component HeroUI: `Button`, `Card`, `Modal`, `Input`, `Sidebar`... không đặt tên tự do (`Frame 1`, `Rectangle 23`...).
- Text style đặt tên đúng theo `HEROUI-FIGMA-KIT-V3-SPECS.md` mục 1: `Heading 1`, `Body sm medium`, `Button base`... không tự đặt tên khác (`Title/Large`, `Text-16`...).
- Giữ cấu trúc variant giống HeroUI làm Figma component properties: `size` (sm/md/lg), `color` (default/primary/danger...), `variant` (solid/bordered/light...).
- Page trong Figma đặt tên theo flow nghiệp vụ, không theo ngày/version: ví dụ `Auth`, `Dashboard - Admin`, `Locker Management`, `Resident App`. Không dùng `Page 1`, `Untitled`.
- Frame tên theo screen thực tế, có hậu tố state: `Login - Default`, `Login - Invalid Credentials`, `Drop Off Parcel - Waiting Approval`, `Locker List - Empty State`, `Locker List - Loaded`, `Incident Detail - Escalated`.

## 5. Icon System

- Icon set chính thức của Boxora: `lucide-react`.
- Không dùng icon set khác nếu user không yêu cầu rõ.
- Không trộn nhiều icon style khác nhau trong cùng file Figma.
- Khi dựng icon trong Figma, dùng style outline nhất quán theo Lucide: stroke đều, round cap/join, optical alignment tốt với text.
- Icon không được hard-code màu riêng. Icon phải kế thừa màu qua `currentColor` hoặc map theo semantic token từ `theme.css` (`--accent`, `--success`, `--warning`, `--danger`, `--default`, `--muted`, `--foreground`...).
- Icon-only action trong UI phải có label/annotation rõ ràng trong Figma để sau này code có thể map sang `aria-label`.
- Không tự chọn icon mới nếu use case đã có mapping trong `BOXORA-VISUAL-SCALE.md`.
- Nếu phát sinh use case/icon mới chưa có mapping → tạo note `Needs design decision — icon chưa chốt`, không tự bịa.

## 6. Light / Dark Mode Workflow

- `theme.css` đã định nghĩa đầy đủ cả `.light` và `.dark`.
- Mặc định làm việc ở Light mode trước cho mọi screen mới. Dark mode chỉ dựng khi user yêu cầu rõ cho screen đó.
- Khi dựng Dark mode, dùng Figma Variables/Modes để map 1:1 theo cặp biến trong `theme.css` (`--surface` light ↔ `--surface` dark...), không tạo style rời rạc riêng cho dark.
- Nếu cần dark mode đồng bộ toàn bộ file ngay từ đầu, user phải nói rõ — không tự mở rộng phạm vi.

## 7. Component States — BẮT BUỘC cover khi dựng component set

Khi dựng bất kỳ component tương tác (Button, Input, Select, Card có action, Menu item...), phải có tối thiểu các state sau nếu HeroUI component đó hỗ trợ:

| State | Bắt buộc cho |
|---|---|
| Default | Tất cả |
| Hover | Button, Link, Menu item, Table row action |
| Focus | Input, Select, TextArea, Button (keyboard nav) |
| Disabled | Button, Input, Select, Checkbox, Radio |
| Error/Invalid | Input, Select, TextArea |
| Loading | Button (submit), Table (skeleton) |
| Empty | Table, danh sách bưu kiện, danh sách tủ khóa, notification list |
| Warning/Incident | Locker/compartment status, maintenance, overdue parcel |

Thứ tự tra cứu khi dựng state:

1. `docs/heroui/react/llms-components.txt` — kiểm tra component đó có built-in state prop không (`isInvalid`, `isDisabled`, `isLoading`...). Nếu có, dùng đúng anatomy đó, không tự vẽ lại.
2. `HEROUI-FIGMA-KIT-V3-SPECS.md` mục 5 — lấy đúng giá trị Focus Ring khi cần render trạng thái focus.
3. `Empty` và `Warning/Incident` không phải state chuẩn của 1 component HeroUI đơn lẻ mà là state ở cấp màn hình/nghiệp vụ — nội dung cụ thể (message, icon, action) tra ở `BOXORA-VISUAL-SCALE.md` mục 6 (Empty/Error State).
4. Nếu vẫn thiếu giá trị cụ thể (ví dụ màu hover chính xác) → `Needs design decision`, không tự đoán theo cảm giác.

`BOXORA-VISUAL-SCALE.md` không định nghĩa lại state visual của component — chỉ định nghĩa nội dung state ở cấp nghiệp vụ (empty/error/incident).

## 8. Content Language

- Copy UI mặc định: **tiếng Việt**, trừ khi màn hình đó rõ ràng target quốc tế hoặc user yêu cầu tiếng Anh.
- Thuật ngữ nghiệp vụ (locker, ngăn tủ, vận đơn, phí quá hạn...) dùng đúng theo bảng thuật ngữ ở `BOXORA-VISUAL-SCALE.md` mục 5.1 — không tự dịch lại theo cách khác giữa các screen.
- Label, placeholder, error message, empty state text — viết tiếng Việt tự nhiên, không dịch máy cứng từ HeroUI example. Tra `BOXORA-VISUAL-SCALE.md` mục 6 trước khi viết empty/error state cho use case đã có trong SRS.
- Giữ tên component/prop bằng tiếng Anh (theo HeroUI), chỉ nội dung hiển thị mới dùng tiếng Việt.

## 9. Update Propagation

- Khi `theme.css` thay đổi giá trị (màu, radius, font) → phải rà lại Figma Styles/Variables tương ứng trong session tiếp theo, không để lệch giữa code và design.
- Khi HeroUI Figma Kit V3 ra bản mới làm thay đổi Typography/Radius/Effect Styles/Spacing → cập nhật lại `HEROUI-FIGMA-KIT-V3-SPECS.md` trước, sau đó mới rà lại các screen đã dựng nếu cần.
- Khi `BOXORA-VISUAL-SCALE.md` thay đổi số liệu layout/nghiệp vụ → áp dụng cho screen mới tạo sau đó; không bắt buộc sửa retroactive các screen cũ trừ khi user yêu cầu.
- Khi có quyết định mới làm thay đổi assumption cũ đã đánh dấu "cần xác nhận lại" (ví dụ tech stack Resident app) → cập nhật ngay dòng đó trong `BOXORA-VISUAL-SCALE.md`, không để tồn đọng cả 2 phiên bản thông tin cùng lúc.

## 10. Completion Gate — bắt buộc trước khi báo xong

Một screen chỉ được xem là hoàn tất khi đạt đủ các điều kiện:

| Nhóm | Điều kiện |
|---|---|
| Scope | Không vi phạm Scope Readiness Lock |
| Source | Đã dùng đúng Source Priority, không đảo nguồn |
| Component | Mọi component đã được xác nhận qua HeroUI React docs hoặc được đánh dấu custom/Needs decision |
| Token | Typography/radius/shadow/blur/focus/spacing lấy từ `HEROUI-FIGMA-KIT-V3-SPECS.md` |
| Color | Màu lấy từ `theme.css`, không dùng token không tồn tại |
| Icon | Icon theo `lucide-react` và đúng mapping nếu có UC |
| Copy | Copy tiếng Việt đúng thuật ngữ trong `BOXORA-VISUAL-SCALE.md` |
| State | Có default/hover/focus/disabled/error/loading/empty/warning nếu component hoặc screen cần |
| Naming | Page/Frame/Layer không dùng tên rác như `Frame 1`, `Rectangle 23` |
| Missing | Mọi thiếu sót đều có note `Needs design decision` rõ ràng |

Nếu một điều kiện chưa đạt, không báo “done”. Ghi rõ blocker hoặc tạo note trong Figma.

## 11. Current Repository Structure

Root folder: `Figma-boxora`

```txt
docs/
  heroui/
    react/
      llms.txt
      llms-components.txt
      llms-patterns.txt
      llms-full.txt
    native/            # KHÔNG dùng — xem mục 1
    all/               # KHÔNG dùng — xem mục 1

theme.css
HEROUI-FIGMA-KIT-V3-SPECS.md
BOXORA-VISUAL-SCALE.md
CLAUDE.md
.mcp.json
skills-lock.json
```

## 12. MCP

- Server đang dùng: `figma-console-mcp`.
- Không tự ý gọi MCP khác ngoài Figma trong flow design.
- Nếu tool call tới `figma-console-mcp` lỗi do auth/permission, báo lại cho user, không thử fallback sang cách khác (ví dụ viết code) để "hoàn thành task".