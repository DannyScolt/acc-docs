## 1. Phiếu thu (2.3.1)

- [x] 1.1 Viết lại section 2.3.1 trong HTML: bảng 16 chức năng (thay bảng 8 cũ)
- [x] 1.2 Thêm State machine 5+2 trạng thái (Nháp → Chờ duyệt → Đã duyệt → Đã ghi sổ → Đã khóa kỳ + Từ chối + Đã hủy)
- [x] 1.3 Thêm Field map 3 nhóm (Thông tin chung, Hạch toán, Công nợ)
- [x] 1.4 Thêm stub UC + Actor cho phiếu thu (suy ra từ format phiếu chi, đánh dấu [CHỜ KẾ TOÁN XÁC NHẬN])

## 2. Phiếu chi (2.3.2)

- [x] 2.1 Viết lại section 2.3.2 trong HTML: bảng 17 chức năng (thay bảng 9 cũ), bao gồm "Chi hoàn tiền KH"
- [x] 2.2 Thêm bảng Actor (4 actors: KT quỹ, Thủ quỹ, KT trưởng, GĐ)
- [x] 2.3 Thêm Use Case luồng chính 11 bước
- [x] 2.4 Thêm Business Rules BR-Q01~Q10 (10 rules)

## 3. Sổ quỹ (2.3.3)

- [x] 3.1 Viết lại section 2.3.3 trong HTML: bảng 12 chức năng (thay bảng 6 cũ), lưu ý CN#4 có "cổ đông"
- [x] 3.2 Thêm bảng Use Case tổng hợp (7 UC: UC-Q01~Q07)
- [x] 3.3 Thêm luồng chính UC-Q01 (7 bước, format ngắn)
- [x] 3.4 Thêm UC-Q02 chi tiết đầy đủ: mục đích, 4 actors, ĐKTT, dữ liệu đầu vào, 8 bước (3 cột), công thức, EX-01/02, BR-Q02-01~05
- [x] 3.5 Thêm UC-Q03 chi tiết đầy đủ: mục đích, 3 actors, bộ lọc 5 nhóm, 7 bước, EX-01/02, BR-Q03-01~05
- [x] 3.6 Thêm UC-Q04 chi tiết đầy đủ: mục đích, 4 actors (có KTNB), 6 nguồn CT, 7 bước
- [x] 3.7 Thêm luồng chính UC-Q05 (5 bước, format ngắn)
- [x] 3.8 Thêm Business Rules BR-Q01~Q09 (9 rules)

## 4. Kiểm kê quỹ (2.3.4)

- [x] 4.1 Viết lại section 2.3.4 trong HTML: bảng 8 chức năng (thay bảng 5 cũ), bao gồm "Nhập theo mệnh giá"
- [x] 4.2 Thêm bảng Use Case (6 UC: UC-KQ01~KQ06)
- [x] 4.3 Thêm luồng chính UC-KQ01 (7 bước) và UC-KQ04 (6 bước)
- [x] 4.4 Thêm Workflow bảng 5 trạng thái (Nháp → Chờ duyệt → Đã duyệt → Đã điều chỉnh → Hủy)
- [x] 4.5 Thêm Business Rules BR-KQ01~KQ10 (10 rules)

## 5. Báo cáo quỹ (2.3.5)

- [x] 5.1 Viết lại section 2.3.5 trong HTML: bảng 9 báo cáo (thay bảng 5 cũ), thêm 4 BC mới
- [x] 5.2 Thêm bảng Use Case (6 UC: UC-BC01~BC06)
- [x] 5.3 Thêm luồng chính UC-BC05 (6 bước)
- [x] 5.4 Thêm Business Rules BR-BC01~BC07 (7 rules)

## 6. Business Rules toàn phân hệ + Bảng định khoản

- [x] 6.1 Thêm section mới "Business Rules Toàn Phân Hệ Quỹ" BR-G01~G08 (8 rules) vào cuối section 2.3
- [x] 6.2 Cập nhật bảng định khoản từ 6→27 nghiệp vụ (lấy từ general-ledger spec), thêm dòng hoàn tiền KH

## 7. Cập nhật file spec lập trình

- [x] 7.1 Cập nhật openspec spec cash-management: state machine 4→7 trạng thái, thêm payment_type refund_return, thêm entity cash_inventory_denomination
- [x] 7.2 Cập nhật openspec spec reports-phase1: thêm 4 báo cáo quỹ mới
- [x] 7.3 Cập nhật openspec spec general-ledger: thêm dòng định khoản hoàn tiền KH

## 8. Review & kiểm tra

- [x] 8.1 Đối chiếu lại toàn bộ HTML section 2.3 với docx gốc — đảm bảo không sót chức năng, UC, BR nào
- [x] 8.2 Kiểm tra HTML valid (không lỗi nesting table/section)
- [x] 8.3 Kiểm tra tính nhất quán: số liệu trong bảng CN khớp với bảng UC, BR code không trùng lặp
