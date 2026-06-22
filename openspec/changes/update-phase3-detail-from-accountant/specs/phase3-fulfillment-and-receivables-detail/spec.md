## ADDED Requirements

### Requirement: Chi tiết hóa giao hàng, công nợ phải thu, thu tiền và báo cáo của Phase 3
Tài liệu Phase 3 SHALL mô tả chi tiết phần xuất kho bán hàng, hàng bán bị trả lại & giảm giá hàng bán, công nợ phải thu, thu tiền khách hàng và báo cáo Phase 3 ở mức tương đương Phase 1.

#### Scenario: Bao phủ đầy đủ các module fulfillment và receivables
- **WHEN** người dùng đọc phần cuối của Phase 3 trong HTML
- **THEN** tài liệu SHALL mô tả đầy đủ các mục 4.8, 4.9, 4.10, 4.11 và 4.12 với actor, use case, luồng chính, business rule, trạng thái, liên kết dữ liệu và bút toán liên quan

### Requirement: Xuất kho bán hàng phải mô tả đồng thời giao hàng và giá vốn
Tài liệu SHALL mô tả module xuất kho bán hàng với các quy tắc kiểm tra tồn, duyệt xuất, ghi sổ, cập nhật tồn kho, tính giá vốn và đảo phiếu xuất.

#### Scenario: Truy vết từ đơn hàng tới xuất kho và giá vốn
- **WHEN** người đọc xem mục xuất kho bán hàng
- **THEN** tài liệu SHALL thể hiện các use case lập phiếu xuất, lập từ đơn hàng, kiểm tra tồn, duyệt, ghi sổ, xuất nhiều đợt, theo dõi tiến độ giao, in/hủy/đảo phiếu và các rule `BR-XK-*`

### Requirement: Hàng bán bị trả lại và giảm giá hàng bán phải mô tả đầy đủ nghiệp vụ giảm trừ doanh thu
Tài liệu SHALL mô tả module hàng bán bị trả lại và giảm giá hàng bán với kiểm tra chất lượng, nhập kho lại, giảm công nợ, hoàn tiền, ghi sổ giảm trừ doanh thu và hóa đơn điều chỉnh.

#### Scenario: Truy vết nghiệp vụ trả lại và giảm giá
- **WHEN** người dùng đọc mục hàng bán bị trả lại & giảm giá hàng bán
- **THEN** tài liệu SHALL mô tả các use case trả hàng, kiểm tra hàng trả, nhập kho, chuyển hàng lỗi, giảm công nợ, hoàn tiền, giảm giá hàng bán, duyệt, ghi sổ, lập hóa đơn điều chỉnh và báo cáo giảm trừ doanh thu cùng các rule `BR-TRA-*`

### Requirement: Công nợ phải thu phải mô tả hạn mức, tuổi nợ và tất toán công nợ
Tài liệu SHALL mô tả module công nợ phải thu với đầy đủ quy tắc hình thành phải thu, kiểm soát hạn mức, theo dõi hạn thanh toán, công nợ quá hạn, tuổi nợ, đánh giá lại ngoại tệ và tất toán công nợ.

#### Scenario: Theo dõi vòng đời công nợ phải thu
- **WHEN** người đọc xem mục công nợ phải thu khách hàng
- **THEN** tài liệu SHALL mô tả các use case ghi nhận phải thu, theo dõi công nợ chi tiết, kiểm tra hạn mức tín dụng, thu tiền nhiều lần, đối trừ công nợ, theo dõi đến hạn/quá hạn, nhắc nợ, aging, đánh giá ngoại tệ, xác nhận, ghi sổ, tất toán và tra cứu lịch sử cùng các rule `BR-CN-*`

### Requirement: Thu tiền khách hàng phải mô tả nhiều hình thức thu và đối chiếu ngân hàng
Tài liệu SHALL mô tả module thu tiền khách hàng với các hình thức thu tiền mặt, thu ngân hàng, thu ngoại tệ, thu đặt cọc, thu cho nhiều hóa đơn và đối chiếu sao kê ngân hàng.

#### Scenario: Truy vết nghiệp vụ thu tiền khách hàng
- **WHEN** người dùng đọc mục thu tiền khách hàng
- **THEN** tài liệu SHALL mô tả các use case lập phiếu thu tiền mặt, lập chứng từ thu ngân hàng, thu nhiều lần cho một hóa đơn, thu một lần cho nhiều hóa đơn, thu đặt cọc, cấn trừ công nợ, thu ngoại tệ, duyệt, ghi sổ, đối chiếu sao kê, hủy, tra cứu, in phiếu thu và báo cáo thu tiền cùng các rule `BR-TT-*`

### Requirement: Báo cáo Phase 3 phải phản ánh doanh thu thuần, phải thu và hiệu quả bán hàng
Tài liệu SHALL mô tả module báo cáo Phase 3 với các chỉ số doanh thu thuần, lợi nhuận gộp, công nợ phải thu, tuổi nợ, tỷ lệ thu hồi công nợ và KPI kinh doanh.

#### Scenario: Kiểm tra báo cáo quản trị của Phase 3
- **WHEN** người đọc xem mục báo cáo bán hàng, doanh thu và công nợ phải thu
- **THEN** tài liệu SHALL mô tả dashboard, báo cáo doanh thu, báo cáo theo khách hàng/mặt hàng/nhân viên, lợi nhuận gộp, công nợ phải thu, tuổi nợ, nợ quá hạn, thu tiền khách hàng, đơn hàng bán và xuất báo cáo cùng các rule `BR-BC-*`

### Requirement: Các module fulfillment và receivables phải mô tả rõ liên kết dữ liệu với phase khác
Tài liệu SHALL chỉ rõ liên kết giữa xuất kho, giá vốn, hóa đơn, công nợ, thu tiền, giảm trừ doanh thu và sổ cái để người đọc có thể đối chiếu xuyên chu trình.

#### Scenario: Truy vết xuyên chu trình cuối Phase 3
- **WHEN** kế toán hoặc BA kiểm tra một giao dịch bán hoàn chỉnh từ giao hàng đến thu tiền hoặc trả lại hàng
- **THEN** tài liệu SHALL chỉ ra rõ điểm nối dữ liệu giữa xuất kho, hóa đơn, công nợ, thu tiền, giảm trừ doanh thu, thuế đầu ra và sổ cái mà không cần suy diễn thêm