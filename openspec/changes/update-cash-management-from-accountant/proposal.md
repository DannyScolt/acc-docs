## Why

Kế toán (Nguyễn Phú Quý) đã review và bổ sung chi tiết cho toàn bộ section 2.3 (Quỹ tiền mặt) trong file quy trình nghiệp vụ Phase 1. File `phase1 (2).docx` chứa nội dung chi tiết hơn nhiều so với file HTML hiện tại: thêm chức năng mới, Use Cases với luồng chính/ngoại lệ, Business Rules, Actor mapping, State machine đầy đủ, và Field map. Cần merge nội dung này vào file HTML quy trình và cập nhật các file spec lập trình tương ứng.

## What Changes

### File HTML quy trình (`ACC-noi-dung-nghiep-vu-theo-phase.html`)
- **2.3.1 Phiếu thu**: Mở rộng từ 8→16 chức năng, thêm state machine (5+2 trạng thái), thêm field map (3 nhóm: thông tin chung, hạch toán, công nợ)
- **2.3.2 Phiếu chi**: Mở rộng từ 9→17 chức năng, thêm nghiệp vụ mới "Chi hoàn tiền khách hàng" (refund_return), thêm 4 Actors, UC với luồng chính 11 bước, BR-Q01~Q10
- **2.3.3 Sổ quỹ**: Mở rộng từ 6→12 chức năng, thêm 7 Use Cases (UC-Q01~Q07) với 3 UC chi tiết đầy đủ (Q02, Q03, Q04), BR-Q01~Q09, công thức tồn quỹ, luồng ngoại lệ
- **2.3.4 Kiểm kê quỹ**: Mở rộng từ 5→8 chức năng, thêm "Nhập theo mệnh giá", 6 Use Cases (UC-KQ01~KQ06), workflow 5 trạng thái, BR-KQ01~KQ10
- **2.3.5 Báo cáo quỹ**: Mở rộng từ 5→9 báo cáo (thêm: thu chi theo khoản mục, thu chi theo đối tượng, chênh lệch kiểm kê, Dashboard quỹ), 6 Use Cases (UC-BC01~BC06), BR-BC01~BC07
- **Thêm mới**: Business Rules toàn phân hệ quỹ BR-G01~G08
- **Bảng định khoản**: Mở rộng từ 6→26 nghiệp vụ

### File spec lập trình
- **cash-management/spec.md**: Cập nhật state machine (4→7 trạng thái), thêm payment_type refund_return, thêm entity cash_inventory_denomination
- **reports-phase1/spec.md**: Thêm 4 báo cáo quỹ mới
- **general-ledger/spec.md**: Thêm dòng định khoản cho nghiệp vụ hoàn tiền KH

## Capabilities

### New Capabilities
- `cash-voucher-update`: Cập nhật Phiếu thu (2.3.1) và Phiếu chi (2.3.2) — mở rộng chức năng, thêm state machine, field map, actors, UC, BR
- `cash-book-update`: Cập nhật Sổ quỹ (2.3.3) — mở rộng chức năng, thêm 7 UC chi tiết, BR, công thức
- `cash-inventory-update`: Cập nhật Kiểm kê quỹ (2.3.4) — mở rộng chức năng, thêm mệnh giá, UC, workflow, BR
- `cash-reports-update`: Cập nhật Báo cáo quỹ (2.3.5) — thêm 4 báo cáo mới, UC, BR
- `cash-global-rules`: Business Rules toàn phân hệ quỹ BR-G01~G08 và bảng định khoản mở rộng

### Modified Capabilities
- `cash-management`: State machine cần thêm trạng thái "Đã ghi sổ", "Đã khóa kỳ", "Từ chối"; thêm payment_type refund_return; thêm entity cash_inventory_denomination
- `reports-phase1`: Thêm 4 báo cáo quỹ mới (thu chi theo khoản mục, thu chi theo đối tượng, chênh lệch kiểm kê, Dashboard quỹ)
- `general-ledger`: Thêm định khoản cho hoàn tiền KH

## Impact

- **ACC-noi-dung-nghiep-vu-theo-phase.html**: Lines 847-1066 (section 2.3 + bảng định khoản) — viết lại toàn bộ
- **Phase1-nghiep-vu-lap-trinh.html**: Chương 4 (Quỹ tiền mặt) + Chương 7 (Báo cáo) cần cập nhật tương ứng
- **openspec specs**: cash-management, reports-phase1, general-ledger cần delta updates
- Sections 2.4 (Ngân hàng) và 2.5 (Sổ cái) KHÔNG thay đổi — kế toán chưa cung cấp nội dung chi tiết
