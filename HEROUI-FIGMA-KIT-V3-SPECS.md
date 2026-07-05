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
| Radius | ✅ Đầy đủ | 11 token với giá trị px chính xác | Không thiếu — đã inspect trực tiếp từ Figma |
| Shadow (6 token) | ✅ Đã lấy đủ từ Figma | 6 tokens với multi-layer shadows đầy đủ (inner, surface, field, switch, tab, overlay) | Không thiếu — đã inspect từ visual samples |
| Blur/Backdrop (2 token) | ✅ Đã lấy đủ từ Figma | blur-blur: BACKGROUND_BLUR radius=12; blur-backdrop: BACKGROUND_BLUR radius=12 + overlay rgba(0,0,0,0.5) | Không thiếu — đã inspect từ Variables + visual samples |
| Focus Ring (2 token) | ✅ Đã lấy từ Figma Variables | ring-offset-width=2, ring-focus-width=4, focus-ring=#F48120; visual implementation bằng drop shadow | Không thiếu — đã inspect từ Variables + visual samples |
| Spacing / Token Visual | ✅ Đã lấy từ Figma Variables | 35 spacing tokens (0→96, giá trị px chính xác) | Component-specific padding/height vẫn cần inspect ở từng component nếu cần pixel-perfect |

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

## 2. Radius ✅ (đã lấy từ Figma)

> **Đã inspect trực tiếp từ trang "Radius" trong HeroUI Figma Kit V3** (page id: `0:1`, frame id: `17421:36561`). Giá trị corner radius đọc chính xác từ Figma node properties (cornerRadius), không suy đoán.

`None → xs → sm → md → lg → xl → 2xl → 2_5xl → 3xl → 4xl → Full`

| Token | Giá trị (px) | Ghi chú |
|---|---|---|
| `radius-none` | 0 | Không bo tròn |
| `radius-xs` | 3 | |
| `radius-sm` | 6 | |
| `radius-md` | 9 | |
| `radius-lg` | 12 | **Token map với `--radius: 0.75rem` (12px) trong `theme.css`** |
| `radius-xl` | 18 | |
| `radius-2xl` | 24 | |
| `radius-2_5xl` | 30 | Token custom của HeroUI (không có trong Tailwind default) |
| `radius-3xl` | 36 | |
| `radius-4xl` | 48 | |
| `radius-full` | 9999 | Bo tròn tối đa — hình tròn hoặc pill shape |

> **Token map với 12px: `radius-lg`**

---

## 3. Effect Styles — Shadows ✅ (đã lấy từ Figma)

> **Đã inspect trực tiếp từ trang "Foundations" → frame "Effect Styles" → container "Shadow" samples.** Tất cả 6 shadow token đều có trong Figma.

### Figma Variables liên quan

| Variable Name | Giá trị | Type | Ghi chú |
|---|---|---|---|
| `shadow-inner` | rgba(0,0,0,0.3) | COLOR | Dùng cho inner shadow |
| `field/shadow` | rgba(0,0,0,0.04) | COLOR | Dùng cho field shadow layer 1 |
| `field/shadow-2` | rgba(0,0,0,0.06) | COLOR | Dùng cho field/surface/overlay layers |
| `overlay-shadow` | rgba(0,0,0,0.06) | COLOR | Dùng cho overlay shadow |
| `depth` | 0 | FLOAT | Base depth value |

### Shadow Token Table (từ visual samples)

HeroUI sử dụng **multi-layer shadows** — mỗi token có thể có nhiều layers shadow chồng lên nhau:

| Token | Layer | Offset X/Y | Blur (radius) | Spread | Color / Opacity | Dùng cho |
|---|---|---|---|---|---|---|
| `shadow-inner` | 1 | 0, 0 | 1 | 0 | #000000 / 30% | Inner shadow (state pressed/inset) |
| `shadow-surface` | 1 | 0, 2 | 4 | 0 | #000000 / 4% | Surface / Card mặc định |
| | 2 | 0, 1 | 2 | 0 | #000000 / 6% | |
| | 3 | 0, 0 | 1 | 0 | #000000 / 6% | |
| `shadow-field` | 1 | 0, 2 | 4 | 0 | #000000 / 4% | Input/Select/TextArea |
| | 2 | 0, 1 | 2 | 0 | #000000 / 6% | |
| | 3 | 0, 0 | 1 | 0 | #000000 / 6% | |
| `shadow-switch` | 1 | 0, 0 | 5 | 0 | #000000 / 2% | Switch component (thumb) |
| | 2 | 0, 2 | 10 | 0 | #000000 / 6% | |
| | 3 | 0, 0 | 1 | 0 | #000000 / 30% | |
| `shadow-tab` | 1 | 0, 2 | 8 | 0 | #000000 / 6% | Tab (active tab indicator/pill) |
| `shadow-overlay` | 1 | 0, 2 | 8 | 0 | #000000 / 6% | Modal/Popover/Dropdown |
| | 2 | 0, -6 | 12 | 0 | #000000 / 3% | |
| | 3 | 0, 14 | 28 | 0 | #000000 / 8% | |

### Ghi chú

- **shadow-field** và **shadow-surface** có cấu hình shadow giống hệt nhau trong Figma samples.
- **shadow-switch** có 3 layers với layer trong cùng (radius: 1, opacity: 30%) tạo hiệu ứng "sharp" cho thumb.
- **shadow-overlay** có layer thứ 2 offset âm (y: -6) tạo hiệu ứng "phóng to" ra phía trên.
- Tất cả shadow đều dùng màu #000000 (đen thuần) với các mức opacity khác nhau.

---

## 4. Effect Styles — Blur ✅ (đã lấy từ Figma)

> **Đã inspect trực tiếp từ:**
> 1. Figma Variables panel → Collection `02_Theme (HeroUI)` → 4 blur-related variables
> 2. Visual samples trên trang "Foundations" → frame "Effect Styles" → container "Blur" / "Backdrop"

### Figma Variables liên quan

| Variable Name | Giá trị | Type | Ghi chú |
|---|---|---|---|
| `blur` | 0 | FLOAT | Base blur value (chưa dùng trong samples) |
| `backdrop` | rgba(0,0,0,0.5) | COLOR | Backdrop overlay color — đen 50% opacity |
| `shadow-scroll-blur` | rgba(246,245,244,0.7) | COLOR | Scroll shadow blur trên nền light |
| `shadow-scroll-blur-on-surface` | rgba(255,255,255,0.7) | COLOR | Scroll shadow blur trên surface |

### Visual Samples (từ Effect Styles frame)

Cả hai samples đều sử dụng **BACKGROUND_BLUR** (Background blur, không phải Layer blur):

| Token | Loại blur | Radius (px) | Overlay Color | Dùng cho | Nguồn |
|---|---|---|---|---|---|
| `blur-blur` | BACKGROUND_BLUR | 12 | Không có overlay (element trong suốt) | Blur trực tiếp trên layer — ảnh minh hoạ cho thấy dùng trên khối màu cam/xám | Visual sample: Effect Styles → container → Blur |
| `blur-backdrop` | BACKGROUND_BLUR | 12 | rgba(0,0,0,0.5) (từ variable `backdrop`) | Backdrop blur — dùng cho overlay/modal background, kính mờ phía sau | Visual sample: Effect Styles → container → Backdrop + Variable `backdrop` |

### Blur Stack (cách HeroUI render)

**Blur sample:**
```
┌─────────────────────────┐
│  Element with IMAGE fill │  ← BACKGROUND_BLUR radius=12
│  (no overlay)            │
└─────────────────────────┘
```

**Backdrop sample:**
```
┌─────────────────────────┐
│  Element with IMAGE fill │  ← BACKGROUND_BLUR radius=12
│  ┌─────────────────────┐│
│  │  Overlay (50% black) ││  ← BACKGROUND_BLUR radius=12 + fill rgba(0,0,0,0.5)
│  └─────────────────────┘│
└─────────────────────────┘
```

### Ghi chú

- Cả `blur-blur` và `blur-backdrop` đều dùng **BACKGROUND_BLUR** với **radius = 12px**.
- Sự khác biệt chính: `blur-backdrop` có thêm overlay layer với màu đen 50% opacity (từ variable `backdrop`), trong khi `blur-blur` không có overlay.
- Variable `blur` (= 0) hiện chưa được dùng trong visual samples — có thể là placeholder cho tương lai.

---

## 5. Effect Styles — Focus Ring ✅ (đã lấy từ Figma Variables + visual samples)

> **Đã inspect trực tiếp từ:**
> 1. Figma Variables panel → Collection `02_Theme (HeroUI)` → 3 variables (ring-offset-width, ring-focus-width, focus-ring)
> 2. Visual samples trên trang "Foundations" → frame "Effect Styles" → container "Focus Ring" / "Focus Ring Shield"

### Figma Variables

| Variable Name | Giá trị | Type | Collection |
|---|---|---|---|
| `ring-offset-width` | 2 | FLOAT | 02_Theme (HeroUI) |
| `ring-focus-width` | 4 | FLOAT | 02_Theme (HeroUI) |
| `focus-ring` | #F48120 (rgb: 244, 129, 32) | COLOR | 02_Theme (HeroUI) |

### Visual Samples (cách HeroUI render focus ring)

HeroUI render focus ring bằng **drop shadow với spread = width, offset = 0, blur = 0** (không dùng stroke):

| Token | Implementation | Width/Spread (px) | Offset (px) | Màu | Nguồn |
|---|---|---|---|---|---|
| `focus-ring` | DROP_SHADOW (inner ring) | 4 | 0 | #F48120 | Variables: `ring-focus-width` + `focus-ring` |
| `focus-ring-shield` | DROP_SHADOW (outer shield) | 2 | 0 | #F6F5F4 (white/near-white) | Variables: `ring-offset-width` |

### Focus Ring visual stack (từ trong ra ngoài)

```
┌─────────────────────────────────┐
│  Shield layer (spread=2, #F6F5F4)  │  ← ring-offset-width
│  ┌─────────────────────────────┐│
│  │  Ring layer (spread=4, #F48120) │  ← ring-focus-width + focus-ring color
│  │  ┌─────────────────────────┐││
│  │  │      Element gốc        │││
│  │  └─────────────────────────┘││
│  └─────────────────────────────┘│
└─────────────────────────────────┘
```

### Ghi chú

- `focus-ring` color (#F48120) **khớp chính xác** với `var(--focus)` trong `theme.css` (`oklch(71.93% 0.1710 53.68)` ≈ #F48120).
- Shield layer dùng màu trắng (#F6F5F4) để tạo hiệu ứng "đệm" giữa ring và nền xung quanh — hữu ích khi element nổi trên ảnh hoặc nền đậm màu.

---

## 6. Spacing / Token Visual ✅ (đã lấy từ Figma Variables)

> **Đã inspect trực tiếp từ Figma Variables API** — Collection `01_Base (Tailwind)`, Group `dimensions/spacing`. Tổng: **35 variables**, tất cả type FLOAT.

**Nguồn:** Figma Variables panel → Collection "01_Base (Tailwind)" → Group "dimensions" → Subgroup "spacing"

| Token | Giá trị (px) | Category | Dùng cho | Vị trí lấy trong Figma Kit |
|---|---|---|---|---|
| `spacing/0` | 0 | spacing | Tailwind base spacing token; dùng làm gap/padding/size khi HeroUI component hoặc layout cần token spacing. | Figma Variables → 01_Base (Tailwind) → dimensions/spacing |
| `spacing/px` | 1 | spacing | Tailwind base spacing token; dùng làm gap/padding/size khi HeroUI component hoặc layout cần token spacing. | Figma Variables → 01_Base (Tailwind) → dimensions/spacing |
| `spacing/0.5` | 2 | spacing | Tailwind base spacing token; dùng làm gap/padding/size khi HeroUI component hoặc layout cần token spacing. | Figma Variables → 01_Base (Tailwind) → dimensions/spacing |
| `spacing/1` | 4 | spacing | Tailwind base spacing token; dùng làm gap/padding/size khi HeroUI component hoặc layout cần token spacing. | Figma Variables → 01_Base (Tailwind) → dimensions/spacing |
| `spacing/1.5` | 6 | spacing | Tailwind base spacing token; dùng làm gap/padding/size khi HeroUI component hoặc layout cần token spacing. | Figma Variables → 01_Base (Tailwind) → dimensions/spacing |
| `spacing/2` | 8 | spacing | Tailwind base spacing token; dùng làm gap/padding/size khi HeroUI component hoặc layout cần token spacing. | Figma Variables → 01_Base (Tailwind) → dimensions/spacing |
| `spacing/2.5` | 10 | spacing | Tailwind base spacing token; dùng làm gap/padding/size khi HeroUI component hoặc layout cần token spacing. | Figma Variables → 01_Base (Tailwind) → dimensions/spacing |
| `spacing/3` | 12 | spacing | Tailwind base spacing token; dùng làm gap/padding/size khi HeroUI component hoặc layout cần token spacing. | Figma Variables → 01_Base (Tailwind) → dimensions/spacing |
| `spacing/3.5` | 14 | spacing | Tailwind base spacing token; dùng làm gap/padding/size khi HeroUI component hoặc layout cần token spacing. | Figma Variables → 01_Base (Tailwind) → dimensions/spacing |
| `spacing/4` | 16 | spacing | Tailwind base spacing token; dùng làm gap/padding/size khi HeroUI component hoặc layout cần token spacing. | Figma Variables → 01_Base (Tailwind) → dimensions/spacing |
| `spacing/5` | 20 | spacing | Tailwind base spacing token; dùng làm gap/padding/size khi HeroUI component hoặc layout cần token spacing. | Figma Variables → 01_Base (Tailwind) → dimensions/spacing |
| `spacing/6` | 24 | spacing | Tailwind base spacing token; dùng làm gap/padding/size khi HeroUI component hoặc layout cần token spacing. | Figma Variables → 01_Base (Tailwind) → dimensions/spacing |
| `spacing/7` | 28 | spacing | Tailwind base spacing token; dùng làm gap/padding/size khi HeroUI component hoặc layout cần token spacing. | Figma Variables → 01_Base (Tailwind) → dimensions/spacing |
| `spacing/8` | 32 | spacing | Tailwind base spacing token; dùng làm gap/padding/size khi HeroUI component hoặc layout cần token spacing. | Figma Variables → 01_Base (Tailwind) → dimensions/spacing |
| `spacing/9` | 36 | spacing | Tailwind base spacing token; dùng làm gap/padding/size khi HeroUI component hoặc layout cần token spacing. | Figma Variables → 01_Base (Tailwind) → dimensions/spacing |
| `spacing/10` | 40 | spacing | Tailwind base spacing token; dùng làm gap/padding/size khi HeroUI component hoặc layout cần token spacing. | Figma Variables → 01_Base (Tailwind) → dimensions/spacing |
| `spacing/11` | 44 | spacing | Tailwind base spacing token; dùng làm gap/padding/size khi HeroUI component hoặc layout cần token spacing. | Figma Variables → 01_Base (Tailwind) → dimensions/spacing |
| `spacing/12` | 48 | spacing | Tailwind base spacing token; dùng làm gap/padding/size khi HeroUI component hoặc layout cần token spacing. | Figma Variables → 01_Base (Tailwind) → dimensions/spacing |
| `spacing/14` | 56 | spacing | Tailwind base spacing token; dùng làm gap/padding/size khi HeroUI component hoặc layout cần token spacing. | Figma Variables → 01_Base (Tailwind) → dimensions/spacing |
| `spacing/16` | 64 | spacing | Tailwind base spacing token; dùng làm gap/padding/size khi HeroUI component hoặc layout cần token spacing. | Figma Variables → 01_Base (Tailwind) → dimensions/spacing |
| `spacing/20` | 80 | spacing | Tailwind base spacing token; dùng làm gap/padding/size khi HeroUI component hoặc layout cần token spacing. | Figma Variables → 01_Base (Tailwind) → dimensions/spacing |
| `spacing/24` | 96 | spacing | Tailwind base spacing token; dùng làm gap/padding/size khi HeroUI component hoặc layout cần token spacing. | Figma Variables → 01_Base (Tailwind) → dimensions/spacing |
| `spacing/28` | 112 | spacing | Tailwind base spacing token; dùng làm gap/padding/size khi HeroUI component hoặc layout cần token spacing. | Figma Variables → 01_Base (Tailwind) → dimensions/spacing |
| `spacing/32` | 128 | spacing | Tailwind base spacing token; dùng làm gap/padding/size khi HeroUI component hoặc layout cần token spacing. | Figma Variables → 01_Base (Tailwind) → dimensions/spacing |
| `spacing/36` | 144 | spacing | Tailwind base spacing token; dùng làm gap/padding/size khi HeroUI component hoặc layout cần token spacing. | Figma Variables → 01_Base (Tailwind) → dimensions/spacing |
| `spacing/40` | 160 | spacing | Tailwind base spacing token; dùng làm gap/padding/size khi HeroUI component hoặc layout cần token spacing. | Figma Variables → 01_Base (Tailwind) → dimensions/spacing |
| `spacing/44` | 176 | spacing | Tailwind base spacing token; dùng làm gap/padding/size khi HeroUI component hoặc layout cần token spacing. | Figma Variables → 01_Base (Tailwind) → dimensions/spacing |
| `spacing/48` | 192 | spacing | Tailwind base spacing token; dùng làm gap/padding/size khi HeroUI component hoặc layout cần token spacing. | Figma Variables → 01_Base (Tailwind) → dimensions/spacing |
| `spacing/52` | 208 | spacing | Tailwind base spacing token; dùng làm gap/padding/size khi HeroUI component hoặc layout cần token spacing. | Figma Variables → 01_Base (Tailwind) → dimensions/spacing |
| `spacing/56` | 224 | spacing | Tailwind base spacing token; dùng làm gap/padding/size khi HeroUI component hoặc layout cần token spacing. | Figma Variables → 01_Base (Tailwind) → dimensions/spacing |
| `spacing/60` | 240 | spacing | Tailwind base spacing token; dùng làm gap/padding/size khi HeroUI component hoặc layout cần token spacing. | Figma Variables → 01_Base (Tailwind) → dimensions/spacing |
| `spacing/64` | 256 | spacing | Tailwind base spacing token; dùng làm gap/padding/size khi HeroUI component hoặc layout cần token spacing. | Figma Variables → 01_Base (Tailwind) → dimensions/spacing |
| `spacing/72` | 288 | spacing | Tailwind base spacing token; dùng làm gap/padding/size khi HeroUI component hoặc layout cần token spacing. | Figma Variables → 01_Base (Tailwind) → dimensions/spacing |
| `spacing/80` | 320 | spacing | Tailwind base spacing token; dùng làm gap/padding/size khi HeroUI component hoặc layout cần token spacing. | Figma Variables → 01_Base (Tailwind) → dimensions/spacing |
| `spacing/96` | 384 | spacing | Tailwind base spacing token; dùng làm gap/padding/size khi HeroUI component hoặc layout cần token spacing. | Figma Variables → 01_Base (Tailwind) → dimensions/spacing |

**Quy ước:** Mỗi token spacing = token name × 4px (ví dụ: `spacing/4` = 4 × 4 = 16px), ngoại trừ `spacing/0` = 0px và `spacing/px` = 1px.

**Lưu ý:** Component-specific padding/height vẫn cần inspect ở từng component nếu cần pixel-perfect.

---

## 7. Quy trình cập nhật khi lấy được số liệu thật

1. Mở HeroUI Figma Kit V3 → tới đúng trang (Radius / Effect Styles / Spacing).
2. Lấy giá trị theo hướng dẫn ở từng mục trên.
3. Thay các dòng `☐ _(điền)_` bằng số thật.
4. Đổi trạng thái của section đó từ ❓ thành ✅ (cả ở Source Status và ở tiêu đề section).
5. Nếu HeroUI ra bản Kit mới làm thay đổi số liệu → cập nhật lại toàn bộ file này, note lại ngày cập nhật ở dưới.

**Lần cập nhật gần nhất:** 2026-07-06
**Người cập nhật:** Claude Code (inspect trực tiếp từ Figma Variables + visual samples)