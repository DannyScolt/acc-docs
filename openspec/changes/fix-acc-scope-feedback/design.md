## Context

File `ACC-noi-dung-nghiep-vu-theo-phase.html` là tài liệu phạm vi nghiệp vụ kế toán 6 phase, dùng để gửi kế toán đọc và phản hồi. Reviewer kế toán (Mạnh Tâm Acc) đã feedback 4 điểm cần sửa. Tài liệu là single HTML file (~2059 dòng) với CSS inline, tab navigation, không có framework.

Chế độ kế toán áp dụng: **TT99/2025/TT-BTC** (có hiệu lực từ 01/01/2026, thay thế TT200). Hệ thống tài khoản TT99 kế thừa phần lớn từ TT200.

## Goals / Non-Goals

**Goals:**
- Kế toán đọc tài liệu biết rõ mình cần phản hồi gì (định khoản Nợ/Có cho từng nghiệp vụ)
- Kế toán không nhầm lẫn giữa "nhập số dư đầu kỳ" và "module quản lý đầy đủ"
- Bảng định khoản mẫu đủ cụ thể để kế toán xác nhận/sửa, không quá chi tiết đến mức thành tài liệu triển khai

**Non-Goals:**
- Không tạo tài liệu thiết kế triển khai cho dev (anh Danny xác nhận "chưa cần")
- Không thay đổi cấu trúc phase hay gộp/tách module
- Không thêm CSS class mới — dùng lại `.report-note` và `<table>` sẵn có
- Không sửa nội dung nghiệp vụ (chỉ bổ sung thông tin thiếu)

## Decisions

### 1. Dùng `.report-note` thay `.notice` cho khung yêu cầu phản hồi

**Lý do:** `.notice` hiện tại có style border-left cam nhỏ, dễ bị bỏ qua. `.report-note` đã có sẵn CSS (background cam `#fff7ed`, border cam `#f97316`, text đậm `#7c2d12`) — nổi bật hơn nhiều, đúng mục đích "cần chú ý".

**Alternative:** Tạo CSS class mới `.feedback-request` → bỏ vì không cần, `.report-note` đã đủ.

### 2. Đặt bảng định khoản trước bảng "Quy tắc nghiệp vụ" mỗi phase

**Lý do:** Kế toán đọc xong chức năng → thấy bảng định khoản → rồi mới đến quy tắc → kết quả bàn giao. Luồng đọc tự nhiên: "nghiệp vụ gì → hạch toán thế nào → quy tắc gì".

**Alternative:** Đặt sau "Tiêu chí nghiệm thu" → bỏ vì kế toán sẽ không cuộn xuống đến đó.

### 3. Bảng định khoản chỉ liệt kê nghiệp vụ chính, 3-6 dòng/phase

**Lý do:** Đây là tài liệu cho kế toán phản hồi, không phải bảng tra cứu đầy đủ. Liệt kê các nghiệp vụ chính để kế toán hiểu pattern, rồi họ bổ sung thêm. Quá nhiều dòng → kế toán ngại đọc.

### 4. Ghi chú opening balance bằng cách thêm text vào cột Mô tả

**Lý do:** Không cần thêm cột mới hay restructure bảng. Chỉ cần append 1 câu vào mô tả hiện tại. Giữ nguyên layout.

**Alternative:** Thêm footnote/ghi chú riêng dưới bảng → bỏ vì kế toán phải nhìn qua lại, kém trực quan.

## Risks / Trade-offs

- **Số TK mẫu có thể không khớp thực tế DN** → Mitigation: ghi rõ "mẫu tham khảo, kế toán vui lòng điều chỉnh theo thực tế doanh nghiệp"
- **TT99 mới, chưa có nhiều tài liệu thực hành** → Mitigation: dùng hệ thống TK cơ bản (111, 112, 131, 331, 511, 632...) vốn không thay đổi giữa TT200 và TT99
- **Bảng định khoản làm tài liệu dài hơn** → Mitigation: mỗi bảng chỉ 3-6 dòng, thêm khoảng ~30 dòng HTML/phase, tổng ~180 dòng — chấp nhận được
