## ADDED Requirements

### Requirement: Bảng key-value 2 cột phải có cột label cố định width nhất quán
Tất cả bảng dạng `Nội dung | Chi tiết` trong tài liệu SHALL hiển thị cột label với width cố định 22% trên mọi bảng, không phụ thuộc vào độ dài nội dung từng bảng.

#### Scenario: Cột label đồng đều trên nhiều bảng liên tiếp
- **WHEN** người dùng đọc nhiều sub-section liên tiếp trong cùng một Phase
- **THEN** cột "Nội dung" của tất cả bảng SHALL có width bằng nhau, tạo cảm giác thẳng hàng khi cuộn trang

#### Scenario: Nội dung label dài không vỡ layout
- **WHEN** label cell chứa text dài như "Ảnh hưởng kế toán / sổ cái / báo cáo"
- **THEN** text SHALL wrap trong cột 22% mà không làm ảnh hưởng đến cột Chi tiết bên cạnh

#### Scenario: Bảng nhiều cột không bị ảnh hưởng
- **WHEN** người dùng xem bảng 3-cột (STT/Chức năng/Mô tả) hoặc 5-cột (bảng định khoản)
- **THEN** các bảng đó SHALL KHÔNG bị thay đổi width hay layout
