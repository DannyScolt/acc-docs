## ADDED Requirements

### Requirement: Chi tiết hóa chính sách giá và hóa đơn bán ra của Phase 3
Tài liệu Phase 3 SHALL mô tả chi tiết chính sách giá, bảng giá, chiết khấu và hóa đơn bán ra ở mức tương đương Phase 1, phản ánh đúng tài liệu nguồn kế toán.

#### Scenario: Bao phủ đầy đủ các module giá và hóa đơn
- **WHEN** người dùng đọc phần Phase 3 trong HTML
- **THEN** tài liệu SHALL mô tả đầy đủ các mục 4.5 và 4.7 với business rules, use case, actor, luồng chính, output, trạng thái và liên kết dữ liệu liên quan

### Requirement: Chính sách giá phải mô tả thứ tự ưu tiên và kiểm soát giá sàn
Tài liệu SHALL mô tả module chính sách giá với thứ tự ưu tiên áp dụng giá, quy tắc hiệu lực bảng giá và cơ chế kiểm soát bán dưới giá tối thiểu.

#### Scenario: Truy vết logic áp dụng giá bán
- **WHEN** người đọc xem mục chính sách giá, bảng giá và chiết khấu
- **THEN** tài liệu SHALL chỉ rõ các use case khai báo bảng giá, giá theo khách hàng/nhóm khách hàng, chính sách chiết khấu, giá sàn, xác định giá khi lập chứng từ, duyệt bán dưới giá tối thiểu, điều chỉnh bảng giá, tra cứu lịch sử giá và ngừng hiệu lực cùng các rule `BR-GIA-*`

### Requirement: Hóa đơn bán ra phải mô tả đầy đủ vòng đời phát hành và điều chỉnh
Tài liệu SHALL mô tả module hóa đơn bán ra với toàn bộ vòng đời từ lập hóa đơn đến phát hành, gửi khách hàng, điều chỉnh, thay thế, hủy và cập nhật kê khai thuế GTGT.

#### Scenario: Truy vết vòng đời hóa đơn bán ra
- **WHEN** người dùng đọc mục hóa đơn bán ra
- **THEN** tài liệu SHALL mô tả các nghiệp vụ lập hóa đơn, lập từ chứng từ bán hàng, phát hành hóa đơn điện tử, gửi hóa đơn, điều chỉnh, thay thế, hủy, tra cứu, cập nhật kê khai thuế, đối chiếu hóa đơn-doanh thu và in/xuất PDF cùng các rule `BR-HDB-*`

### Requirement: Hóa đơn phải liên kết được với doanh thu và thuế đầu ra
Tài liệu SHALL mô tả rõ mối liên hệ giữa hóa đơn bán ra, chứng từ bán hàng, thuế GTGT đầu ra, công nợ phải thu và sổ cái.

#### Scenario: Đối chiếu hóa đơn với doanh thu
- **WHEN** kế toán hoặc tester đối chiếu dữ liệu hóa đơn
- **THEN** tài liệu SHALL nêu rõ rằng hóa đơn được lập từ giao dịch bán hợp lệ, tổng giá trị hóa đơn không vượt giá trị chứng từ bán và dữ liệu hóa đơn phát hành phải được cập nhật vào kê khai thuế GTGT đầu ra

### Requirement: Báo cáo và trạng thái hóa đơn phải có thể kiểm chứng
Tài liệu SHALL mô tả trạng thái hóa đơn và các đầu ra báo cáo liên quan theo cách có thể dùng làm cơ sở kiểm thử nghiệp vụ.

#### Scenario: Kiểm tra trạng thái và báo cáo hóa đơn
- **WHEN** người đọc xem phần hóa đơn bán ra
- **THEN** tài liệu SHALL chỉ rõ luồng trạng thái hóa đơn, các báo cáo hóa đơn bán ra và các điều kiện kiểm soát như không sửa trực tiếp hóa đơn đã phát hành hoặc đã kê khai thuế