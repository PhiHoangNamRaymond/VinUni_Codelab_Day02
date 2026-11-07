## 3.2. Problem Statement (6-field) & Metrics: Chẩn đoán hình ảnh AI (X-quang, MRI)

| Field | Nội dung chi tiết |
| :--- | :--- |
| **1. Actor / Operator** | Bác sĩ Chẩn đoán hình ảnh tại hệ thống y tế Vinmec / VRIC |
| **2. Current Workflow** | Bác sĩ nhận film hình ảnh (MRI, X-quang) qua hệ thống PACS, đối chiếu thông tin lâm sàng trên Hệ thống thông tin bệnh viện, sau đó phân tích thủ công hàng trăm lát cắt, soạn thảo, và ký duyệt báo cáo kết quả (Topol, 2019). |
| **3. Bottleneck** | Khối lượng hình ảnh lớn, đặc biệt đối với MRI có nhiều chuỗi xung và lát cắt, tạo áp lực lên bác sĩ trong giờ cao điểm và ca trực. Các sai sót có thể bao gồm bỏ sót tổn thương và diễn giải sai bất thường. Những tổn thương nhỏ hoặc tinh vi có thể khó phát hiện, tùy thuộc vào vị trí giải phẫu và đặc điểm bệnh lý (Bruno et al., 2015). |
| **4. Business Impact** |  Kéo dài thời gian đọc và trả kết quả, đặc biệt với MRI phức tạp, ảnh hưởng đến SLA dịch vụ.<br>- Tăng nguy cơ bỏ sót tổn thương hoặc chậm phát hiện bất thường có ý nghĩa lâm sàng.<br>- Tăng áp lực nhân lực và hạn chế khả năng xử lý khối lượng ca chụp tăng cao.<br>- AI có tiềm năng hỗ trợ phát hiện tổn thương và cải thiện hiệu quả đọc phim. Các nghiên cứu trên mammography đã chứng minh tiềm năng này, nhưng hiệu quả đối với từng tác vụ X-quang và MRI cần được kiểm chứng độc lập (McKinney et al., 2020; Topol, 2019). |
| **5. Success Metric** | - Giảm 40% thời gian đọc phim sơ bộ của bác sĩ .<br>- Độ nhạy phát hiện tổn thương đạt $\ge 90\%$ (McKinney et al., 2020).<br>- Thời gian trả kết quả MRI rút ngắn xuống dưới 20 phút cho các ca thông thường (Topol, 2019). |
| **6. Operational Boundary** | **Được phép:** AI đóng vai trò là "người đọc thứ hai" khoanh vùng, định vị và gắn nhãn cảnh báo tổn thương (Topol, 2019).<br>**TUYỆT ĐỐI KHÔNG:** AI không được tự động phát hành kết luận cuối cùng lên hệ thống thông tin bệnh viện.<br>**Điểm cần duyệt:** Bác sĩ Chẩn đoán hình ảnh bắt buộc phải kiểm chứng toàn bộ kết quả gợi ý của AI trước khi ký duyệt pháp lý. |

---

### **Danh Mục Tài Liệu Tham Khảo (References)**
Bruno, M. A., Walker, E. A., & Abujudeh, H. H. (2015). Understanding and confronting our mistakes: the epidemiology of error in radiology and strategies for error reduction. RadioGraphics, 35(6), 1668–1676. https://doi.org/10.1148/rg.2015150023

McKinney, S. M., et al. (2020). International evaluation of an AI system for breast cancer screening. Nature, 577(7788), 89–94. https://doi.org/10.1038/s41586-019-1799-6

Topol, E. J. (2019). High-performance medicine: the convergence of human and artificial intelligence. Nature Medicine, 25(1), 44–56. https://doi.org/10.1038/s41591-018-0300-7
