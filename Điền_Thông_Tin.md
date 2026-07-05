Nên điền theo thứ tự này. Không điền lan man từ trên xuống dưới file, vì có mục là **foundation**, có mục là **business decision**.

| Thứ tự | File / mục                                                    | Nên điền gì                                                                                   | Vì sao ưu tiên                                                                                                                                          |
| -----: | ------------------------------------------------------------- | --------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
|      1 | `HEROUI-FIGMA-KIT-V3-SPECS.md` → mục 2 Radius                 | `radius-none` → `radius-4xl`, xác định token nào = `12px`                                     | Đây là token nền cho Card/Button/Input/Modal. `theme.css` đang có `--radius` và `--field-radius = 0.75rem = 12px`, nên phải map với token HeroUI trước. |
|      2 | `HEROUI-FIGMA-KIT-V3-SPECS.md` → mục 6 Spacing / Token Visual | Padding Button/Input/Card/Modal/Table, gap icon-label, field gap, height Button/Input         | Đây là phần ảnh hưởng trực tiếp đến layout khi dựng UI. Nếu thiếu, agent rất dễ tự bịa khoảng cách.                                                     |
|      3 | `HEROUI-FIGMA-KIT-V3-SPECS.md` → mục 5 Focus Ring             | Width, offset, màu thật của `focus-ring` và `focus-ring-shield`                               | Focus state là bắt buộc cho Input/Button/Select. Làm sớm để agent dựng state đúng ngay từ đầu.                                                          |
|      4 | `HEROUI-FIGMA-KIT-V3-SPECS.md` → mục 3 Shadow                 | `shadow-surface`, `shadow-field`, `shadow-overlay` trước; các shadow còn lại sau              | Card/Input/Modal/Popover cần shadow. Ưu tiên 3 token dùng nhiều nhất trước.                                                                             |
|      5 | `HEROUI-FIGMA-KIT-V3-SPECS.md` → mục 4 Blur                   | `blur-backdrop`, `blur-blur`                                                                  | Chỉ cần trước khi dựng Modal/Overlay. Không gấp bằng radius/spacing/focus.                                                                              |
|      6 | `BOXORA-VISUAL-SCALE.md` → mục 4 Responsive theo Role         | Chốt platform Resident, breakpoint Shipper, Operator field mobile, Admin có mobile không      | Phải chốt trước khi dựng frame. Nếu chưa chốt platform mobile, agent sẽ bị kẹt giữa React web, HeroUI Native, Flutter.                                  |
|      7 | `BOXORA-VISUAL-SCALE.md` → mục 2 Dashboard/Admin Layout       | Dashboard Shell, Grid Pattern, dashboard component nội bộ                                     | Đây là khung cho Operator/Admin. Chốt trước khi dựng UC-14 đến UC-29.                                                                                   |
|      8 | `BOXORA-VISUAL-SCALE.md` → mục 3 UI nghiệp vụ Locker          | Trạng thái locker/compartment, parcel badge, approval mode, incident timeline, payment status | Đây là nghiệp vụ riêng SDLMS. HeroUI không định nghĩa sẵn, nên phải chốt để màn hình không bị generic.                                                  |
|      9 | `BOXORA-VISUAL-SCALE.md` → mục 5.2 Tone / Voice               | Tone Resident, tone Admin/Operator, xưng hô, ngày/giờ, tiền tệ, số điện thoại                 | Chốt trước khi viết message, empty state, error state.                                                                                                  |
|     10 | `BOXORA-VISUAL-SCALE.md` → mục 6 Empty/Error State            | Message tiếng Việt, icon/illustration, action chính/phụ                                       | Điền sau tone và icon/status, vì các câu thông báo phải nhất quán.                                                                                      |
|     11 | `BOXORA-VISUAL-SCALE.md` → mục 1 Screen Inventory             | Chưa cần điền thêm nhiều; chỉ cập nhật trạng thái dựng khi đã dựng thật                       | Mục này đã có 29 UC. Không nên sửa nhiều trước khi agent bắt đầu dựng, trừ khi phát sinh screen mới.                                                    |
|     12 | `CLAUDE.md`                                                   | Không cần điền thêm                                                                           | File này là rule vận hành, không phải file dữ liệu còn thiếu. Chỉ sửa khi bạn đổi workflow/source priority/platform rule.                               |
|     13 | `theme.css`                                                   | Không điền, không sửa                                                                         | File này đã chốt. Chỉ dùng để đối chiếu màu/radius/font.                                                                                                |

Thứ tự thực tế nên làm là:

**Đợt 1 — hoàn thiện token HeroUI trước:**
`HEROUI-FIGMA-KIT-V3-SPECS.md` mục **2 → 6 → 5 → 3 → 4**.

**Đợt 2 — chốt quyết định platform/layout:**
`BOXORA-VISUAL-SCALE.md` mục **4 → 2**.

**Đợt 3 — chốt nghiệp vụ và copy:**
`BOXORA-VISUAL-SCALE.md` mục **3 → 5.2 → 6**.

**Đợt 4 — dùng khi bắt đầu dựng UI:**
Cập nhật `Screen Inventory` sau từng screen, không cần điền hết trước.

Lý do: `HEROUI-FIGMA-KIT-V3-SPECS.md` là file token nền, còn `BOXORA-VISUAL-SCALE.md` chỉ chứa phần HeroUI không định nghĩa như screen inventory, dashboard layout, UI nghiệp vụ locker, responsive role, copy và empty/error state.  

Riêng `CLAUDE.md` hiện đã ép agent đọc `theme.css`, `HEROUI-FIGMA-KIT-V3-SPECS.md`, HeroUI React docs, rồi mới đến `BOXORA-VISUAL-SCALE.md`, nên nó không phải file cần điền dữ liệu tiếp. 
