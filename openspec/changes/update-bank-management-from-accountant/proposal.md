## Why

Kế toán Nguyễn Phú Quý gửi file `phase1.docx` bổ sung chi tiết phần **2.4 Tiền gửi ngân hàng** với 33 Use Case (UC-BK-01 ~ UC-BK-33), 39 Business Rules, bút toán chi tiết và workflow tổng thể. HTML hiện tại (section 2.4) chỉ có bảng chức năng đơn giản — cần cập nhật lên format đầy đủ UC/Actor/BR/Bút toán giống section 2.3.

## What Changes

- **Viết lại section 2.4.1 Thu tiền gửi**: 7 UC chi tiết (UC-BK-01~07) thay bảng 7 CN đơn giản. Bao gồm: Actor, ĐKTT, Dữ liệu đầu vào, Luồng chính, BR01~BR18.
- **Viết lại section 2.4.2 Chi tiền gửi**: 6 UC chi tiết (UC-BK-08~13) thay bảng 7 CN. Bao gồm: hạn mức duyệt 2 cấp, BR19~BR27.
- **Viết lại section 2.4.3 Chuyển tiền nội bộ**: 4 UC chi tiết (UC-BK-14~17) với bút toán (Nợ 112-B / Có 112-A), BR28~BR30.
- **Viết lại section 2.4.4 Sao kê ngân hàng**: 6 UC chi tiết (UC-BK-18~23) bao gồm import Excel/CSV, đối chiếu tự động, BR31~BR36.
- **Viết lại section 2.4.5 Đối chiếu ngân hàng**: 5 UC chi tiết (UC-BK-24~28), BR37~BR39.
- **Viết lại section 2.4.6 Báo cáo tiền gửi**: 5 UC chi tiết (UC-BK-29~33).
- **Thêm Workflow tổng thể phân hệ NH**: 11 bước (Lập CT → Nháp → Chờ duyệt → Đã duyệt → Ghi sổ → Sinh bút toán → Cập nhật sổ tiền gửi → Đồng bộ sao kê → Đối chiếu → Khóa kỳ → Báo cáo).
- **Cập nhật spec bank-management**: Thêm 33 UC, 39 BR, workflow tổng thể.

## Capabilities

### New Capabilities
- `bank-management-update`: Cập nhật toàn bộ section 2.4 HTML từ bảng CN đơn giản lên format UC chi tiết đầy đủ (33 UC, 39 BR, bút toán, workflow)

### Modified Capabilities
- `bank-management`: Thêm 33 UC (UC-BK-01~33), 39 Business Rules (BR01~BR39), workflow tổng thể 11 bước, hạn mức duyệt 2 cấp cho chi NH

## Impact

- **HTML**: `ACC-noi-dung-nghiep-vu-theo-phase.html` section 2.4 (hiện tại lines ~1308-1371) — viết lại toàn bộ 6 sub-section
- **Spec**: `openspec/changes/phase1-nghiep-vu-lap-trinh/specs/bank-management/spec.md` — thêm UC, BR, workflow
- **Không ảnh hưởng**: Section 2.3 (đã cập nhật), 2.5 (sổ cái), bảng định khoản (đã có dòng NH)
