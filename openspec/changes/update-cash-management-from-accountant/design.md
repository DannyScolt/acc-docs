## Context

File HTML quy trình nghiệp vụ (`ACC-noi-dung-nghiep-vu-theo-phase.html`) section 2.3 hiện chỉ có bảng chức năng đơn giản (8-9 items mỗi section, không có UC/Actor/BR). Kế toán đã cung cấp file `phase1 (2).docx` với nội dung chi tiết hơn nhiều, yêu cầu áp dụng format đầy đủ cho tất cả 5 sub-sections.

Đồng thời, file lập trình spec (`Phase1-nghiep-vu-lap-trinh.html`) và các openspec specs cần được cập nhật tương ứng để đồng bộ.

**Nguồn dữ liệu authoritative:** `phase1 (2).docx` từ kế toán Nguyễn Phú Quý.

**Phạm vi:** Chỉ section 2.3 (Quỹ tiền mặt). Sections 2.4 (Ngân hàng) và 2.5 (Sổ cái) chưa có docx từ kế toán → giữ nguyên.

## Goals / Non-Goals

**Goals:**
- Merge 100% nội dung từ docx kế toán vào file HTML quy trình, giữ đúng style/CSS hiện có
- Áp dụng format mới (Chức năng + Actor + UC + Luồng chính/ngoại lệ + BR) cho tất cả 5 sub-sections của 2.3
- Mở rộng bảng định khoản từ 6→26 nghiệp vụ
- Cập nhật file spec lập trình để đồng bộ (state machine, entity mới, báo cáo mới)
- Đánh dấu rõ `[CHỜ KẾ TOÁN BỔ SUNG]` cho nội dung docx chưa viết chi tiết

**Non-Goals:**
- KHÔNG thay đổi sections 2.4, 2.5 (chưa có docx)
- KHÔNG thay đổi sections 2.1 (Quản trị), 2.2 (Danh mục), hay 2.3 phần header
- KHÔNG thêm nội dung mà docx không cung cấp (không sáng tạo thêm UC/BR)
- KHÔNG thay đổi CSS/layout/structure tổng thể của file HTML
- KHÔNG implement code — chỉ cập nhật tài liệu nghiệp vụ và spec

## Decisions

### 1. Viết lại toàn bộ section 2.3 thay vì patch từng chỗ

**Rationale:** HTML hiện tại quá đơn giản (chỉ bảng CN), không thể "thêm vào" mà phải viết lại cấu trúc. Mỗi sub-section cần thêm 4-6 blocks mới (Actor, UC, Luồng, BR, State, Field map). Viết lại toàn bộ section 2.3 (lines 847-906) sạch hơn và ít lỗi hơn.

**Alternative:** Patch từng table/block — rejected vì quá nhiều insertion points, dễ lệch nesting.

### 2. Dùng chung State machine và Field map cho Phiếu thu + Phiếu chi

**Rationale:** Docx chỉ viết state machine và field map trong section Phiếu thu. Kế toán nói "phiếu thu phiếu chi cũng thế" → áp dụng cùng format. Phiếu chi thêm field "Đối tượng chi" thay "Đối tượng thu", nhưng cấu trúc giống nhau.

### 3. Giữ nguyên text từ docx, không paraphrase

**Rationale:** Docx là nguồn authoritative từ kế toán. Mô tả chức năng, tên UC, nội dung BR phải giữ nguyên word-for-word. Chỉ format lại thành HTML tables.

### 4. Bảng định khoản lấy từ file spec lập trình (26 dòng) thay vì docx

**Rationale:** File spec lập trình đã có bảng 26 nghiệp vụ đầy đủ hơn (được viết trong change trước). Docx không có bảng định khoản riêng. Cần thêm 1 dòng mới cho "Chi hoàn tiền KH" với `[CẦN KẾ TOÁN XÁC NHẬN]`.

### 5. UC chưa có chi tiết → ghi stub với marker

**Rationale:** Docx chỉ chi tiết 3/7 UC sổ quỹ, 2/6 UC kiểm kê, 1/6 UC báo cáo. Các UC còn lại có tên + actor nhưng chưa có luồng chi tiết. Ghi bảng tổng hợp UC đầy đủ, nhưng phần chi tiết chỉ viết cho UC đã có trong docx, còn lại đánh dấu `[CHỜ KẾ TOÁN BỔ SUNG CHI TIẾT]`.

## Risks / Trade-offs

**[Risk] Docx chưa hoàn chỉnh — nhiều UC thiếu chi tiết**
→ Mitigation: Đánh dấu rõ ràng `[CHỜ KẾ TOÁN BỔ SUNG]`, không tự sáng tạo nội dung. Khi kế toán gửi bổ sung, chỉ cần thay thế stub.

**[Risk] Phiếu thu không có UC riêng trong docx — suy ra từ format Phiếu chi**
→ Mitigation: Kế toán nói "phiếu thu phiếu chi cũng thế", nên tạo UC cho PT theo format tương tự PC nhưng đánh dấu `[SỰ LÝ TỪ FORMAT PHIẾU CHI — CHỜ KẾ TOÁN XÁC NHẬN]`.

**[Risk] "Cổ đông" là đối tượng mới chưa có entity**
→ Mitigation: Ghi nhận trong HTML theo docx, đánh dấu trong spec `[CẦN XÁC NHẬN: cổ đông có phải entity riêng hay thuộc nhóm đối tượng khác?]`.

**[Risk] "Chi hoàn tiền KH" cần TK mới chưa xác nhận**
→ Mitigation: Thêm vào bảng định khoản với `[CẦN KẾ TOÁN XÁC NHẬN: Nợ 131/? Có 111]`.

**[Trade-off] Viết lại toàn bộ section 2.3 → diff lớn**
→ Accepted: Diff lớn nhưng kết quả sạch, dễ review hơn patch rải rác.
