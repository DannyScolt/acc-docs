## ADDED Requirements

### Requirement: Báo cáo thu chi theo khoản mục
Hệ thống SHALL cung cấp báo cáo phân tích thu chi theo khoản mục (mục đích sử dụng tiền).

**Nguồn dữ liệu:** cash_receipt + cash_payment (đã ghi sổ), grouped by expense_category

**Bộ lọc:** Kỳ, Khoản mục, Loại (thu/chi)

#### Scenario: Xem báo cáo thu chi theo khoản mục
- **WHEN** user chọn kỳ và bấm xem báo cáo
- **THEN** hiển thị bảng: Khoản mục, Tổng thu, Tổng chi, Chênh lệch, drill-down → bảng kê chi tiết

### Requirement: Báo cáo thu chi theo đối tượng
Hệ thống SHALL cung cấp báo cáo phân tích thu chi theo đối tượng (KH, NCC, NV).

**Nguồn dữ liệu:** cash_receipt + cash_payment (đã ghi sổ), grouped by customer/supplier/employee

**Bộ lọc:** Kỳ, Loại đối tượng, Đối tượng cụ thể

#### Scenario: Xem báo cáo thu chi theo đối tượng
- **WHEN** user chọn loại đối tượng và kỳ
- **THEN** hiển thị bảng: Đối tượng, Tổng thu, Tổng chi, Số dư, drill-down → phiếu thu/chi

### Requirement: Báo cáo chênh lệch kiểm kê
Hệ thống SHALL cung cấp báo cáo theo dõi chênh lệch qua các đợt kiểm kê quỹ.

**Nguồn dữ liệu:** cash_inventory (đã duyệt)

**Bộ lọc:** Kỳ, Quỹ

#### Scenario: Xem báo cáo chênh lệch kiểm kê
- **WHEN** user chọn kỳ
- **THEN** hiển thị bảng: Ngày kiểm kê, Tồn sổ, Tồn thực tế, Chênh lệch, Trạng thái điều chỉnh

### Requirement: Dashboard quỹ
Hệ thống SHALL cung cấp Dashboard quỹ hiển thị tổng quan tình hình quỹ realtime.

**Nội dung dashboard:**
- Tồn quỹ hiện tại (realtime)
- Biểu đồ thu chi theo thời gian
- Top đối tượng thu/chi
- Cảnh báo quỹ thấp (nếu bật cấu hình)

**Actor:** Ban giám đốc

#### Scenario: Xem dashboard quỹ
- **WHEN** Ban giám đốc mở Dashboard quỹ
- **THEN** hiển thị tổng quan quỹ cập nhật realtime theo BR-BC05
