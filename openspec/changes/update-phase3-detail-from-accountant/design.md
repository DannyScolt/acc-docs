## Context

Phase 3 trong HTML hiện tại mô tả chu trình bán hàng dưới dạng bảng summary cho từng mục 4.2–4.13, trong khi file DOCX từ bộ phận kế toán đã cung cấp cấu trúc chi tiết hơn nhiều: business rule toàn phân hệ, danh sách use case chi tiết, luồng trạng thái, liên kết dữ liệu, bút toán kế toán và báo cáo quản trị. Ngoài vấn đề độ sâu nội dung, cấu trúc hiện tại của HTML còn lệch numbering so với source-of-truth, nổi bật ở các mục 4.9–4.13.

Phase 3 là chương giao cắt mạnh với các phần đã có trong repo: Phase 1 (quỹ, ngân hàng, sổ cái), Phase 2 (kho, nhập xuất, mua hàng) và các change accountant đã hoàn thành cho Phase 5–6. Vì vậy design cần vừa nâng Phase 3 lên chuẩn “chi tiết như Phase 1”, vừa tránh tạo mâu thuẫn với các rule ghi sổ, luồng chứng từ và các cụm nghiệp vụ đã được chốt trước đó.

## Goals / Non-Goals

**Goals:**
- Viết lại Phase 3 theo cấu trúc chi tiết thống nhất với Phase 1: mục tiêu, business rules, use case, actor, luồng chính, kết quả đầu ra, trạng thái, liên kết dữ liệu và bút toán khi tài liệu nguồn có cung cấp.
- Đồng bộ numbering và grouping của Phase 3 theo DOCX accountant để HTML không còn lệch source-of-truth.
- Tách yêu cầu thành các capability OpenSpec đủ rõ để apply theo cụm nghiệp vụ: bán hàng, giá/hóa đơn, giao hàng/công nợ/báo cáo.
- Đồng bộ ảnh hưởng tới `general-ledger` ở mức requirement để trace được các điểm ghi sổ doanh thu, thuế đầu ra, giá vốn, phải thu, thu tiền và giảm trừ doanh thu.

**Non-Goals:**
- Không triển khai phần mềm; chỉ cập nhật tài liệu nghiệp vụ và OpenSpec.
- Không thay đổi nội dung Phase 1, Phase 2, Phase 5 hoặc Phase 6 ngoài phạm vi cross-reference cần thiết trong đặc tả.
- Không tự thêm nghiệp vụ mới nếu DOCX không cung cấp; với các điểm còn mơ hồ sẽ bám sát tài liệu kế toán thay vì suy diễn.
- Không chốt lại tài khoản kế toán chi tiết ngoài phạm vi nguồn hiện có; nếu cần, giữ các ghi chú xác nhận giống pattern của Phase 1/2.

## Decisions

1. **Chia Phase 3 thành 3 capability chính thay vì 1 capability lớn**
   - `phase3-sales-detail`: báo giá, đơn đặt hàng bán, hợp đồng bán, bán hàng hóa/dịch vụ.
   - `phase3-pricing-and-invoicing-detail`: chính sách giá, bảng giá, chiết khấu, hóa đơn bán ra.
   - `phase3-fulfillment-and-receivables-detail`: xuất kho, trả lại/giảm giá, công nợ phải thu, thu tiền, báo cáo.
   - **Rationale:** Phase 3 quá rộng; tách theo cụm giúp đặc tả, review và apply theo khối nghiệp vụ dễ hơn.
   - **Alternative considered:** Một capability duy nhất cho toàn bộ Phase 3. Bị loại vì khó review, khó trace và quá dài.

2. **Lấy DOCX accountant làm source-of-truth cho cấu trúc chương**
   - HTML hiện tại sẽ được remap về trục 4.2–4.12 của tài liệu nguồn.
   - Mục `4.9 Tính giá vốn hàng bán` hiện tại sẽ không giữ như một chapter độc lập nếu source không tách riêng; logic giá vốn sẽ được đặt vào phần xuất kho, bút toán và báo cáo nơi phù hợp.
   - **Rationale:** Giảm lệch số mục và tránh tình trạng HTML tự phát triển cấu trúc riêng không khớp nguồn kế toán.
   - **Alternative considered:** Giữ cấu trúc HTML hiện tại rồi chỉ bổ sung chi tiết. Bị loại vì vẫn để lại lệch numbering và lệch semantics.

3. **Giữ format hiển thị giống Phase 1 và change Phase 2 accountant**
   - Mỗi section sẽ dùng cùng ngôn ngữ trình bày: mô tả module, bảng rule có mã, bảng use case, khối luồng trạng thái, liên kết dữ liệu, bút toán, báo cáo.
   - Không dùng nested table để tránh lặp lại các lỗi format HTML trước đây.
   - **Rationale:** Bảo toàn trải nghiệm đọc thống nhất xuyên phase và giảm rủi ro vỡ layout.
   - **Alternative considered:** Dùng layout mới riêng cho Phase 3. Bị loại vì gây thiếu nhất quán với Phase 1/2.

4. **Dùng mã rule/use case theo đúng tài liệu nguồn thay vì đổi sang prefix chung mới**
   - Ví dụ: `BR-BG-*`, `BR-DH-*`, `BR-GIA-*`, `BR-BH-*`, `BR-HDB-*`, `BR-XK-*`, `BR-TRA-*`, `BR-CN-*`, `BR-TT-*`, `BR-BC-*`.
   - **Rationale:** Các mã này đã tồn tại trong DOCX và phù hợp để trace ngược với tài liệu accountant.
   - **Alternative considered:** Dùng prefix chuẩn hóa như `BR-P3-*`. Bị loại vì làm mất liên kết 1-1 với source.

5. **Cập nhật `general-ledger` dưới dạng delta requirement ở mức liên kết ghi sổ**
   - Chỉ mô tả requirement về khả năng truy vết và đồng bộ rule ghi sổ từ Phase 3, không lặp lại toàn bộ nội dung bán hàng trong capability này.
   - **Rationale:** `general-ledger` nên là capability xuyên suốt về kiểm soát ghi sổ, không trở thành bản sao của tài liệu bán hàng.
   - **Alternative considered:** Không sửa `general-ledger`. Bị loại vì Phase 3 bổ sung nhiều điểm ghi sổ trọng yếu hơn Phase 2.

## Risks / Trade-offs

- **[Rủi ro lệch cấu trúc giữa HTML cũ và DOCX mới]** → Mitigation: remap rõ từng mục 4.2–4.12, không cố giữ nguyên các section trung gian đang lệch.
- **[Phase 3 quá dài, dễ tạo artifact cồng kềnh]** → Mitigation: chia capability theo cụm nghiệp vụ và chia task theo nhóm section rõ ràng.
- **[Mâu thuẫn với Phase 1/2 về kho, quỹ, ngân hàng, sổ cái]** → Mitigation: chỉ cross-reference logic liên quan, cập nhật `general-ledger` ở mức delta requirement và tránh viết đè nội dung phase khác.
- **[Có chỗ trong DOCX gộp/đặt tên chưa hoàn toàn trùng HTML]** → Mitigation: ưu tiên nguyên tắc “source-of-truth từ accountant”, ghi rõ trong proposal/design rằng numbering sẽ được chuẩn hóa lại.
- **[Bảng HTML dài và nặng]** → Mitigation: tiếp tục dùng pattern section hóa như Phase 1, mỗi cụm nghiệp vụ đóng gói thành bảng/khối riêng, tránh nested structure.