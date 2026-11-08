# 🔍 Phase 1 — SCAN: Tìm kiếm cơ hội
Dùng **4 Lenses** để quét qua hoạt động vận hành của các công ty thành viên Vingroup. Ghi lại **5 bài toán/bottleneck** thực tế.
### 📝 List bài toán của tôi:
| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|----------------------------------|------|---------------------|
| 1 | Vinmec | Lặp lại (Repetitive) | Phân tích ảnh X-quang và MRI để hỗ trợ bác sĩ phát hiện dấu hiệu bất thường, giảm thao tác đọc ảnh lặp lại. |
| 2 | Vinmec | AI có thể tốt hơn (AI-upgrade) | Nâng cấp hệ thống hỗ trợ tư vấn và chăm sóc khách hàng bằng AI để giải đáp câu hỏi về dịch vụ, lịch khám, quy trình và hướng dẫn trước khi khám. |
| 3 | VRIC | Tốn thời gian (Time-consuming) | Tìm kiếm, phân loại và tổng hợp bài báo khoa học, bằng sáng chế và tài liệu kỹ thuật phục vụ hoạt động nghiên cứu R&D. |
| 4 | Vinpearl | AI có thể tốt hơn (AI-upgrade) | Xây dựng trợ lý du lịch AI đề xuất lịch trình, nhà hàng và hoạt động giải trí dựa trên ngân sách, sở thích và thời gian lưu trú của khách. |
| 5 | Vincom Retail | Pain từ người khác (Stakeholder Pain) | Phân tích phản hồi của khách thuê mặt bằng để phát hiện các vấn đề về vận hành, lưu lượng khách và chất lượng dịch vụ chung. |

---

# 🃏 Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards

Chọn top 3 từ danh sách SCAN: **#1 (Vinmec: AI-assisted Medical Image Analysis), #3 (VRIC: AI-powered Research Assistant), #4 (Vinpearl: AI-powered Personalized Travel Assistant).**

## Thẻ bài toán tiêu biểu: Card #1 — Vinmec: AI-assisted Medical Image Analysis

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán: Bác sĩ chẩn đoán hình ảnh phải đọc và đánh giá số lượng |
| lớn ảnh X-quang và MRI mỗi ngày. Việc phát hiện, phân tích 
| các dấu hiệu bất thường đòi hỏi nhiều thời gian, sự tập trung |
| và kinh nghiệm chuyên môn. Đặc biệt, vào những thời điểm |
| bệnh viện quá tải, số lượng ảnh cần xử lý tăng cao, tạo áp lực lớn |
| lên đội ngũ bác sĩ và tiềm ẩn nguy cơ ảnh hưởng đến         |
| độ chính xác cũng như chất lượng chẩn đoán.                 │
│ Công ty thành viên: [x] Vinmec                              │
│                                                             │
│ Ai đang đau? Bác sĩ chẩn đoán hình ảnh (Radiologist),       |
| Kỹ thuật viên chẩn đoán hình ảnh (Radiologic Technologist)  │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Bệnh nhân được chỉ định chụp X-quang hoặc MRI.         │
│   → 2. Kỹ thuật viên thực hiện chụp và lưu ảnh vào hệ thống │
│   → 3. Bác sĩ mở và đọc từng bộ ảnh                         │
│   → 4. Bác sĩ xác định dấu hiệu bất thường.                 │
│   → 5. Bác sĩ lập báo cáo và trả kết quả cho bệnh nhân      │
│                                                             │
│ Bước nào tốn nhất? Bước 3-4                                 │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 3-4              │
│ (AI tự động phân tích hình ảnh.                             |
| -> Phát hiện và đánh dấu các vùng nghi ngờ bất thường.      │
| -> Cung cấp kết quả gợi ý để bác sĩ xác nhận trước khi đưa ra kết luận.) |
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ • Giảm thời gian đọc ảnh trung bình: mục tiêu thử nghiệm    |
|  giảm 20–30%.                                               |
| • Sensitivity đạt mục tiêu được bác sĩ chuyên môn xác định. |
| • Theo dõi tỷ lệ bỏ sót bất thường (False-negative rate).   |
| • Theo dõi thời gian trả kết quả (Radiology Turnaround Time).│
│                                                             │
│ Quick Architecture: [x] Computer Vision phân tích ảnh kết hợp|
| Rule-based triage và Human-in-the-loop   │
└─────────────────────────────────────────────────────────────┘
```

## Thẻ bài toán tiêu biểu: Card #3 — VRIC: AI-powered Research Assistant
```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán: Nhà nghiên cứu khoa học phải tìm kiếm và tổng hợp |
| lượng lớn bài báo khoa học, bằng sáng chế và tài liệu kỹ thuật |
| từ nhiều nguồn khác nhau. Việc xác định tài liệu liên quan, |
| so sánh các nghiên cứu trước đó và tìm ra khoảng trống nghiên cứu |
| tốn nhiều thời gian.                                        │
│ Công ty thành viên: [x] VRIC                                │
│                                                             │
│ Ai đang đau? Nhà nghiên cứu khoa học                        │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Nhà nghiên cứu xác định chủ đề cần tìm hiểu.           │
│   → 2. Tìm kiếm tài liệu trên các cơ sở dữ liệu khoa học.   │
│   → 3. Đọc và lọc các bài báo liên quan.                    │
│   → 4. Trích xuất phần nội dung quan trọng có liên quan.    │
│   → 5. Tổng hợp kết quả và viết báo cáo nghiên cứu          │
│                                                             │
│ Bước nào tốn nhất? Bước 3-4 tốn thời gian và có thể         |
| bị lộ lọt dữ liệu đề tài nghiên cứu.                        │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2-4              │
│ (Tự động tìm kiếm tài liệu  -> Đọc và lọc các bài báo       |
| -> Trích xuất phần nội dung quan trọng có liên quan)        │
| -> So sánh phương pháp, dữ liệu và kết quả giữa các paper.  |
| -> Trả lời câu hỏi dựa trên tài liệu có trích dẫn nguồn.    |
| -> Gợi ý các hướng nghiên cứu tiềm năng để nhà nghiên cứu xem xét. |
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ Giảm 50% thời gian tìm kiếm và tổng hợp tài liệu.           |
| Độ chính xác của câu trả lời so với tài liệu gốc.           |
| Tỷ lệ câu trả lời có trích dẫn nguồn hợp lệ trên 90%.       |
| Tỷ lệ tài liệu liên quan được truy xuất (Recall@K).         |
| Mức độ hài lòng của nhà nghiên cứu ở mức tốt (80%) .        │
│                                                             │
│ Quick Architecture: [x] LLM Feature + RAG                   │
└─────────────────────────────────────────────────────────────┘
```

## Thẻ bài toán tiêu biểu: Card #4 - Vinpearl: AI-powered Personalized Travel Assistant

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #4                                       │
│                                                             │
│ Bài toán: Khách du lịch thường phải tự tìm kiếm thông tin về |
| khách sạn, nhà hàng, địa điểm tham quan và hoạt động giải trí.|
| Thông tin có thể nằm trên nhiều nền tảng khác nhau, |
| khiến việc lên lịch trình phù hợp với ngân sách, sở thích và |
| thời gian lưu trú trở nên mất thời gian.                    │
│ Công ty thành viên: [x] Vinpearl                            │
│                                                             │
│ Ai đang đau? Khách du lịch.                                 │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Khách hàng tìm kiếm thông tin về điểm đến.               │
│   → 2. Khách hàng tham khảo khách sạn, nhà hàng và hoạt động giải trí.│
│   → 3. Khách hàng tự so sánh giá và dịch vụ.   │
│   → 4. Khách hàng tự xây dựng lịch trình.      │
│   → 5. Khách hàng liên hệ nhân viên để hỏi thêm hoặc đặt dịch vụ. │
│                                                             │
│ Bước nào tốn nhất? Bước 2-4 (⏱ 20 phút/lượt)                │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2-4              │
│ (Tự động tham khảo khách sạn, nhà hàng và hoạt động giải trí |
| -> So sánh giá và dịch vụ -> Xây dựng lịch trình)           │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ Giảm thời gian tạo lịch trình cho khách hàng dưới 2 phút.   │
| Tỷ lệ khách hàng chấp nhận đề xuất trên 80%.                |
| Mức độ hài lòng của khách hàng trên 80%.                    |
│                                                             │
│ Quick Architecture: [x] LLM + Recommendation System         │
└─────────────────────────────────────────────────────────────┘
```