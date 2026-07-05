# HEROUI-FIGMA-KIT-V3-SPECS.md

## 0. Mục đích file này

File này là bản Markdown hoá các token thị giác **chính thức** lấy từ trang Figma của **HeroUI Figma Kit V3** (Typography, Radius, Effect Styles). Mục tiêu: agent đọc được token gốc của HeroUI (H1, H2, radius, shadow, focus ring...) **mà không phụ thuộc việc HeroUI Figma Kit V3 có đang attach vào file Figma đang làm hay không**.

- File này KHÔNG thay thế `theme.css` (màu vẫn do `theme.css` quyết định — nếu có xung đột, `theme.css` luôn thắng).
- File này KHÔNG thay thế `docs/heroui/react/llms-components.txt` (props/variant/anatomy của component).
- File này chỉ mô tả **hệ thống token nền**: typography, radius, shadow, blur, focus ring, spacing — đúng như HeroUI Kit V3 định nghĩa.
- File này KHÔNG định nghĩa layout dashboard, nghiệp vụ locker, hay copy tiếng Việt — những cái đó thuộc `BOXORA-VISUAL-SCALE.md`.

**Nguồn:** Screenshot trang "Typography", "Radius", "Effect Styles" trong HeroUI Figma Kit V3 (footer ảnh ghi `© 2026 NextUI Inc.` — tên cũ trước rebrand thành HeroUI, khi đối chiếu lại Figma gốc nên kiểm tra đã là bản HeroUI mới nhất hay còn bản NextUI legacy).

**Trạng thái trích xuất:** ✅ = lấy được đầy đủ từ ảnh. ❓ = ảnh không hiện số liệu dạng text, cần lấy trực tiếp trong Figma.

### Source Status (tra nhanh)

| Khu vực | Trạng thái | Đã có gì | Còn thiếu gì |
|---|---|---|---|
| Typography | ✅ Đầy đủ | 16 style, size/line-height/weight (kèm số)/mô tả sử dụng | Không thiếu — đã đủ từ ảnh |
| Radius | ❓ Một phần | Tên 11 token theo đúng thứ tự tăng dần | Giá trị px của từng token |
| Shadow (6 token) | ❓ Một phần | Tên token: Inner/Surface/Field/Switch/Tab/Overlay | Offset X/Y, blur, spread, color/opacity từng token |
| Blur/Backdrop (2 token) | ❓ Một phần | Tên token: Blur/Backdrop | Loại blur, giá trị radius |
| Focus Ring (2 token) | ❓ Một phần | Tên token, suy đoán màu khớp `--focus` | Width viền, offset chính xác |
| Spacing / Token Visual | ❓ Trống hoàn toàn | Không có gì — không có ảnh nguồn cho phần này | Toàn bộ: cần ảnh chụp trang Spacing của Kit hoặc tự inspect |

---

## 1. Typography ✅ (đầy đủ)

Toàn bộ 16 style bên dưới lấy trực tiếp từ trang Typography của HeroUI Figma Kit V3. Font family: **Inter**.

| # | Style name | Weight (tên / số) | Size | Line height | Ghi chú thêm | Mô tả sử dụng (theo HeroUI) |
|---|---|---|---|---|---|---|
| 1 | Heading 1 | Extra Bold / 800 | 36px | 40px | — | Tiêu đề chính của màn hình, chỉ dùng 1 lần/màn hình. Đi cùng Body base. |
| 2 | Heading 2 | Bold / 700 | 24px | 32px | — | Tiêu đề section chính trong màn hình. Cấp bậc dưới Heading 1, dùng vừa phải. Đi cùng Body base. |
| 3 | Heading 3 | Semi Bold / 600 | 20px | 28px | — | Tiêu đề subsection hoặc khối nội dung quan trọng. Đi cùng Body sm hoặc Body base. |
| 4 | Heading 4 | Semi Bold / 600 | 16px | 24px | — | Tiêu đề subsection/panel nhỏ, khối nội dung compact. (Mô tả gốc trong Kit trùng chữ với Heading 3 — có thể là lỗi nội dung của Kit, đối chiếu lại trực tiếp trong Figma nếu cần phân biệt rõ H3 vs H4.) |
| 5 | Body base | Regular / 400 | 16px | 24px | Paragraph spacing 8px | Style đoạn văn mặc định cho hầu hết nội dung. Dùng cho văn bản dài, mô tả, chi tiết. |
| 6 | Body base medium | Medium / 500 | 16px | 24px | Paragraph spacing 8px | Giống Body base nhưng weight medium. Nhấn nhẹ cho điểm chính, label, khối nội dung ngắn. |
| 7 | Body sm | Regular / 400 | 14px | 20px | Paragraph spacing 8px | Văn bản phụ/hỗ trợ. Dùng cho caption, metadata, nội dung ít quan trọng. |
| 8 | Body sm medium | Medium / 500 | 14px | 20px | Paragraph spacing 8px | Giống Body sm nhưng weight medium. Nhấn mạnh hơn cho text nhỏ như inline label, status indicator. |
| 9 | Body xs | Regular / 400 | 12px | 16px | — | Fine print, footnote, UI element dày đặc, không gian hẹp. Không nên dùng quá nhiều. |
| 10 | Body xs medium | Medium / 500 | 12px | 16px | — | Giống Body xs nhưng weight medium. Rõ ràng/cấp bậc hơn trong không gian hẹp như table, input helper. |
| 11 | Link base | Medium / 500 | 16px | 24px | Underlined | Style link mặc định cho navigation/action inline. Dùng trong body content, menu, list. |
| 12 | Link sm | Medium / 500 | 14px | 20px | Underlined | Link inline trong context text nhỏ hơn: caption, footnote, secondary action. |
| 13 | Text field base | Regular / 400 | 16px | 24px | — | Text input trong field chuẩn. Tối ưu đọc ở size trung bình, line height thoải mái. |
| 14 | Text field sm | Regular / 400 | 14px | 20px | — | Text input trong field compact. Layout dày đặc hoặc form phụ, không gian hạn chế. |
| 15 | Button base | Medium / 500 | 16px | 24px | — | Text style chính cho button. Tối ưu đọc và cân đối trong button medium/large. |
| 16 | Button sm | Medium / 500 | 14px | 20px | — | Text style cho button compact. Không gian hạn chế nhưng vẫn giữ độ đọc được. |

### Cách dùng

- Đây là **style name chính thức của HeroUI** — khi tạo Figma Text Style, đặt tên đúng như cột "Style name" (ví dụ `Heading 1`, `Body sm medium`, `Button base`), không đặt tên tự do.
- `BOXORA-VISUAL-SCALE.md` **không** định nghĩa typography riêng — mọi màn hình Boxora dùng đúng 16 style này.
- Nếu một màn hình cần size chữ không có trong bảng trên → dấu hiệu cần xem lại layout, không tự tạo size mới. Nếu thực sự cần, tạo Figma note `Needs design decision`.

---

## 2. Radius ❓ (cần lấy số trong Figma)

Ảnh Figma Kit V3 chỉ hiện **tên token theo thứ tự tăng dần**, không hiện số px dạng text đọc được:

`None → xs → sm → md → lg → xl → 2xl → 2_5xl → 3xl → 4xl → Full`

| Token | Giá trị (px) | Ghi chú |
|---|---|---|
| `radius-none` | ☐ _(điền)_ | Thường = 0px, xác nhận lại trong Figma |
| `radius-xs` | ☐ _(điền)_ | |
| `radius-sm` | ☐ _(điền)_ | |
| `radius-md` | ☐ _(điền)_ | |
| `radius-lg` | ☐ _(điền)_ | |
| `radius-xl` | ☐ _(điền)_ | |
| `radius-2xl` | ☐ _(điền)_ | |
| `radius-2_5xl` | ☐ _(điền)_ | Tên lạ so với Tailwind default → xác nhận đây là token custom của HeroUI, không phải lỗi đọc ảnh |
| `radius-3xl` | ☐ _(điền)_ | |
| `radius-4xl` | ☐ _(điền)_ | |
| `radius-full` | 9999px (suy ra từ hình tròn trong ảnh) | Token duy nhất khẳng định chắc được từ hình dạng visual |

**Việc cần làm khi có Figma Kit V3 mở:**

1. Vào trang "Radius" trong Kit, chọn từng ô vuông mẫu (None, xs, sm...).
2. Xem panel bên phải (Design panel) → mục "Corner radius" → ghi số px vào bảng trên.
3. **Quan trọng:** `theme.css` đã fix `--radius` và `--field-radius` = `0.75rem` (12px). Sau khi điền đủ bảng trên, xác định **token nào trong scale này = 12px** và ghi chú lại ở đây, để khi dựng Card/Button/Input biết map đúng radius style nào của HeroUI Kit ứng với biến của mình.

> Token map với 12px: ☐ _(điền tên token sau khi đối chiếu)_

---

## 3. Effect Styles — Shadows ❓ (cần lấy số trong Figma)

Ảnh chỉ hiện tên 6 shadow style, không hiện offset/blur/spread/color dạng số đọc được (ô mẫu trắng trên nền trắng, gần như invisible trong ảnh chụp):

| Token | Offset X/Y | Blur | Spread | Color / Opacity | Dùng cho (theo tên) |
|---|---|---|---|---|---|
| `shadow-inner` | ☐ | ☐ | ☐ | ☐ | Inner shadow (state pressed/inset) |
| `shadow-surface` | ☐ | ☐ | ☐ | ☐ | Surface / Card mặc định |
| `shadow-field` | ☐ | ☐ | ☐ | ☐ | Input/Select/TextArea |
| `shadow-switch` | ☐ | ☐ | ☐ | ☐ | Switch component (thumb) |
| `shadow-tab` | ☐ | ☐ | ☐ | ☐ | Tab (active tab indicator/pill) |
| `shadow-overlay` | ☐ | ☐ | ☐ | ☐ | Modal/Popover/Dropdown (lớp che overlay) |

**Cách lấy giá trị:** Trong Figma, chọn layer mẫu → panel phải → mục "Effects" → click icon 4 chấm của effect style đang áp → xem chi tiết X/Y/Blur/Spread/Color/Opacity → điền vào bảng.

---

## 4. Effect Styles — Blur ❓ (cần lấy số trong Figma)

| Token | Loại blur (Layer blur / Background blur) | Radius (px) | Dùng cho |
|---|---|---|---|
| `blur-blur` | ☐ | ☐ | Blur trực tiếp trên layer (ảnh minh hoạ cho thấy dùng trên khối màu cam/xám) |
| `blur-backdrop` | ☐ | ☐ | Backdrop blur — dùng cho overlay/modal background, kính mờ phía sau |

**Cách lấy giá trị:** Chọn layer mẫu "Blur"/"Backdrop" trong Kit → panel phải → mục "Effects" → xem loại blur và giá trị Radius.

---

## 5. Effect Styles — Focus Ring ❓ (cần lấy số trong Figma)

Ảnh cho thấy 2 style, viền màu cam bo tròn quanh 1 khối:

| Token | Width viền (px) | Offset (px) | Màu |
|---|---|---|---|
| `focus-ring` | ☐ | ☐ | Có vẻ khớp `var(--focus)` trong `theme.css` (cùng là màu cam accent) — cần xác nhận lại bằng cách lấy mã màu thật trong Figma và so với `oklch(71.93% 0.1710 53.68)` |
| `focus-ring-shield` | ☐ | ☐ | Nhìn giống ring + 1 lớp "shield" (đệm/nền) phía dưới ring — dùng khi ring cần tách biệt khỏi nền xung quanh (ví dụ avatar, icon nổi trên ảnh). **Đây là suy đoán từ hình, cần xác nhận lại công dụng thật trong Figma, không lấy làm chắc.** |

**Cách lấy giá trị:** Chọn layer "Focus Ring" / "Focus Ring Shield" → panel phải → mục "Stroke" (width) và "Effects" (nếu ring là 1 shape riêng đè lên, đo offset bằng khoảng cách giữa cạnh ring và cạnh element gốc).

---

## 6. Spacing / Token Visual ❓ (trống hoàn toàn — chưa có ảnh nguồn)

Không có ảnh chụp trang Spacing/Token của HeroUI Figma Kit V3 trong bộ ảnh đã cung cấp ban đầu (chỉ có Typography, Radius, Effect Styles). Mục này hiện là **khung trống thật**, không có số liệu nào để trích, không suy đoán số.

| Token | Giá trị (px) | Category (gap/padding/size) | Dùng cho | Vị trí lấy trong Figma Kit |
|---|---|---|---|---|
| ☐ | ☐ | ☐ | ☐ | ☐ |
| ☐ | ☐ | ☐ | ☐ | ☐ |

**Cách bổ sung phần này:**

1. Cách nhanh nhất: chụp ảnh trang "Spacing" (hoặc tên tương đương) trong HeroUI Figma Kit V3, gửi giống 3 ảnh Typography/Radius/Effect Styles trước — từ đó điền chính xác như đã làm ở các mục 1–5.
2. Nếu không có trang riêng: tự inspect Auto Layout gap/padding của các component mẫu trong Figma Kit (Button, Input, Card, Modal) rồi ghi lại số.

**Checklist nên lấy khi inspect:**

| Cần lấy | Ghi chú |
|---|---|
| Padding nội bộ Button/Input/Card/Modal/Popover/Table/Tabs | |
| Gap icon–label trong Button | |
| Gap giữa field trong Form | |
| Chiều cao Button theo size (sm/md/lg) | |
| Chiều cao Input theo size (sm/md/lg) | |
| Page/container width nếu Kit có định nghĩa | |

---

## 7. Quy trình cập nhật khi lấy được số liệu thật

1. Mở HeroUI Figma Kit V3 → tới đúng trang (Radius / Effect Styles / Spacing).
2. Lấy giá trị theo hướng dẫn ở từng mục trên.
3. Thay các dòng `☐ _(điền)_` bằng số thật.
4. Đổi trạng thái của section đó từ ❓ thành ✅ (cả ở Source Status và ở tiêu đề section).
5. Nếu HeroUI ra bản Kit mới làm thay đổi số liệu → cập nhật lại toàn bộ file này, note lại ngày cập nhật ở dưới.

**Lần cập nhật gần nhất:** _(điền ngày bạn hoàn tất điền số liệu)_
**Người cập nhật:** _(điền tên)_