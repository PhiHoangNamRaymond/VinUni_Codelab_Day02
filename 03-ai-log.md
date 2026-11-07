
# 03 — AI Log & Reflection (Cá nhân)

> **Lab 02: AI Product Scoping — Vingroup**
>
> **Bài toán:** Vinpearl — Tổng hợp thông tin bàn giao ca khách sạn
>
> **Công cụ AI sử dụng:** ChatGPT

---

## 1. AI đã giúp tôi gì (What AI helped with)

Trong quá trình làm Lab 02, tôi chủ yếu tự tìm hiểu yêu cầu, lựa chọn bài toán và phân tích hướng giải quyết. Tôi sử dụng ChatGPT để tham khảo thêm thông tin, giải đáp các khái niệm chưa rõ và kiểm tra lại những phần còn phân vân.

| Giai đoạn | Cách tôi sử dụng AI | Kết quả |
|---|---|---|
| **Phase 1 — SCAN** | Tham khảo AI về các vấn đề trong hệ sinh thái Vingroup và cách áp dụng 4 góc nhìn của đề bài. | Xác định 5 bài toán thuộc VinFast, Vinhomes, Vinpearl, VinBus và Vinmec. |
| **Phase 2 — QUICK-ASSESS** | Hỏi thêm AI về cách xác định bottleneck, metric và phân biệt Rule, LLM, Agent. | Hoàn thiện 3 Quick Problem Cards cho VinFast, Vinpearl và VinBus. |
| **Phase 3 — DEEP-DIVE** | Tham khảo AI để hiểu rõ hơn về Problem Statement, handoff, operational boundary và cách đánh giá AI Fit. | Phân tích quy trình bàn giao ca Vinpearl, xây dựng workflow 5 bước và lựa chọn LLM có nhân viên kiểm tra kết quả. |
| **Phase 4 — PROTOTYPE** | | |
| **Phase 5 — EVALUATE** | Tham khảo AI về cách đánh giá tính khả thi, rủi ro và phân biệt GO, NOT YET, NO-GO. | Quyết định GO để xây dựng prototype, chưa triển khai thực tế tại Vinpearl. |

## 2. AI trả lời sai hoặc chưa phù hợp ở đâu (Where AI failed)

Trong quá trình tham khảo, tôi nhận thấy một số điểm AI chưa thực sự phù hợp với yêu cầu bài làm.

### 2.1. Một số thông tin chưa có số liệu thực tế

Khi phân tích bài toán Vinpearl, AI có đưa ra các mốc thời gian và chỉ số đánh giá để tham khảo.

Tuy nhiên, tôi chưa có dữ liệu thực tế từ Vinpearl nên không thể khẳng định các con số này chính xác.

Vì vậy, tôi sử dụng thời gian **18 phút/ca** và mục tiêu **10 phút/ca** dưới dạng giả định để phân tích, không coi đây là số liệu của doanh nghiệp.

### 2.2. Cách trình bày chưa đúng yêu cầu

Ở phần Quick Problem Cards, AI ban đầu đưa ra nội dung theo dạng thông thường, chưa đúng khung mẫu trong worksheet.

Tôi phải yêu cầu điều chỉnh lại cách trình bày để các Card có đầy đủ thông tin và dễ theo dõi hơn.

### 2.3. Workflow có chỗ chưa hợp lý

Khi tham khảo cách thể hiện sơ đồ, thứ tự một số bước và hướng mũi tên chưa đúng.

Tôi kiểm tra lại quy trình và điều chỉnh theo thứ tự:

**Ghi nhận công việc → Tổng hợp yêu cầu → Viết ghi chú → Ca sau tiếp nhận → Trưởng ca xác nhận.**

Qua đó tôi nhận thấy AI có thể hỗ trợ kiểm tra nhưng không phải lúc nào cũng đưa ra kết quả chính xác ngay từ đầu.

## 3. Tôi đã điều chỉnh cách sử dụng AI như thế nào (How I fixed prompts & boundaries)

### 3.1. Đặt câu hỏi cụ thể hơn

Ban đầu tôi chủ yếu hỏi AI về các khái niệm và hướng làm bài. Sau đó, tôi bổ sung thêm bối cảnh để câu trả lời sát với đề tài Vinpearl hơn.

Ví dụ, thay vì chỉ hỏi "LLM là gì?", tôi hỏi thêm về sự khác nhau giữa Rule, LLM và Agent khi áp dụng vào việc tổng hợp ghi chú bàn giao ca.

### 3.2. Kiểm tra số liệu và giả định

Tôi không sử dụng trực tiếp các con số AI đề xuất như dữ liệu thực tế.

Những số liệu chưa được kiểm chứng được ghi rõ là giả định hoặc mục tiêu thử nghiệm. Điều này giúp báo cáo tránh đưa ra kết luận quá chắc chắn khi chưa có dữ liệu.

### 3.3. Giữ quyền quyết định ở người thực hiện

Trong bài toán Vinpearl, tôi lựa chọn giải pháp LLM chỉ hỗ trợ đọc và tóm tắt ghi chú.

AI không được tự xác nhận công việc đã hoàn thành hoặc tự bàn giao thay nhân viên. Kết quả phải được nhân viên kiểm tra trước khi sử dụng.

Tương tự, khi làm bài LAB, tôi dùng AI để tham khảo và giải đáp, còn việc lựa chọn đề tài, đánh giá và quyết định nội dung cuối cùng vẫn do tôi thực hiện.

### 3.4. Đối chiếu với yêu cầu bài LAB

Tôi kiểm tra các nội dung theo worksheet và tham khảo cách trình bày của các bạn trong nhóm.

Những phần chưa phù hợp được điều chỉnh lại để thống nhất giữa `01-problem-scan.md`, `02-deep-dive-report.md` và `04-workflow-diagram.png`.

## 4. Bài học rút ra (Reflection)

- **Cần hiểu bài toán trước khi chọn AI:** Trước tiên phải biết quy trình hiện tại đang gặp khó khăn ở đâu, sau đó mới xem AI có phù hợp hay không.

- **Không phải lúc nào cũng cần Agent:** Với bài toán bàn giao ca Vinpearl, LLM là đủ để hỗ trợ đọc và tóm tắt ghi chú. Không cần AI tự thực hiện toàn bộ quy trình.

- **Số liệu cần có căn cứ:** Những con số chưa được kiểm chứng chỉ nên dùng làm giả định, không trình bày như kết quả thực tế.

- **AI chỉ là công cụ hỗ trợ:** AI giúp tôi tìm hiểu nhanh hơn và có thêm góc nhìn, nhưng tôi vẫn cần tự kiểm tra và đánh giá những thông tin nhận được.

- **Cần có Human-in-the-loop:** Đối với quy trình bàn giao ca, nhân viên phải là người kiểm tra và xác nhận kết quả, tránh trường hợp AI bỏ sót hoặc tự tạo thông tin.

Qua Lab 02, tôi hiểu rõ hơn cách xác định một bài toán phù hợp để ứng dụng AI và tầm quan trọng của việc kiểm soát kết quả do AI tạo ra.

---

## 5. Prototype & Boundary Test

**Trạng thái:** 

### 5.1. Quá trình xây dựng prototype
