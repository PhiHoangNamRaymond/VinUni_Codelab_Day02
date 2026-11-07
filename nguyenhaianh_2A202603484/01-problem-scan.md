# 🔍 Báo Cáo Quét Cơ Hội & Đánh Giá Nhanh — AI Product Scoping (Vin Smart Future)

* **Học viên:** Nguyễn Hải Anh
* **Vai trò:** AI Product Engineer — Vin Smart Future (Vingroup)
* **Mục tiêu:** Quét tìm các điểm nghẽn (bottlenecks) trong quy trình vận hành thực tế tại các công ty thành viên Vingroup, phân loại theo 4 Lenses, và thực hiện đánh giá sơ bộ (Quick-Assess) cho top 3 bài toán tiềm năng.

---

# 🔍 Phase 1 — SCAN: Quét Tìm Cơ Hội Tối Ưu Hóa Bằng AI (Vingroup)

Sử dụng **4 Lenses** (Lặp lại, Tốn thời gian, AI có thể tốt hơn, Pain từ người khác) để khảo sát quy trình tác nghiệp tại các đơn vị thành viên:

| # | Đơn vị thành viên (Subsidiary) | Phân loại (Lens) | Mô tả chi tiết bài toán & Bottleneck thực tế | Tác nhân chịu ảnh hưởng (Actor) |
|---|---|---|---|---|
| **1** | **Xanh SM (GSM)** | **Tốn thời gian & Khẩn cấp** | Điều phối viên phải xử lý thủ công các trường hợp xe điện báo pin nguy cấp (< 5%) hoặc cạn pin giữa hành trình đón khách: vừa tra vị trí GPS, kiểm tra trạm sạc khả dụng, tính toán cự ly, vừa viết tin hướng dẫn và liên hệ điều xe cứu hộ sạc pin di động (mất 15–20 phút/vụ). | Tài xế Xanh SM, Điều phối viên trung tâm điều vận (Dispatcher) |
| **2** | **VinFast** | **Lặp lại & Dễ sai sót** | Đối soát số liệu và hoá đơn trạm sạc đối tác ngoài: Hàng tuần kế toán phải đối chiếu thủ công hàng chục nghìn phiên sạc giữa log cổng sạc đối tác và dữ liệu thanh toán VinFast E-Mobility, mất 3–4 ngày làm việc mỗi kỳ chốt công nợ. | Chuyên viên kế toán đối soát công nợ trạm sạc VinFast |
| **3** | **Vinhomes** | **AI có thể tốt hơn** | Phân loại, gán nhãn và điều hướng tự động khiếu nại cư dân trên ứng dụng Vinhomes Resident: Hiện tại nhân viên lễ tân/CSKH phải đọc từng phiếu, phân loại thủ công vào các phòng ban kỹ thuật/an ninh/vệ sinh, dẫn đến thời gian phản hồi ban đầu kéo dài 8–12 giờ và câu trả lời rập khuôn. | Cư dân các khu đô thị Vinhomes, Bộ phận CSKH & Kỹ thuật tòa nhà |
| **4** | **Vinmec** | **Tốn thời gian** | Soạn thảo bản tóm tắt hồ sơ bệnh án xuất viện (Discharge Summary): Bác sĩ điều trị phải rà soát thủ công kết quả xét nghiệm máu, chẩn đoán hình ảnh, diễn tiến bệnh và chỉ định đơn thuốc để tổng hợp văn bản tóm tắt bằng ngôn ngữ y khoa dễ hiểu, mất 25–35 phút/bệnh nhân. | Bác sĩ điều trị, Điều dưỡng viên hành chính tại Vinmec |
| **5** | **Vinpearl / VinWonders** | **Pain từ người khác** | Giám sát và tổng hợp phản hồi/khiếu nại đa kênh (OTA reviews, Google Maps, fanpage, email CSKH): Hiện tại quản lý khách sạn nhận phản ánh tiêu cực trễ sau 24–48 giờ khi du khách đã trả phòng, không kịp can thiệp xử lý tại chỗ để giữ chân khách hàng. | Trưởng ca trực tiếp khách hàng (Duty Manager), Khách lưu trú Vinpearl |
| **6** | **Xanh SM (GSM)** | **Lặp lại** | Tự động phân tích và phân loại lý do hủy chuyến của khách hàng và tài xế từ ghi âm cuộc gọi tổng đài và ghi chú ngắn, nhằm phát hiện sớm các "điểm nóng" thiếu xe hoặc lỗi ứng dụng theo thời gian thực. | Bộ phận Tối ưu hóa Mạng lưới Điều vận (Ops Excellence) |

---

# 🃏 Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards

Chọn **Top 3 bài toán tiềm năng nhất** từ bảng SCAN để phân tích sâu theo cấu trúc Quick Problem Card:
1. **Card #1:** Xanh SM — Điều phối cứu hộ sạc pin di động & Hướng dẫn trạm sạc khẩn cấp khi xe nguy cấp
2. **Card #2:** VinFast — Tự động đối soát dữ liệu phiên sạc đối tác trạm sạc ngoài
3. **Card #3:** Vinhomes — Hệ thống phân loại & điều hướng thông minh phản ánh cư dân trên App Vinhomes Resident

---

## 📌 QUICK PROBLEM CARD #1: Xanh SM — Điều phối cứu hộ & Hướng dẫn trạm sạc khẩn cấp

```text
┌────────────────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                                                  │
│                                                                                        │
│ Bài toán (1 câu): Hỗ trợ điều phối viên Xanh SM ra quyết định khẩn cấp khi xe báo      │
│ pin dưới 5%: tự động chặn điều hướng xa (> 5km), kích hoạt xe cứu hộ sạc di động và    │
│ soạn sẵn dự thảo chỉ dẫn có gắn thẻ kiểm soát [DRAFT_ONLY].                            │
│                                                                                        │
│ Công ty thành viên: [x] Xanh SM (GSM)   [ ] VinFast   [ ] Vinhomes   [ ] Vinmec        │
│                                                                                        │
│ Ai đang đau (Actor)?                                                                   │
│   • Tài xế: Hoang mang khi xe sắp hết pin giữa đường, nguy cơ chết máy gây tắc đường.  │
│   • Điều phối viên (Dispatcher): Quá tải áp lực, dễ nhầm lẫn cự ly trong giờ cao điểm. │
│                                                                                        │
│ Workflow thủ công hiện tại (5 bước):                                                   │
│   1. Tài xế gọi điện thoại/bấm SOS trên app báo pin cạn (< 5%)                         │
│   ──> 2. Điều phối viên tra cứu tọa độ GPS của xe trên hệ thống giám sát xe              │
│   ──> 3. Mở bản đồ mạng lưới trạm sạc VinFast, đo cự ly và tìm trụ sạc tương thích      │
│   ──> 4. Nhập tay tin nhắn SMS/In-app hướng dẫn tài xế di chuyển hoặc chờ cứu hộ       │
│   ──> 5. Gọi điện thoại riêng sang bộ phận Đội xe cứu hộ sạc pin di động (nếu cạn pin)│
│                                                                                        │
│ Bước nào tốn thời gian/lỗi nhất?                                                       │
│   • Bước 3 & 4: Tra cứu cự ly an toàn và soạn tin hướng dẫn (⏱ 10 - 12 phút/vụ).        │
│                                                                                        │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                                                  │
│   • Hỗ trợ Bước 3 & 4: LLM đóng vai trò Co-pilot, tự động đọc mức pin và toạ độ GPS,   │
│     nếu pin < 5% thì cấm tuyệt đối chỉ dẫn trạm > 5km, tự động trigger lệnh cứu hộ     │
│     dispatch_mobile_charger và soạn bản nháp [DRAFT_ONLY] để Dispatcher duyệt 1-click. │
│                                                                                        │
│ Đo thành công bằng gì (Metric có số)?                                                  │
│   1. Giảm thời gian xử lý sự cố từ 15 phút ──> dưới 2.5 phút/vụ (giảm 83% thời gian).   │
│   2. 0% trường hợp xe cạn pin < 5% bị chỉ dẫn đến trạm xa > 5km (Tuân thủ ranh giới).   │
│   3. 100% tin nhắn do AI soạn thảo đều có gắn thẻ [DRAFT_ONLY] qua xét duyệt con người.│
│                                                                                        │
│ Quick Architecture: [ ] No AI   [ ] Rule   [x] LLM Feature   [ ] Agent                 │
└────────────────────────────────────────────────────────────────────────────────────────┘
```

---

## 📌 QUICK PROBLEM CARD #2: VinFast — Tự Động Đối Soát Dữ Liệu Phiên Sạc Trạm Ngoài

```text
┌────────────────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                                                  │
│                                                                                        │
│ Bài toán (1 câu): Tự động trích xuất, chuẩn hóa định dạng và đối chiếu bất thường giữa │
│ tệp log phiên sạc từ các đối tác trạm sạc nhượng quyền với dữ liệu thanh toán VinFast. │
│                                                                                        │
│ Công ty thành viên: [ ] Xanh SM   [x] VinFast   [ ] Vinhomes   [ ] Vinmec              │
│                                                                                        │
│ Ai đang đau (Actor)?                                                                   │
│   • Chuyên viên đối soát công nợ VinFast E-Mobility: Mệt mỏi vì phải xử lý hàng trăm   │
│     file Excel đa định dạng, phát hiện sai lệch số kWh thủ công bằng VLOOKUP.          │
│                                                                                        │
│ Workflow thủ công hiện tại (4 bước):                                                   │
│   1. Tải file sao kê phiên sạc từ cổng portal của 12+ đối tác nhượng quyền trụ sạc     │
│   ──> 2. Chuyển đổi định dạng ngày giờ, đơn vị điện năng kWh về cùng một chuẩn chung    │
│   ──> 3. Dò khớp từng mã xe (VIN), mã cổng sạc và thời gian bắt đầu/kết thúc           │
│   ──> 4. Lập báo cáo chênh lệch số liệu và soạn email gửi giải trình cho đối tác       │
│                                                                                        │
│ Bước nào tốn thời gian/lỗi nhất?                                                       │
│   • Bước 2 & 3: Xử lý định dạng lệch chuẩn và đối chiếu dòng lệch (⏱ 180 phút/đối tác).│
│                                                                                        │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                                                  │
│   • Bước 2: Tự động nhận diện cấu trúc file mới bằng LLM parser/Function Calling;       │
│     kết hợp Rule-based script để so khớp số học chính xác tuyệt đối ở Bước 3.          │
│                                                                                        │
│ Đo thành công bằng gì (Metric có số)?                                                  │
│   1. Rút ngắn chu kỳ đối soát từ 4 ngày làm việc xuống dưới 4 giờ/kỳ thanh toán.       │
│   2. Độ chính xác nhận diện cột và chuẩn hóa trường dữ liệu đạt ≥ 99.5%.                │
│                                                                                        │
│ Quick Architecture: [ ] No AI   [x] Rule + LLM Parser   [ ] Pure LLM   [ ] Agent       │
└────────────────────────────────────────────────────────────────────────────────────────┘
```

---

## 📌 QUICK PROBLEM CARD #3: Vinhomes — Phân Loại & Điều Hướng Thông Minh Phản Ánh Cư Dân

```text
┌────────────────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                                                  │
│                                                                                        │
│ Bài toán (1 câu): Tự động đọc hiểu ngôn ngữ tự nhiên tiếng Việt từ phản ánh cư dân    │
│ trên App Vinhomes Resident, trích xuất thực thể (tòa nhà, số căn, phân loại sự cố)     │
│ và định tuyến chính xác đến tổ kỹ thuật/ban quản lý tương ứng.                         │
│                                                                                        │
│ Công ty thành viên: [ ] Xanh SM   [ ] VinFast   [x] Vinhomes   [ ] Vinmec              │
│                                                                                        │
│ Ai đang đau (Actor)?                                                                   │
│   • Cư dân: Bực bội vì phản ánh mùi rác, thang máy hỏng mất nửa ngày mới có phản hồi.  │
│   • Lễ tân tòa nhà: Quá tải vì phải tiếp nhận hàng nghìn ticket/ngày, chuyển nhầm ban. │
│                                                                                        │
│ Workflow thủ công hiện tại (4 bước):                                                   │
│   1. Cư dân gửi phản ánh dạng văn bản kèm ảnh trên App Vinhomes Resident               │
│   ──> 2. Nhân viên CSKH đọc nội dung, suy luận loại sự cố (kỹ thuật, an ninh, vệ sinh)  │
│   ──> 3. Nhân viên gán nhãn ticket và chọn forward thủ công tới tổ vận hành liên quan   │
│   ──> 4. Gõ tin nhắn xác nhận tiếp nhận gửi lại cho cư dân                             │
│                                                                                        │
│ Bước nào tốn thời gian/lỗi nhất?                                                       │
│   • Bước 2 & 3: Đọc hiểu và phân luồng ticket (⏱ 15 - 20 phút/ticket vào giờ cao điểm).│
│                                                                                        │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                                                  │
│   • Hỗ trợ Bước 2, 3 & 4: LLM trích xuất intent (kỹ thuật, vệ sinh, trật tự) và mức    │
│     độ khẩn cấp, tự động gán nhãn ticket và dự thảo tin nhắn phản hồi lịch sự.         │
│                                                                                        │
│ Đo thành công bằng gì (Metric có số)?                                                  │
│   1. Giảm thời gian phản hồi xác nhận ban đầu cho cư dân từ 8 giờ ──> dưới 5 phút.    │
│   2. Độ chính xác phân loại và điều hướng ticket đạt ≥ 92%.                            │
│   3. Giảm 70% tải công việc phân loại thủ công cho nhân viên lễ tân/CSKH.              │
│                                                                                        │
│ Quick Architecture: [ ] No AI   [ ] Rule   [x] LLM Feature   [ ] Agent                 │
└────────────────────────────────────────────────────────────────────────────────────────┘
```

---

# 🎯 Nhận Định & Lựa Chọn Đề Xuất Cho Nhóm

* **Đề xuất lựa chọn bài toán:** Nhóm chọn **Card #1 (Xanh SM — Hỗ trợ điều phối cứu hộ sạc pin di động & hướng dẫn trạm sạc khẩn cấp)** làm bài toán trọng tâm để thực hiện Deep-Dive.
* **Lý do kỹ thuật và vận hành:**
  1. **Tính cấp thiết cao:** Tác động trực tiếp đến an toàn xe điện và hiệu suất đón khách theo thời gian thực (real-time operation).
  2. **Ranh giới vận hành rõ ràng (Operational Boundaries):** Có ranh giới cứng có thể định lượng hóa và kiểm thử tự động bằng code (`pin < 5%`, `cự ly > 5km`, bắt buộc thẻ kiểm duyệt `[DRAFT_ONLY]`).
  3. **AI Fit phù hợp:** Sử dụng kiến trúc **LLM Feature có Human-in-the-Loop (HITL)**, cân bằng hoàn hảo giữa tính tự động hóa và an toàn tuyệt đối.

