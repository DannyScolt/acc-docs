## ADDED Requirements

### Requirement: Chi tiết hóa chu trình Procure-to-Pay của Phase 2
Tài liệu Phase 2 SHALL mô tả chi tiết chu trình mua hàng và công nợ phải trả ở mức tương đương Phase 1, bao gồm actor, điều kiện, dữ liệu đầu vào, luồng chính, kết quả, workflow và business rules.

#### Scenario: Bao phủ đầy đủ các phân hệ procurement và AP
- **WHEN** người dùng đọc Phase 2 trong HTML
- **THEN** tài liệu SHALL mô tả chi tiết các mục 3.2 đến 3.10, bao gồm yêu cầu mua, đơn mua, hợp đồng mua, mua hàng hóa/dịch vụ, hóa đơn mua vào, công nợ phải trả, thanh toán nhà cung cấp, trả lại hàng mua, giảm giá hàng mua và đối chiếu công nợ

### Requirement: Danh sách use case cho mua hàng và AP
Tài liệu SHALL có danh sách use case có mã rõ ràng cho các nghiệp vụ mua hàng và công nợ phải trả của Phase 2.

#### Scenario: Truy xuất use case theo module
- **WHEN** người đọc xem từng module Phase 2 liên quan đến mua hàng và AP
- **THEN** tài liệu SHALL hiển thị danh sách use case tương ứng với actor và tên nghiệp vụ để kế toán/dev/tester có thể đối chiếu

### Requirement: Luồng chính và workflow cho chứng từ mua hàng
Tài liệu SHALL mô tả workflow và luồng chính cho các chứng từ mua hàng, hóa đơn đầu vào và thanh toán nhà cung cấp.

#### Scenario: Mô tả trạng thái chứng từ mua
- **WHEN** người dùng xem các nghiệp vụ mua hàng và thanh toán
- **THEN** tài liệu SHALL chỉ rõ các trạng thái tối thiểu như nháp, chờ duyệt, đã duyệt, hoàn thành, hủy hoặc trạng thái tương đương phù hợp với từng chứng từ

### Requirement: Business rules cho công nợ phải trả và thanh toán nhà cung cấp
Tài liệu SHALL xác định business rules có mã cho công nợ phải trả, thanh toán nhà cung cấp, trả lại hàng mua và bù trừ công nợ.

#### Scenario: Kiểm soát thanh toán và đối chiếu công nợ
- **WHEN** người dùng đọc phần công nợ phải trả và thanh toán nhà cung cấp
- **THEN** tài liệu SHALL mô tả các quy tắc kiểm soát như thanh toán một phần, thanh toán theo hóa đơn, giới hạn ghi sổ, xử lý trả lại/giảm giá và quy tắc bù trừ/đối chiếu công nợ
