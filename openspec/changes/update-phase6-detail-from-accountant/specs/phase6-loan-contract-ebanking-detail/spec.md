## ADDED Requirements

### Requirement: Chi tiết hóa cụm vay, hợp đồng và ngân hàng điện tử của Phase 6
Tài liệu Phase 6 SHALL mô tả chi tiết các mục 7.5 đến 7.7 ở mức tương đương Phase 1, bao gồm khoản vay, lịch trả nợ, chi phí lãi vay, hợp đồng tài chính, mốc thanh toán, e-banking, đối chiếu và kiểm soát bảo mật.

#### Scenario: Bao phủ đầy đủ vay, hợp đồng và e-banking
- **WHEN** người dùng đọc các mục 7.5 đến 7.7 trong HTML
- **THEN** tài liệu SHALL mô tả rõ actor, use case có mã, điều kiện, luồng chính, kết quả, trạng thái và business rules cho từng cụm nghiệp vụ

### Requirement: Khế ước vay phải có trạng thái và lịch trả nợ rõ ràng
Tài liệu SHALL mô tả các use case cho khai báo khoản vay, khai báo lãi suất, lập lịch trả nợ, ghi nhận giải ngân, ghi nhận thanh toán gốc/lãi, cảnh báo đến hạn và báo cáo dư nợ.

#### Scenario: Theo dõi một khoản vay trong kỳ
- **WHEN** người dùng xem phần khế ước vay
- **THEN** tài liệu SHALL chỉ rõ được các trạng thái hoặc bước xử lý tối thiểu từ khai báo khoản vay, giải ngân, theo dõi dư nợ, tính lãi, trả nợ đến báo cáo đối chiếu sổ cái

### Requirement: Hợp đồng phải liên kết được với hóa đơn, thu chi và mốc thanh toán
Tài liệu SHALL mô tả các use case và business rules cho việc khai báo hợp đồng, khai báo mốc thanh toán, liên kết hóa đơn, liên kết thu chi, theo dõi tiến độ thực hiện và cảnh báo đến hạn.

#### Scenario: Review hợp đồng theo tiến độ tài chính
- **WHEN** người dùng xem phần hợp đồng
- **THEN** tài liệu SHALL mô tả cách truy vết hợp đồng tới hóa đơn, công nợ, dòng tiền và tình trạng thực hiện của từng mốc thanh toán

### Requirement: Ngân hàng điện tử phải có kiểm soát phân quyền, trạng thái giao dịch và đối chiếu
Tài liệu SHALL mô tả các use case và business rules cho kết nối ngân hàng điện tử, tra cứu số dư/giao dịch, khởi tạo giao dịch, duyệt giao dịch, tạo chứng từ, đối chiếu sổ phụ và xử lý giao dịch lệch.

#### Scenario: Rà soát kiểm soát e-banking
- **WHEN** người dùng xem phần ngân hàng điện tử
- **THEN** tài liệu SHALL chỉ rõ các kiểm soát tối thiểu về quyền truy cập, trạng thái giao dịch, log xử lý, điều kiện tự động hạch toán và xử lý giao dịch chưa khớp
