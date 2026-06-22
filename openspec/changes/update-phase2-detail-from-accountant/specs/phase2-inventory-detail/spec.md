## ADDED Requirements

### Requirement: Chi tiết hóa nghiệp vụ kho trong Phase 2
Tài liệu Phase 2 SHALL mô tả chi tiết nghiệp vụ nhận hàng, nhập kho, chuyển kho, kiểm kê và tồn kho ở mức tương đương Phase 1.

#### Scenario: Bao phủ đầy đủ các phân hệ kho của Phase 2
- **WHEN** người dùng đọc các mục 3.5 và 3.11.1 đến 3.11.4
- **THEN** tài liệu SHALL mô tả chi tiết nhận hàng/nhập kho, chuyển kho, kiểm kê & điều chỉnh tồn kho, thẻ kho & tồn kho với actor, điều kiện, input, luồng chính, kết quả và business rules

### Requirement: Luồng nhận hàng và nhập kho có thể truy vết
Tài liệu SHALL mô tả rõ mối liên hệ giữa đơn mua, nhận hàng và nhập kho.

#### Scenario: Truy vết từ mua hàng sang kho
- **WHEN** người dùng xem nghiệp vụ nhận hàng hoặc nhập kho
- **THEN** tài liệu SHALL chỉ rõ chứng từ nguồn, điều kiện nhận một phần/đủ, ảnh hưởng tồn kho và liên kết với mua hàng hoặc hóa đơn nếu có

### Requirement: Business rules cho kiểm kê và điều chỉnh tồn kho
Tài liệu SHALL xác định các quy tắc có mã cho kiểm kê, điều chỉnh chênh lệch và báo cáo tồn kho.

#### Scenario: Kiểm soát tồn kho và điều chỉnh
- **WHEN** người dùng đọc phần kiểm kê và điều chỉnh tồn kho
- **THEN** tài liệu SHALL mô tả điều kiện điều chỉnh, quy tắc không âm kho (nếu áp dụng), xử lý chênh lệch và ảnh hưởng tới báo cáo tồn kho
