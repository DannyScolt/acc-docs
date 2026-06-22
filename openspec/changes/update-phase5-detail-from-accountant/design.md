## Context

Phase 1 đã được nâng lên mức chi tiết cao với cấu trúc gồm phân hệ, danh sách chức năng, use case có mã, actor, điều kiện, luồng chính, trạng thái chứng từ, business rules có mã, workflow tổng thể, bảng định khoản và tiêu chí nghiệm thu. Trong khi đó Phase 5 hiện vẫn chủ yếu là các bảng `STT / Chức năng / Mô tả` và một flow tổng quan ngắn, chưa đủ để kế toán review hoặc để dev/tester triển khai mà không tự suy diễn.

Phase 5 bao phủ chuỗi nghiệp vụ hóa đơn điện tử và thuế: kết nối nền tảng hóa đơn, quản lý hóa đơn đầu vào/đầu ra, kiểm tra hợp lệ và cảnh báo rủi ro, xử lý hóa đơn sai sót, bảng kê hóa đơn, kê khai thuế, giấy nộp tiền và báo cáo thuế. Các nội dung này giao cắt mạnh với Phase 1 ở quỹ, ngân hàng, sổ cái và các nguyên tắc khóa kỳ/truy vết chứng từ nguồn. Vì vậy change này cần giữ nguyên khung phân hệ Phase 5 nhưng nâng độ sâu lên mức tương đương Phase 1.

## Goals / Non-Goals

**Goals:**
- Viết lại Phase 5 theo chuẩn chi tiết thống nhất với Phase 1: phân hệ rõ, use case có mã, actor, điều kiện, dữ liệu đầu vào, luồng chính, luồng ngoại lệ, kết quả, workflow/trạng thái và business rules.
- Chi tiết hóa cụm hóa đơn điện tử gồm kết nối nền tảng, hóa đơn đầu vào, hóa đơn đầu ra, kiểm tra hợp lệ/cảnh báo rủi ro và xử lý hóa đơn sai sót.
- Chi tiết hóa cụm kê khai thuế gồm bảng kê hóa đơn, tờ khai thuế, giấy nộp tiền và báo cáo thuế.
- Mở rộng bảng định khoản mẫu, quy tắc nghiệp vụ chung và tiêu chí nghiệm thu để kế toán/dev/tester có thể dùng làm căn cứ review và kiểm thử.
- Đồng bộ các ảnh hưởng ghi sổ của Phase 5 với capability `general-ledger`.

**Non-Goals:**
- Không thay đổi nội dung Phase 1 đã hoàn thiện.
- Không triển khai phần mềm; chỉ cập nhật tài liệu HTML và OpenSpec.
- Không chi tiết hóa Phase 2, Phase 3, Phase 4 hoặc Phase 6 trong change này.
- Không chốt các tài khoản kế toán đặc thù doanh nghiệp nếu nguồn hiện tại chưa đủ; chỉ ghi nhận chỗ cần xác nhận.

## Decisions

1. **Giữ nguyên khung phân hệ 6.1–6.9, chỉ nâng độ sâu bên trong**
   - Phase 5 hiện đã có khung phân hệ hợp lý theo mạch nghiệp vụ hóa đơn điện tử và thuế.
   - Thay vì tách/gộp lại chương lớn, change này giữ nguyên cấu trúc 6.1–6.9 để tránh ảnh hưởng bố cục toàn tài liệu và tập trung vào chi tiết hóa nội dung mỗi phân hệ.

2. **Chia Phase 5 thành 3 capability chính**
   - `phase5-einvoice-detail`: bao phủ 6.2–6.6.
   - `phase5-tax-declaration-detail`: bao phủ 6.7–6.9.
   - `phase5-reporting-controls-detail`: bao phủ 6.1 và phần cuối phase gồm định khoản, quy tắc chung, kết quả bàn giao, tiêu chí nghiệm thu.
   - Rationale: Phase 5 đủ rộng để cần tách theo cụm nghiệp vụ chính, giúp review/apply theo logical area thay vì một spec quá lớn.

3. **Dùng mã use case và business rules theo prefix riêng cho Phase 5**
   - UC đề xuất: `UC-EINV-*` cho nghiệp vụ hóa đơn điện tử, `UC-TAX-*` cho bảng kê/tờ khai/nghĩa vụ thuế.
   - Rule đề xuất: `BR-EINV-*`, `BR-TAX-*`, `BR-P5-G-*` cho quy tắc chung toàn giai đoạn.
   - Rationale: Giữ traceability giống Phase 1 nhưng tránh nhầm với mã ngân hàng/quỹ/sổ cái đã tồn tại.

4. **Mỗi phân hệ phải được viết theo một khung cố định**
   - Khung mục tiêu: Mục tiêu → Actor → Danh sách chức năng/use case → Điều kiện & dữ liệu đầu vào → Luồng chính → Luồng ngoại lệ (nếu cần) → Kết quả → Business rules → Workflow/trạng thái → Ảnh hưởng kế toán/thuế/báo cáo.
   - Rationale: Đây là cách gần nhất với chuẩn Phase 1 và giúp các phân hệ Phase 5 đồng nhất với nhau.

5. **Không dùng nested table trong HTML**
   - Mỗi nhóm use case hoặc nhóm rule dùng bảng độc lập hoặc list/paragraph rõ ràng.
   - Rationale: Tránh lỗi HTML khó đọc, khó bảo trì, và phù hợp cách đã áp dụng ở cập nhật phần sổ cái.

6. **Bảng định khoản mẫu và rule chung chỉ là lớp cuối, không thay cho rule từng phân hệ**
   - Bảng định khoản được mở rộng bằng ngữ cảnh và ví dụ phát sinh thuế; rule chung chỉ nêu nguyên tắc toàn phase.
   - Rule vận hành chi tiết vẫn phải xuất hiện ngay trong từng phân hệ 6.2–6.9.
   - Rationale: Tránh tài liệu bị “dồn rule xuống cuối” làm dev/test phải tự map ngược.

7. **Delta `general-ledger` chỉ mô tả ảnh hưởng ghi sổ, không thay thế các spec Phase 5 mới**
   - Capability `general-ledger` sẽ nhận thêm requirement về truy vết bút toán từ hóa đơn đầu vào/đầu ra, kê khai, khấu trừ và nộp thuế.
   - Rationale: Giữ ranh giới rõ giữa nghiệp vụ Phase 5 và logic ghi sổ tổng hợp.

## Risks / Trade-offs

- **[Phase 5 rộng và nhiều điểm giao cắt]** → Chia capability theo cụm hóa đơn / kê khai / controls để dễ review và apply từng phần.
- **[Có thể tự suy diễn rule thuế quá mức]** → Chỉ ghi các rule chắc chắn từ tài liệu hiện có và chuẩn hóa ở mức quy trình; chỗ đặc thù doanh nghiệp thì ghi chú cần xác nhận.
- **[Nội dung HTML sẽ dài hơn nhiều]** → Dùng heading, bảng 2 cột và nhóm use case/rule ngắn để giữ tài liệu đọc được như Phase 1.
- **[Trùng lặp với Phase 1 về quỹ/ngân hàng/sổ cái]** → Chỉ cross-reference ở phần ảnh hưởng kế toán và workflow, không sửa trực tiếp các section Phase 1 trong change này.
