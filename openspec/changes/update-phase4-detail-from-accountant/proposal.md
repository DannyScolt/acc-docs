## Why

Phase 4 trong HTML hiện đã có khung module đúng nhưng nội dung bên trong vẫn chủ yếu ở mức bảng chức năng tóm tắt, chưa đủ chi tiết để kế toán review quy trình tổng hợp cuối kỳ, khóa kỳ và lập báo cáo tài chính như một đặc tả nghiệp vụ thống nhất. File nguồn từ bộ phận kế toán đã cung cấp đầy đủ use case, actor, luồng nghiệp vụ, business rule, liên kết phân hệ và kết quả đầu ra cho Phase 4, nên cần cập nhật lại toàn bộ phần này theo đúng độ sâu của tài liệu nguồn.

## What Changes

- Viết lại toàn bộ các section nghiệp vụ chính của Phase 4 theo format chi tiết giống Phase 1, thay cho cấu trúc summary `STT / Chức năng / Mô tả` hiện tại.
- Chi tiết hóa các phân hệ **5.2 đến 5.9** theo DOCX accountant, bao gồm: chứng từ nghiệp vụ khác & bút toán tổng hợp, quyết toán tạm ứng & phân bổ chi phí, cấu hình bút toán kết chuyển, kết chuyển cuối kỳ & xác định kết quả kinh doanh, kiểm tra đối chiếu trước khóa kỳ, khóa kỳ & mở lại kỳ, sổ sách kế toán tổng hợp và báo cáo tài chính.
- Bổ sung cho từng module: use case có mã, actor, luồng nghiệp vụ, luồng chính, business rules, liên kết với phân hệ khác và kết quả đầu ra như tài liệu kế toán đã mô tả.
- Giữ nguyên khung chương mục lớn của Phase 4 khi đã khớp tài liệu nguồn, nhưng nâng toàn bộ độ sâu nội dung để có thể dùng làm cơ sở triển khai, kiểm thử và review nghiệp vụ.
- Cập nhật OpenSpec để phản ánh đầy đủ yêu cầu Phase 4 ở mức có thể dùng làm nền cho implementation sau này.

## Capabilities

### New Capabilities
- `phase4-adjustments-and-period-close-detail`: Chi tiết hóa chứng từ nghiệp vụ khác, quyết toán tạm ứng, phân bổ chi phí, cấu hình kết chuyển và các bước kết chuyển cuối kỳ của Phase 4.
- `phase4-reconciliation-and-ledger-detail`: Chi tiết hóa kiểm tra đối chiếu trước khóa kỳ, khóa kỳ/mở lại kỳ và hệ thống sổ sách kế toán tổng hợp của Phase 4.
- `phase4-financial-reporting-detail`: Chi tiết hóa báo cáo tài chính, kiểm tra cân đối báo cáo, drill-down và quản lý phiên bản báo cáo của Phase 4.

### Modified Capabilities
- `general-ledger`: Mở rộng các yêu cầu liên quan ghi sổ, kết chuyển, khóa kỳ, sổ kế toán tổng hợp và truy vết báo cáo tài chính khi Phase 4 được chi tiết hóa theo tài liệu kế toán.

## Impact

- **HTML**: `ACC-noi-dung-nghiep-vu-theo-phase.html` phần Phase 4 sẽ được viết lại sâu hơn, đặc biệt các section [5.2](ACC-noi-dung-nghiep-vu-theo-phase.html:2532) đến [5.9](ACC-noi-dung-nghiep-vu-theo-phase.html:2631).
- **OpenSpec**: Cần thêm các capability spec mới cho nghiệp vụ Phase 4 và cập nhật delta spec `general-ledger` để đồng bộ logic ghi sổ, kết chuyển và lập báo cáo.
- **Tài liệu nghiệp vụ**: Phase 4 sẽ chuyển từ mức summary sang mức detailed spec, nhưng vẫn giữ khung chapter hiện tại vì đã tương đối khớp nguồn accountant.
- **Phụ thuộc nghiệp vụ**: Cần giữ đồng bộ với Phase 1 (sổ cái, quỹ, ngân hàng), Phase 2 (mua hàng, kho) và Phase 3 (doanh thu, công nợ phải thu) để các bước đối chiếu, kết chuyển và báo cáo tài chính không mâu thuẫn.