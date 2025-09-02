# Vi phạm nguyên tắc ARIA

## 🚨 Nguyên tắc vàng

> **"No ARIA is better than bad ARIA"**

---

## 1. ❌ Sử dụng ARIA khi đã có HTML có sẵn

**Đây là lỗi phổ biến nhất.** Tại sao phải "chế" lại một nút từ `<div>` khi đã có sẵn thẻ `<button>` làm điều đó một cách hoàn hảo?

### ❌ Code chưa đúng (BAD ARIA)

```html
<!-- Đây là một nút xấu được chế tạo thủ công -->
<div 
  role="button" 
  tabindex="0" 
  onclick="handleClick()" 
  onkeypress="handleClick()"> <!-- Phải tự thêm event cho bàn phím -->
  Tải thêm
</div>
```

**Vấn đề:**
1. Phải tự quản lý `tabindex`
2. Phải tự thêm event `onkeypress` để bắt phím Space/Enter
3. Không có trạng thái `:active` (nhấn giữ) mặc định như button
4. Dài dòng và dễ hỏng

### ✅ Code đúng (Sử dụng HTML thuần)

```html
<!-- Đây là một nút đúng chuẩn -->
<button onclick="handleClick()">Tải thêm</button>
```

**Tự động có:**
- `role="button"`
- Focusable bằng tab
- Có thể kích hoạt bằng cả Space và Enter
- Trạng thái `:active`
- Styles mặc định phù hợp với OS

---

## 2. ❌ Sử dụng aria-hidden trên phần tử có thể focus

**Thảm họa:** Ẩn một phần tử khỏi screen reader nhưng vẫn để nó focus được. Người dùng screen reader sẽ nghe thấy... không có gì khi họ tab tới nó.

### ❌ Code chưa đúng (Rất tệ)

```html
<!-- Một icon "X" để đóng modal -->
<div 
  class="close-button" 
  tabindex="0" 
  aria-hidden="true" <!-- Ẩn khỏi screen reader -->
  onclick="closeModal()">
  ×
</div>
```

**Vấn đề:**
- Người dùng tab tới và thấy focus, nhưng screen reader không đọc gì
- Họ không biết đây là cái gì và để làm gì
- **TỆ HƠN CẢ LÀ KHÔNG DÙNG ARIA**

### ✅ Code đúng

#### Cách 1: Dùng button và aria-label
```html
<button 
  class="close-button" 
  aria-label="Đóng hộp thoại" <!-- Cung cấp nghĩa cho icon -->
  onclick="closeModal()">
  ×
</button>
```

#### Cách 2: Dùng text ẩn về mặt hình ảnh
```html
<button class="close-button" onclick="closeModal()">
  <span aria-hidden="true">×</span> <!-- Chỉ ẩn icon đi với SR -->
  <span class="visually-hidden">Đóng hộp thoại</span> <!-- Nhưng cung cấp text thay thế -->
</button>
```

---

## 3. ❌ Không cập nhật trạng thái ARIA

**ARIA không chỉ để khai báo, mà còn để động.** Nếu trạng thái của widget thay đổi mà thuộc tính ARIA không được cập nhật, nó sẽ cung cấp thông tin sai.

### ❌ Code chưa đúng (Trạng thái tĩnh, không cập nhật)

```html
<button 
  aria-expanded="false" <!-- Luôn luôn là false, ngay cả khi mở -->
  onclick="toggleMenu()"> 
  Menu
</button>
<ul id="menu" style="display: none;">
  <li>Item 1</li>
  <li>Item 2</li>
</ul>

<script>
  function toggleMenu() {
    const menu = document.getElementById('menu');
    // Chỉ thay đổi style, QUÊN cập nhật ARIA!
    if(menu.style.display === 'none') {
      menu.style.display = 'block';
    } else {
      menu.style.display = 'none';
    }
  }
</script>
```

**Vấn đề:**
- Screen reader vẫn báo "đóng" (collapsed) ngay cả khi menu đã mở
- Người dùng nhận được thông tin sai lệch

### ✅ Code đúng (Cập nhật trạng thái động)

```html
<button 
  id="menuButton"
  aria-expanded="false" 
  aria-controls="menu" <!-- Khai báo nó điều khiển cái gì -->
  onclick="toggleMenu()"> 
  Menu
</button>
<ul id="menu" style="display: none;">
  <li>Item 1</li>
  <li>Item 2</li>
</ul>

<script>
  function toggleMenu() {
    const menu = document.getElementById('menu');
    const button = document.getElementById('menuButton');
    
    const isExpanded = menu.style.display === 'block';
    
    // Cập nhật CẢ UI LẪN trạng thái ARIA
    menu.style.display = isExpanded ? 'none' : 'block';
    button.setAttribute('aria-expanded', !isExpanded); // CẬP NHẬT QUAN TRỌNG
  }
</script>
```

---

## 4. ❌ Sử dụng role không phù hợp hoặc gây nhầm lẫn

**Gán một role không đúng với chức năng thực sự của phần tử sẽ đánh lừa người dùng.**

### ❌ Code chưa đúng (Gán role sai)

```html
<!-- Giả sử đây là một tiêu đề, nhưng lại gán role là nút -->
<h3 role="button">Thông tin sản phẩm</h3>
```

**Vấn đề:**
- Screen reader sẽ thông báo "Thông tin sản phẩm, nút"
- Người dùng mong đợi nó có thể được nhấn, nhưng thực tế nó chỉ là một tiêu đề
- Làm hỏng cấu trúc điều hướng của trang (heading navigation)

### ✅ Code đúng (Dùng đúng thẻ ngữ nghĩa)

```html
<!-- Chỉ cần dùng đúng thẻ tiêu đề -->
<h3>Thông tin sản phẩm</h3>
<!-- Screen reader sẽ đọc "Thông tin sản phẩm, heading level 3" -->
```

---

## 5. ❌ Sử dụng aria-label ghi đè lên nội dung có nghĩa

**`aria-label` rất mạnh mẽ, nhưng nó sẽ ghi đè lên tất cả nội dung bên trong phần tử.** Dùng sai sẽ làm mất thông tin.

### ❌ Code chưa đúng (Xung đột nhãn)

```html
<!-- Một nút có cả text và aria-label -->
<button aria-label="Đóng cửa sổ">
  <span class="icon">X</span>
  <span class="text">Kết thúc phiên làm việc</span>
</button>
```

**Vấn đề:**
- `aria-label` "Đóng cửa sổ" sẽ ghi đè hoàn toàn nội dung "Kết thúc phiên làm việc"
- Screen reader chỉ đọc "Đóng cửa sổ, nút", làm mất thông tin quan trọng

### ✅ Code đúng (Nhất quán giữa hình ảnh và văn bản)

#### Cách 1: Nếu chỉ dùng icon, dùng aria-label
```html
<button aria-label="Kết thúc phiên làm việc">
  <span class="icon">X</span>
</button>
```

#### Cách 2: Nếu có cả text, KHÔNG dùng aria-label
```html
<button>
  <span class="icon">X</span>
  <span class="text">Kết thúc phiên làm việc</span>
</button>
<!-- Screen reader sẽ đọc "Kết thúc phiên làm việc, nút" -->
```

---

## 📊 Tóm tắt các vi phạm ARIA

| Vi phạm | Vấn đề | Giải pháp |
|---------|---------|-----------|
| **Dùng ARIA khi có HTML** | Code dài, dễ hỏng, thiếu tính năng | Sử dụng HTML ngữ nghĩa có sẵn |
| **aria-hidden + focusable** | Focus được nhưng SR không đọc | Không ẩn phần tử focusable |
| **Không cập nhật trạng thái** | Thông tin sai lệch | Cập nhật ARIA cùng với UI |
| **Role không phù hợp** | Đánh lừa người dùng | Dùng đúng thẻ HTML |
| **aria-label ghi đè** | Mất thông tin quan trọng | Nhất quán giữa label và nội dung |

---

## 💡 Kết luận

Các ví dụ trên cho thấy việc hiểu rõ bản chất của từng thuộc tính ARIA là **cực kỳ quan trọng**.

### Nguyên tắc thực hành
1. **Luôn ưu tiên** sử dụng HTML ngữ nghĩa trước
2. **Chỉ dùng ARIA** khi thực sự hiểu vấn đề đang giải quyết
3. **Không có giải pháp HTML thuần túy** nào khác
4. **Kiểm tra với screen reader** là bắt buộc sau khi thêm ARIA

### Lời khuyên
> **🎯 Bắt đầu với HTML đúng, sau đó bổ sung ARIA khi cần thiết. Đừng để ARIA trở thành "crutch" cho HTML kém.**

---

## 🔍 Checklist kiểm tra ARIA

### Trước khi sử dụng ARIA
- [ ] Đã thử dùng HTML ngữ nghĩa chưa?
- [ ] Có thực sự cần ARIA không?
- [ ] Hiểu rõ thuộc tính ARIA định dùng?

### Sau khi thêm ARIA
- [ ] Đã test với screen reader chưa?
- [ ] Trạng thái ARIA có được cập nhật động không?
- [ ] Không có xung đột với HTML có sẵn?
- [ ] Role có phù hợp với chức năng thực tế?

