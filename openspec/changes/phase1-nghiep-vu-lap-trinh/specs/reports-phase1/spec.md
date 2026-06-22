## ADDED Requirements

### Requirement: Báo cáo quỹ tiền mặt
Hệ thống SHALL cung cấp các báo cáo liên quan quỹ tiền mặt.

| Báo cáo | Nguồn dữ liệu | Bộ lọc | Drill-down |
|----------|---------------|--------|------------|
| Sổ quỹ tiền mặt | cash_receipt (approved) + cash_payment (approved) | Ngày, KH/NCC, nhân viên | → phiếu thu/chi |
| Bảng kê phiếu thu | cash_receipt | Kỳ, trạng thái, receipt_type | → phiếu thu |
| Bảng kê phiếu chi | cash_payment | Kỳ, trạng thái, payment_type | → phiếu chi |
| Báo cáo tồn quỹ | opening_balance(111) + cash_receipt - cash_payment | Ngày | — |
| Báo cáo dòng tiền tiền mặt | cash_receipt + cash_payment grouped by type | Kỳ | → bảng kê |
| Báo cáo thu chi theo khoản mục | cash_receipt + cash_payment grouped by expense_category | Kỳ, Khoản mục, Loại | → bảng kê chi tiết |
| Báo cáo thu chi theo đối tượng | cash_receipt + cash_payment grouped by customer/supplier/employee | Kỳ, Loại đối tượng | → phiếu thu/chi |
| Báo cáo chênh lệch kiểm kê | cash_inventory (approved) | Kỳ, Quỹ | — |
| Dashboard quỹ | Tổng hợp realtime | — | — |

**Công thức tồn quỹ:**
```
Tồn cuối = Opening(111) + SUM(approved receipts in period) - SUM(approved payments in period)
```

#### Scenario: Xuất sổ quỹ tiền mặt
- **WHEN** user chọn khoảng thời gian và bấm xuất
- **THEN** hệ thống xuất Excel/PDF chứa: tồn đầu kỳ, danh sách phát sinh (ngày, số CT, diễn giải, thu, chi, tồn lũy kế), tồn cuối kỳ

#### Scenario: Lọc sổ quỹ theo đối tượng
- **WHEN** user lọc theo customer_id hoặc supplier_id
- **THEN** chỉ hiển thị phiếu thu/chi liên quan đối tượng đó

#### Scenario: Xem báo cáo thu chi theo khoản mục
- **WHEN** user chọn kỳ và bấm xem báo cáo
- **THEN** hiển thị bảng: Khoản mục, Tổng thu, Tổng chi, Chênh lệch, drill-down → bảng kê chi tiết

#### Scenario: Xem báo cáo thu chi theo đối tượng
- **WHEN** user chọn loại đối tượng và kỳ
- **THEN** hiển thị bảng: Đối tượng, Tổng thu, Tổng chi, Số dư, drill-down → phiếu thu/chi

#### Scenario: Xem báo cáo chênh lệch kiểm kê
- **WHEN** user chọn kỳ
- **THEN** hiển thị bảng: Ngày kiểm kê, Tồn sổ, Tồn thực tế, Chênh lệch, Trạng thái điều chỉnh

#### Scenario: Xem dashboard quỹ
- **WHEN** Ban giám đốc mở Dashboard quỹ
- **THEN** hiển thị: Tồn quỹ hiện tại (realtime), biểu đồ thu chi theo thời gian, top đối tượng thu/chi, cảnh báo quỹ thấp (nếu bật cấu hình)

### Requirement: Báo cáo tiền gửi ngân hàng
Hệ thống SHALL cung cấp các báo cáo liên quan tiền gửi ngân hàng.

| Báo cáo | Nguồn dữ liệu | Bộ lọc | Drill-down |
|----------|---------------|--------|------------|
| Sổ tiền gửi ngân hàng | bank_receipt + bank_payment + bank_transfer (approved) | TK NH, ngày | → chứng từ NH |
| Bảng kê thu ngân hàng | bank_receipt | Kỳ, TK NH, trạng thái | → chứng từ thu NH |
| Bảng kê chi ngân hàng | bank_payment | Kỳ, TK NH, trạng thái | → chứng từ chi NH |
| Báo cáo số dư NH | opening_balance(112x) + receipts - payments | TK NH | — |
| Báo cáo GD chưa đối chiếu | bank_statement_line WHERE is_matched = false | TK NH, kỳ | → sao kê |

**Công thức số dư NH:**
```
Số dư cuối = Opening(112x) + SUM(approved bank receipts) - SUM(approved bank payments) ± transfers
```

#### Scenario: Xem sổ tiền gửi theo tài khoản NH
- **WHEN** user chọn bank_account và khoảng thời gian
- **THEN** hiển thị: tồn đầu kỳ, danh sách phát sinh (thu, chi, chuyển), tồn cuối kỳ theo TK NH đó

#### Scenario: Báo cáo giao dịch chưa đối chiếu
- **WHEN** user xem báo cáo GD chưa đối chiếu
- **THEN** hiển thị 2 phần: (1) chứng từ kế toán chưa khớp sao kê, (2) giao dịch sao kê chưa khớp chứng từ

### Requirement: Báo cáo sổ cái & cân đối
Hệ thống SHALL cung cấp các báo cáo kế toán tổng hợp.

| Báo cáo | Nguồn dữ liệu | Bộ lọc | Drill-down |
|----------|---------------|--------|------------|
| Sổ cái | journal_entry_line | TK, kỳ, đối tượng | → chứng từ gốc |
| Nhật ký chung | journal_entry + lines | Ngày, loại CT, TK | → chứng từ gốc |
| Cân đối phát sinh | journal_entry_line (aggregated) | Kỳ | → sổ cái TK |

#### Scenario: Xuất sổ cái
- **WHEN** user chọn tài khoản, kỳ và bấm xuất Excel/PDF
- **THEN** file xuất chứa: tên TK, số dư đầu kỳ, danh sách bút toán (ngày CT, số CT, diễn giải, TK đối ứng, Nợ, Có), cộng phát sinh, số dư cuối kỳ

#### Scenario: Xuất bảng cân đối phát sinh
- **WHEN** user chọn kỳ và bấm xuất
- **THEN** file xuất chứa: bảng tất cả TK với cột Dư đầu kỳ Nợ/Có, Phát sinh Nợ/Có, Dư cuối kỳ Nợ/Có, dòng tổng cộng (Nợ = Có)

### Requirement: Format xuất báo cáo
Hệ thống SHALL hỗ trợ xuất tất cả báo cáo ra Excel và PDF.

#### Scenario: Xuất Excel
- **WHEN** user bấm "Xuất Excel" trên bất kỳ báo cáo nào
- **THEN** hệ thống tạo file .xlsx với header = tên báo cáo + bộ lọc, body = dữ liệu bảng, footer = dòng tổng cộng

#### Scenario: Xuất PDF
- **WHEN** user bấm "Xuất PDF"
- **THEN** hệ thống tạo file .pdf với layout phù hợp in A4, có header doanh nghiệp, tên báo cáo, bảng dữ liệu, chữ ký (nếu cần)

#### Scenario: In phiếu thu/chi
- **WHEN** user bấm "In" trên phiếu thu hoặc phiếu chi
- **THEN** hệ thống hiển thị preview theo mẫu phiếu thu/chi chuẩn kế toán, cho phép in
