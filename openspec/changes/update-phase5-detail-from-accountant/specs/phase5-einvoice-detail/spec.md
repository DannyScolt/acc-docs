## ADDED Requirements

### Requirement: Chi tiết hóa cụm hóa đơn điện tử của Phase 5
Tài liệu Phase 5 SHALL mô tả chi tiết các phân hệ kết nối nền tảng hóa đơn điện tử, hóa đơn đầu vào, hóa đơn đầu ra, kiểm tra hợp lệ/cảnh báo rủi ro và xử lý hóa đơn sai sót ở mức tương đương Phase 1.

#### Scenario: Bao phủ đầy đủ các phân hệ hóa đơn điện tử
- **WHEN** người dùng đọc các mục 6.2 đến 6.6 trong HTML
- **THEN** tài liệu SHALL mô tả rõ mục tiêu, actor, use case, điều kiện, dữ liệu đầu vào, luồng chính, kết quả, business rules và workflow cho từng phân hệ

### Requirement: Quản lý hóa đơn đầu vào và đầu ra bằng use case có mã
Tài liệu SHALL có danh sách use case có mã rõ ràng cho nghiệp vụ hóa đơn đầu vào và hóa đơn đầu ra của Phase 5.

#### Scenario: Truy xuất use case theo phân hệ hóa đơn
- **WHEN** người dùng xem phân hệ hóa đơn đầu vào hoặc hóa đơn đầu ra
- **THEN** tài liệu SHALL hiển thị danh sách use case tương ứng để kế toán/dev/tester có thể đối chiếu từng nghiệp vụ cụ thể

### Requirement: Kiểm soát hợp lệ hóa đơn và xử lý sai sót bằng business rules có mã
Tài liệu SHALL xác định business rules có mã cho kiểm tra hợp lệ hóa đơn, cảnh báo rủi ro, điều chỉnh, thay thế, hủy và truy vết hồ sơ xử lý hóa đơn sai sót.

#### Scenario: Rà soát xử lý hóa đơn sai sót
- **WHEN** người dùng đọc phần kiểm tra hợp lệ hoặc xử lý hóa đơn sai sót
- **THEN** tài liệu SHALL mô tả điều kiện cảnh báo, trạng thái xử lý và các quy tắc bắt buộc để ngăn sửa trực tiếp hóa đơn gốc đã phát hành

### Requirement: Workflow hóa đơn điện tử có thể truy vết end-to-end
Tài liệu SHALL mô tả workflow từ kết nối nền tảng hóa đơn, đồng bộ hóa đơn, kiểm tra hợp lệ, liên kết chứng từ kế toán cho tới trạng thái sẵn sàng hạch toán/kê khai.

#### Scenario: Theo dõi vòng đời một hóa đơn điện tử
- **WHEN** người dùng xem workflow của một hóa đơn đầu vào hoặc đầu ra
- **THEN** tài liệu SHALL chỉ rõ các trạng thái tối thiểu như mới nhận, chờ kiểm tra, hợp lệ/sai lệch, đã liên kết chứng từ, đã hạch toán hoặc trạng thái tương đương phù hợp với phân hệ
