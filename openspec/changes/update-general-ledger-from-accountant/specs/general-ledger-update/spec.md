## ADDED Requirements

### Requirement: Section 2.5 HTML — UC chi tiết phân hệ Sổ cái & hệ thống tài khoản
HTML section 2.5 SHALL được cập nhật từ dạng bảng chức năng tóm tắt sang nội dung chi tiết cho 4 phân hệ con và bộ business rules toàn phân hệ.

#### Scenario: Hiển thị đầy đủ 4 phân hệ con của section 2.5
- **WHEN** người dùng mở tài liệu HTML phạm vi nghiệp vụ Phase 1
- **THEN** section 2.5 SHALL hiển thị đầy đủ 2.5.1 Ghi sổ kế toán, 2.5.2 Sổ cái, 2.5.3 Sổ nhật ký chung và 2.5.4 Bảng cân đối phát sinh theo format chi tiết

### Requirement: Section 2.5.1 — Ghi sổ kế toán chi tiết
HTML SHALL mô tả chi tiết mục tiêu, actor, chức năng, luồng chính, kết quả và business rules cho phân hệ ghi sổ kế toán.

#### Scenario: Nội dung chi tiết 2.5.1 xuất hiện trong tài liệu
- **WHEN** người dùng đọc subsection 2.5.1
- **THEN** tài liệu SHALL hiển thị Mục tiêu, Actor, Chức năng, Luồng chính 9 bước, Kết quả, BR-GL-01 đến BR-GL-07

### Requirement: Section 2.5.2 — Sổ cái chi tiết
HTML SHALL mô tả chi tiết mục tiêu, actor, chức năng, luồng chính, kết quả và business rules cho phân hệ sổ cái.

#### Scenario: Nội dung chi tiết 2.5.2 xuất hiện trong tài liệu
- **WHEN** người dùng đọc subsection 2.5.2
- **THEN** tài liệu SHALL hiển thị Mục tiêu, Actor, Chức năng, Luồng chính 8 bước, Kết quả, BR-LEDGER-01 đến BR-LEDGER-04

### Requirement: Section 2.5.3 — Sổ nhật ký chung chi tiết
HTML SHALL mô tả chi tiết mục tiêu, actor, chức năng, luồng chính, kết quả và business rules cho phân hệ sổ nhật ký chung.

#### Scenario: Nội dung chi tiết 2.5.3 xuất hiện trong tài liệu
- **WHEN** người dùng đọc subsection 2.5.3
- **THEN** tài liệu SHALL hiển thị Mục tiêu, Actor, Chức năng, Luồng chính 6 bước, Kết quả, BR-JE-01 đến BR-JE-04

### Requirement: Section 2.5.4 — Bảng cân đối phát sinh chi tiết
HTML SHALL mô tả chi tiết mục tiêu, actor, chức năng, luồng chính, kết quả và business rules cho bảng cân đối phát sinh.

#### Scenario: Nội dung chi tiết 2.5.4 xuất hiện trong tài liệu
- **WHEN** người dùng đọc subsection 2.5.4
- **THEN** tài liệu SHALL hiển thị Mục tiêu, Actor, Chức năng, Luồng chính 9 bước, Kết quả, BR-TB-01 đến BR-TB-04

### Requirement: Business Rules toàn phân hệ Sổ cái & hệ thống tài khoản
HTML SHALL có một block business rules toàn phân hệ để tập hợp các nguyên tắc kiểm soát chung cho sổ cái và hệ thống tài khoản.

#### Scenario: Hiển thị bộ rule toàn phân hệ
- **WHEN** người dùng đọc cuối section 2.5
- **THEN** tài liệu SHALL hiển thị đầy đủ BR-GLOBAL-01 đến BR-GLOBAL-20 trong một block riêng biệt trước Bảng định khoản mẫu — Giai đoạn 1
