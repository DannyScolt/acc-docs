## ADDED Requirements

### Requirement: Nhập số dư tài khoản đầu kỳ (OpeningBalance)
Hệ thống SHALL cho phép nhập số dư Nợ / Có đầu kỳ cho từng tài khoản kế toán.

**Entity: `opening_balance`**

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | UUID | ✓ | PK |
| company_id | UUID(FK) | ✓ | → company |
| fiscal_year_id | UUID(FK) | ✓ | → fiscal_year |
| account_id | UUID(FK) | ✓ | → account |
| debit_amount | DECIMAL(18,2) | ✓ | Default: 0 |
| credit_amount | DECIMAL(18,2) | ✓ | Default: 0 |
| is_locked | BOOLEAN | ✓ | Default: false |

**Validation:**
- Mỗi tài khoản chỉ có 1 record opening_balance per fiscal_year
- Tài khoản có nature = debit → credit_amount MUST = 0, và ngược lại
- Tài khoản nature = both → cho phép cả 2

#### Scenario: Nhập số dư đầu kỳ
- **WHEN** kế toán nhập debit_amount hoặc credit_amount cho 1 tài khoản
- **THEN** hệ thống ghi nhận và hiển thị trong bảng cân đối số dư đầu kỳ

#### Scenario: Kiểm tra cân đối số dư
- **WHEN** kế toán yêu cầu kiểm tra cân đối
- **THEN** hệ thống kiểm tra: SUM(debit_amount) = SUM(credit_amount) cho tất cả opening_balance; nếu lệch → hiển thị chênh lệch và danh sách tài khoản

#### Scenario: Khóa số dư đầu kỳ
- **WHEN** kế toán trưởng xác nhận đúng và khóa
- **THEN** tất cả opening_balance của fiscal_year đó set is_locked = true, không cho sửa nữa

### Requirement: Công nợ phải thu đầu kỳ chi tiết (ARInvoiceOpening)
Hệ thống SHALL cho phép nhập công nợ phải thu chi tiết theo từng khách hàng và từng hóa đơn.

**Entity: `ar_invoice_opening`** (skeleton — sẽ mở rộng ở Phase 3)

| Field | Type | Required | Phase 1 | Mở rộng ở |
|-------|------|----------|---------|-----------|
| id | UUID | ✓ | ✓ | |
| company_id | UUID(FK) | ✓ | ✓ | |
| fiscal_year_id | UUID(FK) | ✓ | ✓ | |
| customer_id | UUID(FK) | ✓ | ✓ | |
| invoice_number | VARCHAR(50) | ✓ | ✓ | |
| invoice_date | DATE | ✓ | ✓ | |
| due_date | DATE | | ✓ | Phase 3 → tính tuổi nợ |
| original_amount | DECIMAL(18,2) | ✓ | ✓ | |
| paid_amount | DECIMAL(18,2) | ✓ | ✓ (default 0) | Phase 3 → auto-update khi thu tiền |
| remaining_amount | DECIMAL(18,2) | ✓ | ✓ (= original - paid) | Phase 3 → auto-calc |
| account_id | UUID(FK) | ✓ | ✓ (default 131) | |
| currency | VARCHAR(3) | ✓ | ✓ (default VND) | Phase 3 → ngoại tệ |
| description | TEXT | | ✓ | |

**Cân đối:** SUM(remaining_amount) GROUP BY customer_id MUST = opening_balance WHERE account = 131 per customer (nếu theo dõi chi tiết)

#### Scenario: Nhập công nợ phải thu chi tiết
- **WHEN** kế toán nhập thông tin hóa đơn (invoice_number, invoice_date, original_amount, due_date) cho 1 khách hàng
- **THEN** hệ thống tạo ar_invoice_opening, tự tính remaining_amount = original_amount - paid_amount

#### Scenario: Kiểm tra cân đối công nợ phải thu
- **WHEN** kế toán yêu cầu kiểm tra
- **THEN** SUM(remaining_amount) theo customer MUST khớp với opening_balance của TK 131 chi tiết theo customer; lệch → hiển thị danh sách chênh lệch

#### Scenario: Import công nợ phải thu từ Excel
- **WHEN** kế toán upload file Excel theo mẫu (customer_code, invoice_number, invoice_date, due_date, original_amount, paid_amount)
- **THEN** hệ thống validate (customer tồn tại, amount > 0, date hợp lệ), import thành công nếu không lỗi

### Requirement: Công nợ phải trả đầu kỳ chi tiết (APInvoiceOpening)
Hệ thống SHALL cho phép nhập công nợ phải trả chi tiết theo từng nhà cung cấp và từng hóa đơn.

**Entity: `ap_invoice_opening`** (skeleton — sẽ mở rộng ở Phase 2)

| Field | Type | Required | Phase 1 | Mở rộng ở |
|-------|------|----------|---------|-----------|
| id | UUID | ✓ | ✓ | |
| company_id | UUID(FK) | ✓ | ✓ | |
| fiscal_year_id | UUID(FK) | ✓ | ✓ | |
| supplier_id | UUID(FK) | ✓ | ✓ | |
| invoice_number | VARCHAR(50) | ✓ | ✓ | |
| invoice_date | DATE | ✓ | ✓ | |
| due_date | DATE | | ✓ | Phase 2 → tính tuổi nợ |
| original_amount | DECIMAL(18,2) | ✓ | ✓ | |
| paid_amount | DECIMAL(18,2) | ✓ | ✓ (default 0) | Phase 2 → auto-update khi thanh toán |
| remaining_amount | DECIMAL(18,2) | ✓ | ✓ (= original - paid) | Phase 2 → auto-calc |
| account_id | UUID(FK) | ✓ | ✓ (default 331) | |
| currency | VARCHAR(3) | ✓ | ✓ (default VND) | |
| description | TEXT | | ✓ | |

#### Scenario: Nhập công nợ phải trả chi tiết
- **WHEN** kế toán nhập thông tin hóa đơn NCC
- **THEN** hệ thống tạo ap_invoice_opening với remaining_amount = original_amount - paid_amount

#### Scenario: Kiểm tra cân đối công nợ phải trả
- **WHEN** kế toán yêu cầu kiểm tra
- **THEN** SUM(remaining_amount) theo supplier MUST khớp opening_balance TK 331 chi tiết theo supplier

### Requirement: Tồn kho đầu kỳ (InventoryOpening)
Hệ thống SHALL cho phép nhập số lượng, đơn giá, giá trị tồn đầu kỳ theo từng kho và từng mặt hàng.

**Entity: `inventory_opening`** (skeleton — sẽ mở rộng ở Phase 2)

| Field | Type | Required | Phase 1 | Mở rộng ở |
|-------|------|----------|---------|-----------|
| id | UUID | ✓ | ✓ | |
| company_id | UUID(FK) | ✓ | ✓ | |
| fiscal_year_id | UUID(FK) | ✓ | ✓ | |
| warehouse_id | UUID(FK) | ✓ | ✓ | |
| product_id | UUID(FK) | ✓ | ✓ | |
| quantity | DECIMAL(18,4) | ✓ | ✓ | Phase 2 → auto-update nhập/xuất |
| unit_cost | DECIMAL(18,4) | ✓ | ✓ | Phase 2 → recalc theo costing_method |
| total_value | DECIMAL(18,2) | ✓ | ✓ (= qty × unit_cost) | |
| account_id | UUID(FK) | ✓ | ✓ (156/152) | |

**Cân đối:** SUM(total_value) MUST = opening_balance WHERE account IN (152, 156)

#### Scenario: Nhập tồn kho đầu kỳ
- **WHEN** kế toán nhập quantity và unit_cost cho product tại warehouse
- **THEN** hệ thống tính total_value = quantity × unit_cost, tạo inventory_opening

#### Scenario: Kiểm tra cân đối tồn kho
- **WHEN** kế toán kiểm tra cân đối
- **THEN** SUM(total_value) theo account MUST khớp opening_balance cho TK 152/156

### Requirement: Tài sản cố định đầu kỳ (FixedAssetOpening)
Hệ thống SHALL cho phép nhập nguyên giá, hao mòn lũy kế, giá trị còn lại của TSCĐ.

**Entity: `fixed_asset_opening`** (skeleton — sẽ mở rộng ở Phase 6)

| Field | Type | Required | Phase 1 | Mở rộng ở |
|-------|------|----------|---------|-----------|
| id | UUID | ✓ | ✓ | |
| company_id | UUID(FK) | ✓ | ✓ | |
| fiscal_year_id | UUID(FK) | ✓ | ✓ | |
| asset_code | VARCHAR(30) | ✓ | ✓ | |
| asset_name | VARCHAR(255) | ✓ | ✓ | |
| category | VARCHAR(100) | | ✓ | Phase 6 → danh mục TSCĐ chi tiết |
| department_id | UUID(FK) | | ✓ | Phase 6 → điều chuyển |
| purchase_date | DATE | | ✓ | |
| start_depreciation_date | DATE | | ✓ | Phase 6 → tính khấu hao |
| useful_life_months | INTEGER | | ✓ | Phase 6 → tính khấu hao |
| original_cost | DECIMAL(18,2) | ✓ | ✓ | |
| accumulated_depreciation | DECIMAL(18,2) | ✓ | ✓ | Phase 6 → auto-update |
| net_book_value | DECIMAL(18,2) | ✓ | ✓ (= original - accumulated) | Phase 6 → auto-calc |
| asset_account_id | UUID(FK) | ✓ | ✓ (211) | |
| depreciation_account_id | UUID(FK) | ✓ | ✓ (2141) | |

#### Scenario: Nhập TSCĐ đầu kỳ
- **WHEN** kế toán nhập asset_code, asset_name, original_cost, accumulated_depreciation
- **THEN** hệ thống tính net_book_value = original_cost - accumulated_depreciation

#### Scenario: Kiểm tra cân đối TSCĐ
- **WHEN** kế toán kiểm tra
- **THEN** SUM(original_cost) MUST khớp opening_balance TK 211, SUM(accumulated_depreciation) MUST khớp TK 2141

### Requirement: Công cụ dụng cụ đầu kỳ (ToolOpening)
Hệ thống SHALL cho phép nhập giá trị ban đầu, giá trị đã phân bổ, giá trị còn lại của CCDC.

**Entity: `tool_opening`** (skeleton — sẽ mở rộng ở Phase 6)

| Field | Type | Required | Phase 1 | Mở rộng ở |
|-------|------|----------|---------|-----------|
| id | UUID | ✓ | ✓ | |
| company_id | UUID(FK) | ✓ | ✓ | |
| fiscal_year_id | UUID(FK) | ✓ | ✓ | |
| tool_code | VARCHAR(30) | ✓ | ✓ | |
| tool_name | VARCHAR(255) | ✓ | ✓ | |
| department_id | UUID(FK) | | ✓ | |
| original_value | DECIMAL(18,2) | ✓ | ✓ | |
| allocated_value | DECIMAL(18,2) | ✓ | ✓ | Phase 6 → auto-update |
| remaining_value | DECIMAL(18,2) | ✓ | ✓ (= original - allocated) | |
| allocation_months | INTEGER | | ✓ | Phase 6 → phân bổ định kỳ |
| account_id | UUID(FK) | ✓ | ✓ (153/242) | |

#### Scenario: Nhập CCDC đầu kỳ
- **WHEN** kế toán nhập tool_code, tool_name, original_value, allocated_value
- **THEN** hệ thống tính remaining_value = original_value - allocated_value

### Requirement: Chi phí trả trước đầu kỳ (PrepaidOpening)
Hệ thống SHALL cho phép nhập giá trị còn lại và thời gian phân bổ của chi phí trả trước.

**Entity: `prepaid_opening`** (skeleton — sẽ mở rộng ở Phase 6)

| Field | Type | Required | Phase 1 | Mở rộng ở |
|-------|------|----------|---------|-----------|
| id | UUID | ✓ | ✓ | |
| company_id | UUID(FK) | ✓ | ✓ | |
| fiscal_year_id | UUID(FK) | ✓ | ✓ | |
| code | VARCHAR(30) | ✓ | ✓ | |
| name | VARCHAR(255) | ✓ | ✓ | |
| original_value | DECIMAL(18,2) | ✓ | ✓ | |
| allocated_value | DECIMAL(18,2) | ✓ | ✓ | Phase 6 → auto-update |
| remaining_value | DECIMAL(18,2) | ✓ | ✓ | |
| remaining_months | INTEGER | | ✓ | Phase 6 → phân bổ định kỳ |
| expense_account_id | UUID(FK) | | ✓ | Phase 6 → TK chi phí đích |
| account_id | UUID(FK) | ✓ | ✓ (242) | |

#### Scenario: Nhập chi phí trả trước đầu kỳ
- **WHEN** kế toán nhập code, name, original_value, allocated_value, remaining_months
- **THEN** hệ thống tính remaining_value = original_value - allocated_value

#### Scenario: Import tất cả số dư đầu kỳ từ Excel
- **WHEN** kế toán upload file Excel tổng hợp theo mẫu (bao gồm tất cả loại: TK tổng hợp, công nợ, tồn kho, TSCĐ, CCDC, chi phí trả trước)
- **THEN** hệ thống phân tách theo loại, validate, import vào các bảng tương ứng
