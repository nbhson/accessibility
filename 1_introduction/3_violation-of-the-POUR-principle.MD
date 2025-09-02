# Vi phạm nguyên tắc POUR

## 🎯 Tổng quan

Chúng ta sẽ đi qua từng chữ cái trong **POUR** với các ví dụ phổ biến và cách khắc phục.

---

## 🔍 P - Perceivable (Có thể nhận biết)

**Yêu cầu:** Thông tin và thành phần giao diện phải được trình bày theo cách mà người dùng có thể nhận biết được.

### Ví dụ 1: Hình ảnh thiếu alt text

**Vi phạm:** Người dùng screen reader không thể biết hình ảnh chứa gì.

#### ❌ Code chưa đúng
```html
<img src="chart-sales-q3.png"> <!-- Thiếu alt text -->
```

#### ✅ Code đúng
```html
<img src="chart-sales-q3.png" alt="Biểu đồ thể hiện doanh số quý 3 tăng 20% so với quý 2">
```

### Ví dụ 2: Video không có phụ đề

**Vi phạm:** Người dùng khiếm thính không thể tiếp cận thông tin trong audio.

#### ❌ Code chưa đúng
```html
<video controls>
  <source src="huong-dan.mp4" type="video/mp4">
  <!-- Không có track phụ đề -->
</video>
```

#### ✅ Code đúng
```html
<video controls>
  <source src="huong-dan.mp4" type="video/mp4">
  <track src="subtitles-vi.vtt" kind="subtitles" srclang="vi" label="Tiếng Việt">
  <!-- Đường dẫn đến file phụ đề -->
</video>
```

---

## ⌨️ O - Operable (Có thể vận hành)

**Yêu cầu:** Các thành phần giao diện và điều hướng phải có thể vận hành được.

### Ví dụ 1: Nút không thể focus bằng bàn phím

**Vi phạm:** Người dùng chỉ dùng bàn phím không thể chọn nút để kích hoạt.

#### ❌ Code chưa đúng (Dùng `<div>` giả làm nút)
```html
<div class="btn" onclick="submitForm()">Gửi</div>
<!-- Div không focusable được, không thể kích hoạt bằng Space/Enter -->
```

#### ✅ Code đúng (Dùng thẻ `<button>`)
```html
<button class="btn" onclick="submitForm()">Gửi</button>
<!-- Button focusable và kích hoạt được bằng Space/Enter -->
```

### Ví dụ 2: Thứ tự tab không hợp lý

**Vi phạm:** Thứ tự điều hướng bằng Tab nhảy loạn, không theo trật tự trực quan.

#### ❌ Code chưa đúng (Sử dụng tabindex sai cách)
```html
<input type="text" tabindex="3">
<input type="text" tabindex="1"> <!-- Tab tới đây đầu tiên -->
<input type="text" tabindex="2"> <!-- Rồi tới đây -->
<button tabindex="99">Gửi</button> <!-- Cuối cùng mới tới đây -->
```

#### ✅ Code đúng (Để thứ tự tab tự nhiên theo DOM)
```html
<input type="text"> <!-- Tab thứ 1 -->
<input type="text"> <!-- Tab thứ 2 -->
<input type="text"> <!-- Tab thứ 3 -->
<button>Gửi</button> <!-- Tab thứ 4 -->
<!-- Thứ tự tab sẽ đúng với thứ tự nhìn thấy trên màn hình -->
```

---

## 📝 U - Understandable (Dễ hiểu)

**Yêu cầu:** Thông tin và cách vận hành giao diện phải dễ hiểu.

### Ví dụ 1: Thông báo lỗi không rõ ràng

**Vi phạm:** Người dùng không hiểu lỗi là gì và cách sửa nó.

#### ❌ Code chưa đúng
```html
<input type="email" id="email">
<!-- Khi lỗi, chỉ đổi màu viền thành đỏ, không có text mô tả -->
```

#### ✅ Code đúng
```html
<label for="email">Email:</label>
<input type="email" id="email" aria-describedby="email-error">
<span id="email-error" style="color: red; display: none;">
    Vui lòng nhập một địa chỉ email hợp lệ.
</span>
<!-- Khi lỗi, hiển thị dòng thông báo và dùng aria-describedby để liên kết -->
```

### Ví dụ 2: Hướng dẫn bằng màu sắc đơn thuần

**Vi phạm:** Người dùng mù màu không phân biệt được.

#### ❌ Code chưa đúng
```html
<p>Trường bắt buộc phải được <span style="color: red;">tô màu đỏ</span>.</p>
<input type="text" style="border-color: red;"> <!-- Chỉ dùng màu -->
```

#### ✅ Code đúng (Kết hợp hình ảnh và văn bản)
```html
<p>Trường bắt buộc phải được đánh dấu.</p>
<input type="text" aria-required="true" style="border-color: red;">
<span class="required-asterisk" aria-hidden="true">*</span>
<!-- Dùng ký hiệu * kết hợp với màu sắc và thuộc tính ARIA -->
```

---

## 🔧 R - Robust (Vững chắc)

**Yêu cầu:** Nội dung phải đủ mạnh mẽ để có thể được hiểu thống nhất bởi nhiều loại công nghệ hỗ trợ.

### Ví dụ 1: Form không có label được liên kết chính thức

**Vi phạm:** Screen reader không biết ô input này dùng để làm gì.

#### ❌ Code chưa đúng (Label ảo - placeholder thay label)
```html
<input type="text" placeholder="Nhập tên của bạn">
<!-- Placeholder biến mất khi nhập, không phải là label thật sự -->
```

#### ✅ Code đúng (Label được liên kết rõ ràng)
```html
<label for="name">Nhập tên của bạn:</label>
<input type="text" id="name">
<!-- Screen reader sẽ đọc to label khi input được focus -->
```

### Ví dụ 2: Custom widget không có thông tin ARIA

**Vi phạm:** Một nút "giả" được tạo từ `<div>` không cung cấp bất kỳ thông tin nào cho screen reader.

#### ❌ Code chưa đúng (Widget "câm")
```html
<div class="custom-switch" onclick="toggleSwitch()">
  <div class="switch-handle"></div>
</div>
<!-- Screen reader chỉ đọc được là "div", không biết đây là công tắc hay trạng thái của nó -->
```

#### ✅ Code đúng (Bổ sung vai trò và trạng thái bằng ARIA)
```html
<div class="custom-switch" role="switch" aria-checked="false" tabindex="0" onclick="toggleSwitch()">
  <div class="switch-handle"></div>
</div>
```

**Giải thích ARIA:**
- `role="switch"`: Báo cho SR biết đây là một công tắc
- `aria-checked="false"`: Báo cho SR biết trạng thái hiện tại là tắt
- `tabindex="0"`: Cho phép phần tử này focus được bằng tab

---

## 📊 Tóm tắt các vi phạm thường gặp

| Nguyên tắc | Vi phạm phổ biến | Giải pháp |
|------------|------------------|-----------|
| **Perceivable** | Thiếu alt text, không có phụ đề | Thêm alt text, track phụ đề |
| **Operable** | Không focus được, tab order sai | Dùng đúng HTML, để tab tự nhiên |
| **Understandable** | Lỗi không rõ, chỉ dùng màu | Thông báo rõ ràng, kết hợp nhiều tín hiệu |
| **Robust** | Thiếu label, widget "câm" | Label chính thức, ARIA roles |

---

## 💡 Kết luận

Các ví dụ trên cho thấy việc tuân thủ **POUR** không quá phức tạp:

### Nguyên tắc chính
1. **Sử dụng đúng thẻ HTML** cho đúng mục đích
2. **Cung cấp thông tin thay thế** cho nội dung đa phương tiện
3. **Kiểm tra thường xuyên** với công cụ như Lighthouse

### Lợi ích
- **Dễ dàng phát hiện** lỗi cơ bản
- **Cải thiện trải nghiệm** cho tất cả người dùng
- **Code sạch** và maintainable

---

## 🔍 Công cụ kiểm tra

### Lighthouse (Chrome DevTools)
- Quét lỗi accessibility cơ bản
- Điểm số POUR
- Gợi ý cải thiện

### axe DevTools
- Phát hiện vi phạm WCAG
- Báo cáo chi tiết
- Hướng dẫn sửa lỗi

> **🎯 Lời khuyên:** Bắt đầu với HTML ngữ nghĩa đúng, sau đó bổ sung ARIA khi cần thiết.