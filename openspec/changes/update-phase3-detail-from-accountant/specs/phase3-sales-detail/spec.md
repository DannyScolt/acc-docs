## ADDED Requirements

### Requirement: Chi tiết hóa cụm chứng từ bán hàng đầu chu trình của Phase 3
Tài liệu Phase 3 SHALL mô tả chi tiết các nghiệp vụ đầu chu trình bán hàng ở mức tương đương Phase 1, bao gồm báo giá, đơn đặt hàng bán, hợp đồng bán và chứng từ bán hàng hóa/dịch vụ.

#### Scenario: Bao phủ đầy đủ các module đầu chu trình bán hàng
- **WHEN** người dùng đọc phần Phase 3 trong HTML
- **THEN** tài liệu SHALL mô tả đầy đủ các mục 4.2, 4.3, 4.4 và 4.6 với actor, use case, luồng chính, business rule, kết quả đầu ra và trạng thái liên quan

### Requirement: Báo giá phải có use case và business rules có thể truy vết
Tài liệu SHALL mô tả module báo giá với danh sách use case và business rules có mã theo tài liệu nguồn kế toán.

#### Scenario: Truy vết nghiệp vụ báo giá
- **WHEN** người đọc xem mục báo giá
- **THEN** tài liệu SHALL thể hiện tối thiểu các nghiệp vụ lập báo giá, áp dụng bảng giá, theo dõi trạng thái, chuyển đơn hàng, chuyển chứng từ bán hàng, in/gửi báo giá và hủy báo giá cùng các rule `BR-BG-*`

### Requirement: Đơn đặt hàng bán phải mô tả luồng giao hàng và hoàn thành
Tài liệu SHALL mô tả module đơn đặt hàng bán với các quy tắc kiểm soát duyệt đơn, giao nhiều đợt, theo dõi số lượng giao và trạng thái hoàn thành.

#### Scenario: Truy xuất workflow đơn đặt hàng bán
- **WHEN** người đọc xem mục đơn đặt hàng bán
- **THEN** tài liệu SHALL chỉ rõ ít nhất các nghiệp vụ lập đơn, lập từ báo giá, duyệt, kiểm tra tồn khả dụng, theo dõi số lượng đã giao/chưa giao, chuyển chứng từ bán hàng, hủy đơn và luồng trạng thái đơn hàng cùng các rule `BR-DH-*`

### Requirement: Hợp đồng bán phải mô tả kiểm soát thực hiện và thanh lý
Tài liệu SHALL mô tả module hợp đồng bán với các nghiệp vụ điều khoản thanh toán, điều khoản giao hàng, theo dõi thực hiện, cảnh báo đến hạn, thanh lý và dừng thực hiện.

#### Scenario: Theo dõi vòng đời hợp đồng bán
- **WHEN** người đọc xem mục hợp đồng bán
- **THEN** tài liệu SHALL thể hiện luồng trạng thái hợp đồng, liên kết với báo giá/đơn hàng/chứng từ bán/hóa đơn/công nợ và các rule `BR-HD-*`

### Requirement: Chứng từ bán hàng hóa và dịch vụ phải gắn với doanh thu, thuế và công nợ
Tài liệu SHALL mô tả module bán hàng hóa/dịch vụ như trung tâm ghi nhận doanh thu của Phase 3, bao gồm bán thu tiền ngay, bán chịu, duyệt chứng từ, ghi sổ và hoàn thành chứng từ.

#### Scenario: Truy vết từ chứng từ bán sang doanh thu và công nợ
- **WHEN** người dùng đọc mục bán hàng hóa/dịch vụ
- **THEN** tài liệu SHALL mô tả các use case lập chứng từ, kiểm tra giá và chiết khấu, duyệt bán, thu tiền ngay, bán chịu, lập hóa đơn, ghi sổ, hủy, tra cứu và đóng chứng từ cùng các rule `BR-BH-*`

### Requirement: Các module đầu chu trình bán hàng phải chỉ ra liên kết dữ liệu liên phân hệ
Tài liệu SHALL mô tả rõ liên kết dữ liệu giữa báo giá, đơn bán, hợp đồng và chứng từ bán hàng với các phân hệ kho, hóa đơn, công nợ và thu tiền.

#### Scenario: Truy vết xuyên module của chu trình bán hàng
- **WHEN** kế toán, BA hoặc tester đối chiếu một chứng từ đầu chu trình bán hàng
- **THEN** tài liệu SHALL chỉ rõ upstream/downstream flow giữa báo giá, đơn hàng, hợp đồng, bán hàng, hóa đơn, xuất kho, công nợ và thu tiền để không cần suy diễn thêm