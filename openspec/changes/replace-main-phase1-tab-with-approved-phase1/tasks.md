## 1. Xác định ranh giới thay thế an toàn trong file tổng

- [x] 1.1 Xác định chính xác wrapper `tab-phase-1` và phạm vi section Phase 1 hiện tại trong `ACC-noi-dung-nghiep-vu-theo-phase.html`
- [x] 1.2 Xác định phần nội dung nào trong `ACC-dac-ta-nghiep-vu-phase-1.html` sẽ được dùng làm nguồn chuyển vào file tổng, và phần shell nào phải loại bỏ
- [x] 1.3 Ghi nhận các định danh cần giữ nguyên để không phá tab navigation: `tab-phase-1`, `#phase-1`, các anchor và cấu trúc tab hiện có

## 2. Thay tab Phase 1 cũ bằng nội dung Phase 1 chuẩn

- [x] 2.1 Thay gần như toàn bộ nội dung section Phase 1 cũ trong file tổng bằng nội dung đã chuẩn hóa từ file Phase 1 riêng
- [x] 2.2 Giữ nguyên wrapper tab-panel và section IDs, chỉ thay phần thân nội dung để cơ chế tab không đổi
- [x] 2.3 Thích nghi nội dung từ file độc lập vào file tổng: loại bỏ `doctype/head/body/style` và các wrapper không phù hợp với tab layout hiện tại

## 3. Đồng bộ hiển thị và cấu trúc trong bối cảnh file chính

- [x] 3.1 Rà lại heading, numbering, anchors nội bộ và thứ tự section của tab Phase 1 sau khi thay
- [x] 3.2 Kiểm tra xem các class dùng bởi Phase 1 chuẩn đã được file tổng hỗ trợ đầy đủ hay cần chỉnh tối thiểu để hiển thị đúng
- [x] 3.3 Đảm bảo tab Phase 1 mới nhìn đồng bộ với file tổng nhưng vẫn giữ được tinh thần “bản đã duyệt” của file chuẩn

## 4. Xác minh không ảnh hưởng phần còn lại của tài liệu tabbed

- [x] 4.1 Kiểm tra tab navigation, tab switching và mục lục nhanh vẫn trỏ đúng đến Phase 1
- [x] 4.2 Kiểm tra các tab khác (Overview, Phase 2–6, Appendix) không bị ảnh hưởng bởi thay đổi ở tab Phase 1
- [x] 4.3 Kiểm tra cấu trúc HTML cuối cùng không lỗi tag lồng, không mất đóng mở `div/section`, và vẫn phù hợp cho print/PDF flow của file tổng
