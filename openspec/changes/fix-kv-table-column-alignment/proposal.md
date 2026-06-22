## Why

Các bảng 2 cột dạng key-value (`Nội dung | Chi tiết`) trong tài liệu HTML hiện dùng `table-layout: auto`, khiến browser tự tính width khác nhau cho từng bảng — cột label khi 42%, khi 48% — nhìn lệch nhau và khó đọc khi so sánh nhiều section liên tiếp.

## What Changes

- Thêm CSS rule cố định cột đầu tiên của bảng 2-cột dạng key-value thành width nhất quán
- Áp dụng `table-layout: fixed` cho nhóm bảng `Nội dung | Chi tiết` (55 bảng)
- Không thay đổi nội dung, cấu trúc HTML hay bảng nhiều cột khác (3-col, 5-col)

## Capabilities

### New Capabilities
- `kv-table-alignment`: CSS fix căn chỉnh cột label-value nhất quán trên toàn tài liệu

### Modified Capabilities
<!-- không có thay đổi spec-level behavior -->

## Impact

- File duy nhất bị ảnh hưởng: `ACC-noi-dung-nghiep-vu-theo-phase.html`
- Chỉ sửa phần `<style>` trong `<head>` — thêm CSS rule mới
- Không ảnh hưởng nội dung, print layout, tab structure hay các phase khác
