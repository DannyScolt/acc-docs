## Context

Phase 4 trong HTML hiện tại đã có khung module tương đối khớp với tài liệu accountant ở các mục 5.2–5.9, nhưng phần nội dung bên trong vẫn chủ yếu là bảng summary liệt kê chức năng. Trong khi đó, file DOCX kế toán đã cung cấp chi tiết hơn nhiều: use case có mã, actor, luồng nghiệp vụ, luồng chính, business rule, liên kết với phân hệ khác và kết quả đầu ra cho từng module tổng hợp cuối kỳ.

Phase 4 là lớp nghiệp vụ hội tụ dữ liệu từ gần như toàn bộ hệ thống: quỹ, ngân hàng, công nợ phải thu, công nợ phải trả, kho, doanh thu, thuế và sổ cái. Vì vậy design cần ưu tiên hai điều: nâng độ sâu tài liệu mà không làm vỡ cấu trúc hiện tại vốn đã khá đúng, và bảo đảm mọi mô tả mới vẫn nhất quán với các phase/accounting change đã hoàn thành trước đó.

## Goals / Non-Goals

**Goals:**
- Viết lại Phase 4 theo chuẩn chi tiết thống nhất với Phase 1: use case, actor, luồng nghiệp vụ, luồng chính, business rules, liên kết phân hệ, output, bút toán và tiêu chí kiểm tra.
- Giữ khung chapter lớn 5.2–5.9 khi đã phù hợp với source accountant, chỉ nâng độ sâu nội dung bên trong.
- Tách Phase 4 thành các capability OpenSpec rõ ràng theo cụm nghiệp vụ: điều chỉnh & kết chuyển, đối chiếu & sổ cái, báo cáo tài chính.
- Đồng bộ yêu cầu với `general-ledger` để trace được luồng ghi sổ, kết chuyển, khóa kỳ và truy vết từ báo cáo về sổ sách/chứng từ gốc.

**Non-Goals:**
- Không triển khai phần mềm; chỉ cập nhật tài liệu nghiệp vụ và OpenSpec.
- Không thay đổi lại cấu trúc lớn của Phase 4 nếu không có mâu thuẫn thực sự với DOCX accountant.
- Không mở rộng thêm các phân hệ riêng mới ngoài những gì tài liệu nguồn đã mô tả.
- Không chỉnh sửa nội dung phase khác ngoài phạm vi cross-reference cần thiết để giữ tính nhất quán nghiệp vụ.

## Decisions

1. **Giữ nguyên trục 5.2–5.9, không remap lớn như Phase 3**
   - HTML hiện tại đã tương đối khớp với source accountant ở cấp section lớn.
   - Thay đổi chính sẽ là rewrite nội dung bên trong mỗi section từ summary sang detailed spec.
   - **Rationale:** Tránh thay đổi cấu trúc không cần thiết, giảm rủi ro lan sang TOC, anchor và mối liên hệ giữa các phase.
   - **Alternative considered:** Tái cấu trúc lại toàn bộ Phase 4. Bị loại vì chưa có bằng chứng lệch cấu trúc mạnh như Phase 3.

2. **Chia Phase 4 thành 3 capability nghiệp vụ**
   - `phase4-adjustments-and-period-close-detail`: chứng từ nghiệp vụ khác, quyết toán tạm ứng, phân bổ, cấu hình kết chuyển, kết chuyển cuối kỳ.
   - `phase4-reconciliation-and-ledger-detail`: đối chiếu trước khóa kỳ, khóa/mở kỳ, sổ kế toán tổng hợp.
   - `phase4-financial-reporting-detail`: bộ báo cáo tài chính, kiểm tra cân đối, drill-down và versioning báo cáo.
   - **Rationale:** Phase 4 có thể chia tự nhiên theo dòng nghiệp vụ và dòng báo cáo, giúp review/apply đơn giản hơn.
   - **Alternative considered:** Gom tất cả vào một capability `phase4-closing-detail`. Bị loại vì quá lớn và khó trace.

3. **Mỗi section phải nâng từ “liệt kê chức năng” thành “đặc tả kiểm thử được”**
   - Không chỉ nêu module có chức năng gì, mà phải thể hiện ai làm, theo luồng nào, rule kiểm soát nào áp dụng, output là gì, và liên kết phân hệ nào được dùng.
   - **Rationale:** Đây là giá trị cốt lõi của tài liệu accountant và là khoảng thiếu lớn nhất hiện tại.
   - **Alternative considered:** Chỉ thêm business rules tổng quát ở cuối Phase 4. Bị loại vì không đủ để dùng làm source cho implementation/test.

4. **Giữ pattern hiển thị giống Phase 1/2/3 accountant-style**
   - Mỗi module sẽ dùng mô hình lặp: mô tả module → rules/use cases → flow/linkage/output → nếu cần thì trạng thái hoặc bảng liên hệ.
   - Tránh nested table để không gây lỗi format HTML.
   - **Rationale:** Duy trì tính thống nhất của tài liệu toàn repo và hạn chế lỗi trình bày.
   - **Alternative considered:** Chuyển sang layout riêng cho Phase 4. Bị loại vì làm mất tính liên tục xuyên phase.

5. **Cập nhật `general-ledger` ở góc nhìn close/reporting controls**
   - Delta spec cho `general-ledger` sẽ nhấn vào ghi sổ chứng từ tổng hợp, kết chuyển, kiểm tra đối chiếu, khóa kỳ và truy vết từ báo cáo về sổ cái/chứng từ.
   - **Rationale:** Phase 4 là nơi hội tụ các control cuối kỳ, nên cần bổ sung capability xuyên suốt này.
   - **Alternative considered:** Chỉ cập nhật spec Phase 4 mới mà không đụng `general-ledger`. Bị loại vì sẽ làm đứt traceability với core accounting controls.

## Risks / Trade-offs

- **[Phase 4 hội tụ dữ liệu từ nhiều phân hệ, dễ mâu thuẫn mô tả]** → Mitigation: bám sát source accountant và chỉ cross-reference, không tự tái định nghĩa logic ở phase khác.
- **[Vì khung section hiện tại đã ổn, dễ chủ quan và chỉ chỉnh nhẹ]** → Mitigation: coi mỗi mục 5.2–5.9 là một module cần rewrite ở mức đặc tả, không chỉ bổ sung vài dòng rule.
- **[Số lượng control/rule nhiều, tài liệu dài]** → Mitigation: chia capability theo cụm close, reconciliation/ledger, reporting; chia task nhỏ theo từng section.
- **[Báo cáo tài chính và đối chiếu cuối kỳ là vùng nhạy cảm với tính đúng sai kế toán]** → Mitigation: giữ nguyên tinh thần tài liệu nguồn, không tự thêm công thức hoặc quy định ngoài source nếu chưa có căn cứ.
- **[Nguy cơ lặp với Phase 1 general ledger hoặc Phase 5 reporting/tax]** → Mitigation: chỉ mô tả các control cuối kỳ và mối liên hệ cần thiết, không sao chép nguyên nội dung phase khác.