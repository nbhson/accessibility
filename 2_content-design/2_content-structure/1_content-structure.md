# Cấu trúc nội dung

## 🎯 Tổng quan

**Cấu trúc nội dung** là một trong những khía cạnh quan trọng nhất của khả năng tiếp cận kỹ thuật số. Khi bạn xây dựng website hoặc app sử dụng các phần tử cấu trúc thay vì chỉ dựa vào CSS, bạn cung cấp ngữ cảnh quan trọng cho người dùng công nghệ hỗ trợ (AT) như trình đọc màn hình.

### Lợi ích của cấu trúc ngữ nghĩa
- **Đường viền nội dung:** Làm outline cho trang
- **Điểm neo:** Cho phép điều hướng dễ dàng
- **Ý nghĩa tự nhiên:** Truyền tải thông tin cho AT
- **Giảm ARIA:** Ít cần bổ sung thuộc tính ARIA

> **💡 Lưu ý:** Module này tập trung vào các phần tử cấu trúc quan trọng nhất. Xem thêm khóa học Learn HTML để hiểu chi tiết về HTML và cấu trúc ngữ nghĩa.

---

## 🏗️ Landmarks (Điểm mốc)

### Mục đích
Landmarks giúp người dùng AT hiểu bố cục tổng thể của trang và điều hướng đến các vùng nội dung lớn.

### So sánh HTML vs ARIA

| HTML landmark | ARIA landmark role | Mô tả |
|---------------|-------------------|-------|
| `<header>` | `banner` | Đầu trang, logo, navigation chính |
| `<aside>` | `complementary` | Nội dung bổ sung, sidebar |
| `<footer>` | `contentinfo` | Cuối trang, thông tin liên hệ |
| `<nav>` | `navigation` | Menu điều hướng |
| `<main>` | `main` | Nội dung chính của trang |
| `<form>` | `form` | Biểu mẫu (cần name attribute) |
| `<section>` | `region` | Phần nội dung (cần name attribute) |

> **⚠️ Lưu ý:** `<form>` và `<section>` cần thuộc tính `name` để trở nên accessible.

### Ví dụ cấu trúc tốt

#### ❌ Không nên
```html
<div>
    <div>...</div>
</div>
<div>
    <p>Stamp collecting, also known as philately...</p>
</div>
<div>
    <p>© 2022 - Stamps R Awesome</p>
</div>
```

#### ✅ Nên làm
```html
<header>
    <nav>...</nav>
</header>
<main>
    <section aria-label="Introduction to stamp collecting">
        <p>Stamp collecting, also known as philately...</p>
    </section>
</main>
<footer>
    <p>© 2022 - Stamps R Awesome</p>
</footer>
```

---

## 📝 Headings (Tiêu đề)

### Nguyên tắc cơ bản
- **6 cấp độ:** `<h1>` đến `<h6>`
- **Thứ tự quan trọng:** Không bỏ qua cấp độ
- **H1:** Thông tin quan trọng nhất của trang
- **H6:** Thông tin ít quan trọng nhất

### Tại sao thứ tự quan trọng?
AT users sử dụng headings như cách chính để điều hướng nội dung. Thứ tự sai sẽ gây nhầm lẫn.

### Lời khuyên về styling
**Tách biệt CSS khỏi cấp độ heading** để có thể:
- Tùy chỉnh style linh hoạt
- Duy trì thứ tự cấp độ đúng
- Không dùng CSS để "giả" headings

### Ví dụ cấu trúc heading

#### ❌ Không nên
```html
<div>
    <h3>Stamps</h3>
    <p>Stamp collecting, also known as philately...</p>
</div>
<div>
    <h3>How do I start a stamp collection?</h3>
    <h2>Equipment you will need</h2>
    <h4>...</h4>
    <h2>How to acquire stamps</h2>
    <h4>...</h4>
</div>
```

**Vấn đề:** Bỏ qua H1, thứ tự H2 → H3 → H4 không logic

#### ✅ Nên làm
```html
<header>
    <h1>Stamp collecting</h1>
</header>
<main>
    <section aria-label="Introduction to stamp collecting">
        <h2>What is stamp collecting?</h2>
        <p>Stamp collecting, also known as philately...</p>
    </section>
    
    <section aria-label="Start a stamp collection">
        <h2>How do I start a stamp collection?</h2>
        <h3>Required equipment</h3>
        <p>...</p>
        <h3>How to acquire stamps</h3>
        <p>...</p>
        <h3>Organizations you can join</h3>
        <p>...</p>
    </section>
</main>
```

**Ưu điểm:** Thứ tự logic H1 → H2 → H3, cấu trúc rõ ràng

---

## 📋 Lists (Danh sách)

### Ba loại danh sách HTML
1. **Ordered `<ol>`** - Danh sách có thứ tự
2. **Unordered `<ul>`** - Danh sách không có thứ tự  
3. **Description `<dl>`** - Danh sách mô tả

### Lợi ích cho accessibility
- **AT users:** Biết tên danh sách và số lượng item
- **Điều hướng:** "Item 1 of 5, Item 2 of 5..."
- **Cognitive disorders:** Nội dung có điểm, dễ hiểu
- **Reading disabilities:** Whitespace nhiều, nội dung ngắn gọn

### Ví dụ danh sách

#### ❌ Không nên
```html
<div>
    <p>How do I start a stamp collection?</p>
    <p>Equipment you will need</p>
    <div>
        <p>Small tongs with rounded tips</p>
        <p>Stamp hinges</p>
        <p>Stockbook or album</p>
        <p>Magnifying glass</p>
        <p>Stamps</p>
    </div>
</div>
```

#### ✅ Nên làm
```html
<div>
    <h1>How do I start a stamp collection?</h1>
    <h2>Equipment you will need</h2>
    <ol>
        <li>Small tongs with rounded tips</li>
        <li>Stamp hinges</li>
        <li>Stockbook or album</li>
        <li>Magnifying glass</li>
        <li>Stamps</li>
    </ol>
</div>
```

---

## 📊 Tables (Bảng)

### Hai loại bảng chính
1. **Layout tables** - Chỉ để bố cục
2. **Data tables** - Chứa dữ liệu có cấu trúc

---

## 🎨 Layout Tables

### Mục đích
Tạo bố cục trực quan, thường dùng trong email, newsletter, quảng cáo.

### Quy tắc quan trọng
- **Không dùng** `<th>`, `<caption>` (truyền tải mối quan hệ)
- **Ẩn khỏi AT** với `role="presentation"` hoặc `aria-hidden="true"`

### Ví dụ layout table

#### ❌ Không nên
```html
<table>
    <caption>My stamp collection</caption>
    <tr>
        <th>[Stamp Image 1]</th>
        <th>[Stamp Image 2]</th>
        <th>[Stamp Image 3]</th>
    </tr>
</table>
```

#### ✅ Nên làm
```html
<table role="presentation">
    <tr>
        <td>[Stamp Image 1]</td>
        <td>[Stamp Image 2]</td>
        <td>[Stamp Image 3]</td>
    </tr>
</table>
```

---

## 📈 Data Tables

### Mục đích
Tổ chức dữ liệu có cấu trúc, phải accessible cho AT users.

### Cấu trúc cơ bản
- **Header cells:** `<th>` để đánh dấu cột/dòng
- **Data cells:** `<td>` để chứa dữ liệu
- **Caption:** Mô tả bảng (không bắt buộc nhưng khuyến khích)

### Cấu trúc phức tạp
Với bảng phức tạp, có thể cần:
- `<rowgroup>`, `<colgroup>`
- `<caption>`
- Thuộc tính `scope`

### Ví dụ data table

#### ❌ Không nên
```html
<table>
    <tr>
        <td>Animal</td>
        <td>Year</td>
        <td>Condition</td>
    </tr>
    <tr>
        <td>Bird</td>
        <td>1947</td>
        <td>Fair</td>
    </tr>
    <tr>
        <td>Lion</td>
        <td>1982</td>
        <td>Good</td>
    </tr>
</table>
```

**Vấn đề:** Không có header cells, AT không hiểu cấu trúc

#### ✅ Nên làm
```html
<table>
    <caption>My stamp collection</caption>
    <tr>
        <th>Animal</th>
        <th>Year</th>
        <th>Condition</th>
    </tr>
    <tr>
        <td>Bird</td>
        <td>1947</td>
        <td>Fair</td>
    </tr>
    <tr>
        <td>Lion</td>
        <td>1982</td>
        <td>Good</td>
    </tr>
</table>
```

**Ưu điểm:** Có header cells, AT hiểu được mối quan hệ dữ liệu

---

## 💡 Tóm tắt

### Nguyên tắc chính
1. **Sử dụng HTML ngữ nghĩa** thay vì chỉ CSS
2. **Landmarks** để tạo cấu trúc trang
3. **Headings** theo thứ tự logic
4. **Lists** để nhóm thông tin liên quan
5. **Tables** với cấu trúc đúng mục đích

### Lợi ích
- **AT users:** Hiểu cấu trúc và điều hướng dễ dàng
- **Developers:** Code sạch, maintainable
- **SEO:** Cải thiện khả năng tìm kiếm
- **Performance:** Ít cần ARIA bổ sung

### Checklist kiểm tra
- [ ] Có landmarks rõ ràng (header, main, nav, footer)?
- [ ] Headings theo thứ tự logic (H1 → H2 → H3)?
- [ ] Lists sử dụng đúng thẻ HTML?
- [ ] Tables có cấu trúc phù hợp với mục đích?
- [ ] Không dùng CSS để "giả" cấu trúc?

> **🎯 Lời khuyên:** Bắt đầu với HTML ngữ nghĩa đúng, sau đó bổ sung ARIA khi cần thiết. Cấu trúc tốt = Accessibility tốt!

---

## 📚 Tài liệu tham khảo

- **Page Structure** [Page Structure](https://www.w3.org/WAI/tutorials/page-structure/)
- **Semantics in HTML:** [Semantics in HTML](https://developer.mozilla.org/en-US/docs/Glossary/Semantics#semantics_in_html)
- **100 elements available:** [100 elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements)
- **ARIA: landmark role:** [ARIA: landmark role](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Reference/Roles/landmark_role#best_practices)


