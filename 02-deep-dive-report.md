# 🏗️ Phase 3 — DEEP-DIVE (Nhóm)

**Bài toán đã chọn:** Card #1 — Vinpearl · Lọc phản ánh về vệ sinh phòng từ đánh giá của khách. [Xem Problem Scan](01-problem-scan.md)

**Phạm vi:** Rà soát đánh giá dạng văn bản theo lô 30 bản ghi và chuẩn bị danh sách để bộ phận buồng phòng kiểm tra. Quy trình và thời lượng dưới đây là giả định từ Problem Scan, cần được ca trưởng xác nhận và đo trên dữ liệu thực tế.

## 3.1. Current-State Workflow

Quy trình rà soát đánh giá và bàn giao phản ánh về vệ sinh phòng của ca trưởng Vinpearl.

```text
┌────────────────────────────┐       ┌────────────────────────────┐
│ Bước 1 [Handoff]           │       │ Bước 2 [Bottleneck]        │
│ Mở danh sách               │       │ Đọc và xác định            │
│ đánh giá                   │ ────→ │ phản ánh vệ sinh phòng     │
│ Ai: Ca trưởng              │       │ Ai: Ca trưởng              │
│ Thời gian: 1 phút          │       │ Thời gian: 6 phút          │
│ In: Nguồn phản hồi         │       │ In: Lô 30 đánh giá         │
│ Out: Lô 30 đánh giá        │       │ Out: Mục cần ghi nhận      │
└────────────────────────────┘       └────────────────────────────┘
                                                    │
                                                    ▼
┌────────────────────────────┐       ┌────────────────────────────┐
│ Bước 4 [Handoff]           │       │ Bước 3 [Bottleneck]        │
│ Bàn giao danh sách         │       │ Ghi mã đánh giá            │
│ cho bộ phận buồng phòng    │ ←──── │ và trích đoạn phản ánh     │
│ Ai: Ca trưởng              │       │ Ai: Ca trưởng              │
│ Thời gian: 1 phút          │       │ Thời gian: 4 phút          │
│ In: Danh sách tổng hợp     │       │ In: Mục cần ghi nhận       │
│ Out: Danh sách đã bàn giao │       │ Out: Danh sách tổng hợp    │
└────────────────────────────┘       └────────────────────────────┘
```

**Tổng cộng ước tính 12 phút/lô 30 đánh giá**, trong đó bước 2–3 chiếm 10 phút. Thời gian trên kết thúc khi ca trưởng chuyển danh sách. Bộ phận buồng phòng xử lý phản ánh theo quy trình riêng.

---

## 3.2. Problem Statement (6-field) — Vin Smart Future Standard

| Field | Nội dung |
|---|---|
| **1. Actor / Operator** | Ca trưởng Vinpearl phụ trách rà soát phản hồi của khách. Bộ phận buồng phòng tiếp nhận danh sách đã duyệt để xác minh và xử lý. |
| **2. Current Workflow** | Ca trưởng mở danh sách đánh giá, đọc từng bản ghi, ghi mã và trích đoạn phản ánh về vệ sinh phòng vào danh sách tổng hợp rồi chuyển cho buồng phòng. Ước tính 12 phút/lô 30 đánh giá. |
| **3. Bottleneck** | Bước 2–3 mất khoảng 10 phút/lô. Phản ánh có thể nằm giữa nhiều chủ đề hoặc được diễn đạt gián tiếp, ví dụ khách viết “ga giường còn tóc”. Ca trưởng phải đọc ngữ cảnh và đối chiếu đúng đoạn với mã đánh giá. |
| **4. Business Impact** | Mỗi lô chiếm khoảng 10 phút công rà soát của ca trưởng. Nếu đạt mục tiêu giảm 30%, thời gian tiết kiệm theo mốc giả định là 3 phút/lô. Phản ánh bị bỏ sót có thể không đến được bộ phận buồng phòng để kiểm tra. Cần đo số lô thực tế và tỷ lệ bỏ sót khi đọc tay để định lượng tác động theo ca. |
| **5. Success Metric** | Giảm **ít nhất 30%** thời gian rà soát so với đọc tay, tính cả chạy công cụ, đối chiếu, sửa và rà thủ công các trường hợp phải chuyển dự phòng. Nếu baseline đo được là 10 phút/lô thì mục tiêu là **tối đa 7 phút/lô**. Đầu ra LLM trước khi duyệt phải phát hiện **ít nhất 90%** đánh giá có phản ánh vệ sinh phòng theo nhãn chuẩn. |
| **6. Operational Boundary** | LLM chỉ nhận mã nội bộ và nội dung đánh giá đã ẩn danh. Mô hình chỉ tạo bản nháp gồm mã đánh giá, nhãn và trích đoạn có trong văn bản đầu vào. Cấm tự thêm chi tiết, liên hệ khách, tạo yêu cầu xử lý hoặc chuyển danh sách. Ca trưởng đối chiếu bản gốc, bổ sung phản ánh bị sót và duyệt trước khi chuyển. |

---

## 3.3. Future-State Flow & AI Fit

**AI Fit** — Chọn **LLM Feature** để đọc ngữ cảnh và trích đoạn phản ánh. Rule lọc từ khóa làm mốc so sánh. Ca trưởng duyệt và bàn giao theo quy trình cố định.

| Kiến trúc | Mức phù hợp với bài toán |
|---|---|
| **Rule / State-Machine** | Lọc từ khóa cho kết quả dễ kiểm tra và có chi phí xử lý thấp. Đây là mốc so sánh để đo xem LLM có phát hiện thêm các phản ánh viết gián tiếp hoặc xuất hiện trong đánh giá nhiều chủ đề hay không. Rule cũng kiểm tra định dạng, mã và trích đoạn ở đầu ra LLM. |
| **LLM Feature** | Đọc từng đánh giá theo ngữ cảnh, gắn nhãn và trích đoạn trong một tác vụ có đầu vào và đầu ra cố định. Ca trưởng giữ quyền quyết định nội dung bàn giao. |
| **Agentic Loop** | Quy trình có thứ tự cố định, với một lần phân loại và một lần duyệt. Tra cứu nhiều nguồn, lập kế hoạch và tự thực hiện hành động sẽ làm tăng chi phí và phạm vi kiểm thử. |

**Quy trình tương lai (Future-State)**

```text
┌────────────────────────────┐       ┌────────────────────────────┐
│ Bước 1                     │       │ Bước 2 [AI]                │
│ Mở lô đánh giá và          │       │ LLM gắn nhãn và            │
│ ẩn danh nội dung           │ ────→ │ trích đoạn theo mã         │
│ trước khi gọi mô hình      │       │ đánh giá                   │
└────────────────────────────┘       └────────────────────────────┘
                                                    │
                                                    ▼
┌────────────────────────────┐       ┌────────────────────────────┐
│ Bước 4 [HITL]              │       │ Bước 3                     │
│ Ca trưởng đối chiếu,       │       │ Kiểm tra mã, nhãn,         │
│ sửa, duyệt và bàn giao     │ ←──── │ định dạng và trích đoạn    │
│ cho buồng phòng            │       │ so với nguồn               │
└────────────────────────────┘       └────────────────────────────┘
                                                    │
                                                    ▼
                                     ┌────────────────────────────┐
                                     │ Fallback ở bước 3          │
                                     │ Rà thủ công mục lỗi hoặc   │
                                     │ cả lô rồi sang bước 4.     │
                                     └────────────────────────────┘
```

- **🔵 AI Step:** LLM trả một kết quả cho mỗi mã với nhãn `co_phan_anh`, `khong_co_phan_anh` hoặc `can_xem_lai`. Với nhãn `co_phan_anh`, trích đoạn phải xuất hiện nguyên văn trong đánh giá đã ẩn danh. Nội dung đánh giá được xử lý như dữ liệu đầu vào. Hệ thống kiểm tra đủ mã, không trùng mã, đúng nhãn và trích đoạn khớp nguồn.
- **🟢 Human Step (HITL):** Ca trưởng xem bản nháp cùng nội dung nguồn, kiểm tra cả đánh giá được gắn nhãn không có phản ánh để phát hiện mục bị sót, rồi sửa và duyệt danh sách. Thời gian đọc lại được tính vào kết quả thử nghiệm.
- **↩️ Fallback:** Ca trưởng đọc thủ công các bản ghi có nhãn `can_xem_lai` hoặc lỗi kiểm tra. Nếu LLM không phản hồi hoặc đầu ra cả lô không đọc được, ca trưởng quay lại quy trình thủ công cho cả lô. Danh sách chỉ được chuyển sau khi ca trưởng duyệt.

---

# 🏁 Phase 5 — EVALUATE (Nhóm, 20 min)

### AI Readiness Checklist

| Câu hỏi trong worksheet | Trạng thái | Bằng chứng hoặc việc cần làm |
|---|---|---|
| Có sẵn dữ liệu mẫu/logs sạch để test? | ☐ Chưa xác nhận | Repo hiện có bản mô tả bài toán. Cần bộ đánh giá được phép sử dụng, đã ẩn danh và được gán nhãn bởi người hiểu nghiệp vụ. |
| Rủi ro khi AI sai có nằm trong tầm kiểm soát qua HITL hoặc Fallback? | ☐ Chưa kiểm chứng | Thiết kế có kiểm tra đầu ra, duyệt thủ công và luồng dự phòng. Cần thử các trường hợp bỏ sót, trích đoạn sai, mã thiếu hoặc trùng, đánh giá chứa chỉ dẫn và lỗi gọi mô hình trước khi xác nhận. |
| Stakeholders sẵn sàng thay đổi quy trình làm việc cũ? | ☐ Chưa xác nhận | Cần ca trưởng xác nhận cách duyệt bản nháp và bộ phận buồng phòng xác nhận thông tin tối thiểu cần nhận khi bàn giao. |

### Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future

- [ ] **GO (Bắt đầu xây dựng Prototype)** — Bắt đầu phát triển với phạm vi hẹp.
- [x] **NOT YET (Cần tích lũy thêm dữ liệu/xác lập baseline)** — Chuẩn bị mẫu, đo đọc tay và xác nhận luồng duyệt.
- [ ] **NO-GO (Không khả thi / Rule-based tốt hơn)** — Dừng phương án LLM nếu rule đạt yêu cầu với chi phí thấp hơn hoặc thử nghiệm cho thấy LLM không đáp ứng điều kiện.

**Justification (Lý giải quyết định dựa trên bằng chứng kỹ thuật và chi phí)**

Mốc 10 phút/lô là ước tính. Nếu ca trưởng vẫn phải đọc kỹ cả 30 đánh giá để phát hiện mục bị bỏ sót, thời gian kiểm tra có thể làm mất phần tiết kiệm do LLM mang lại. Cần đo thời gian thực tế và chi phí gọi mô hình trên mỗi lô trước khi đánh giá lợi ích.

1. **Chuẩn bị dữ liệu.** Dùng đánh giá đã ẩn danh và gán nhãn theo từng mã. Bộ mẫu gồm đánh giá có phản ánh trực tiếp, phản ánh gián tiếp, đánh giá nhiều chủ đề và đánh giá không liên quan. Tách lô thử khỏi lô dùng để chỉnh từ khóa hoặc prompt.
2. **Đo ba phương án.** So sánh đọc tay, lọc từ khóa và LLM trên cùng các lô 30 đánh giá. Đổi thứ tự xử lý giữa các lô hoặc phân công người rà soát khác nhau để giảm ảnh hưởng của việc nhớ nội dung. Đo thời gian từ lúc bắt đầu đọc hoặc chạy công cụ đến khi có danh sách đã duyệt. Đếm số đánh giá dương tính đúng chia cho tổng số đánh giá dương tính theo nhãn chuẩn để tính tỷ lệ phát hiện trước duyệt. Ghi thêm số cảnh báo nhầm và chi phí gọi mô hình/lô.
3. **Xét lại quyết định.** Chuyển sang **GO** cho prototype phạm vi hẹp khi có dữ liệu được phép sử dụng, ca trưởng xác nhận luồng duyệt và kết quả thử cho thấy LLM đạt cả hai ngưỡng. Nếu rule cũng đạt các ngưỡng với chi phí tổng thấp hơn, chọn **NO-GO cho LLM** và dùng kết quả rule làm căn cứ.
