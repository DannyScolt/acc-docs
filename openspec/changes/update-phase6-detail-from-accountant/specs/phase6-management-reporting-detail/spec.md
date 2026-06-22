## ADDED Requirements

### Requirement: Chi tiết hóa cụm quản trị và tổng hợp kiểm soát của Phase 6
Tài liệu Phase 6 SHALL mô tả chi tiết mục 7.8 và các phần tổng hợp cuối phase ở mức tương đương Phase 1, bao gồm dashboard quản trị, phân tích tài chính, dự báo dòng tiền, ngân sách, bảng định khoản mẫu, quy tắc chung, kết quả bàn giao và tiêu chí nghiệm thu.

#### Scenario: Bao phủ đầy đủ quản trị và kiểm soát Phase 6
- **WHEN** người dùng đọc phần 7.8 và các phần tổng hợp của Phase 6 trong HTML
- **THEN** tài liệu SHALL mô tả rõ các use case có mã, business rules, workflow, kiểm soát và tiêu chí nghiệm thu tương ứng với dashboard, phân tích, dự báo dòng tiền và ngân sách

### Requirement: Dashboard, phân tích tài chính, dự báo dòng tiền và ngân sách phải tách rõ operational scope
Tài liệu SHALL giữ nguyên heading 7.8 nhưng phân biệt rõ các nhóm nghiệp vụ dashboard, financial analysis, cash forecasting và budget control như các phạm vi hoạt động riêng bên trong mục này.

#### Scenario: Review các scope bên trong mục 7.8
- **WHEN** người dùng xem phần dashboard quản trị, phân tích tài chính, dự báo dòng tiền và ngân sách
- **THEN** tài liệu SHALL cho phép phân biệt rõ mục tiêu, dữ liệu đầu vào, workflow và kết quả của từng nhóm nghiệp vụ thay vì chỉ là một bảng chức năng chung

### Requirement: Phase 6 phải có bảng định khoản và quy tắc chung đủ ngữ cảnh
Tài liệu SHALL mở rộng bảng định khoản mẫu và quy tắc nghiệp vụ chung của Giai đoạn 6 bằng các bút toán, rule có mã và ghi chú kiểm soát phù hợp với tài sản, phân bổ, lương, giá thành, vay và e-banking.

#### Scenario: Đối chiếu định khoản và rule chung của Phase 6
- **WHEN** người dùng xem phần bảng định khoản mẫu hoặc quy tắc nghiệp vụ chung của Giai đoạn 6
- **THEN** tài liệu SHALL giúp đối chiếu được các nghiệp vụ mở rộng với ảnh hưởng kế toán, quyền xử lý, kỳ khóa và truy vết chứng từ nguồn

### Requirement: Kết quả bàn giao và tiêu chí nghiệm thu của Phase 6 phải kiểm chứng được theo từng nhóm module
Tài liệu SHALL xác định kết quả bàn giao và tiêu chí nghiệm thu chi tiết cho các cụm tài sản/phân bổ, lương/giá thành, vay/hợp đồng/e-banking và quản trị nâng cao.

#### Scenario: Đánh giá readiness của Phase 6
- **WHEN** kế toán, BA hoặc tester review cuối Phase 6
- **THEN** họ SHALL có thể dùng các mục kết quả bàn giao và tiêu chí nghiệm thu để xác định liệu phạm vi mở rộng nâng cao đã đủ rõ để triển khai, kiểm thử và nghiệm thu hay chưa
