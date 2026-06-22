## 1. Thu tiền gửi (2.4.1)

- [x] 1.1 Viết lại section 2.4.1 trong HTML: 7 UC chi tiết (UC-BK-01~07), thay bảng 7 CN đơn giản
- [x] 1.2 UC-BK-01: Actor, ĐKTT, Dữ liệu nhập (10 trường), Luồng chính 5 bước, BR01~BR04
- [x] 1.3 UC-BK-02: Thu tiền KH qua NH, Luồng 6 bước, BR05~BR07 (bút toán Nợ 112 / Có 131)
- [x] 1.4 UC-BK-03: Thu khác qua NH (lãi, hoàn thuế, cổ tức, thanh lý), BR08~BR09
- [x] 1.5 UC-BK-04: Đính kèm CT, BR10~BR12 (file type, size limit)
- [x] 1.6 UC-BK-05: Duyệt CT thu, BR13~BR14 (tách người lập/duyệt)
- [x] 1.7 UC-BK-06: Hủy CT, BR15~BR16
- [x] 1.8 UC-BK-07: Ghi sổ, BR17~BR18

## 2. Chi tiền gửi (2.4.2)

- [x] 2.1 Viết lại section 2.4.2: 6 UC chi tiết (UC-BK-08~13)
- [x] 2.2 UC-BK-08~10: Lập CT chi, TT NCC, Chi khác — BR19~BR23
- [x] 2.3 UC-BK-11: Duyệt CT chi với hạn mức 2 cấp (<50tr → 1 cấp, ≥50tr → 2 cấp) — BR24
- [x] 2.4 UC-BK-12~13: Hủy CT chi, Ghi sổ chi — BR25~BR27

## 3. Chuyển tiền nội bộ (2.4.3)

- [x] 3.1 Viết lại section 2.4.3: 4 UC chi tiết (UC-BK-14~17) với bút toán
- [x] 3.2 UC-BK-14: Chuyển giữa TK NH (Nợ 112-B / Có 112-A), BR28~BR29
- [x] 3.3 UC-BK-15~16: Nộp tiền mặt vào NH / Rút tiền NH về quỹ, BR30
- [x] 3.4 UC-BK-17: Phí chuyển tiền (Nợ 642/635 / Có 112)

## 4. Sao kê ngân hàng (2.4.4)

- [x] 4.1 Viết lại section 2.4.4: 6 UC chi tiết (UC-BK-18~23)
- [x] 4.2 UC-BK-18~19: Nhập sao kê (Excel/CSV) + API tự động, BR31~BR34
- [x] 4.3 UC-BK-20~21: Xem GD sao kê + Đối chiếu tự động (accuracy ≥80%), BR35
- [x] 4.4 UC-BK-22~23: Đánh dấu khớp (one-to-one), Theo dõi chưa khớp, BR36

## 5. Đối chiếu ngân hàng (2.4.5)

- [x] 5.1 Viết lại section 2.4.5: 5 UC chi tiết (UC-BK-24~28)
- [x] 5.2 UC-BK-24~25: Đối chiếu sổ/sao kê + Xử lý lệch, BR37~BR38
- [x] 5.3 UC-BK-26~28: Biên bản, Khóa kỳ, Lịch sử, BR39

## 6. Báo cáo tiền gửi (2.4.6)

- [x] 6.1 Viết lại section 2.4.6: 5 UC chi tiết (UC-BK-29~33)

## 7. Workflow tổng thể + Cập nhật spec

- [x] 7.1 Thêm section "Workflow tổng thể phân hệ Tiền gửi ngân hàng" (11 bước) vào cuối section 2.4
- [x] 7.2 Cập nhật spec bank-management: thêm state machine 7 TT, hạn mức duyệt, đối chiếu tự động

## 8. Review & kiểm tra

- [x] 8.1 Đối chiếu HTML section 2.4 với docx gốc — đảm bảo không sót UC, BR nào
- [x] 8.2 Kiểm tra HTML valid (table nesting)
- [x] 8.3 Kiểm tra section 2.3, 2.5 không bị ảnh hưởng
