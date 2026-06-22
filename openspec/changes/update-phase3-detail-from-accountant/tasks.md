## 1. Chuẩn hóa cấu trúc Phase 3 theo tài liệu accountant

- [ ] 1.1 Đối chiếu section Phase 3 hiện tại trong `ACC-noi-dung-nghiep-vu-theo-phase.html` với DOCX accountant để lập mapping cũ → mới cho các mục 4.2 đến 4.12
- [ ] 1.2 Cập nhật heading, mô tả mở đầu và numbering của Phase 3 để khớp source-of-truth từ DOCX
- [ ] 1.3 Loại bỏ hoặc hấp thụ lại các section đang lệch cấu trúc hiện tại như `4.9 Tính giá vốn hàng bán`, `4.11 Bù trừ công nợ & đối trừ chứng từ`, `4.13 Báo cáo...` vào đúng vị trí theo tài liệu nguồn

## 2. Chi tiết hóa cụm bán hàng đầu chu trình

- [ ] 2.1 Viết lại section 4.2 Báo giá theo format chi tiết như Phase 1 với business rules, use case, actor, luồng chính, output và trạng thái
- [ ] 2.2 Viết lại section 4.3 Đơn đặt hàng bán theo format chi tiết như Phase 1 với luồng giao hàng, duyệt đơn và trạng thái đơn hàng
- [ ] 2.3 Viết lại section 4.4 Hợp đồng bán theo format chi tiết như Phase 1 với điều khoản thanh toán, điều khoản giao hàng, thực hiện hợp đồng và thanh lý/dừng thực hiện
- [ ] 2.4 Viết lại section 4.6 Bán hàng hóa / dịch vụ theo format chi tiết như Phase 1 với doanh thu, thuế, bán thu tiền ngay, bán chịu, ghi sổ và hoàn thành chứng từ
- [ ] 2.5 Bổ sung các khối liên kết dữ liệu liên phân hệ cho báo giá, đơn hàng, hợp đồng và chứng từ bán hàng

## 3. Chi tiết hóa chính sách giá và hóa đơn bán ra

- [ ] 3.1 Viết lại section 4.5 Chính sách giá, bảng giá & chiết khấu với business rules có mã, use case và thứ tự ưu tiên áp dụng giá
- [ ] 3.2 Bổ sung luồng áp dụng giá và kiểm soát giá sàn khi lập báo giá/đơn hàng/chứng từ bán hàng
- [ ] 3.3 Viết lại section 4.7 Hóa đơn bán ra với luồng phát hành, gửi khách hàng, điều chỉnh, thay thế, hủy và kê khai thuế GTGT đầu ra
- [ ] 3.4 Bổ sung luồng trạng thái hóa đơn, liên kết dữ liệu với bán hàng/công nợ/sổ cái và các báo cáo hóa đơn liên quan

## 4. Chi tiết hóa giao hàng, giảm trừ doanh thu và phải thu khách hàng

- [ ] 4.1 Viết lại section 4.8 Xuất kho bán hàng với kiểm tra tồn, duyệt phiếu xuất, ghi sổ, cập nhật tồn kho, tính giá vốn và đảo phiếu xuất
- [ ] 4.2 Viết lại section 4.9 Hàng bán bị trả lại & giảm giá hàng bán với kiểm tra hàng trả, nhập kho lại, giảm công nợ, hoàn tiền, hóa đơn điều chỉnh và báo cáo giảm trừ doanh thu
- [ ] 4.3 Viết lại section 4.10 Công nợ phải thu khách hàng với hạn mức tín dụng, đến hạn/quá hạn, aging, đối trừ, đánh giá ngoại tệ và tất toán công nợ
- [ ] 4.4 Viết lại section 4.11 Thu tiền khách hàng với thu tiền mặt, thu ngân hàng, thu nhiều hóa đơn, thu đặt cọc, thu ngoại tệ, duyệt, ghi sổ và đối chiếu sao kê
- [ ] 4.5 Bổ sung các khối liên kết xuyên chu trình giữa xuất kho, giá vốn, hóa đơn, công nợ, thu tiền và giảm trừ doanh thu

## 5. Chi tiết hóa báo cáo, bút toán và đối chiếu với OpenSpec

- [ ] 5.1 Viết lại section 4.12 Báo cáo bán hàng, doanh thu & công nợ phải thu theo format chi tiết như Phase 1 với dashboard, doanh thu thuần, lợi nhuận gộp, aging, nợ quá hạn và KPI bán hàng
- [ ] 5.2 Cập nhật bảng định khoản mẫu — Giai đoạn 3 để phản ánh đầy đủ doanh thu, thuế đầu ra, giá vốn, phải thu, thu tiền và giảm trừ doanh thu theo DOCX
- [ ] 5.3 Cập nhật quy tắc nghiệp vụ chung của Giai đoạn 3 để đồng bộ với business rules mới của tài liệu accountant
- [ ] 5.4 Hoàn thiện capability `phase3-sales-detail` theo nội dung HTML đã chi tiết hóa
- [ ] 5.5 Hoàn thiện capability `phase3-pricing-and-invoicing-detail` theo nội dung HTML đã chi tiết hóa
- [ ] 5.6 Hoàn thiện capability `phase3-fulfillment-and-receivables-detail` theo nội dung HTML đã chi tiết hóa
- [ ] 5.7 Cập nhật delta spec `general-ledger` để đồng bộ các điểm ghi sổ từ nghiệp vụ Phase 3
- [ ] 5.8 Rà soát cuối toàn bộ Phase 3 để đảm bảo không còn section chỉ dừng ở bảng summary, không phát sinh nested table và không mâu thuẫn với Phase 1 / Phase 2