## MODIFIED Requirements

### Requirement: State machine chứng từ quỹ
Hệ thống SHALL sử dụng state machine 5+2 trạng thái cho chứng từ quỹ (phiếu thu, phiếu chi), thay vì 4 trạng thái hiện tại.

**Trạng thái chính (5):**
1. Nháp (draft)
2. Chờ duyệt (pending_approval)
3. Đã duyệt (approved)
4. Đã ghi sổ (posted) — MỚI
5. Đã khóa kỳ (period_locked) — MỚI

**Trạng thái phụ (2):**
- Từ chối (rejected) — MỚI, từ Chờ duyệt quay về
- Đã hủy (cancelled) — từ Nháp hoặc Chờ duyệt

**Chuyển đổi:**
- draft → pending_approval (gửi duyệt)
- pending_approval → approved (duyệt)
- pending_approval → rejected (từ chối)
- approved → posted (ghi sổ)
- posted → period_locked (khóa kỳ)
- draft → cancelled (hủy)
- pending_approval → cancelled (hủy)

#### Scenario: Chuyển trạng thái ghi sổ
- **WHEN** chứng từ ở trạng thái approved
- **THEN** hệ thống cho phép chuyển sang posted, sinh journal_entry

#### Scenario: Chuyển trạng thái khóa kỳ
- **WHEN** chứng từ ở trạng thái posted và kế toán trưởng khóa kỳ
- **THEN** chứng từ chuyển sang period_locked, không cho sửa/xóa/hủy

#### Scenario: Từ chối duyệt
- **WHEN** người duyệt từ chối chứng từ pending_approval
- **THEN** chứng từ chuyển sang rejected, bắt buộc nhập lý do từ chối

### Requirement: Payment type mới — refund_return
Entity `cash_payment` SHALL hỗ trợ thêm payment_type = `refund_return` cho nghiệp vụ "Chi hoàn tiền khách hàng".

**Side effects khi duyệt:**
- Sinh journal_entry: Nợ `[CẦN KẾ TOÁN XÁC NHẬN: 131 hay TK khác?]` / Có 111
- Có thể liên kết đến customer_id (giảm công nợ phải thu hoặc ghi nhận chi phí)

#### Scenario: Lập phiếu chi hoàn tiền KH
- **WHEN** user tạo phiếu chi với payment_type = refund_return
- **THEN** bắt buộc chọn customer_id, hệ thống gợi ý TK đối ứng

### Requirement: Entity cash_inventory_denomination
Hệ thống SHALL hỗ trợ entity mới `cash_inventory_denomination` để kiểm kê chi tiết theo mệnh giá.

| Field | Type | Required | Ghi chú |
|-------|------|----------|---------|
| id | UUID | YES | PK |
| cash_inventory_id | UUID(FK) | YES | → cash_inventory |
| denomination | DECIMAL(18,2) | YES | Mệnh giá (500000, 200000, 100000...) |
| quantity | INTEGER | YES | Số lượng tờ/đồng |
| amount | DECIMAL(18,2) | YES | = denomination × quantity |

#### Scenario: Nhập kiểm kê theo mệnh giá
- **WHEN** thủ quỹ kiểm kê quỹ
- **THEN** nhập số lượng cho từng mệnh giá, hệ thống tính tổng tự động
