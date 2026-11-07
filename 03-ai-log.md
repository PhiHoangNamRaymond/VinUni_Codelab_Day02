# 03 — AI Log & Reflection (Cá nhân)

> **Lab 02: AI Product Scoping — Vin Smart Future**
> **Học viên:** Vũ Xuân Trường — Mã SV: 2A202603433
> **Trợ lý AI sử dụng:** ZCode (GLM), Google Gemini, ChatGPT — vai trò thought-partner trong suốt 6 phase của lab.

---

## 1. AI đã giúp tôi gì (What AI helped with)

| Giai đoạn | Cách tôi dùng AI | Kết quả cụ thể |
|---|---|---|
| **Phase 1 — SCAN** | Tôi yêu cầu AI **tra cứu internet** về pain point thực tế của VinFast, Xanh SM, Vinhomes, Vinmec, Vinpearl (2023–2025) thay vì tự brainstorm trong đầu. | AI tổng hợp được bằng chứng có thật: lỗi sạc VF8 dừng sau 3–5% pin (firmware 8.3.10.11), TrustScore ~3/5, vụ "Day 12 of VinFast EV Nightmare". Bảng SCAN của tôi vì vậy **có căn cứ thực tế** thay vì đoán mò. |
| **Phase 2 — QUICK-ASSESS** | Tôi dùng AI để **draft Quick Problem Cards** (workflow 5 bước, metric có số) rồi tự đọc lại, chỉnh số liệu cho hợp lý. | 3 cards hoàn thành nhanh gấp ~3 lần tự viết; phần "vị trí AI nhảy vào bước nào" AI gợi ý khá sắc. |
| **Phase 3 — DEEP-DIVE** | Tôi nhờ AI **phản biện theo đúng prompt trong worksheet**: *"Đóng vai CFO và Trưởng phòng Vận hành khắt khe, chỉ ra 3 điểm yếu về logic, metric, và vì sao rule-based có thể tốt hơn AI"*. | AI chỉ ra: (1) metric "giảm 50% viral post" khó đoán nhân-quả, (2) bước duyệt của Supervisor có thể thành bottleneck mới, (3) phân loại severity hoàn toàn có thể làm bằng rule. Tôi đã sửa cả 3: metric viral thành chỉ số phụ, thêm SLA duyệt 5 phút, và hạ AI Fit về LLM Feature (chỉ soạn thảo) thay vì Agent. |
| **Phase 4 — PROTOTYPE** | AI viết khung `prompt_prototype.py` (SYSTEM_PROMPT + gọi Gemini SDK); tôi hiểu và tinh chỉnh ranh giới. | Code chạy được 2 adversarial tests chỉ sau 2 vòng sửa. |

## 2. AI trả lời sai / hallucination ở đâu (Where AI failed)

* **Chỉ số ảo (số liệu bịa):** Bản draft đầu tiên của AI tự gán *"VinFast mất 2 triệu USD/tháng vì CSKH chậm"* và *"tỷ lệ hủy chuyến Xanh SM 25%"* — **không có nguồn nào xác thực**. Tôi bắt buộc phải soát từng con số; các số không kiểm chứng được tôi hoặc xóa, hoặc ghi rõ "ước tính". Chỉ giữ lại số có nguồn thật (TrustScore, giá khám Vinmec 690k/1.1M, firmware version).
* **Hiểu sai ngữ cảnh repo:** Đầu buổi, AI định nhét luôn phần đề xuất deep-dive vào cuối `01-problem-scan.md`; tôi phải chỉ lại README — mỗi deliverable là **một file riêng** (`01`, `02`, `03`, `04`). Bài học: AI không tự đọc kỹ yêu cầu nộp bài nếu người dùng không đưa đủ ngữ cảnh.
* **Rate limit & nguồn chập chờn:** Vài truy vấn internet bị lỗi "concurrency limit exceeded", một kết quả chỉ trả về trang PR chính thức (Vinpearl) chứ không có phản hồi thật của khách — AI suýt kết luận *"không có pain nào"* trong khi việc Vinpearl phải tung check-in online + nhận diện gương mặt chính là bằng chứng gián tiếp của ùn tắc quầy.
* **Prompt quá ngắn → output rập khuôn:** Lần đầu tôi chỉ gõ *"cho tôi 10 idea Vingroup"*, AI trả về list chung chung (chatbot CSKH, dự báo nhu cầu...) giống mọi dự án mẫu. Phải viết lại prompt có vai trò rõ ("Tôi là AI Engineer tại Vin Smart Future"), kèm 4 lenses và yêu cầu chứng cứ, kết quả mới dùng được.

## 3. Tôi đã sửa prompt / ranh giới ra sao (How I fixed prompts & boundaries)

1. **Prompt có vai trò + ràng buộc chứng cứ:** Thêm *"kèm con số/bằng chứng thực tế 2023–2025, nếu không có nguồn thì ghi rõ ước tính"* → hallucination giảm hẳn.
2. **Prompt phản biện từ worksheet:** Cho AI đóng vai CFO/Vận hành khắt khe để bới lỗi chính bài làm của mình — đúng kỹ thuật stress-test mà lab khuyến nghị.
3. **Ranh giới khi dùng AI (phản chiếu ranh giới của sản phẩm):** Giống như CSKH Co-pilot trong bài bị cấm tự gửi phản hồi cho khách, tôi cũng duyệt 100% output của AI trước khi đưa vào bài nộp — AI **soạn thảo**, tôi **quyết định**. Không con số nào lọt vào bài mà không qua tôi kiểm tra nguồn.
4. **Kiểm chứng chéo:** Mọi claim quan trọng (lỗi sạc, TrustScore, app cư dân mất dữ liệu) tôi đều yêu cầu nguồn và đối chiếu tay trước khi ghi vào bảng SCAN.

## 4. Bài học rút ra (Reflection)

* AI là **thought-partner xuất sắc cho việc tìm và cấu trúc hóa bài toán**, nhưng là **nguồn dữ liệu kém tin cậy** — mọi con số đều phải có nguồn độc lập.
* Ranh giới vận hành (`[DRAFT_ONLY]`, HITL, fallback) mà tôi thiết kế cho sản phẩm lại chính là cách tôi dùng AI trong lab: AI draft → người duyệt → mới phát hành. Nguyên lý an toàn là một.
* Prompt ngắn cho kết quả rập khuôn; prompt có vai trò, lens và yêu cầu chứng cứ cho kết quả đáng giá gấp nhiều lần.
