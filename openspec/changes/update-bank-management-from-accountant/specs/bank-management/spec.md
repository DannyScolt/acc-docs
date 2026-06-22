## MODIFIED Requirements

### Requirement: Use Case chi tiết phân hệ Tiền gửi ngân hàng
Spec `bank-management` SHALL được cập nhật với 33 UC (UC-BK-01 ~ UC-BK-33), 39 Business Rules (BR01 ~ BR39), bút toán chi tiết và workflow tổng thể.

**Thay đổi chính:**
1. Thêm entity fields: `posted_at`, `rejected_reason` cho bank_receipt và bank_payment (tương tự cash vouchers)
2. Thêm status values: `posted`, `period_locked`, `rejected` cho state machine 7 trạng thái
3. Thêm approval threshold: Chi NH ≥ 50 triệu cần 2 cấp duyệt (BR24)
4. Thêm bank statement matching: BR35 accuracy ≥ 80%, BR36 one-to-one match

#### Scenario: State machine 7 trạng thái cho chứng từ NH
- **WHEN** chứng từ NH được tạo
- **THEN** áp dụng state machine: Draft → Pending → Approved → Posted → Period Locked (+ Rejected, Cancelled)

#### Scenario: Hạn mức duyệt chi NH
- **WHEN** phiếu chi NH có số tiền ≥ 50 triệu
- **THEN** yêu cầu 2 cấp duyệt (BR24)

#### Scenario: Đối chiếu tự động sao kê
- **WHEN** hệ thống đối chiếu sao kê với CT
- **THEN** so khớp theo số tiền, ngày, nội dung, mã tham chiếu; độ chính xác ≥ 80% (BR35)
