## Context

HTML `ACC-noi-dung-nghiep-vu-theo-phase.html` section 2.5 hiện chỉ có bảng tóm tắt chức năng cho 4 nhóm: Ghi sổ kế toán, Sổ cái, Sổ nhật ký chung và Bảng cân đối phát sinh. Người dùng cung cấp nội dung kế toán chi tiết hơn, tương tự mức chi tiết đã cập nhật cho section 2.3 Tiền mặt/Quỹ và 2.4 Tiền gửi ngân hàng.

Spec nền `general-ledger` trong change `phase1-nghiep-vu-lap-trinh` đã có các requirement cốt lõi cho journal entry, sổ cái, nhật ký chung và bảng cân đối phát sinh. Change này bổ sung lớp mô tả nghiệp vụ chi tiết hơn cho tài liệu HTML và mở rộng delta spec để capture các business rules theo mã BR-GL, BR-LEDGER, BR-JE, BR-TB và BR-GLOBAL.

## Goals / Non-Goals

**Goals:**
- Viết lại section 2.5 theo format chi tiết dạng bảng `Nội dung / Chi tiết` cho từng phân hệ con.
- Bổ sung đầy đủ mục tiêu, actor, chức năng, luồng chính, kết quả và business rules cho 2.5.1 ~ 2.5.4.
- Thêm block Business Rules toàn phân hệ Sổ cái & hệ thống tài khoản với BR-GLOBAL-01 ~ BR-GLOBAL-20.
- Cập nhật delta spec `general-ledger` để phản ánh các rule và scenario mới.
- Giữ ranh giới section: nội dung mới nằm sau 2.5 và trước `Bảng định khoản mẫu — Giai đoạn 1`.

**Non-Goals:**
- Không sửa section 2.3 hoặc 2.4.
- Không thay đổi bảng định khoản mẫu Giai đoạn 1 trong lần cập nhật này.
- Không thiết kế thêm database schema mới ngoài những gì spec nền `general-ledger` đã có.
- Không triển khai phần mềm, chỉ cập nhật tài liệu nghiệp vụ/spec.

## Decisions

1. **Giữ cấu trúc 4 subsection 2.5.1 ~ 2.5.4**
   - Rationale: Đây là cấu trúc hiện có trong HTML và khớp nội dung kế toán bổ sung.
   - Alternative considered: Thêm subsection mới cho Business Rules toàn phân hệ dưới số 2.5.5. Không chọn vì nội dung người dùng cung cấp là block rules toàn phân hệ, không phải module chức năng độc lập.

2. **Dùng bảng hai cột `Nội dung / Chi tiết` cho từng subsection**
   - Rationale: Nội dung kế toán cung cấp đã ở format này, dễ đọc và ít tạo nested table.
   - Alternative considered: Dùng nhiều bảng nhỏ cho actor/flow/rules. Không chọn vì section 2.5 sẽ dài và khó scan.

3. **Giữ mã rule nguyên văn theo tài liệu kế toán**
   - Rationale: `BR-GL-*`, `BR-LEDGER-*`, `BR-JE-*`, `BR-TB-*`, `BR-GLOBAL-*` giúp kế toán/dev đối chiếu trực tiếp.
   - Alternative considered: Chuẩn hóa lại sang một chuỗi BR duy nhất. Không chọn để tránh mất traceability với tài liệu gốc.

4. **Delta spec dùng ADDED requirements thay vì sửa toàn bộ requirement cũ**
   - Rationale: Spec nền đã có entity/scenario cốt lõi; change này bổ sung mô tả chi tiết và rule mới mà không thay đổi hành vi đã mô tả.
   - Alternative considered: MODIFIED toàn bộ requirement cũ. Không chọn để tránh copy lại nhiều nội dung entity/table không liên quan trực tiếp tới thiếu sót HTML.

## Risks / Trade-offs

- **Nội dung dài hơn đáng kể** → Giảm rủi ro bằng format bảng hai cột, giữ các rule trong một dòng có phân tách rõ ràng.
- **Có thể trùng một số rule với spec nền** → Chấp nhận trùng ở mức mô tả vì rule mới có mã định danh kế toán riêng và phục vụ đối chiếu nghiệp vụ.
- **HTML có thể phát sinh lỗi table nesting nếu dùng bảng trong bảng** → Không dùng nested table; mỗi subsection là một bảng độc lập.
- **Một số rule liên quan module ngoài Phase 1 như TSCĐ, lương** → Giữ nguyên vì người dùng cung cấp trong phạm vi chức năng ghi sổ từ các phân hệ, nhưng không triển khai thêm module ngoài tài liệu.
