## Why

Phần **2.5 Sổ cái & hệ thống tài khoản** trong HTML hiện mới dừng ở mức bảng chức năng tóm tắt, trong khi tài liệu kế toán bổ sung đã mô tả chi tiết hơn cho 4 phân hệ con: ghi sổ kế toán, sổ cái, nhật ký chung và bảng cân đối phát sinh. Cần cập nhật để tài liệu Phase 1 phản ánh đầy đủ mục tiêu, actor, luồng chính, kết quả và business rules của phân hệ sổ cái, đồng bộ với mức chi tiết đã áp dụng cho phần 2.3 và 2.4.

## What Changes

- Viết lại section **2.5.1 Ghi sổ kế toán** từ bảng chức năng thành nội dung chi tiết gồm: Mục tiêu, Actor, Chức năng, Luồng chính 9 bước, Kết quả và BR-GL-01 ~ BR-GL-07.
- Viết lại section **2.5.2 Sổ cái** thành nội dung chi tiết gồm: Mục tiêu, Actor, Chức năng, Luồng chính 8 bước, Kết quả và BR-LEDGER-01 ~ BR-LEDGER-04.
- Viết lại section **2.5.3 Sổ nhật ký chung** thành nội dung chi tiết gồm: Mục tiêu, Actor, Chức năng, Luồng chính 6 bước, Kết quả và BR-JE-01 ~ BR-JE-04.
- Viết lại section **2.5.4 Bảng cân đối phát sinh** thành nội dung chi tiết gồm: Mục tiêu, Actor, Chức năng, Luồng chính 9 bước, Kết quả và BR-TB-01 ~ BR-TB-04.
- Thêm section **Business Rules toàn phân hệ Sổ cái & hệ thống tài khoản** với BR-GLOBAL-01 ~ BR-GLOBAL-20.
- Cập nhật spec `general-ledger` để bổ sung các yêu cầu chi tiết tương ứng với nội dung HTML mới, bao gồm các actor, luồng nghiệp vụ, điều kiện kiểm soát kỳ kế toán, truy vết chứng từ nguồn, đa chi nhánh / đa đơn vị hạch toán và các ràng buộc business rules toàn phân hệ.

## Capabilities

### New Capabilities
- `general-ledger-update`: Cập nhật toàn bộ section 2.5 HTML từ bản tóm tắt sang format đặc tả chi tiết theo tài liệu kế toán bổ sung.

### Modified Capabilities
- `general-ledger`: Mở rộng requirement của phân hệ sổ cái để phản ánh chi tiết 4 phân hệ con (ghi sổ, sổ cái, nhật ký chung, bảng cân đối phát sinh) và bộ business rules toàn phân hệ.

## Impact

- **HTML**: `ACC-noi-dung-nghiep-vu-theo-phase.html` section 2.5 sẽ được viết lại toàn bộ theo format chi tiết.
- **Spec**: `openspec/changes/phase1-nghiep-vu-lap-trinh/specs/general-ledger/spec.md` là nguồn tham chiếu hiện có và cần được mở rộng bằng delta spec trong change mới.
- **Phạm vi không đổi**: Không thay đổi section 2.4 (tiền gửi ngân hàng), bảng định khoản mẫu, hay các section Phase 2 trở đi ngoài việc giữ ranh giới hiển thị đúng sau 2.5.
