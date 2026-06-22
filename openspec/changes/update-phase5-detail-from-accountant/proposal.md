## Why

Phase 5 hiện mới ở mức khung phân hệ và bảng chức năng tóm tắt, chưa đủ chi tiết để kế toán review, dev triển khai hoặc tester kiểm thử theo cùng chuẩn như Phase 1. Cần nâng Phase 5 lên mức có use case, actor, điều kiện, luồng chính, workflow, business rules, ảnh hưởng kế toán/thuế và tiêu chí nghiệm thu rõ ràng.

## What Changes

- Giữ khung phân hệ Phase 5 hiện có, nhưng viết lại các mục 6.1 đến 6.9 theo chuẩn chi tiết giống Phase 1.
- Chi tiết hóa cụm **hóa đơn điện tử** gồm kết nối nền tảng hóa đơn, quản lý hóa đơn đầu vào, quản lý hóa đơn đầu ra, kiểm tra hợp lệ/cảnh báo rủi ro và xử lý hóa đơn sai sót.
- Chi tiết hóa cụm **kê khai và nghĩa vụ thuế** gồm bảng kê hóa đơn mua vào/bán ra, kê khai thuế/tờ khai thuế, giấy nộp tiền và báo cáo thuế.
- Bổ sung danh sách use case có mã, actor, điều kiện, dữ liệu đầu vào, luồng chính, luồng ngoại lệ, kết quả, workflow/trạng thái và business rules có mã cho từng phân hệ.
- Mở rộng bảng định khoản mẫu, quy tắc nghiệp vụ chung, kết quả bàn giao và tiêu chí nghiệm thu của Phase 5 để có thể dùng làm checklist review/kiểm thử.
- Bổ sung/cập nhật OpenSpec để phản ánh đầy đủ yêu cầu Phase 5 ở mức có thể dùng làm cơ sở triển khai và kiểm thử.

## Capabilities

### New Capabilities
- `phase5-einvoice-detail`: Chi tiết hóa nghiệp vụ hóa đơn điện tử trong Phase 5, bao gồm kết nối nền tảng hóa đơn, hóa đơn đầu vào, hóa đơn đầu ra, kiểm tra hợp lệ/cảnh báo rủi ro và xử lý hóa đơn sai sót.
- `phase5-tax-declaration-detail`: Chi tiết hóa nghiệp vụ bảng kê hóa đơn, kê khai thuế, tờ khai thuế, giấy nộp tiền và báo cáo thuế trong Phase 5.
- `phase5-reporting-controls-detail`: Chi tiết hóa bảng định khoản mẫu, quy tắc nghiệp vụ chung, workflow tổng thể, kết quả bàn giao và tiêu chí nghiệm thu của Phase 5.

### Modified Capabilities
- `general-ledger`: Mở rộng yêu cầu liên quan ảnh hưởng ghi sổ và đối chiếu sổ cái từ nghiệp vụ hóa đơn điện tử, thuế GTGT đầu vào/đầu ra, khấu trừ thuế và nộp thuế của Phase 5.

## Impact

- **HTML**: `ACC-noi-dung-nghiep-vu-theo-phase.html` phần Phase 5 sẽ được viết lại sâu hơn, đặc biệt các section 6.1 đến 6.9 và phần cuối Phase 5.
- **Spec**: Change mới sẽ bổ sung các capability riêng cho Phase 5 và delta spec cho `general-ledger` để phản ánh logic ghi sổ/đối chiếu liên quan thuế và hóa đơn.
- **Phụ thuộc nghiệp vụ**: Cần giữ nhất quán với Phase 1 về quỹ, ngân hàng, sổ cái và các nguyên tắc không ghi sổ vào kỳ khóa, truy vết chứng từ nguồn, không sửa trực tiếp chứng từ đã hoàn tất.
