## 1. Proposal & scope alignment

- [x] 1.1 Rà soát và chốt phạm vi mở rộng của module Số dư đầu kỳ trong proposal
- [x] 1.2 Chốt các điểm lệch cần làm rõ giữa tài liệu nghiệp vụ và tài liệu kỹ thuật (due_date, tiền mặt/ngân hàng đầu kỳ, mở khóa)

## 2. Business specification updates

- [x] 2.1 Mở rộng bảng chức năng tại mục `2.2.10. Số dư đầu kỳ` trong `ACC-noi-dung-nghiep-vu-theo-phase.html`
- [x] 2.2 Bổ sung Use Case chi tiết cho “Nhập số dư đầu kỳ” gồm actor, điều kiện tiên quyết, luồng chính và luồng ngoại lệ
- [x] 2.3 Bổ sung đầy đủ Business Rules cho quyền thao tác, import, đối chiếu, khóa/mở khóa và audit log

## 3. Technical specification updates

- [x] 3.1 Cập nhật chương `Số dư đầu kỳ` trong `Phase1-nghiep-vu-lap-trinh.html` để phản ánh các chức năng quản lý dữ liệu còn thiếu
- [x] 3.2 Bổ sung rõ luồng nhập và đối chiếu cho tiền mặt đầu kỳ và số dư ngân hàng đầu kỳ
- [x] 3.3 Đồng bộ lại các rule skeleton Phase 1 với AR/AP/tồn kho/TSCĐ/CCDC/CPTT và giữ rõ ranh giới phase sau

## 4. Verification & consistency review

- [x] 4.1 Kiểm tra chéo list chức năng, use case, rules và technical spec để tránh mâu thuẫn nội bộ
- [x] 4.2 Kiểm tra các role/quyền liên quan đến khóa và mở khóa phù hợp với RBAC đã mô tả
- [x] 4.3 Review lại tài liệu cuối cùng theo góc nhìn BA/dev/QA trước khi apply
