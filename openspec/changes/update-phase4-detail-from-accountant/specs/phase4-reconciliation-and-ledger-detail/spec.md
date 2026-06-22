## ADDED Requirements

### Requirement: Chi tiết hóa đối chiếu, khóa kỳ và sổ kế toán tổng hợp của Phase 4
Tài liệu Phase 4 SHALL mô tả chi tiết các nghiệp vụ kiểm tra đối chiếu trước khóa kỳ, khóa kỳ/mở lại kỳ và hệ thống sổ sách kế toán tổng hợp ở mức tương đương Phase 1, với đầy đủ use case, actor, luồng nghiệp vụ, business rules, linkage và output.

#### Scenario: Bao phủ đầy đủ nhóm nghiệp vụ đối chiếu và sổ sách
- **WHEN** người dùng đọc phần giữa và cuối của Phase 4 trong HTML
- **THEN** tài liệu SHALL mô tả đầy đủ các mục 5.6, 5.7 và 5.8 với use case, actor, luồng nghiệp vụ, luồng chính, business rules, liên kết phân hệ và kết quả đầu ra

### Requirement: Đối chiếu trước khóa kỳ phải bao phủ toàn bộ số liệu trọng yếu
Tài liệu SHALL mô tả module kiểm tra đối chiếu trước khóa kỳ với các bước kiểm tra chứng từ chưa ghi sổ, cân đối Nợ/Có, kết chuyển lãi/lỗ, quỹ, ngân hàng, công nợ phải thu, công nợ phải trả, tồn kho, thuế và cảnh báo số liệu bất thường; đầu ra phải có danh sách lỗi hoặc biên bản đối chiếu.

#### Scenario: Kiểm tra readiness trước khóa kỳ
- **WHEN** người đọc xem mục kiểm tra đối chiếu trước khóa kỳ
- **THEN** tài liệu SHALL chỉ rõ các điều kiện không cho khóa kỳ khi còn lỗi, các liên kết với từng phân hệ nguồn và kết quả đầu ra dạng danh sách lỗi, biên bản đối chiếu hoặc báo cáo kiểm tra

### Requirement: Khóa kỳ và mở lại kỳ phải được kiểm soát bằng phân quyền và audit log
Tài liệu SHALL mô tả module khóa kỳ & mở lại kỳ với quy tắc chỉ người có quyền mới được khóa hoặc mở kỳ, bắt buộc nhập lý do mở kỳ, lưu lịch sử khóa/mở kỳ và không cho xóa audit log.

#### Scenario: Truy vết vòng đời khóa kỳ
- **WHEN** người dùng đọc mục khóa kỳ & mở lại kỳ
- **THEN** tài liệu SHALL mô tả các use case khóa kỳ, chặn thêm/sửa/xóa, kiểm tra điều kiện trước khóa, mở lại kỳ, ghi nhận lý do, lưu lịch sử và khóa lại kỳ sau điều chỉnh cùng các rule kiểm soát đi kèm

### Requirement: Sổ kế toán tổng hợp phải hỗ trợ tra cứu, drill-down và xuất dữ liệu nhất quán
Tài liệu SHALL mô tả module sổ sách kế toán tổng hợp với quy tắc chỉ hiển thị chứng từ đã ghi sổ, chi tiết phải khớp sổ cái, tổng Nợ bằng tổng Có và dữ liệu xuất phải khớp dữ liệu hiển thị, đồng thời hỗ trợ lọc/tra cứu và drill-down về chứng từ gốc.

#### Scenario: Truy xuất sổ kế toán tổng hợp
- **WHEN** người đọc xem mục sổ sách kế toán tổng hợp
- **THEN** tài liệu SHALL mô tả các use case sổ nhật ký chung, sổ cái, sổ chi tiết tài khoản, bảng cân đối phát sinh, bảng cân đối tài khoản, lọc/tra cứu, drill-down chứng từ gốc và xuất sổ sách cùng các điều kiện kiểm soát quyền xem và dữ liệu nguồn
