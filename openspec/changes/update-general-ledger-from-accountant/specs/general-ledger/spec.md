## ADDED Requirements

### Requirement: Chi tiết nghiệp vụ ghi sổ kế toán trong tài liệu nghiệp vụ
Tài liệu và đặc tả phân hệ `general-ledger` SHALL mô tả chi tiết nghiệp vụ ghi sổ kế toán với đầy đủ mục tiêu, actor, chức năng, luồng xử lý, kết quả và business rules.

#### Scenario: Ghi sổ từ chứng từ đã duyệt
- **WHEN** chứng từ nguồn từ các phân hệ được duyệt
- **THEN** hệ thống SHALL lấy cấu hình hạch toán, sinh bút toán Nợ/Có, kiểm tra cân đối, kiểm tra kỳ kế toán, ghi Journal Entry, cập nhật sổ cái, cập nhật số dư và ghi Audit Log

#### Scenario: Kiểm soát business rules ghi sổ
- **WHEN** hệ thống thực hiện ghi sổ kế toán
- **THEN** hệ thống MUST đảm bảo BR-GL-01 đến BR-GL-07, bao gồm cân đối Nợ/Có, không ghi sổ chứng từ chưa duyệt, không sửa trực tiếp bút toán đã ghi sổ, điều chỉnh qua bút toán điều chỉnh hoặc đảo, không ghi vào kỳ đã khóa, bắt buộc liên kết chứng từ nguồn và không ghi sổ trùng chứng từ nguồn

### Requirement: Chi tiết nghiệp vụ sổ cái trong tài liệu nghiệp vụ
Tài liệu và đặc tả phân hệ `general-ledger` SHALL mô tả đầy đủ nghiệp vụ tra cứu sổ cái theo tài khoản, kỳ, đối tượng và phạm vi quản trị.

#### Scenario: Xem sổ cái với điều kiện lọc mở rộng
- **WHEN** người dùng truy cập sổ cái
- **THEN** hệ thống SHALL cho phép xem theo tài khoản, kỳ, đối tượng, phòng ban, chi nhánh và dự án; hiển thị số dư đầu kỳ, phát sinh Nợ/Có, số dư cuối kỳ và cho phép drill-down về chứng từ gốc

#### Scenario: Kiểm soát business rules sổ cái
- **WHEN** dữ liệu được hiển thị trên sổ cái
- **THEN** hệ thống MUST đảm bảo BR-LEDGER-01 đến BR-LEDGER-04, bao gồm lấy dữ liệu trực tiếp từ Journal Entry đã ghi sổ, không hiển thị bút toán chưa ghi sổ, tính đúng số dư cuối kỳ và giới hạn dữ liệu theo quyền được cấp

### Requirement: Chi tiết nghiệp vụ nhật ký chung trong tài liệu nghiệp vụ
Tài liệu và đặc tả phân hệ `general-ledger` SHALL mô tả đầy đủ nghiệp vụ xem nhật ký chung với các bộ lọc và truy vết về chứng từ nguồn.

#### Scenario: Xem nhật ký chung theo thời gian và bộ lọc
- **WHEN** người dùng mở nhật ký chung và chọn khoảng thời gian
- **THEN** hệ thống SHALL truy vấn dữ liệu, sắp xếp theo ngày, cho phép lọc theo tài khoản, loại chứng từ, người lập, số chứng từ và cho phép xem chi tiết bút toán hoặc chứng từ nguồn

#### Scenario: Kiểm soát business rules nhật ký chung
- **WHEN** dữ liệu được hiển thị trên nhật ký chung
- **THEN** hệ thống MUST đảm bảo BR-JE-01 đến BR-JE-04, bao gồm chỉ hiển thị bút toán đã ghi sổ, số Journal duy nhất, không chỉnh sửa trực tiếp và mọi dòng đều truy xuất được chứng từ nguồn

### Requirement: Chi tiết nghiệp vụ bảng cân đối phát sinh trong tài liệu nghiệp vụ
Tài liệu và đặc tả phân hệ `general-ledger` SHALL mô tả đầy đủ nghiệp vụ lập bảng cân đối phát sinh với các chiều phân tích quản trị.

#### Scenario: Lập bảng cân đối phát sinh theo nhiều chiều
- **WHEN** người dùng chọn kỳ kế toán và đơn vị hạch toán
- **THEN** hệ thống SHALL lấy dữ liệu từ sổ cái, tính số dư đầu kỳ, phát sinh Nợ, phát sinh Có, số dư cuối kỳ, kiểm tra cân đối và hiển thị báo cáo theo chi nhánh, phòng ban, dự án hoặc so sánh nhiều kỳ

#### Scenario: Kiểm soát business rules bảng cân đối phát sinh
- **WHEN** hệ thống lập bảng cân đối phát sinh
- **THEN** hệ thống MUST đảm bảo BR-TB-01 đến BR-TB-04, bao gồm tổng phát sinh Nợ bằng tổng phát sinh Có, dữ liệu lấy từ sổ cái, chỉ dùng dữ liệu đã ghi sổ và cho phép drill-down đến tài khoản cùng chứng từ

### Requirement: Business rules toàn phân hệ sổ cái và hệ thống tài khoản
Tài liệu và đặc tả phân hệ `general-ledger` SHALL xác định rõ bộ business rules toàn phân hệ để thống nhất kiểm soát hạch toán, khóa kỳ, truy vết và phân quyền.

#### Scenario: Áp dụng business rules toàn phân hệ
- **WHEN** người dùng thao tác trong phân hệ sổ cái và hệ thống tài khoản
- **THEN** hệ thống MUST đảm bảo BR-GLOBAL-01 đến BR-GLOBAL-20, bao gồm sơ đồ tài khoản TT200/TT133, cân bằng Nợ/Có, kiểm soát ghi sổ, không xóa bút toán đã ghi sổ, truy vết chứng từ nguồn, khóa/mở khóa kỳ, audit log, hỗ trợ đa năm tài chính, đa chi nhánh, xuất báo cáo và kiểm soát phân quyền
