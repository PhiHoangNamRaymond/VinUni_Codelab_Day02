# 01 — Problem Scan & Quick Assess

* **Lab 02: AI Product Scoping — Vin Smart Future**
* **Học viên:** Dương Văn Công — Mã SV: 2A202603468
* **Vai trò:** AI Product Engineer, Vin Smart Future (Vingroup)

---

# 🔍 Phase 1 — SCAN: 5 bài toán thực tế

Sử dụng **4 Lenses** (Lặp lại, Tốn thời gian, AI có thể tốt hơn, Pain từ người khác) để khảo sát quy trình tác nghiệp tại các công ty thành viên Vingroup.

| # | Subsidiary | Lens | Mô tả ngắn bài toán (kèm chứng cứ thực tế) |
|---|---|---|---|
| 1 | **VinFast** | Tốn thời gian | **Kiểm tra hồ sơ nhà cung cấp:** Nhân viên phải kiểm tra nhiều giấy tờ, chứng chỉ và thông tin nhà cung cấp, dễ mất thời gian hoặc bỏ sót. Báo cáo VinFast 2024 cho biết có 227 nhà cung cấp mới được sàng lọc và 320 nhà cung cấp hiện tại được đánh giá. |
| 2 | **Vinhomes** | Lặp lại | **Kiểm tra bảo trì tòa nhà:** Nhân viên kỹ thuật phải kiểm tra định kỳ thang máy, hệ thống điện, PCCC và ghi lại kết quả. Công việc lặp lại nhiều lần, có thể xảy ra thiếu sót khi tổng hợp báo cáo. |
| 3 | **Vinpearl** | AI có thể tốt hơn | **Bàn giao ca khách sạn:** Nhân viên lễ tân phải ghi lại tình trạng phòng và những yêu cầu chưa xử lý. Nếu ghi chép thiếu có thể ảnh hưởng ca sau. AI có thể giúp tóm tắt và kiểm tra thông tin bàn giao. |
| 4 | **VinBus** | Lặp lại | **Phân loại báo cáo lỗi xe buýt:** Nhân viên cần đọc và tổng hợp các báo cáo lỗi xe. Các báo cáo có cách mô tả khác nhau nên việc phân loại có thể mất thời gian. AI có thể hỗ trợ nhóm các lỗi giống nhau. |
| 5 | **Vinmec** | Pain từ người khác | **Kiểm tra giấy tờ trước khi khám:** Bệnh nhân có thể quên mang giấy tờ hoặc thiếu thông tin bảo hiểm, phải bổ sung khi đến bệnh viện. Điều này gây mất thời gian cho cả bệnh nhân và nhân viên tiếp đón. AI có thể hỗ trợ nhắc nhở giấy tờ cần chuẩn bị. |

**Nguồn tham khảo:**
- VinFast – Báo cáo phát triển bền vững: https://vinfastauto.us/investor-relations/Sustainability
- Vinhomes: https://vinhomes.vn/
- Vinpearl – Tuyển dụng quản lý lễ tân: https://www.topcv.vn/viec-lam/quan-ly-le-tan/1792876.html
- VinBus: https://vinbus.vn/
- Vinmec: https://www.vinmec.com/vie/
---


## 🃏 Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards

Chọn top 3 từ bảng SCAN: **#1 (VinFast), #3 (Vinpearl), #4 (VinBus).**

*Các số liệu dưới đây là mục tiêu giả định, chưa phải số liệu thực tế.*

### Card #1 — VinFast: Kiểm tra hồ sơ nhà cung cấp

```text
┌──────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1 (SCAN #1)                              │
│                                                              │
│ Bài toán: Nhân viên phải kiểm tra nhiều hồ sơ, chứng chỉ      │
│ nhà cung cấp, dễ mất thời gian hoặc bỏ sót thông tin.         │
│ Công ty thành viên: [x] VinFast                               │
│                                                              │
│ Ai đang gặp khó khăn (Actor)?                                 │
│ Nhân viên mua hàng và bộ phận quản lý chất lượng.             │
│                                                              │
│ Workflow hiện tại (5 bước):                                   │
│  1. Nhận hồ sơ từ nhà cung cấp                                │
│  --> 2. Kiểm tra giấy tờ và chứng chỉ                         │
│  --> 3. Đối chiếu với yêu cầu công ty                         │
│  --> 4. Yêu cầu bổ sung nếu thiếu                             │
│  --> 5. Chuyển quản lý xem xét                                │
│                                                              │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2–3.                    │
│ Phải đọc và đối chiếu nhiều giấy tờ, dễ bỏ sót.               │
│                                                              │
│ AI có thể hỗ trợ bước nào? Bước 2–3.                          │
│ Đọc hồ sơ, tìm thông tin thiếu và tóm tắt kết quả.            │
│                                                              │
│ Đo thành công bằng gì (Metric có số)?                         │
│ - Giảm thời gian kiểm tra từ 30 xuống 15 phút/hồ sơ.          │
│ - Phát hiện >= 90% thông tin thiếu khi thử nghiệm.            │
│                                                              │
│ Quick Architecture: [ ] No AI [ ] Rule [x] LLM [ ] Agent     │
│ Lý do: LLM đọc hiểu nhiều loại văn bản khác nhau.             │
└──────────────────────────────────────────────────────────────┘
```

### Card #2 — Vinpearl: Tổng hợp bàn giao ca khách sạn

```text
┌──────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2 (SCAN #3)                              │
│                                                              │
│ Bài toán: Nhân viên lễ tân phải ghi lại công việc chưa        │
│ xử lý để bàn giao cho ca sau, dễ thiếu thông tin.             │
│ Công ty thành viên: [x] Vinpearl                              │
│                                                              │
│ Ai đang gặp khó khăn (Actor)?                                 │
│ Nhân viên lễ tân và trưởng ca khách sạn.                      │
│                                                              │
│ Workflow hiện tại (5 bước):                                   │
│  1. Ghi lại công việc trong ca                                │
│  --> 2. Tổng hợp yêu cầu khách chưa xử lý                     │
│  --> 3. Ghi chú các vấn đề cần bàn giao                       │
│  --> 4. Ca sau đọc và tiếp nhận công việc                     │
│  --> 5. Trưởng ca kiểm tra lại                                │
│                                                              │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2–3.                    │
│ Phải đọc nhiều ghi chú, có thể bỏ sót công việc.              │
│                                                              │
│ AI có thể hỗ trợ bước nào? Bước 2–3.                          │
│ Tóm tắt ghi chú, liệt kê việc chưa hoàn thành.                │
│                                                              │
│ Đo thành công bằng gì (Metric có số)?                         │
│ - Giảm thời gian bàn giao từ 18 xuống 10 phút/ca.              │
│ - Phát hiện >= 90% công việc chưa hoàn thành.                 │
│                                                              │
│ Quick Architecture: [ ] No AI [ ] Rule [x] LLM [ ] Agent     │
│ Lý do: LLM có thể tóm tắt và hiểu các ghi chú khác nhau.      │
└──────────────────────────────────────────────────────────────┘
```

### Card #3 — VinBus: Phân loại báo cáo lỗi xe buýt

```text
┌──────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3 (SCAN #4)                              │
│                                                              │
│ Bài toán: Nhân viên phải đọc và phân loại báo cáo lỗi xe,     │
│ nhưng mỗi tài xế có cách mô tả khác nhau.                     │
│ Công ty thành viên: [x] VinBus                                │
│                                                              │
│ Ai đang gặp khó khăn (Actor)?                                 │
│ Nhân viên điều hành và bộ phận kỹ thuật.                      │
│                                                              │
│ Workflow hiện tại (5 bước):                                   │
│  1. Tài xế báo lỗi xe                                        │
│  --> 2. Nhân viên tiếp nhận và ghi thông tin                  │
│  --> 3. Đọc mô tả và phân loại lỗi                            │
│  --> 4. Chuyển báo cáo cho bộ phận kỹ thuật                   │
│  --> 5. Kỹ thuật viên kiểm tra và xử lý                       │
│                                                              │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3.                      │
│ Mô tả lỗi khác nhau nên dễ nhầm khi phân loại.                │
│                                                              │
│ AI có thể hỗ trợ bước nào? Bước 3.                            │
│ Đọc mô tả, nhóm lỗi giống nhau và gợi ý phân loại.            │
│                                                              │
│ Đo thành công bằng gì (Metric có số)?                         │
│ - Giảm thời gian phân loại từ 10 xuống 3 phút/báo cáo.        │
│ - Độ chính xác phân loại đạt >= 90% khi thử nghiệm.           │
│                                                              │
│ Quick Architecture: [ ] No AI [ ] Rule [x] LLM [ ] Agent     │
│ Lý do: LLM hiểu được nhiều cách mô tả lỗi khác nhau.          │
└──────────────────────────────────────────────────────────────┘
```
