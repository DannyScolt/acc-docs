## ADDED Requirements

### Requirement: Chi tiết hóa các nghiệp vụ điều chỉnh và kết chuyển cuối kỳ của Phase 4
Tài liệu Phase 4 SHALL mô tả chi tiết các nghiệp vụ điều chỉnh và kết chuyển cuối kỳ ở mức tương đương Phase 1, bao gồm chứng từ nghiệp vụ khác, quyết toán tạm ứng, phân bổ chi phí, cấu hình kết chuyển và các bước kết chuyển cuối kỳ, với đầy đủ use case, actor, luồng nghiệp vụ, business rules, linkage và output.

#### Scenario: Bao phủ đầy đủ nhóm nghiệp vụ điều chỉnh cuối kỳ
- **WHEN** người dùng đọc phần Phase 4 trong HTML
- **THEN** tài liệu SHALL mô tả đầy đủ các mục 5.2, 5.3, 5.4 và 5.5 với use case, actor, luồng nghiệp vụ, luồng chính, business rule, liên kết phân hệ và kết quả đầu ra

### Requirement: Chứng từ nghiệp vụ khác phải có quy tắc kiểm soát ghi sổ rõ ràng
Tài liệu SHALL mô tả module chứng từ nghiệp vụ khác & bút toán tổng hợp với các quy tắc về kỳ kế toán mở, số chứng từ không trùng, cân đối Nợ/Có, duyệt chứng từ, ghi sổ, hủy/điều chỉnh và đính kèm hồ sơ chứng từ.

#### Scenario: Truy vết chứng từ nghiệp vụ khác
- **WHEN** người đọc xem mục chứng từ nghiệp vụ khác & bút toán tổng hợp
- **THEN** tài liệu SHALL chỉ rõ các use case lập chứng từ, hạch toán nhiều dòng, kiểm tra cân đối, khai báo VAT, sinh chứng từ từ hóa đơn điều chỉnh, hạch toán gộp/chi tiết, đính kèm hồ sơ, duyệt, ghi sổ và hủy/điều chỉnh cùng các rule kiểm soát liên quan

### Requirement: Quyết toán tạm ứng và phân bổ chi phí phải mô tả giới hạn phân bổ và giá trị còn lại
Tài liệu SHALL mô tả module quyết toán tạm ứng & phân bổ chi phí với các quy tắc về không quyết toán vượt tạm ứng, không phân bổ vượt giá trị còn lại, không phân bổ trùng kỳ, xử lý khoản còn lại không âm và lưu lịch sử phân bổ.

#### Scenario: Kiểm soát quyết toán và phân bổ định kỳ
- **WHEN** người dùng đọc mục quyết toán tạm ứng & phân bổ chi phí
- **THEN** tài liệu SHALL mô tả các use case quyết toán tạm ứng, đối chiếu tạm ứng nhân viên, ghi nhận chi phí chờ phân bổ, khai báo kỳ phân bổ, lập bút toán phân bổ, kiểm tra trùng kỳ và theo dõi giá trị còn lại cùng các business rule tương ứng

### Requirement: Cấu hình kết chuyển phải mô tả rõ cặp tài khoản và điều kiện hợp lệ
Tài liệu SHALL mô tả module cấu hình bút toán kết chuyển với quy tắc không trùng cấu hình, không xóa dữ liệu đã sử dụng, không sửa dữ liệu đã khóa kỳ, chỉ ngừng sử dụng thay vì xóa và không cho kết chuyển nếu thiếu cấu hình hợp lệ.

#### Scenario: Kiểm tra tính hợp lệ của cấu hình kết chuyển
- **WHEN** người đọc xem mục cấu hình bút toán kết chuyển
- **THEN** tài liệu SHALL mô tả các use case danh mục tài khoản kết chuyển, cặp kết chuyển mặc định, thêm/sửa cặp kết chuyển, ngừng sử dụng và kiểm tra cấu hình với các điều kiện kiểm soát đi kèm

### Requirement: Kết chuyển cuối kỳ phải mô tả đầy đủ luồng xác định kết quả kinh doanh
Tài liệu SHALL mô tả module kết chuyển cuối kỳ & xác định kết quả kinh doanh với quy tắc chỉ chạy trong kỳ mở, lấy dữ liệu từ lần kết chuyển gần nhất, không tính trùng số liệu, kiểm soát kết chuyển lãi/lỗ và lưu lịch sử khi hủy/chạy lại.

#### Scenario: Truy vết luồng kết chuyển cuối kỳ
- **WHEN** người dùng đọc mục kết chuyển cuối kỳ & xác định kết quả kinh doanh
- **THEN** tài liệu SHALL mô tả các use case lập chứng từ kết chuyển, kết chuyển doanh thu, kết chuyển chi phí, tự động tính số tiền kết chuyển, lấy dữ liệu từ lần gần nhất, xác định kết quả kinh doanh, kết chuyển lãi/lỗ, kiểm tra số dư bất thường và hủy/tính lại kết chuyển cùng các rule liên quan
