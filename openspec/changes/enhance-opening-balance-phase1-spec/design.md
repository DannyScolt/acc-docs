## Context

Module `2.2.10. Số dư đầu kỳ` trong tài liệu nghiệp vụ gốc mới mô tả danh sách chức năng ở mức khái quát: nhập các loại số dư, import, kiểm tra cân đối và khóa số dư đầu kỳ. Trong quá trình rà soát với `Phase1-nghiep-vu-lap-trinh.html`, đã lộ ra ba vấn đề:

1. Tài liệu nghiệp vụ thiếu lớp vận hành: chưa mô tả rõ xem/sửa/xóa khi chưa khóa, mở khóa, lịch sử thay đổi, export/báo cáo và xử lý import thực tế.
2. Tài liệu nghiệp vụ và tài liệu kỹ thuật có vài điểm lệch nhau: ví dụ công nợ đầu kỳ yêu cầu có hạn thanh toán trong file gốc, nhưng bản kỹ thuật đang xem đây là trường mở rộng; phần tiền mặt/ngân hàng đầu kỳ có trong list chức năng nhưng chưa được đặc tả kỹ ở full spec.
3. Phase 1 chỉ nên nhập skeleton đầu kỳ cho AR/AP/tồn kho/TSCĐ/CCDC/CPTT; không nên kéo tuổi nợ, khấu hao, phân bổ định kỳ, điều chuyển, thanh lý hoặc vận hành đầy đủ của Phase 2/3/6 vào change này.

Stakeholders chính của change này là BA, kế toán trưởng, lập trình viên và QA — những người cần một đặc tả đủ chặt để triển khai module Số dư đầu kỳ mà không hiểu sai phạm vi Phase 1.

## Goals / Non-Goals

**Goals:**
- Làm rõ đầy đủ chức năng vận hành của module Số dư đầu kỳ trong Phase 1.
- Đồng bộ lại nghiệp vụ gốc và bản kỹ thuật ở các điểm đang lệch.
- Bổ sung use case, luồng ngoại lệ và business rules để BA/dev/QA cùng dùng được.
- Giữ ranh giới Phase 1 rõ ràng: cho nhập đầu kỳ và đối chiếu với sổ cái, không mở rộng sang vòng đời nghiệp vụ đầy đủ của các phase sau.

**Non-Goals:**
- Không thiết kế API, payload hoặc UI chi tiết mức wireframe.
- Không thêm nghiệp vụ đầy đủ cho công nợ, kho, TSCĐ, CCDC, chi phí trả trước thuộc Phase 2/3/6.
- Không thay đổi code ứng dụng trong design này.
- Không giải quyết kiến trúc triển khai DB/cloud/on-prem — đây là chủ đề khác ngoài phạm vi opening balance.

## Decisions

### Decision 1: Tách nhóm chức năng thành 6 lớp thay vì chỉ “nhập / kiểm tra / khóa”
**Quyết định:** Đặc tả mới sẽ chia module Số dư đầu kỳ thành 6 nhóm: quản lý dữ liệu, import, đối chiếu, khóa/mở khóa, lịch sử/audit và báo cáo/export.

**Lý do:** Đây là cách phản ánh đúng nhu cầu vận hành thực tế và bám tinh thần các phân hệ khác trong tài liệu gốc (đều có import/export, audit, trạng thái, đối chiếu).

**Alternative rejected:** Giữ nguyên list 12 chức năng cũ rồi chỉ thêm vài rule bên dưới. Cách này gọn hơn nhưng không đủ cho triển khai.

### Decision 2: Bổ sung đầy đủ đối chiếu chi tiết theo từng loại số dư
**Quyết định:** Không giữ một dòng “kiểm tra cân đối số dư” chung chung; thay vào đó phải tách rõ đối chiếu TK tổng hợp, AR, AP, tồn kho, tiền mặt, tiền gửi, TSCĐ, CCDC và chi phí trả trước.

**Lý do:** Các nhóm dữ liệu này có công thức đối chiếu khác nhau và map sang các tài khoản tổng hợp khác nhau (111, 112, 131, 331, 152/156, 211/214, 242...). Nếu gộp chung sẽ khó test và dễ bỏ sót.

**Alternative rejected:** Chỉ giữ một chức năng “kiểm tra cân đối” và giải thích bằng note. QA và dev sẽ khó chuyển thành checklist kiểm thử rõ ràng.

### Decision 3: Giữ skeleton Phase 1 cho AR/AP/tồn kho/TSCĐ/CCDC/CPTT
**Quyết định:** Cho phép nhập đầu kỳ đầy đủ ở mức skeleton và đối chiếu với sổ cái, nhưng không đưa các hành vi đầy đủ của phase sau vào capability này.

**Lý do:** File gốc đã định vị rõ AR đầy đủ ở Phase 3, AP và kho ở Phase 2, tài sản/CCDC/CPTT ở Phase 6. Change này phải làm rõ đầu kỳ mà không làm mờ ranh giới phase.

**Alternative rejected:** Thêm luôn tuổi nợ, khấu hao, phân bổ định kỳ hoặc điều chuyển vào đặc tả này. Điều đó sẽ làm phình Phase 1 sai phạm vi.

### Decision 4: Hạn thanh toán của công nợ đầu kỳ được nhập ngay trong Phase 1
**Quyết định:** Dữ liệu AR/AP opening SHALL cho phép nhập `due_date` ngay từ đầu kỳ, nhưng các chức năng tuổi nợ/cảnh báo/quản trị đến hạn vẫn để ở phase sau.

**Lý do:** Tài liệu gốc đã nêu rõ công nợ đầu kỳ theo chứng từ và hạn thanh toán. Không nhập ngay sẽ làm lệch với nguồn nghiệp vụ gốc.

**Alternative rejected:** Để `due_date` hoàn toàn sang phase sau. Cách này đơn giản cho kỹ thuật nhưng mất thông tin đầu vào mà nghiệp vụ đã yêu cầu.

### Decision 5: Bổ sung rõ tiền mặt đầu kỳ và ngân hàng đầu kỳ như luồng nhập riêng
**Quyết định:** Đặc tả phải mô tả rõ nhập số dư tiền mặt đầu kỳ và số dư tài khoản ngân hàng đầu kỳ, thay vì chỉ ngầm hiểu qua `opening_balance`.

**Lý do:** File gốc đã liệt kê riêng hai chức năng này. Nếu bản kỹ thuật không làm rõ, BA/dev sẽ dễ bỏ qua luồng thao tác hoặc chỉ dựa vào số dư tài khoản tổng hợp.

**Alternative rejected:** Xem chúng là hệ quả tự nhiên của nhập TK 111 / 112 nên không cần chức năng riêng. Điều đó khiến tài liệu khó dùng với người nghiệp vụ.

### Decision 6: Mở khóa là chức năng có quyền cao, bắt buộc audit và lý do
**Quyết định:** Mở khóa số dư đầu kỳ chỉ dành cho role có quyền cao (`unlock_opening`), phải ghi lý do và audit log; tài liệu sẽ nêu rõ đây là thao tác ngoại lệ.

**Lý do:** Mở khóa có rủi ro cao và ảnh hưởng độ tin cậy của dữ liệu đầu kỳ.

**Alternative considered:** Chỉ admin được mở khóa; hoặc admin và kế toán trưởng đều được mở khóa. Change này sẽ không khóa cứng tên role, mà khóa theo permission để tài liệu nghiệp vụ và kỹ thuật có thể thống nhất bằng quyền hệ thống.

## Risks / Trade-offs

- **[Mở rộng quá tay sang phase sau]** → Mitigation: Ghi rõ “skeleton only” cho AR/AP/kho/TSCĐ/CCDC/CPTT và nêu explicit non-goals.
- **[Mâu thuẫn giữa file nghiệp vụ và file kỹ thuật]** → Mitigation: Dùng change này để chốt lại wording thống nhất ở các điểm lệch như `due_date`, tiền mặt/ngân hàng đầu kỳ, unlock permission.
- **[Chức năng quá nhiều làm list dài]** → Mitigation: Gom theo nhóm vận hành và ưu tiên các chức năng thật sự ảnh hưởng BA/dev/QA; không lôi thêm workflow UI chi tiết.
- **[Quyền mở khóa bị hiểu theo vai trò cứng]** → Mitigation: Đặc tả theo permission (`unlock_opening`) và nêu ví dụ role điển hình thay vì hard-code duy nhất một role.

## Open Questions

- Do nghiệp vụ có muốn định nghĩa danh mục “quỹ” riêng hay chỉ quản lý tiền mặt đầu kỳ theo TK 111 / tiểu khoản tiền mặt?
- Ở tài liệu nghiệp vụ cuối cùng, có muốn gọi thẳng role “Admin hoặc Kế toán trưởng” cho mở khóa, hay muốn chuẩn hóa theo quyền hệ thống `unlock_opening`?
- Có cần xuất riêng “biên bản đối chiếu số dư đầu kỳ” hay chỉ cần báo cáo + Excel đối chiếu?
