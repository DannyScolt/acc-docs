## Context

Hiện tại tài liệu `ACC-noi-dung-nghiep-vu-theo-phase.html` chỉ có callout lộ trình cho Giai đoạn 1. Ta cần bổ sung callout lộ trình chi tiết cho các Giai đoạn 2 đến 6.

## Goals / Non-Goals

**Goals:**
- Thêm lộ trình triển khai theo từng tuần dưới dạng `<div class="callout">` vào đầu mỗi giai đoạn (từ Giai đoạn 2 đến Giai đoạn 6).
- Điều chỉnh thời gian các giai đoạn sao cho tổng thời gian triển khai 6 giai đoạn là đúng 52 tuần (1 năm) cho đội ngũ 2 người.

**Non-Goals:**
- Không thay đổi lộ trình của Giai đoạn 1.
- Không thay đổi mã nguồn phần mềm, chỉ sửa tài liệu HTML nghiệp vụ.

## Decisions

1. **Vị trí chèn callout lộ trình trong HTML:**
   - Chèn ngay sau `<div class="phase-intro-card">...</div>` và trước tiêu đề `<h3>` đầu tiên của mỗi giai đoạn.
   - Rationale: Giúp người đọc dễ dàng thấy được lộ trình tổng thể của giai đoạn ngay khi bắt đầu đọc chương đó, nhất quán với cách hiển thị của Phase 1.

2. **Phân bổ thời gian (tổng cộng 52 tuần):**
   - Phase 1: 10 tuần (fixed).
   - Phase 2: 10 tuần.
   - Phase 3: 10 tuần.
   - Phase 4: 6 tuần.
   - Phase 5: 6 tuần.
   - Phase 6: 10 tuần.
   - Rationale: Giúp phân bổ thời gian hợp lý cho team 2 người thực hiện các đầu việc từ thiết kế, phát triển đến kiểm thử và nghiệm thu.

## Risks / Trade-offs

- **Lỗi thẻ đóng mở HTML:** Việc chèn thủ công vào file HTML lớn có thể dẫn đến lỗi cú pháp (như nested div, thiếu thẻ đóng).
- **Biện pháp giảm thiểu:** Sử dụng python script để chèn chính xác dựa trên markers duy nhất và kiểm tra cú pháp HTML sau khi chỉnh sửa.
