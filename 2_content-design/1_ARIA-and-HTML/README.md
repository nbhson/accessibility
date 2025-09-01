# ARIA và HTML

## 🎯 Tổng quan

### HTML - Nền tảng accessibility
**HTML** cung cấp ngữ nghĩa mặc định cho trình duyệt và công nghệ hỗ trợ.

```html
<button>Click me</button>
```
✅ Tự động có vai trò nút, focus bằng bàn phím, kích hoạt bằng Space/Enter

### ARIA - Bổ sung thông tin
**ARIA** cung cấp thông tin accessibility khi HTML không đủ.

| Thành phần | Ví dụ | Mô tả |
|------------|-------|-------|
| **Roles** | `role="navigation"` | Định nghĩa chức năng |
| **Properties** | `aria-label="Đóng menu"` | Cung cấp thông tin mô tả |
| **States** | `aria-expanded="false"` | Cho biết trạng thái hiện tại |

> **🚨 Nguyên tắc vàng:** "No ARIA is better than bad ARIA" - Luôn ưu tiên HTML có sẵn. Chỉ dùng ARIA khi HTML không đủ.

## 🔄 Mối quan hệ giữa POUR và ARIA

### POUR - "CHIẾN LƯỢC" (What & Why)
**POUR** là nguyên tắc cấp cao trả lời: *"Trang web accessible cần như thế nào?"*

| Nguyên tắc | Mô tả | Ví dụ |
|------------|-------|-------|
| **P**erceivable | Thông tin hiển thị được | Hình ảnh có alt text |
| **O**perable | Giao diện dễ sử dụng | Điều hướng bằng bàn phím |
| **U**nderstandable | Thông tin dễ hiểu | Ngôn ngữ rõ ràng, đơn giản |
| **R**obust | Tương thích công nghệ | Hoạt động với AT hiện tại/tương lai |

### ARIA - "CÔNG CỤ" (How)
**ARIA** là kỹ thuật cụ thể trả lời: *"Làm thế nào đạt được POUR?"*

**Cung cấp thuộc tính HTML:** `role`, `aria-label`, `aria-expanded`...

### Ví dụ thực tế: Menu dropdown

**POUR nói:** 
- "Người dùng phải biết menu đang mở/đóng" (Perceivable)
- "Có thể dùng bàn phím mở/đóng" (Operable)

**ARIA thực hiện:**
```html
<button aria-expanded="false" aria-haspopup="true">
  Menu
</button>
```
- `aria-expanded` → Thông báo trạng thái (Perceivable)
- JavaScript → Quản lý sự kiện bàn phím (Operable)

## 📊 So sánh trực quan

| Đặc điểm | POUR | ARIA |
|----------|------|------|
| **Bản chất** | Nguyên tắc, Triết lý | Kỹ thuật, Công cụ |
| **Mục đích** | Định hướng mục tiêu accessibility | Cung cấp phương tiện kỹ thuật |
| **Mức độ** | Trừu tượng, cấp cao | Cụ thể, cấp thấp (code) |
| **Ví dụ** | "Thông tin phải dễ hiểu" | `aria-describedby` liên kết input với hướng dẫn |
| **Mối quan hệ** | "What" (Cái gì cần làm) | "How" (Làm thế nào thực hiện) |

## 💡 Kết luận

### POUR = Hiến pháp
**POUR** là bộ khung quy định mục tiêu và quyền cơ bản của trang web accessible.

### ARIA = Bộ luật
**ARIA** là công cụ cụ thể giúp developer biến mục tiêu trừu tượng thành hiện thực trong code.

### Cách sử dụng
1. **Dùng POUR** để định hướng và đánh giá thiết kế
2. **Dùng ARIA** (thận trọng) để triển khai

---

## 🎯 Tóm tắt

- **HTML** = Nền tảng, cung cấp ngữ nghĩa mặc định
- **ARIA** = Bổ sung khi HTML không đủ
- **POUR** = Chiến lược (What & Why)
- **ARIA** = Công cụ (How)
- **Nguyên tắc:** HTML trước, ARIA sau

> **💡 Lời khuyên:** Bắt đầu với HTML ngữ nghĩa, chỉ thêm ARIA khi thực sự cần thiết.