## ADDED Requirements

### Requirement: Quản lý doanh nghiệp (Company)
Hệ thống SHALL cho phép khởi tạo và quản lý thông tin doanh nghiệp sử dụng phần mềm kế toán.

**Entity: `company`**

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | UUID | ✓ | PK, auto |
| name | VARCHAR(255) | ✓ | Tên công ty |
| tax_code | VARCHAR(20) | ✓ | Mã số thuế, unique |
| address | TEXT | | Địa chỉ |
| phone | VARCHAR(20) | | Điện thoại |
| email | VARCHAR(100) | | Email |
| representative | VARCHAR(100) | | Người đại diện |
| logo_url | VARCHAR(500) | | URL logo |
| accounting_regime | ENUM | ✓ | tt200 \| tt133 |
| costing_method | ENUM | ✓ | weighted_avg \| fifo |
| tax_method | ENUM | ✓ | deduction \| direct |
| tax_period | ENUM | ✓ | monthly \| quarterly |
| base_currency | VARCHAR(3) | ✓ | Default: VND |
| is_active | BOOLEAN | ✓ | Default: true |
| created_at | TIMESTAMP | ✓ | auto |
| updated_at | TIMESTAMP | ✓ | auto |

#### Scenario: Khởi tạo doanh nghiệp thành công
- **WHEN** admin nhập đầy đủ thông tin bắt buộc (name, tax_code, accounting_regime, costing_method, tax_method, tax_period)
- **THEN** hệ thống tạo record company, tự động tạo hệ thống tài khoản mặc định theo chế độ kế toán đã chọn

#### Scenario: Trùng mã số thuế
- **WHEN** admin nhập tax_code đã tồn tại trong hệ thống
- **THEN** hệ thống từ chối và hiển thị lỗi "Mã số thuế đã tồn tại"

### Requirement: Cấu hình năm tài chính (FiscalYear)
Hệ thống SHALL cho phép khai báo năm tài chính, ngày bắt đầu, ngày kết thúc và kỳ kế toán.

**Entity: `fiscal_year`**

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | UUID | ✓ | PK |
| company_id | UUID(FK) | ✓ | → company |
| year | INTEGER | ✓ | Năm tài chính |
| start_date | DATE | ✓ | Ngày bắt đầu |
| end_date | DATE | ✓ | Ngày kết thúc |
| period_type | ENUM | ✓ | monthly \| quarterly \| yearly |
| is_closed | BOOLEAN | ✓ | Default: false |
| closed_at | TIMESTAMP | | Ngày khóa |
| closed_by | UUID(FK) | | → user |

#### Scenario: Tạo năm tài chính
- **WHEN** admin khai báo năm tài chính với start_date và end_date hợp lệ (end > start, không trùng năm đã có)
- **THEN** hệ thống tạo fiscal_year và tự sinh các kỳ kế toán con theo period_type

#### Scenario: Khóa kỳ kế toán
- **WHEN** kế toán trưởng khóa kỳ cho 1 tháng/quý
- **THEN** mọi chứng từ có ngày thuộc kỳ đó SHALL không được tạo mới, sửa, duyệt hoặc hủy (trừ khi mở khóa kỳ)

### Requirement: Cấu hình chi nhánh và phòng ban
Hệ thống SHALL cho phép khai báo chi nhánh / đơn vị phụ thuộc và phòng ban / bộ phận.

**Entity: `branch`**

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | UUID | ✓ | PK |
| company_id | UUID(FK) | ✓ | → company |
| code | VARCHAR(20) | ✓ | Unique trong company |
| name | VARCHAR(255) | ✓ | |
| address | TEXT | | |
| is_active | BOOLEAN | ✓ | Default: true |

**Entity: `department`**

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | UUID | ✓ | PK |
| company_id | UUID(FK) | ✓ | → company |
| branch_id | UUID(FK) | | → branch |
| code | VARCHAR(20) | ✓ | Unique trong company |
| name | VARCHAR(255) | ✓ | |
| is_active | BOOLEAN | ✓ | Default: true |

#### Scenario: Tạo chi nhánh
- **WHEN** admin tạo chi nhánh với code unique trong company
- **THEN** hệ thống tạo branch, dữ liệu sau này có thể phân quyền theo branch

#### Scenario: Tạo phòng ban
- **WHEN** admin tạo phòng ban, có thể gắn vào branch hoặc để trống
- **THEN** hệ thống tạo department phục vụ phân quyền và tập hợp chi phí

### Requirement: Cấu hình mẫu số chứng từ (NumberingRule)
Hệ thống SHALL cho phép thiết lập quy tắc đánh số chứng từ tự động cho mỗi loại chứng từ.

**Entity: `document_type`**

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | UUID | ✓ | PK |
| company_id | UUID(FK) | ✓ | → company |
| code | VARCHAR(20) | ✓ | vd: CASH_RECEIPT, CASH_PAYMENT, BANK_RECEIPT... |
| name | VARCHAR(100) | ✓ | |
| status_flow | JSONB | ✓ | ["draft","pending_approval","approved","cancelled"] |

**Entity: `numbering_rule`**

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | UUID | ✓ | PK |
| company_id | UUID(FK) | ✓ | → company |
| document_type_id | UUID(FK) | ✓ | → document_type |
| prefix | VARCHAR(10) | ✓ | vd: PT, PC, TNH, CNH |
| separator | VARCHAR(2) | | Default: - |
| include_year | BOOLEAN | ✓ | Default: true |
| include_month | BOOLEAN | ✓ | Default: true |
| sequence_length | INTEGER | ✓ | Default: 4 (→ 0001) |
| reset_period | ENUM | ✓ | monthly \| yearly \| never |
| current_sequence | INTEGER | ✓ | Default: 0 |

#### Scenario: Sinh số chứng từ tự động
- **WHEN** user tạo chứng từ mới thuộc document_type có numbering_rule
- **THEN** hệ thống sinh số theo format: `{prefix}{separator}{year}{month}{separator}{sequence}` (vd: PT-202601-0001), tự tăng sequence, đảm bảo unique

#### Scenario: Reset sequence theo kỳ
- **WHEN** reset_period = monthly và sang tháng mới
- **THEN** sequence reset về 0, số chứng từ tiếp tục từ 0001

### Requirement: Quản lý người dùng (User)
Hệ thống SHALL cho phép admin tạo, cập nhật, khóa, mở khóa tài khoản người dùng.

**Entity: `user`**

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | UUID | ✓ | PK |
| company_id | UUID(FK) | ✓ | → company |
| username | VARCHAR(50) | ✓ | Unique trong company |
| email | VARCHAR(100) | ✓ | |
| password_hash | VARCHAR(255) | ✓ | Bcrypt |
| full_name | VARCHAR(100) | ✓ | |
| phone | VARCHAR(20) | | |
| department_id | UUID(FK) | | → department |
| employee_id | UUID(FK) | | → employee |
| status | ENUM | ✓ | active \| locked \| disabled |
| last_login_at | TIMESTAMP | | |
| session_timeout_minutes | INTEGER | ✓ | Default: 30 |
| created_at | TIMESTAMP | ✓ | |
| updated_at | TIMESTAMP | ✓ | |

#### Scenario: Tạo tài khoản người dùng
- **WHEN** admin tạo user với username unique, email hợp lệ, password đủ mạnh (≥8 ký tự, có chữ hoa + số)
- **THEN** hệ thống tạo user với status = active

#### Scenario: Khóa tài khoản
- **WHEN** admin khóa tài khoản (status → locked)
- **THEN** user không thể đăng nhập, phiên đang hoạt động bị kết thúc, ghi audit_log

#### Scenario: Tự động đăng xuất khi hết phiên
- **WHEN** user không thao tác trong session_timeout_minutes phút
- **THEN** hệ thống tự động kết thúc phiên, user phải đăng nhập lại

### Requirement: Vai trò & phân quyền (Role-Based Access Control)
Hệ thống SHALL triển khai RBAC với phân quyền theo chức năng, phân hệ, dữ liệu và duyệt chứng từ.

**Entity: `role`**

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | UUID | ✓ | PK |
| company_id | UUID(FK) | ✓ | → company |
| name | VARCHAR(100) | ✓ | vd: Admin, Kế toán trưởng, Thủ quỹ |
| description | TEXT | | |
| is_system | BOOLEAN | ✓ | Default: false (role mặc định không xóa được) |

**Entity: `permission`**

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | UUID | ✓ | PK |
| role_id | UUID(FK) | ✓ | → role |
| module | VARCHAR(50) | ✓ | vd: cash, bank, master_data, general_ledger |
| feature | VARCHAR(50) | ✓ | vd: cash_receipt, customer, account |
| action | ENUM | ✓ | view \| create \| edit \| delete \| approve \| export |

**Entity: `user_role`**

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| user_id | UUID(FK) | ✓ | → user |
| role_id | UUID(FK) | ✓ | → role |

**Entity: `data_permission`** (phân quyền theo dữ liệu)

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | UUID | ✓ | PK |
| role_id | UUID(FK) | ✓ | → role |
| scope_type | ENUM | ✓ | branch \| department \| warehouse \| bank_account |
| scope_id | UUID | ✓ | ID của đối tượng phân quyền |

#### Scenario: Kiểm tra quyền trước thao tác
- **WHEN** user thực hiện bất kỳ thao tác nào (xem, tạo, sửa, xóa, duyệt, xuất)
- **THEN** hệ thống kiểm tra user có role chứa permission tương ứng (module + feature + action), nếu không có → chặn và hiển thị "Bạn không có quyền thực hiện thao tác này"

#### Scenario: Phân quyền theo dữ liệu
- **WHEN** user có data_permission scope_type = warehouse, scope_id = warehouse_A
- **THEN** user chỉ xem/thao tác được dữ liệu liên quan warehouse_A, các kho khác bị ẩn

#### Scenario: Sao chép quyền từ vai trò khác
- **WHEN** admin sao chép quyền từ role_A sang role_B
- **THEN** hệ thống copy tất cả permission và data_permission từ role_A tạo bản sao cho role_B

### Requirement: Nhật ký truy vết (Audit Log)
Hệ thống SHALL ghi nhận mọi thao tác quan trọng vào audit_log, không cho phép sửa hoặc xóa thủ công.

**Entity: `audit_log`**

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | BIGSERIAL | ✓ | PK, auto-increment |
| company_id | UUID(FK) | ✓ | → company |
| user_id | UUID(FK) | ✓ | → user |
| action | ENUM | ✓ | create \| update \| delete \| approve \| cancel \| lock \| unlock \| login \| logout |
| entity_type | VARCHAR(50) | ✓ | vd: cash_receipt, customer, account |
| entity_id | UUID | ✓ | ID record bị thay đổi |
| old_value | JSONB | | Dữ liệu trước thay đổi |
| new_value | JSONB | | Dữ liệu sau thay đổi |
| ip_address | VARCHAR(45) | | |
| user_agent | VARCHAR(500) | | |
| created_at | TIMESTAMP | ✓ | auto, immutable |

#### Scenario: Ghi nhật ký thay đổi chứng từ
- **WHEN** user tạo/sửa/duyệt/hủy bất kỳ chứng từ nào
- **THEN** hệ thống ghi audit_log với old_value (trước) và new_value (sau), entity_type và entity_id

#### Scenario: Bảo vệ nhật ký
- **WHEN** bất kỳ ai (kể cả admin) cố sửa hoặc xóa audit_log
- **THEN** hệ thống SHALL từ chối — audit_log chỉ cho phép INSERT và SELECT

#### Scenario: Tra cứu nhật ký
- **WHEN** admin tra cứu audit_log với bộ lọc (user, thời gian, entity_type, action)
- **THEN** hệ thống hiển thị danh sách kết quả, cho phép xem chi tiết old/new value, xuất Excel/PDF

### Requirement: Cách ly dữ liệu multi-tenant
Hệ thống SHALL cách ly dữ liệu giữa các doanh nghiệp và chi nhánh.

#### Scenario: Cách ly theo doanh nghiệp
- **WHEN** user thuộc company_A truy vấn bất kỳ dữ liệu nào
- **THEN** hệ thống SHALL tự động lọc theo company_id = company_A, không trả về dữ liệu của company khác

#### Scenario: Cách ly theo chi nhánh
- **WHEN** user có data_permission chỉ cho branch_X
- **THEN** dữ liệu hiển thị SHALL chỉ bao gồm record có branch_id = branch_X hoặc branch_id IS NULL

#### Scenario: Bảo vệ dữ liệu đã khóa kỳ
- **WHEN** chứng từ có ngày thuộc fiscal_year.period đã is_closed = true
- **THEN** hệ thống SHALL chặn tạo mới, sửa, duyệt, hủy chứng từ trong kỳ đó (trừ khi user có quyền unlock_period)
