## Context

Tài liệu `ACC-noi-dung-nghiep-vu-theo-phase.html` có 55 bảng dạng `Nội dung | Chi tiết` (key-value 2 cột). Hiện tại tất cả dùng `table-layout: auto` — browser tính width từng bảng độc lập dựa trên nội dung → cột label dao động 42–48% → nhìn lệch khi đọc nhiều section liên tiếp.

Ngoài ra còn có: 30 bảng `Mã | Quy tắc`, 27 bảng `Bước | Mô tả`, 70 bảng 3-cột, 5 bảng định khoản 5-cột. Chỉ nhóm `Nội dung | Chi tiết` là cần fix vì đây là nhóm xuất hiện dày nhất trong Phase 1–6.

## Goals / Non-Goals

**Goals:**
- Cột label (`Nội dung`) cố định width nhất quán trên tất cả 55 bảng key-value
- Sửa CSS 1 chỗ duy nhất, không sửa HTML từng bảng
- Không ảnh hưởng bảng nhiều cột khác

**Non-Goals:**
- Không fix bảng `Mã | Quy tắc`, `Bước | Mô tả` hay các bảng khác (chưa được yêu cầu)
- Không thay đổi màu sắc, font, padding hay bất kỳ style nào khác

## Decisions

**Dùng CSS attribute selector thay vì thêm class vào HTML**

Thay vì thêm `class="kv-table"` vào 55 thẻ `<table>` trong HTML, dùng selector CSS nhắm vào bảng có `<th>` đầu tiên là "Nội dung":

```css
/* Không làm được với CSS thuần — CSS không thể select by text content */
```

Vì CSS không thể select element theo text content, cần một trong hai cách:

| Cách | Mô tả | Chọn |
|------|-------|------|
| **A. Thêm class `kv-table` vào HTML** | `replace_all` đổi `<tr><th>Nội dung</th><th>Chi tiết</th>` thành có class trên `<table>` | ✅ Chọn |
| **B. CSS `:has()` selector** | `table:has(th:first-child)` — không đủ chính xác, sẽ nhắm nhầm bảng khác | ❌ |

→ **Quyết định: Cách A** — dùng `replace_all` đổi pattern `<table>\n      <tr><th>Nội dung</th><th>Chi tiết</th></tr>` thành `<table class="kv-table">\n      <tr><th>Nội dung</th><th>Chi tiết</th></tr>`, sau đó thêm CSS:

```css
table.kv-table {
  table-layout: fixed;
}
table.kv-table td:first-child,
table.kv-table th:first-child {
  width: 22%;
}
```

Width 22% — đủ cho các label dài nhất ("Ảnh hưởng kế toán", "Actor & Quyền") mà không chiếm quá nhiều không gian.

## Risks / Trade-offs

- **Print layout**: `table-layout: fixed` với width 22% trên A4 (~170mm nội dung) → cột label ~37mm, cột nội dung ~133mm — hợp lý, không bị cắt chữ.
- **Label dài**: "Ảnh hưởng kế toán / sổ cái / báo cáo" (~40 ký tự) sẽ wrap trong 22% — nhưng `vertical-align: top` đã có sẵn nên không vấn đề.
- **replace_all risk**: Pattern `<table>\n      <tr><th>Nội dung</th><th>Chi tiết</th></tr>` đủ unique để không match nhầm bảng khác.
