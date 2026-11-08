# Báo cáo Phân tích sâu --- AI hỗ trợ chẩn đoán hình ảnh tại Vinmec / VRIC
## 3.1. Current-State Workflow

### 3.1.1. Quy trình hiện tại

Theo mô tả bài toán, bác sĩ tiếp nhận hình ảnh từ PACS, đối chiếu thông
tin lâm sàng trên hệ thống thông tin bệnh viện, đọc và phân tích hình
ảnh, sau đó soạn thảo và ký duyệt báo cáo.

``` text
┌──────────────────────┐
│ Bước 1               │
│ Tiếp nhận yêu cầu    │
│ chẩn đoán và ảnh     │
│ từ PACS              │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│ Bước 2               │
│ Đối chiếu thông tin  │
│ bệnh nhân / chỉ định │
│ trên HIS và hồ sơ    │
│ lâm sàng             │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│ Bước 3 🔴            │
│ Bác sĩ đọc hình ảnh  │
│ X-quang / nhiều      │
│ chuỗi xung và lát cắt│
│ MRI                  │
│                      │
│ Bottleneck:          │
│ khối lượng ảnh lớn,  │
│ tổn thương tinh vi   │
│ có thể khó nhận biết │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│ Bước 4               │
│ Tổng hợp phát hiện,  │
│ soạn thảo báo cáo    │
│ chẩn đoán hình ảnh   │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│ Bước 5 🟢            │
│ Bác sĩ kiểm tra,     │
│ ký duyệt và phát     │
│ hành kết quả         │
└──────────────────────┘
```
🔴 = Bottlenecks,
Bước 3 --- đọc và rà soát lượng lớn hình ảnh, đặc biệt các ca MRI có nhiều chuỗi xung và lát cắt. Bước 4 cũng có thể tiêu tốn thời gian khi bác sĩ tổng hợp phát hiện thành báo cáo.

> **Giới hạn dữ liệu hiện có:** Không có thời gian trung bình cho từng bước, tổng thời gian đọc một ca, số ca/ngày, tỷ lệ bỏ sót hoặc số liệu SLA hiện tại. Vì vậy, báo cáo không gán số phút giả định cho từng bước. Cần đo baseline trực tiếp tại đơn vị trước khi dùng làm căn cứ đầu tư.

## 3.2. Problem Statement (6-field) & Metrics: Chẩn đoán hình ảnh AI (X-quang, MRI)

| Field | Nội dung chi tiết |
| :--- | :--- |
| **1. Actor / Operator** | Bác sĩ Chẩn đoán hình ảnh tại hệ thống y tế Vinmec / VRIC |
| **2. Current Workflow** | Bác sĩ nhận film hình ảnh (MRI, X-quang) qua hệ thống PACS, đối chiếu thông tin lâm sàng trên Hệ thống thông tin bệnh viện, sau đó phân tích thủ công hàng trăm lát cắt, soạn thảo, và ký duyệt báo cáo kết quả (Topol, 2019). |
| **3. Bottleneck** | Khối lượng hình ảnh lớn, đặc biệt đối với MRI có nhiều chuỗi xung và lát cắt, tạo áp lực lên bác sĩ trong giờ cao điểm và ca trực. Các sai sót có thể bao gồm bỏ sót tổn thương và diễn giải sai bất thường. Những tổn thương nhỏ hoặc tinh vi có thể khó phát hiện, tùy thuộc vào vị trí giải phẫu và đặc điểm bệnh lý (Bruno et al., 2015). Chưa có số liệu nội bộ định lượng tỷ lệ lỗi hoặc thời gian xử lý từng bước.|
| **4. Business Impact** | Kéo dài thời gian đọc và trả kết quả, đặc biệt với MRI phức tạp, ảnh hưởng đến SLA dịch vụ.<br>- Tăng nguy cơ bỏ sót tổn thương hoặc chậm phát hiện bất thường có ý nghĩa lâm sàng.<br>- Tăng áp lực nhân lực và hạn chế khả năng xử lý khối lượng ca chụp tăng cao.<br>- AI có tiềm năng hỗ trợ phát hiện tổn thương và cải thiện hiệu quả đọc phim. Các nghiên cứu trên mammography đã chứng minh tiềm năng này, nhưng hiệu quả đối với từng tác vụ X-quang và MRI cần được kiểm chứng độc lập (McKinney et al., 2020; Topol, 2019). |
| **5. Success Metric** | Các mục tiêu đề xuất cần pilot xác nhận: <br>- Giảm 40% thời gian đọc phim sơ bộ của bác sĩ .<br>- Độ nhạy phát hiện tổn thương đạt $\ge 90\%$ (McKinney et al., 2020).<br>- Thời gian trả kết quả MRI rút ngắn xuống dưới 20 phút cho các ca thông thường (Topol, 2019). |
| **6. Operational Boundary** | **Được phép:** AI đóng vai trò là "người đọc thứ hai" khoanh vùng, định vị và gắn nhãn cảnh báo tổn thương (Topol, 2019).<br>**TUYỆT ĐỐI KHÔNG:** AI không được tự động phát hành kết luận cuối cùng lên hệ thống thông tin bệnh viện.<br>**Điểm cần duyệt:** Bác sĩ Chẩn đoán hình ảnh bắt buộc phải kiểm chứng toàn bộ kết quả gợi ý của AI trước khi ký duyệt pháp lý. |

---

### **Danh Mục Tài Liệu Tham Khảo (References)**
Bruno, M. A., Walker, E. A., & Abujudeh, H. H. (2015). Understanding and confronting our mistakes: the epidemiology of error in radiology and strategies for error reduction. RadioGraphics, 35(6), 1668–1676. https://doi.org/10.1148/rg.2015150023

McKinney, S. M., et al. (2020). International evaluation of an AI system for breast cancer screening. Nature, 577(7788), 89–94. https://doi.org/10.1038/s41586-019-1799-6

Topol, E. J. (2019). High-performance medicine: the convergence of human and artificial intelligence. Nature Medicine, 25(1), 44–56. https://doi.org/10.1038/s41591-018-0300-7


---

## 3.3. Future-State Flow & AI Fit
**AI Fit:** Chọn kiến trúc **hybrid: Rule-based orchestration + mô hình Computer Vision chuyên biệt + Human-in-the-loop**

* **Quy trình tương lai (Future-State):**

``` text
┌──────────────────────────────┐
│ Bước 1 — Tiếp nhận ca chụp   │
│ PACS gửi ảnh và metadata     │
│ Bác sĩ xem chỉ định lâm sàng │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│ Bước 2 — Rule-based QC       │
│ Kiểm tra định dạng, metadata,│
│ modality, vùng giải phẫu,    │
│ chất lượng và phạm vi hỗ trợ │
└──────────────┬───────────────┘
               │
       ┌───────┴────────┐
       │ Đạt điều kiện? │
       └───┬────────┬───┘
          Có        Không
           │          └───────────────┐
           ▼                          ▼
┌──────────────────────────────┐   ↩️ FALLBACK
│ Bước 3 — 🔵 AI Imaging Model │   Chuyển đọc phim thủ công;
│ Phân tích ảnh theo tác vụ    │   ghi nhận lý do không chạy AI
│ đã được thẩm định            │
│ Phát hiện / khoanh vùng      │
│ dấu hiệu nghi ngờ            │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│ Bước 4 — Rule kiểm tra output│
│ Kiểm tra schema, trạng thái, │
│ độ tin cậy và điều kiện      │
│ cảnh báo / không kết luận    │
└──────────────┬───────────────┘
               │
       ┌───────┴──────────────┐
       │ Output hợp lệ và     │
       │ đủ điều kiện hiển thị?│
       └───┬──────────────┬───┘
          Có             Không
           │               └──────────────┐
           ▼                              ▼
┌──────────────────────────────┐       ↩️ FALLBACK
│ Bước 5 — 🔵 Hiển thị gợi ý   │       Không dùng kết quả AI;
│ Overlay vùng nghi ngờ, nhãn, │       bác sĩ đọc thủ công
│ điểm tin cậy và giới hạn     │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│ Bước 6 — 🟢 Bác sĩ review    │
│ Mở ảnh gốc, đối chiếu gợi ý,│
│ thông tin lâm sàng; chấp nhận│
│ / chỉnh sửa / bác bỏ         │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│ Bước 7 — Báo cáo và ký duyệt │
│ Bác sĩ hoàn thiện kết luận,  │
│ ký duyệt và phát hành theo   │
│ quy trình bệnh viện          │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│ Bước 8 — Audit & Monitoring  │
│ Lưu phiên bản model, output, │
│ thao tác bác sĩ, thời gian,  │
│ lỗi và phản hồi để giám sát  │
└──────────────────────────────┘
```


------------------------------------------------------------------------

# PHASE 5 --- EVALUATE

## 5.1. AI Readiness Checklist
### AI Readiness Checklist:
1. [v] Chúng tôi có sẵn dữ liệu mẫu/logs sạch để test?
2. [v] Rủi ro khi AI sai có nằm trong tầm kiểm soát (qua HITL hoặc Fallback)?
3. [v] Stakeholders sẵn sàng thay đổi quy trình làm việc cũ?


### Quyết định cuối cùng của Ban Giám Đốc Vinmec:
[x] **GO (Bắt đầu xây dựng Prototype):** Bắt đầu phát triển với scope hẹp.
[v] **NOT YET (Cần tích lũy thêm dữ liệu/xác lập baseline):** Trì hoãn để chuẩn bị thêm.
[x] **NO-GO (Không khả thi / Rule-based tốt hơn):** Hủy bỏ dự án AI này.

**Justification (Lý giải quyết định dựa trên bằng chứng kỹ thuật và chi phí):**
> **1. Cần xây dựng bộ dữ liệu hình ảnh y tế gắn với chẩn đoán của bác sĩ trước khi đánh giá AI.** <br>
Bước nền tảng là tổng hợp dữ liệu PACS gồm ảnh X-quang/MRI và kết luận chẩn đoán tương ứng trong báo cáo của bác sĩ. Các dữ liệu cần được liên kết đúng theo từng ca bệnh, loại phương thức chẩn đoán hình ảnh, vùng giải phẫu và thời điểm thực hiện; đồng thời cần rà soát tính đầy đủ, chất lượng ảnh và tính nhất quán của thông tin chẩn đoán. Nếu chỉ có ảnh mà không có kết luận đối chiếu đáng tin cậy, nhóm dự án chưa có cơ sở phù hợp để đánh giá mô hình phát hiện bất thường.

> **2. Kết luận trong báo cáo bác sĩ cần được chuẩn hóa thành dữ liệu tham chiếu phù hợp với từng tác vụ AI.** <br> 
Báo cáo chẩn đoán dạng văn bản không mặc nhiên cung cấp nhãn đủ chi tiết để huấn luyện hoặc kiểm thử mọi chức năng. Tùy mục tiêu như phát hiện, định vị hay phân đoạn tổn thương, có thể cần bác sĩ chuyên khoa rà soát, chuẩn hóa thuật ngữ và bổ sung nhãn/annotation trên ảnh. Những trường hợp không rõ ràng hoặc có ý kiến chẩn đoán khác nhau cần có quy trình thẩm định để xác lập dữ liệu tham chiếu (reference standard).
---