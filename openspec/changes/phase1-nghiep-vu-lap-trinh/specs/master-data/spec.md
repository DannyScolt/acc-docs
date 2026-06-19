## ADDED Requirements

### Requirement: Hệ thống tài khoản kế toán (Account)
Hệ thống SHALL cho phép khai báo và quản lý hệ thống tài khoản kế toán theo cấu trúc cây cha-con.

**Entity: `account`**

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | UUID | ✓ | PK |
| company_id | UUID(FK) | ✓ | → company |
| code | VARCHAR(20) | ✓ | Unique trong company, vd: 111, 1111 |
| name | VARCHAR(255) | ✓ | |
| parent_id | UUID(FK) | | → account (tài khoản cha) |
| level | INTEGER | ✓ | 1 = tổng hợp, 2+ = chi tiết |
| nature | ENUM | ✓ | debit \| credit \| both |
| account_type | ENUM | ✓ | asset \| liability \| equity \| revenue \| expense |
| is_detail | BOOLEAN | ✓ | true = cho phép ghi sổ, false = chỉ tổng hợp |
| is_active | BOOLEAN | ✓ | Default: true |
| has_transactions | BOOLEAN | ✓ | Default: false (auto-update khi có phát sinh) |

#### Scenario: Tạo tài khoản con
- **WHEN** user thêm tài khoản chi tiết với parent_id trỏ đến tài khoản cha hợp lệ
- **THEN** hệ thống tạo account với level = parent.level + 1, code MUST bắt đầu bằng parent.code

#### Scenario: Không xóa tài khoản đã phát sinh
- **WHEN** user cố xóa tài khoản có has_transactions = true
- **THEN** hệ thống SHALL từ chối, chỉ cho phép ngừng sử dụng (is_active = false)

#### Scenario: Import hệ thống tài khoản
- **WHEN** user upload file Excel theo mẫu (code, name, parent_code, nature, account_type)
- **THEN** hệ thống validate tất cả dòng, báo lỗi nếu có (trùng code, parent không tồn tại), import thành công nếu không lỗi

### Requirement: Danh mục khách hàng (Customer)
Hệ thống SHALL cho phép quản lý danh mục khách hàng với phân nhóm, hạn mức công nợ và điều khoản thanh toán.

**Entity: `customer_group`**

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | UUID | ✓ | PK |
| company_id | UUID(FK) | ✓ | → company |
| code | VARCHAR(20) | ✓ | |
| name | VARCHAR(100) | ✓ | |

**Entity: `customer`**

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | UUID | ✓ | PK |
| company_id | UUID(FK) | ✓ | → company |
| code | VARCHAR(20) | ✓ | Unique trong company |
| name | VARCHAR(255) | ✓ | |
| tax_code | VARCHAR(20) | | |
| address | TEXT | | |
| contact_person | VARCHAR(100) | | |
| phone | VARCHAR(20) | | |
| email | VARCHAR(100) | | |
| group_id | UUID(FK) | | → customer_group |
| region | VARCHAR(100) | | Khu vực |
| credit_limit | DECIMAL(18,2) | | Hạn mức công nợ tối đa |
| payment_term_days | INTEGER | | Số ngày được nợ |
| payment_method | ENUM | | cash \| bank_transfer \| both |
| default_account_id | UUID(FK) | | → account (default: 131) |
| is_active | BOOLEAN | ✓ | Default: true |
| created_at | TIMESTAMP | ✓ | |
| updated_at | TIMESTAMP | ✓ | |

#### Scenario: Kiểm tra trùng mã số thuế
- **WHEN** user thêm khách hàng với tax_code đã tồn tại trong company
- **THEN** hệ thống cảnh báo "Mã số thuế trùng với khách hàng [tên]", cho phép tiếp tục nếu user xác nhận

#### Scenario: Ngừng theo dõi khách hàng
- **WHEN** user đặt is_active = false cho khách hàng
- **THEN** khách hàng SHALL không xuất hiện trong dropdown chọn khách hàng trên chứng từ mới, nhưng chứng từ/công nợ cũ vẫn hiển thị

#### Scenario: Kiểm tra hạn mức công nợ
- **WHEN** user tạo chứng từ làm tăng công nợ phải thu của khách hàng (ở Phase 3)
- **THEN** hệ thống kiểm tra tổng công nợ hiện tại + số tiền mới ≤ credit_limit, cảnh báo nếu vượt

### Requirement: Danh mục nhà cung cấp (Supplier)
Hệ thống SHALL cho phép quản lý danh mục nhà cung cấp tương tự khách hàng.

**Entity: `supplier_group`**

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | UUID | ✓ | PK |
| company_id | UUID(FK) | ✓ | → company |
| code | VARCHAR(20) | ✓ | |
| name | VARCHAR(100) | ✓ | |

**Entity: `supplier`**

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | UUID | ✓ | PK |
| company_id | UUID(FK) | ✓ | → company |
| code | VARCHAR(20) | ✓ | Unique trong company |
| name | VARCHAR(255) | ✓ | |
| tax_code | VARCHAR(20) | | |
| address | TEXT | | |
| contact_person | VARCHAR(100) | | |
| phone | VARCHAR(20) | | |
| email | VARCHAR(100) | | |
| group_id | UUID(FK) | | → supplier_group |
| payment_term_days | INTEGER | | Số ngày được nợ |
| payment_method | ENUM | | cash \| bank_transfer \| both |
| default_account_id | UUID(FK) | | → account (default: 331) |
| is_active | BOOLEAN | ✓ | Default: true |
| created_at | TIMESTAMP | ✓ | |
| updated_at | TIMESTAMP | ✓ | |

#### Scenario: Kiểm tra trùng mã số thuế NCC
- **WHEN** user thêm nhà cung cấp với tax_code đã tồn tại
- **THEN** hệ thống cảnh báo, cho phép tiếp tục nếu user xác nhận

#### Scenario: Import nhà cung cấp từ Excel
- **WHEN** user upload file Excel theo mẫu
- **THEN** hệ thống validate (trùng code, tax_code format), import thành công nếu không lỗi

### Requirement: Danh mục nhân viên (Employee)
Hệ thống SHALL cho phép quản lý danh mục nhân viên và liên kết với tài khoản người dùng.

**Entity: `employee`**

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | UUID | ✓ | PK |
| company_id | UUID(FK) | ✓ | → company |
| code | VARCHAR(20) | ✓ | Unique trong company |
| full_name | VARCHAR(100) | ✓ | |
| department_id | UUID(FK) | | → department |
| position | VARCHAR(100) | | Chức vụ |
| phone | VARCHAR(20) | | |
| email | VARCHAR(100) | | |
| is_active | BOOLEAN | ✓ | Default: true |

#### Scenario: Liên kết nhân viên với user
- **WHEN** admin gắn employee_id vào user
- **THEN** user.employee_id → employee, khi user tạo chứng từ tạm ứng, hệ thống tự gắn employee

### Requirement: Danh mục hàng hóa, vật tư, dịch vụ (Product)
Hệ thống SHALL cho phép quản lý danh mục hàng hóa với nhiều đơn vị tính, giá bán, định mức tồn kho và tài khoản hạch toán mặc định.

**Entity: `product_group`**

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | UUID | ✓ | PK |
| company_id | UUID(FK) | ✓ | → company |
| code | VARCHAR(20) | ✓ | |
| name | VARCHAR(100) | ✓ | |
| parent_id | UUID(FK) | | → product_group (cây) |

**Entity: `product`**

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | UUID | ✓ | PK |
| company_id | UUID(FK) | ✓ | → company |
| code | VARCHAR(30) | ✓ | Unique trong company |
| name | VARCHAR(255) | ✓ | |
| product_type | ENUM | ✓ | goods \| material \| service |
| group_id | UUID(FK) | | → product_group |
| primary_unit | VARCHAR(20) | ✓ | Đơn vị tính chính |
| default_price | DECIMAL(18,2) | | Giá bán mặc định |
| min_stock | DECIMAL(18,4) | | Tồn tối thiểu |
| max_stock | DECIMAL(18,4) | | Tồn tối đa |
| inventory_account_id | UUID(FK) | | → account (156 / 152) |
| cogs_account_id | UUID(FK) | | → account (632) |
| revenue_account_id | UUID(FK) | | → account (511) |
| expense_account_id | UUID(FK) | | → account (641/642) |
| is_active | BOOLEAN | ✓ | Default: true |

**Entity: `product_unit`** (đơn vị tính quy đổi)

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | UUID | ✓ | PK |
| product_id | UUID(FK) | ✓ | → product |
| unit_name | VARCHAR(20) | ✓ | vd: thùng, hộp |
| conversion_rate | DECIMAL(18,6) | ✓ | 1 unit này = ? primary_unit |

#### Scenario: Quy đổi đơn vị tính
- **WHEN** user chọn đơn vị tính phụ khi nhập chứng từ
- **THEN** hệ thống tự quy đổi về đơn vị tính chính theo conversion_rate

#### Scenario: Cảnh báo tồn kho
- **WHEN** tồn kho của product tại warehouse < min_stock hoặc > max_stock
- **THEN** hệ thống hiển thị cảnh báo trên dashboard và danh sách tồn kho

### Requirement: Danh mục kho (Warehouse)
Hệ thống SHALL cho phép quản lý danh mục kho và phân quyền theo kho.

**Entity: `warehouse`**

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | UUID | ✓ | PK |
| company_id | UUID(FK) | ✓ | → company |
| code | VARCHAR(20) | ✓ | Unique trong company |
| name | VARCHAR(100) | ✓ | |
| address | TEXT | | |
| manager_employee_id | UUID(FK) | | → employee |
| is_default | BOOLEAN | ✓ | Default: false |
| is_active | BOOLEAN | ✓ | Default: true |

#### Scenario: Chỉ 1 kho mặc định
- **WHEN** user đặt is_default = true cho 1 kho
- **THEN** hệ thống tự set is_default = false cho các kho khác trong company

### Requirement: Danh mục tài khoản ngân hàng (BankAccount)
Hệ thống SHALL cho phép quản lý tài khoản ngân hàng của doanh nghiệp.

**Entity: `bank_account`**

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | UUID | ✓ | PK |
| company_id | UUID(FK) | ✓ | → company |
| account_number | VARCHAR(30) | ✓ | Số tài khoản |
| bank_name | VARCHAR(100) | ✓ | |
| branch_name | VARCHAR(100) | | Chi nhánh NH |
| account_holder | VARCHAR(100) | ✓ | Chủ tài khoản |
| currency | VARCHAR(3) | ✓ | Default: VND |
| accounting_account_id | UUID(FK) | ✓ | → account (112x) |
| is_default | BOOLEAN | ✓ | Default: false |
| is_active | BOOLEAN | ✓ | Default: true |

#### Scenario: Gắn tài khoản kế toán
- **WHEN** user tạo bank_account và chọn accounting_account_id
- **THEN** mọi chứng từ thu/chi NH liên quan bank_account này SHALL dùng accounting_account_id làm TK tiền gửi

### Requirement: Danh mục khoản mục chi phí (ExpenseCategory)
Hệ thống SHALL cho phép khai báo khoản mục chi phí theo cấu trúc cây cha-con.

**Entity: `expense_category`**

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | UUID | ✓ | PK |
| company_id | UUID(FK) | ✓ | → company |
| code | VARCHAR(20) | ✓ | |
| name | VARCHAR(100) | ✓ | |
| parent_id | UUID(FK) | | → expense_category |
| is_active | BOOLEAN | ✓ | Default: true |

#### Scenario: Phân cấp khoản mục chi phí
- **WHEN** user tạo khoản mục chi phí con với parent_id hợp lệ
- **THEN** hệ thống tạo node con, code MUST unique trong company
