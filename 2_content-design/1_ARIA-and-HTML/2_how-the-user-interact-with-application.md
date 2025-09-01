# Cách người dùng tương tác với ứng dụng

## 🗺️ POUR + ARIA: Bản đồ và Công cụ

**POUR** = Bản đồ định hướng  
**ARIA** = Công cụ giải quyết vấn đề

Hãy phân tích từng nhóm khuyết tật và cách POUR & ARIA hỗ trợ họ.

---

## 👁️ 1. Khuyết tật Thị giác

### Cách tương tác
- **Screen Reader:** Đọc nội dung bằng phím tắt
- **Trình phóng to:** Zoom màn hình
- **Mù màu:** Dựa vào độ tương phản và tín hiệu khác màu

### Vấn đề chính
Screen reader chỉ đọc được **VĂN BẢN** và **THÔNG TIN NGỮ NGHĨA**. `<div>` đẹp không phải là nút!

### Giải pháp POUR + ARIA

#### 🔍 Perceivable (Nhận biết)
| Vấn đề | Giải pháp |
|--------|-----------|
| **Hình ảnh** | `alt="Mô tả hình ảnh"` |
| **Cấu trúc** | `<h1>`, `<nav>`, `<button>` thay vì `<div>` |
| **Màu sắc** | Độ tương phản cao + biểu tượng/văn bản |

#### ⌨️ Operable (Vận hành)
- **Focus:** Mọi thứ có thể focus được
- **Tab order:** Thứ tự logic
- **Landmarks:** `role="navigation"`, `role="main"`

#### 📝 Understandable (Hiểu được)
- **Form:** `<label>` + `aria-describedby`
- **Hướng dẫn:** Rõ ràng, đơn giản

#### 🔧 Robust (Vững chắc) - ARIA
```html
<!-- Thông báo tự động -->
<div role="alert">Tin nhắn mới!</div>

<!-- Menu trạng thái -->
<button aria-expanded="true">Menu</button>

<!-- Nội dung động -->
<div aria-live="polite">Kết quả tìm kiếm...</div>
```

---

## 🦽 2. Khuyết tật Vận động

### Cách tương tác
- **Bàn phím:** Tab, Enter, Space
- **Switch device:** Thiết bị chuyển đổi
- **Điều khiển giọng nói:** Voice control

### Vấn đề chính
- Không điều hướng được bằng bàn phím
- Target (vùng nhấp) quá nhỏ
- Thứ tự tab loạn

### Giải pháp POUR + ARIA

#### ⌨️ Operable (Vận hành) - Then chốt
| Yêu cầu | Giải pháp |
|---------|-----------|
| **Focus rõ ràng** | CSS focus indicator |
| **Tab order** | Logic, theo dòng chảy |
| **Skip links** | "Bỏ qua nội dung" |
| **Target size** | Tối thiểu 44x44px |

#### 🔧 Robust (Vững chắc) - ARIA
```html
<!-- Modal trigger -->
<button aria-haspopup="true">Mở modal</button>

<!-- Trạng thái hiện tại -->
<button aria-pressed="true">Đã chọn</button>
```

---

## 🧠 3. Khuyết tật Nhận thức

### Cách tương tác
- Khó tập trung
- Xử lý thông tin phức tạp
- Đọc hiểu chậm

### Vấn đề chính
- Bố cục rối rắm
- Ngôn ngữ phức tạp
- Chuyển động liên tục
- Hướng dẫn không rõ

### Giải pháp POUR + ARIA

#### 🔍 Perceivable + 📝 Understandable
| Vấn đề | Giải pháp |
|--------|-----------|
| **Ngôn ngữ** | Đơn giản, ngắn gọn |
| **Cấu trúc** | Heading, danh sách rõ ràng |
| **Form** | Hướng dẫn dễ hiểu |
| **Animation** | `prefers-reduced-motion` |

#### 🔧 ARIA hỗ trợ
```html
<!-- Hướng dẫn quan trọng -->
<div aria-live="polite">Bước tiếp theo: Nhập email</div>
```

---

## 👂 4. Khuyết tật Thính giác

### Cách tương tác
- **Đọc mắt:** Chủ yếu
- **Không nghe:** Video, audio

### Vấn đề chính
Nội dung âm thanh không có bản text thay thế.

### Giải pháp POUR + ARIA

#### 🔍 Perceivable (Nhận biết) - Tuyệt đối
| Yêu cầu | Giải pháp |
|---------|-----------|
| **Video** | Phụ đề (Captions) |
| **Audio** | Bản chép (Transcript) |
| **Cảnh báo âm thanh** | Cảnh báo hình ảnh/văn bản |

> **💡 Lưu ý:** ARIA ít dùng cho nhóm này. Trọng tâm là nội dung thay thế bằng văn bản.

---

## 🧪 Cách kiểm tra thực tế

### 3 bước đơn giản

#### 1. ⌨️ Test bàn phím
- Chỉ dùng **Tab, Enter, Space**
- Kiểm tra: Biết đang ở đâu? Vào được mọi nơi?

#### 2. 🔊 Test Screen Reader
- **Mac:** VoiceOver (miễn phí)
- **Windows:** NVDA (miễn phí)
- Kiểm tra: Hiểu được cấu trúc và nội dung?

#### 3. 🔍 Công cụ kiểm tra
- **Lighthouse** (Chrome DevTools)
- **axe extension**
- Quét lỗi cơ bản: thiếu alt text, contrast...

---

## 🎯 Tóm tắt

| Nhóm khuyết tật | POUR chính | ARIA quan trọng |
|-----------------|------------|-----------------|
| **Thị giác** | Perceivable, Operable | `role`, `aria-expanded`, `aria-live` |
| **Vận động** | Operable | `aria-haspopup`, `aria-pressed` |
| **Nhận thức** | Perceivable, Understandable | `aria-live` (hạn chế) |
| **Thính giác** | Perceivable | Ít dùng ARIA |

> **💡 Kết luận:** POUR làm kim chỉ nam, ARIA làm công cụ kỹ thuật. Kết hợp cả hai để xây dựng sản phẩm dành cho tất cả mọi người.