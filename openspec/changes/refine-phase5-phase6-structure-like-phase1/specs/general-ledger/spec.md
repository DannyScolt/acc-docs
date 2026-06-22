## ADDED Requirements

### Requirement: Cấu trúc refine của Phase 5 và Phase 6 phải tăng độ rõ của checkpoint ghi sổ
Tài liệu `general-ledger` SHALL phản ánh rằng khi Phase 5 và Phase 6 được chia nhỏ thành các cụm vận hành rõ hơn, các điểm phát sinh ghi sổ, phê duyệt, khóa kỳ và truy vết chứng từ nguồn cũng phải được xác định rõ hơn theo từng checkpoint.

#### Scenario: Review posting checkpoints sau khi refine
- **WHEN** người dùng đối chiếu các cụm nghiệp vụ nhỏ hơn của Phase 5 hoặc Phase 6 với nguyên tắc sổ cái
- **THEN** tài liệu SHALL giúp xác định rõ hơn cụm nào chỉ review dữ liệu, cụm nào tạo bút toán, cụm nào yêu cầu phê duyệt hoặc bị chặn bởi khóa kỳ

## IMPLEMENTATION STATUS: DONE

Phân loại posting checkpoint sau khi refine:

**Phase 5 — chỉ review dữ liệu (không tạo bút toán):**
- 6.2.x Kết nối / đồng bộ HĐĐT
- 6.3.1 Tiếp nhận & tra cứu hóa đơn đầu vào
- 6.5.1 Kiểm tra tự động & phân loại cảnh báo
- 6.7.1 Lập & rà soát bảng kê
- 6.8.1 Lập tờ khai (trước khi chốt)

**Phase 5 — tạo bút toán / ảnh hưởng sổ cái:**
- 6.3.2 Liên kết chứng từ (liên kết hóa đơn với chứng từ kế toán)
- 6.8.2 Chốt tờ khai & nộp thuế (lập giấy nộp tiền → ghi giảm tiền)

**Phase 6 — chỉ review / theo dõi:**
- 7.0 Workflow tổng thể
- 7.8.1–7.8.3 Dashboard / phân tích / dự báo / ngân sách

**Phase 6 — tạo bút toán:**
- 7.1.2 Khấu hao định kỳ (TK 627/641/642 — 214)
- 7.2.2 Phân bổ CCDC / CPTT (TK 627/641/642 — 242)
- 7.3.2 Hạch toán lương (TK 622/627/641/642 — 334)
- 7.3.3 Trả lương (TK 334 — 111/112)
- 7.4.3 Kết chuyển giá thành (TK 154/155/632)
- 7.5.2 Giải ngân & lãi vay (TK 112 — 341; TK 635 — 335)
- 7.5.3 Thanh toán nợ (TK 341 — 112)
- 7.7.2 Tạo chứng từ từ giao dịch e-banking (theo bản chất nghiệp vụ)
