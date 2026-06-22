## ADDED Requirements

### Requirement: Chi tiết hóa cụm bảng kê, kê khai và nghĩa vụ thuế của Phase 5
Tài liệu Phase 5 SHALL mô tả chi tiết các mục 6.7 đến 6.9 ở mức tương đương Phase 1, bao gồm bảng kê hóa đơn, kê khai thuế/tờ khai thuế, giấy nộp tiền và báo cáo thuế.

#### Scenario: Bao phủ đầy đủ quy trình kê khai thuế
- **WHEN** người dùng đọc các mục 6.7 đến 6.9 trong HTML
- **THEN** tài liệu SHALL mô tả rõ actor, điều kiện, dữ liệu đầu vào, luồng chính, kết quả, business rules và workflow cho các nghiệp vụ bảng kê, tờ khai và nghĩa vụ thuế

### Requirement: Bảng kê hóa đơn có logic đối chiếu rõ ràng
Tài liệu SHALL mô tả các use case và business rules cho việc lập bảng kê hóa đơn mua vào/bán ra, đối chiếu với chứng từ kế toán và phát hiện hóa đơn thiếu/thừa.

#### Scenario: Đối chiếu bảng kê với dữ liệu kế toán
- **WHEN** người dùng xem phần bảng kê hóa đơn mua vào hoặc bán ra
- **THEN** tài liệu SHALL chỉ rõ nguồn dữ liệu, điều kiện đưa hóa đơn vào bảng kê, các bước rà soát sai lệch và kết quả chốt bảng kê

### Requirement: Tờ khai thuế có workflow và versioning rõ ràng
Tài liệu SHALL mô tả workflow cho việc lập, kiểm tra, chốt, xuất và điều chỉnh tờ khai thuế cùng các quy tắc lưu phiên bản.

#### Scenario: Tạo hoặc điều chỉnh một tờ khai thuế
- **WHEN** người dùng xem phần kê khai thuế và tờ khai thuế
- **THEN** tài liệu SHALL mô tả các trạng thái tối thiểu như nháp, chờ kiểm tra, đã chốt, đã nộp hoặc điều chỉnh/bổ sung cùng các business rules liên quan

### Requirement: Giấy nộp tiền và nghĩa vụ thuế có thể truy vết tới thanh toán thực tế
Tài liệu SHALL mô tả use case, trạng thái và business rules cho giấy nộp tiền, theo dõi đã nộp/chưa nộp và đối chiếu nghĩa vụ thuế.

#### Scenario: Theo dõi tình trạng nộp thuế
- **WHEN** người dùng xem phần giấy nộp tiền và báo cáo thuế
- **THEN** tài liệu SHALL chỉ rõ cách xác định nghĩa vụ thuế, lập giấy nộp tiền, cập nhật trạng thái nộp và đối chiếu với chứng từ thanh toán liên quan
