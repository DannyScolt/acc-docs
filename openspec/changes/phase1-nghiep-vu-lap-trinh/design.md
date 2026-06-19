## Context

Phase 1 của phần mềm kế toán ACC bao gồm: quản trị hệ thống, danh mục dùng chung, số dư đầu kỳ, quỹ tiền mặt, tiền gửi ngân hàng, và sổ cái. Tài liệu nghiệp vụ hiện tại (`ACC-noi-dung-nghiep-vu-theo-phase.html`) mô tả ~180 chức năng ở mức kế toán review, nhưng thiếu data model, validation rules, state machine, side effects, và định khoản chi tiết.

**Vấn đề forward reference**: Phase 1 yêu cầu nhập số dư đầu kỳ chi tiết cho công nợ (theo hóa đơn), tồn kho (theo kho × mặt hàng), TSCĐ, CCDC — nhưng các entity này thuộc Phase 2/3/6. Cần quyết định schema skeleton ngay Phase 1.

**Output**: Tạo file HTML `Phase1-nghiep-vu-lap-trinh.html` chứa đặc tả kỹ thuật hoàn chỉnh cho lập trình viên.

## Goals / Non-Goals

**Goals:**
- Chuyển đổi mọi chức năng Phase 1 từ mô tả nghiệp vụ sang đặc tả kỹ thuật mà dev có thể code trực tiếp
- Giải quyết forward reference bằng skeleton entity — schema tối thiểu cho opening balance, ghi rõ sẽ mở rộng ở Phase nào
- Mở rộng bảng định khoản từ 6 dòng → ~25 nghiệp vụ đầy đủ, đánh dấu chỗ cần kế toán xác nhận
- Cung cấp data model (~35 entity), state machine, validation, side effects, quyền cho mỗi nghiệp vụ

**Non-Goals:**
- Không triển khai code — chỉ tạo tài liệu đặc tả
- Không thiết kế UI/UX chi tiết (wireframe, mockup)
- Không viết API spec (REST endpoint, payload) — tập trung business logic layer
- Không thay thế tài liệu hiện tại cho kế toán — tạo file mới song song
- Không mở rộng sang Phase 2-6

## Decisions

### Decision 1: Dùng skeleton entity cho opening balance (Phương án B)

**Quyết định**: Phase 1 sẽ dựng sẵn các bảng `ar_invoice_opening`, `ap_invoice_opening`, `inventory_opening`, `fixed_asset_opening`, `tool_opening`, `prepaid_opening` với schema tối thiểu đủ chứa opening balance chi tiết.

**Lý do**: Tài liệu hiện tại ở mục 2.2.10 đã ghi rõ "chi tiết theo từng khách hàng, hóa đơn, hạn thanh toán" và "chi tiết theo từng kho, từng mặt hàng" — nếu Phase 1 chỉ nhập số dư tổng (Phương án A), khách hàng sẽ phải nhập lại khi sang Phase 2/3, gây phiền và mất tin tưởng.

**Alternative rejected**: Phương án A (chỉ giữ số dư tổng theo tài khoản) — đơn giản hơn nhưng yêu cầu re-import dữ liệu ở các Phase sau.

### Decision 2: Phân 3 mức chi tiết cho đặc tả chức năng

**Quyết định**:
- **FULL block** (~40-50 chức năng): nghiệp vụ có side effect / định khoản — mô tả đầy đủ input fields, validation, state transition, side effects, định khoản, quyền, edge cases
- **COMPACT block** (~50-60 chức năng): CRUD danh mục có validation đặc biệt — liệt kê fields, validation rules chính, quyền
- **REFERENCE** (~80-90 chức năng): tra cứu / xuất báo cáo — chỉ tham chiếu entity + bộ lọc + drill-down

**Lý do**: 180+ chức năng mà viết FULL block tất cả → tài liệu quá dài (>100 trang), phần lớn CRUD đơn giản không cần mức chi tiết đó.

### Decision 3: State machine thống nhất cho tất cả chứng từ Phase 1

**Quyết định**: Mọi chứng từ (phiếu thu/chi, thu/chi NH, chuyển nội bộ) dùng chung state machine: `Draft → Pending Approval → Approved → Cancelled`. Chỉ chứng từ `Approved` mới sinh journal entry.

**Lý do**: Phase 1 chưa có nghiệp vụ phức tạp (trả lại hàng, giảm giá, ...) nên không cần trạng thái bổ sung. Giữ đơn giản để dev triển khai nhanh, Phase 2/3 mới mở rộng nếu cần.

### Decision 4: Journal entry sinh tự động từ chứng từ, không cho sửa trực tiếp

**Quyết định**: Khi chứng từ chuyển sang `Approved`, hệ thống tự động sinh `journal_entry` + `journal_entry_line`. Bút toán không cho sửa trực tiếp — muốn sửa phải hủy chứng từ gốc rồi tạo lại.

**Lý do**: Đảm bảo tính toàn vẹn dữ liệu — mọi bút toán trên sổ cái đều truy vết được về chứng từ gốc. Đây là quy tắc đã nêu ở mục 2.5.1.6 trong tài liệu hiện tại.

### Decision 5: Bảng định khoản đánh dấu rõ chỗ cần kế toán xác nhận

**Quyết định**: Mỗi dòng định khoản ghi rõ TK Nợ, TK Có, điều kiện áp dụng. Những chỗ có nhiều phương án (vd: phí NH hạch toán 6427 hay 635? Kiểm kê thừa hạch toán 3381 hay 711?) đánh dấu `[CẦN KẾ TOÁN XÁC NHẬN]` kèm các phương án để kế toán chọn.

**Lý do**: Dev không thể tự quyết chọn tài khoản kế toán. Bảng đầy đủ + đánh dấu rõ giúp kế toán fill nhanh, tránh trả lại tài liệu nhiều vòng.

### Decision 6: Format output là HTML cùng style với file hiện tại

**Quyết định**: File output `Phase1-nghiep-vu-lap-trinh.html` dùng cùng CSS framework với `ACC-noi-dung-nghiep-vu-theo-phase.html` để đồng bộ visual.

**Lý do**: Đội dự án đã quen đọc file HTML hiện tại, giữ format thống nhất tránh friction.

## Risks / Trade-offs

- **[Schema skeleton có thể phải refactor ở Phase sau]** → Mitigation: Ghi rõ trong mỗi skeleton entity field nào "sẽ mở rộng ở Phase X", dev biết trước schema sẽ evolve
- **[Bảng định khoản có chỗ chưa chốt với kế toán]** → Mitigation: Đánh dấu `[CẦN KẾ TOÁN XÁC NHẬN]`, dev có thể build trước phần đã chốt, chờ kế toán xác nhận phần còn lại
- **[Tài liệu ~40-45 trang, dài]** → Mitigation: Tổ chức theo module, có mục lục + internal links, dev chỉ cần đọc module đang làm
- **[Forward reference cho ngoại tệ]** → Phase 1 cấu hình tiền tệ (mục 2.1.1.5) nhưng chưa rõ có phát sinh nghiệp vụ ngoại tệ ngay Phase 1 không. Tài liệu sẽ đánh dấu phần chênh lệch tỷ giá là `[CẦN KẾ TOÁN XÁC NHẬN]`
