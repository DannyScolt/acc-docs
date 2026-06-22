## Context

HTML file `ACC-noi-dung-nghiep-vu-theo-phase.html` section 2.4 hiện chỉ có 6 sub-section với bảng chức năng đơn giản (mỗi bảng 4-7 dòng STT/Chức năng/Mô tả). Kế toán gửi file `phase1.docx` bổ sung chi tiết với 33 UC, 39 BR, bút toán và workflow tổng thể cho toàn bộ phân hệ Tiền gửi ngân hàng.

Section 2.3 (Tiền mặt/Quỹ) đã được cập nhật theo format tương tự trong change trước (`update-cash-management-from-accountant`).

## Goals / Non-Goals

**Goals:**
- Viết lại toàn bộ section 2.4 trong HTML theo format UC chi tiết từ docx kế toán
- Giữ nguyên cấu trúc 6 sub-section (2.4.1 ~ 2.4.6)
- Thêm 33 UC với Actor, Luồng chính, Business Rules, Bút toán
- Thêm Workflow tổng thể phân hệ NH
- Cập nhật spec `bank-management` cho dev

**Non-Goals:**
- Không thay đổi section 2.3 (đã xong), 2.5 (sổ cái)
- Không thay đổi bảng định khoản (đã có dòng NH từ change trước)
- Không thêm/sửa section khác ngoài 2.4

## Decisions

1. **Viết lại toàn bộ section 2.4**: Thay thế 6 bảng CN đơn giản bằng nội dung UC chi tiết. Giữ heading h3 cho sub-section, thêm h4/h5 cho UC.

2. **UC coding scheme UC-BK-xx**: Giữ nguyên mã UC từ docx (UC-BK-01 ~ UC-BK-33). Không đổi thành UC-NH vì kế toán đã dùng UC-BK.

3. **BR coding BR01~BR39**: Giữ nguyên mã BR liên tục từ docx. Khác với section 2.3 (BR-Q, BR-KQ, BR-BC, BR-G), section 2.4 dùng BR số thứ tự đơn giản theo docx gốc.

4. **Bút toán inline**: Docx có bút toán ngay trong UC (VD: Nợ 112 / Có 131). Đưa vào HTML dưới dạng inline text trong mô tả BR, không tạo bảng định khoản riêng (đã có trong bảng định khoản chung).

5. **Workflow tổng thể**: Thêm section "Workflow tổng thể phân hệ Tiền gửi ngân hàng" với 11 bước dạng flow, đặt cuối section 2.4 trước 2.5.

## Risks / Trade-offs

- **Docx dùng format khác section 2.3**: Section 2.3 có UC chi tiết đầy đủ (Mục đích, Actor, ĐKTT, Luồng chính 3 cột, EX, BR riêng UC). Section 2.4 docx ngắn gọn hơn (chỉ có Luồng chính, BR, một số có Actor/ĐKTT). Giữ nguyên mức chi tiết từ docx, không bổ sung thêm.
- **BR numbering khác nhau**: Section 2.3 dùng prefix (BR-Q, BR-KQ...), section 2.4 dùng số thứ tự (BR01~BR39). Giữ theo docx để kế toán dễ đối chiếu.
