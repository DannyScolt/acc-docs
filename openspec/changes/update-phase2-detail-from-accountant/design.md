## Context

Phase 1 đã được nâng lên mức chi tiết cao với use case, actor, luồng chính, business rules, workflow và ảnh hưởng kế toán cho các phân hệ nền tảng, quỹ, ngân hàng và sổ cái. Trong khi đó Phase 2 hiện vẫn chủ yếu là các bảng `STT / Chức năng / Mô tả`, chưa đủ để kế toán review đầy đủ hoặc để dev/tester triển khai mà không tự suy diễn.

Phase 2 bao phủ chu trình mua hàng, nhập kho, hóa đơn đầu vào, công nợ phải trả, thanh toán nhà cung cấp và kho. Đây là chu trình có nhiều điểm giao nhau với Phase 1: thanh toán qua quỹ/ngân hàng, ghi sổ sổ cái, công nợ phải trả và tồn kho. Vì vậy cần nâng Phase 2 lên cùng độ sâu với Phase 1.

## Goals / Non-Goals

**Goals:**
- Viết lại Phase 2 theo chuẩn chi tiết thống nhất: danh sách UC, actor, điều kiện, dữ liệu đầu vào, luồng chính, kết quả, business rules, workflow và ảnh hưởng kế toán.
- Ưu tiên chi tiết hóa chu trình Procure-to-Pay: yêu cầu mua → đơn mua → hợp đồng → mua hàng/dịch vụ → nhận hàng/nhập kho → hóa đơn đầu vào → công nợ phải trả → thanh toán → trả lại/giảm giá → đối chiếu.
- Chi tiết hóa kho Phase 2: nhập kho, chuyển kho, kiểm kê, điều chỉnh tồn, thẻ kho và báo cáo tồn.
- Bổ sung các rule có mã để kế toán/dev/tester có thể trace requirement.
- Giữ nguyên cấu trúc phase tổng thể, chỉ nâng độ sâu nội dung Phase 2.

**Non-Goals:**
- Không thay đổi nội dung Phase 1 đã cập nhật.
- Không triển khai phần mềm, chỉ cập nhật tài liệu nghiệp vụ và OpenSpec.
- Không chi tiết hóa Phase 3–6 trong change này.
- Không chốt các tài khoản kế toán còn cần kế toán xác nhận nếu tài liệu nguồn chưa đủ; ghi chú rõ nếu cần xác nhận.

## Decisions

1. **Chia Phase 2 thành 3 capability chính**
   - `phase2-procurement-detail`: mua hàng, hợp đồng, hóa đơn, AP, thanh toán và đối chiếu công nợ.
   - `phase2-inventory-detail`: nhận hàng, nhập kho, chuyển kho, kiểm kê và tồn kho.
   - `phase2-reporting-detail`: báo cáo, định khoản, quy tắc chung và nghiệm thu.
   - Rationale: Phase 2 quá rộng để quản lý trong một capability duy nhất; chia theo cụm giúp apply/review dễ hơn.

2. **Dùng prefix mã rõ ràng cho use case và business rules**
   - UC đề xuất: `UC-P2-xx` cho use case Phase 2.
   - Rule đề xuất: `BR-P2-PO-*`, `BR-P2-PUR-*`, `BR-P2-AP-*`, `BR-P2-INV-*`, `BR-P2-RPT-*`, `BR-P2-G-*`.
   - Rationale: Giữ traceability giống Phase 1 nhưng tránh nhầm với mã BR của quỹ/ngân hàng/sổ cái.

3. **Không dùng nested table trong HTML**
   - Mỗi UC hoặc nhóm rule dùng bảng độc lập hoặc paragraph/list đơn giản.
   - Rationale: Tránh lỗi HTML table nesting và giữ tài liệu dễ đọc.

4. **Giữ bảng định khoản mẫu Phase 2 nhưng mở rộng bằng rule/ghi chú**
   - Rationale: Bảng định khoản hiện có là điểm kiểm soát kế toán quan trọng; change này không thay thế hoàn toàn mà bổ sung ngữ cảnh, rule và các nghiệp vụ còn thiếu nếu có.

## Risks / Trade-offs

- **Phase 2 rất rộng** → Chia task theo cụm nghiệp vụ để có thể apply tuần tự và kiểm tra từng phần.
- **Thiếu tài liệu kế toán nguồn cho một số ngoại lệ** → Ghi rõ các điểm cần kế toán xác nhận thay vì tự suy diễn.
- **Nội dung HTML dài hơn nhiều** → Dùng format giống Phase 1, heading rõ ràng, bảng/lists ngắn theo từng UC.
- **Có thể trùng với logic Phase 1 về thanh toán/ngân hàng/sổ cái** → Cross-reference bằng mô tả ảnh hưởng kế toán, không sửa Phase 1 trong change này.
