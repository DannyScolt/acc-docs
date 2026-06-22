## ADDED Requirements

### Requirement: Chi tiết hóa báo cáo tài chính của Phase 4
Tài liệu Phase 4 SHALL mô tả chi tiết bộ báo cáo tài chính, kiểm tra cân đối báo cáo, drill-down và quản lý phiên bản báo cáo ở mức tương đương Phase 1, với đủ use case, actor, luồng nghiệp vụ, business rules, linkage và output.

#### Scenario: Bao phủ đầy đủ module báo cáo tài chính
- **WHEN** người dùng đọc mục 5.9 trong Phase 4 của HTML
- **THEN** tài liệu SHALL mô tả đầy đủ các use case lập báo cáo tài chính, bảng cân đối kế toán, báo cáo kết quả hoạt động kinh doanh, báo cáo lưu chuyển tiền tệ, thuyết minh BCTC, kiểm tra cân đối, drill-down, xuất báo cáo và lưu phiên bản

### Requirement: Báo cáo tài chính phải lấy dữ liệu từ sổ kế toán đã ghi sổ
Tài liệu SHALL mô tả rõ rằng bộ báo cáo tài chính chỉ lấy dữ liệu đã ghi sổ và phải khớp với sổ cái, kết chuyển cuối kỳ và các tài khoản tiền khi áp dụng; không được phát hành báo cáo nếu dữ liệu chưa cân hoặc chưa kết chuyển.

#### Scenario: Kiểm tra nguồn dữ liệu của BCTC
- **WHEN** người đọc xem mục báo cáo tài chính
- **THEN** tài liệu SHALL nêu rõ các điều kiện như chỉ lấy dữ liệu đã ghi sổ, bảng cân đối kế toán phải cân giữa tài sản và nguồn vốn, báo cáo kết quả hoạt động kinh doanh phải khớp kết chuyển cuối kỳ và báo cáo lưu chuyển tiền tệ phải khớp tài khoản tiền

### Requirement: Báo cáo tài chính phải hỗ trợ kiểm tra lỗi và truy vết nguồn số liệu
Tài liệu SHALL mô tả khả năng kiểm tra cân đối báo cáo và drill-down từ chỉ tiêu báo cáo xuống sổ sách và chứng từ gốc, đồng thời nêu rõ output khi phát hiện lỗi.

#### Scenario: Truy vết từ chỉ tiêu báo cáo xuống dữ liệu nguồn
- **WHEN** kế toán trưởng hoặc người review kiểm tra một chỉ tiêu trên báo cáo tài chính
- **THEN** tài liệu SHALL chỉ rõ có thể truy xuất về sổ cái, sổ chi tiết và chứng từ phát sinh, đồng thời không cho phát hành báo cáo khi hệ thống phát hiện lỗi cân đối hoặc lệch chỉ tiêu

### Requirement: Phiên bản và file xuất báo cáo tài chính phải được quản lý riêng
Tài liệu SHALL mô tả việc xuất báo cáo tài chính ra PDF/Excel và lưu các phiên bản báo cáo đã phát hành như snapshot riêng biệt, không ghi đè phiên bản cũ.

#### Scenario: Kiểm soát phiên bản báo cáo tài chính
- **WHEN** người dùng phát hành hoặc lưu báo cáo tài chính theo kỳ
- **THEN** tài liệu SHALL mô tả rằng hệ thống lưu phiên bản riêng, không ghi đè báo cáo đã phát hành và file xuất phải đúng mẫu quy định
