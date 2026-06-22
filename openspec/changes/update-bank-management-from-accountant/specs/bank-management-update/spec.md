## ADDED Requirements

### Requirement: Section 2.4 HTML — UC chi tiết phân hệ Tiền gửi ngân hàng

HTML section 2.4 SHALL được viết lại với 33 UC chi tiết, 39 Business Rules, bút toán và workflow tổng thể.

### 2.4.1. Thu tiền gửi ngân hàng (UC-BK-01 ~ UC-BK-07)

**UC-BK-01: Lập chứng từ thu ngân hàng**
- Mục đích: Ghi nhận khoản tiền vào tài khoản ngân hàng
- Actor: Kế toán ngân hàng, Kế toán tổng hợp
- Điều kiện: Đã khai báo TK ngân hàng, Kỳ kế toán chưa khóa
- Dữ liệu nhập: Số CT (Auto/Manual), Ngày CT (✓), Ngày hạch toán (✓), TK ngân hàng (✓), Đối tượng, Nội dung thu (✓), Số tiền (✓), Loại thu (✓), Tiền tệ (✓), Tỷ giá (nếu ngoại tệ)
- Luồng: Chọn "Thu ngân hàng" → Nhập thông tin → Chọn loại thu (Thu KH / Thu khác) → HT kiểm tra → Lưu "Nháp"
- BR01: Số tiền > 0
- BR02: Ngày hạch toán không nằm trong kỳ khóa
- BR03: TK ngân hàng phải đang hoạt động
- BR04: Không cho sửa số tiền sau khi ghi sổ

**UC-BK-02: Thu tiền khách hàng qua ngân hàng**
- Actor: Kế toán công nợ, Kế toán ngân hàng
- Luồng: Chọn KH → HT hiển thị CN chưa TT → Chọn hóa đơn → Nhập số tiền → HT phân bổ CN → Lưu CT
- BR05: Không thu vượt công nợ nếu không cho phép thu trước
- BR06: Sau ghi sổ: Nợ 112 / Có 131
- BR07: Công nợ tự động giảm

**UC-BK-03: Thu khác qua ngân hàng**
- Mục đích: Ghi nhận thu không phải CN KH (lãi tiền gửi, hoàn thuế, cổ tức, thanh lý)
- Luồng: Chọn loại thu khác → Chọn TK đối ứng → Nhập số tiền → Lưu CT
- BR08: Bắt buộc TK đối ứng
- BR09: Tự sinh bút toán theo TK chọn

**UC-BK-04: Đính kèm chứng từ ngân hàng**
- Mục đích: Lưu giấy báo Có, sao kê, CT điện tử
- Luồng: Mở CT → Upload file → Lưu file đính kèm
- BR10: Chỉ cho phép PDF/JPG/PNG/XLSX
- BR11: Kích thước file ≤ 20MB
- BR12: Lưu lịch sử upload

**UC-BK-05: Duyệt chứng từ thu ngân hàng**
- Actor: Kế toán trưởng
- Luồng: Mở DS chờ duyệt → Kiểm tra CT → Chọn Duyệt → Trạng thái: Nháp → Chờ duyệt → Đã duyệt
- BR13: Người lập không được tự duyệt
- BR14: CT đã duyệt không được sửa

**UC-BK-06: Hủy chứng từ thu ngân hàng**
- Luồng: Chọn CT → Chọn Hủy → Nhập lý do → HT ghi log
- BR15: Bắt buộc nhập lý do
- BR16: Không được hủy nếu đã khóa kỳ

**UC-BK-07: Ghi sổ thu ngân hàng**
- Luồng: Chọn CT đã duyệt → Chọn Ghi sổ → HT sinh bút toán → Cập nhật sổ tiền gửi → Cập nhật sổ cái
- BR17: Chỉ CT đã duyệt mới được ghi sổ
- BR18: Sau ghi sổ: Trạng thái = Đã ghi sổ

### 2.4.2. Chi tiền gửi ngân hàng (UC-BK-08 ~ UC-BK-13)

**UC-BK-08: Lập chứng từ chi ngân hàng**
- Luồng: Chọn Chi NH → Nhập thông tin TT → Chọn đối tượng nhận tiền → Lưu CT
- BR19: Số tiền chi ≤ số dư khả dụng (nếu bật kiểm soát quỹ)
- BR20: TK ngân hàng phải hoạt động

**UC-BK-09: Thanh toán nhà cung cấp qua ngân hàng**
- Luồng: Chọn NCC → HT hiển thị CN cần TT → Chọn hóa đơn → Nhập số tiền → Ghi nhận TT
- BR21: Nợ 331 / Có 112
- BR22: CN phải trả giảm tương ứng

**UC-BK-10: Chi khác qua ngân hàng**
- Ví dụ: Nộp thuế, Trả lương, TT chi phí
- BR23: Bắt buộc chọn TK chi phí hoặc CN tương ứng

**UC-BK-11: Duyệt chứng từ chi**
- Luồng: Nháp → Chờ duyệt → Đã duyệt → Ghi sổ
- BR24: Áp dụng quy trình phê duyệt theo hạn mức (<50 triệu → 1 cấp, ≥50 triệu → 2 cấp)

**UC-BK-12: Hủy chứng từ chi**
- BR25: Bắt buộc ghi lý do
- BR26: Lưu audit log

**UC-BK-13: Ghi sổ chi ngân hàng**
- BR27: Sinh bút toán: Nợ TK liên quan / Có 112

### 2.4.3. Chuyển tiền nội bộ (UC-BK-14 ~ UC-BK-17)

**UC-BK-14: Chuyển tiền giữa các TK ngân hàng**
- Luồng: Chọn TK nguồn → Chọn TK đích → Nhập số tiền → Nhập phí (nếu có) → Ghi sổ
- Bút toán: Nợ 112-B / Có 112-A
- BR28: Không được chuyển cùng một TK
- BR29: TK nguồn phải đủ số dư

**UC-BK-15: Nộp tiền mặt vào ngân hàng**
- Luồng: Chọn quỹ tiền mặt → Chọn TK NH → Nhập số tiền → Ghi sổ
- Bút toán: Nợ 112 / Có 111

**UC-BK-16: Rút tiền ngân hàng về quỹ**
- Bút toán: Nợ 111 / Có 112
- BR30: Không cho phép âm quỹ ngân hàng

**UC-BK-17: Theo dõi phí chuyển tiền**
- Luồng: Nhập phí → Chọn TK chi phí → Ghi sổ
- Bút toán: Nợ 642/635 / Có 112

### 2.4.4. Sao kê ngân hàng (UC-BK-18 ~ UC-BK-23)

**UC-BK-18: Nhập sao kê ngân hàng**
- Actor: Kế toán ngân hàng
- Luồng: Chọn TK NH → Upload Excel/CSV → Mapping cột → Import
- BR31: Không import trùng giao dịch
- BR32: Kiểm tra định dạng file

**UC-BK-19: Kết nối lấy sao kê tự động**
- Luồng: Kết nối API NH → Chọn khoảng thời gian → Đồng bộ dữ liệu
- BR33: Chỉ lấy giao dịch chưa tồn tại
- BR34: Lưu log đồng bộ

**UC-BK-20: Xem danh sách giao dịch sao kê**
- Lọc: Theo TK, Theo ngày, Theo số tiền, Theo trạng thái đối chiếu

**UC-BK-21: Tự động gợi ý đối chiếu**
- Luồng: HT đọc GD sao kê → So sánh với CT (Số tiền, Ngày, Nội dung, Mã tham chiếu) → Đưa ra DS đề xuất
- BR35: Độ chính xác đối chiếu ≥ 80%

**UC-BK-22: Đánh dấu giao dịch đã khớp**
- Luồng: Người dùng xác nhận → HT liên kết GD với CT
- BR36: Một GD sao kê chỉ được khớp một lần

**UC-BK-23: Theo dõi giao dịch chưa khớp**
- Màn hình: DS chưa khớp, Quá hạn đối chiếu, Chưa có CT kế toán

### 2.4.5. Đối chiếu ngân hàng (UC-BK-24 ~ UC-BK-28)

**UC-BK-24: Đối chiếu sổ tiền gửi với sao kê**
- Luồng: Chọn TK → Chọn kỳ → HT tính (Số dư sổ KT, Số dư sao kê, Chênh lệch) → Hiển thị kết quả
- BR37: Chỉ đối chiếu theo từng TK

**UC-BK-25: Xử lý giao dịch lệch**
- Luồng: Chọn GD lệch → Chọn phương án (Tạo CT bổ sung / Điều chỉnh / Bỏ qua) → Ghi nhận xử lý
- BR38: Phải lưu lý do xử lý

**UC-BK-26: Lập biên bản đối chiếu ngân hàng**
- Nội dung: Số dư đầu kỳ, Phát sinh thu, Phát sinh chi, Chênh lệch, Kết quả xử lý
- Output: PDF/Excel

**UC-BK-27: Khóa kỳ đối chiếu**
- Luồng: Hoàn tất đối chiếu → Chọn Khóa kỳ → HT khóa dữ liệu
- BR39: Không sửa CT thuộc kỳ đã khóa

**UC-BK-28: Xem lịch sử đối chiếu**
- Chức năng: Tra cứu, In lại biên bản, Xem người thực hiện

### 2.4.6. Báo cáo tiền gửi ngân hàng (UC-BK-29 ~ UC-BK-33)

**UC-BK-29: Sổ tiền gửi ngân hàng**
- Thông tin: Tồn đầu kỳ, Thu, Chi, Tồn cuối kỳ — theo từng TK NH

**UC-BK-30: Bảng kê thu ngân hàng**
- Bộ lọc: Từ ngày → đến ngày, TK NH, Người lập

**UC-BK-31: Bảng kê chi ngân hàng**
- Tương tự bảng kê thu

**UC-BK-32: Báo cáo số dư ngân hàng**
- Hiển thị: TK, Ngân hàng, Số dư

**UC-BK-33: Báo cáo giao dịch chưa đối chiếu**
- Thông tin: Ngày GD, Nội dung, Số tiền, TK, Trạng thái

### Workflow tổng thể phân hệ Tiền gửi ngân hàng

Lập CT → Nháp → Chờ duyệt → Đã duyệt → Ghi sổ → Sinh bút toán KT → Cập nhật sổ tiền gửi → Đồng bộ sao kê → Đối chiếu NH → Khóa kỳ đối chiếu → Báo cáo
