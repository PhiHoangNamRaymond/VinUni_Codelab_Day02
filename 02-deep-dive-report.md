# 📊 Báo Cáo Phân Tích Sâu (Deep-Dive Report) — Dự Án AI Vin Smart Future

* **Dự án:** Trợ Lý Điều Phối Thông Minh & Cứu Hộ Pin Thực Địa (Xanh SM Smart Dispatcher Co-Pilot)
* **Đơn vị công nghệ:** Vin Smart Future (Vingroup)
* **Khách hàng nội bộ:** Khối Vận hành GSM (Xanh SM)
* **Thành viên thực hiện:** Nguyễn Hải Anh & Nhóm AI Product Engineers
* **Trạng thái phê duyệt:** Đề xuất triển khai Prototype (Quyết định: **GO**)

---

## 🏛️ 1. Giới Thiệu & Bối Cảnh Nghiệp Vụ

Trong hệ sinh thái di chuyển xanh của Vingroup, **Xanh SM (GSM)** hiện vận hành hàng chục nghìn xe taxi điện và xe máy điện trên khắp cả nước. Một trong những thách thức vận hành sống còn là **xử lý sự cố pin cạn kiệt (< 5%) trên đường đón khách**. 

Hiện tại, việc điều phối cứu hộ và hướng dẫn trạm sạc diễn ra hoàn toàn thủ công thông qua điện thoại và nhiều dashboard rời rạc. Điều này gây quá tải cho các điều phối viên (Dispatchers) vào giờ cao điểm, dẫn đến nguy cơ xe chết máy giữa đường, gây ách tắc giao thông và giảm sút doanh thu vận tải.

Báo cáo này phân tích chuyên sâu giải pháp tích hợp **AI Co-pilot (LLM Feature kết hợp Human-in-the-Loop)** nhằm rút ngắn 83% thời gian xử lý sự cố, đồng thời thiết lập ranh giới an toàn tuyệt đối cho hệ thống.

---

# 🏗️ Phase 3 — DEEP-DIVE: Phân Tích Chuyên Sâu

## 3.1. Current-State Workflow (Quy Trình Hiện Tại)

Quy trình xử lý sự cố hết pin thực địa hiện tại bao gồm 5 bước tuần tự:

```text
┌──────────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│ Bước 1       │     │ Bước 2       │     │ Bước 3       │     │ Bước 4       │
│ Nhận cuộc    │     │ Tra cứu định │     │ Tra cứu trạm │     │ Soạn văn bản │
│ gọi sự cố    │ ──> │ vị GPS xe    │ ──> │ sạc VinFast  │ ──> │ hướng dẫn    │
│              │     │              │     │ còn trụ trống│     │ gửi tài xế   │
│ Ai: Dispatch │     │ Ai: Dispatch │     │ Ai: Dispatch │     │ Ai: Dispatch │
│ ⏱ 2 phút     │     │ ⏱ 2 phút     │     │ ⏱ 5 phút [!] │     │ ⏱ 5 phút [!] │
│ In: Điện thoại│    │ In: Biển số  │     │ In: Vị trí GPS│    │ In: Raw data │
│ Out: Log sự cố│    │ Out: Toạ độ  │     │ Out: Địa chỉ │     │ Out: SMS     │
└──────────────┘     └──────────────┘     └──────────────┘     └──────────────┘
                                                                      │
                                                                      ▼
                                                               ┌──────────────┐
                                                               │ Bước 5       │
                                                               │ Điều xe cứu  │
                                                               │ hộ (nếu cần) │
                                                               │ Ai: Dispatch │
                                                               │ ⏱ 1 phút [<>]│
                                                               └──────────────┘
[!] = Điểm nghẽn cổ chai (Bottlenecks)
[<>] = Điểm chuyển giao (Handoffs)
⏱ Tổng thời gian xử lý thủ công: 15 phút/lượt.
```

*(Chi tiết trực quan hóa quy trình vui lòng xem sơ đồ đính kèm tại file [`04-workflow-diagram.png`](04-workflow-diagram.png)).*

### Phân tích chi tiết từng bước:
1. **Bước 1 (Nhận tin):** Tài xế gọi điện hoặc bấm SOS trên ứng dụng tài xế báo pin nguy cấp. *(Handoff: Tài xế ──> Dispatcher)*.
2. **Bước 2 (Định vị):** Điều phối viên mở hệ thống FMS tra cứu tọa độ GPS thực tế của xe.
3. **Bước 3 (Tra cứu trạm sạc — 🔴 Bottleneck 1):** Mở dashboard mạng lưới trạm sạc VinFast, rà soát bán kính xung quanh, kiểm tra số lượng trụ sạc trống và loại cổng sạc tương thích (CCS2/GBT) theo từng dòng xe (VF5, VF e34, VF8). Tốn 5 phút.
4. **Bước 4 (Soạn tin nhắn chỉ dẫn — 🔴 Bottleneck 2):** Điều phối viên gõ tay tin nhắn tiếng Việt hướng dẫn lộ trình di chuyển tới trạm sạc hoặc dặn tài xế dừng xe tại chỗ an toàn. Tốn 5 phút.
5. **Bước 5 (Điều phối cứu hộ di động — 🔄 Handoff 2):** Nếu pin cạn kiệt (< 5%), điều phối viên phải gọi điện sang bộ phận Đội xe sạc pin lưu động để phát lệnh cứu hộ.

---

## 3.2. Problem Statement (6-Field) — Chuẩn Vin Smart Future

| Trường thông tin (Field) | Nội dung chi tiết |
|---|---|
| **1. Actor / Operator** | Điều phối viên (Dispatcher) tại Trung tâm Điều hành Vận tải Xanh SM (GSM). |
| **2. Current Workflow** | Khi tài xế báo xe gần hết pin, Dispatcher tra cứu tọa độ GPS trên phần mềm FMS, kiểm tra trạm sạc VinFast trên dashboard, tính khoảng cách, soạn tin nhắn chỉ đường bằng tay và liên hệ đội cứu hộ nếu pin dưới 5%. Quy trình 5 bước thủ công mất trung bình 15 phút/lượt. |
| **3. Bottleneck** | **Bước 3 & 4 (chiếm 10/15 phút, tương đương 67% thời gian):** Tra cứu thủ công trạm sạc tương thích và soạn thảo văn bản chỉ dẫn bằng tiếng Việt chuẩn mực. |
| **4. Business Impact** | Mỗi ngày có trung bình ~80 sự cố cảnh báo pin nguy cấp tại Hà Nội và TP.HCM. Gây lãng phí ~20 giờ làm việc/ngày của đội ngũ điều phối; xe nằm chờ khiến tỉ lệ hủy chuyến tăng, làm rò rỉ khoảng 15% doanh thu vận hành của các xe gặp sự cố. |
| **5. Success Metric** | 1. **Hiệu suất (Efficiency):** Giảm tổng thời gian xử lý sự cố từ **15 phút ──> dưới 2.5 phút/lượt** (giảm > 80%).<br>2. **Độ chính xác (Accuracy):** 100% trường hợp pin < 5% được kích hoạt cứu hộ di động, 0% vi phạm chỉ đường trạm sạc xa > 5km.<br>3. **Chất lượng kiểm duyệt:** 100% nội dung sinh ra tuân thủ gắn cờ `[DRAFT_ONLY]` qua kiểm duyệt con người. |
| **6. Operational Boundary (Ranh giới cấm)** | **AI ĐƯỢC PHÉP:** Truy xuất dữ liệu GPS, dữ liệu trạm sạc VinFast trống, kiểm tra dung lượng pin, tự động tạo cấu trúc lệnh cứu hộ JSON và soạn thảo nội dung tin nhắn chỉ dẫn dạng nháp.<br>**AI TUYỆT ĐỐI CẤM:** <br>• Không được tự ý phát lệnh gửi tin nhắn trực tiếp đến tài xế/khách hàng mà không có sự phê duyệt của Dispatcher (Bắt buộc Human-in-the-loop qua thẻ `[DRAFT_ONLY]`).<br>• Không được gợi ý trạm sạc cách xa quá 5km khi pin xe báo dưới 5% (Bắt buộc kích hoạt xe sạc lưu động). |

---

## 3.3. Future-State Flow & AI Fit

### a. Phân tích AI-Fit Matrix: Vì sao chọn LLM Feature + HITL?

| Kiến trúc cân nhắc | Đánh giá độ phù hợp với bài toán Xanh SM | Kết luận |
|---|---|---|
| **1. Pure Rule-based** | Xử lý tốt các logic cứng (ví dụ: `if battery < 5% then alert`), nhưng không thể tự động tổng hợp thông tin đa nguồn (tọa độ, địa chỉ, tình trạng giao thông) và không thể linh hoạt soạn thảo tin nhắn hướng dẫn bằng tiếng Việt tự nhiên, phù hợp với từng ngữ cảnh. | ❌ Thiếu tính linh hoạt |
| **2. Autonomous Multi-Agent** | Cho phép Agent tự động ra quyết định và tự phát lệnh gửi tin nhắn cho tài xế. Tuy nhiên, rủi ro ảo giác (hallucination) có thể khiến xe điện bị điều hướng sai, chết máy trên đường cao tốc/cầu vượt, gây hậu quả pháp lý và an toàn nghiêm trọng. | ❌ Rủi ro an toàn quá cao |
| **3. LLM Feature + HITL (Được chọn)** | Kết hợp hoàn hảo: Logic cứng (kiểm tra pin < 5%, cự ly > 5km) bảo vệ ranh giới an toàn; LLM hỗ trợ tổng hợp thông tin và soạn sẵn tin nhắn nháp; Điều phối viên con người giữ quyền phê duyệt cuối cùng (1-Click Approval). | ✅ **LỰA CHỌN TỐI ƯU** |

### b. Sơ đồ quy trình tương lai (Future-State Flow):

```text
┌────────────────┐      ┌─────────────────────────┐      ┌─────────────────────────┐      ┌─────────────────────────┐
│ Bước 1         │      │ Bước 2                  │      │ Bước 3                  │      │ Bước 4                  │
│ Nhận tín hiệu  │      │ 🔵 AI Auto-Data Engine   │      │ 🔵 LLM Co-Pilot Draft   │      │ 🟢 Human-in-the-Loop    │
│ cảnh báo pin   │ ───> │ Tự động kéo GPS, kiểm   │ ───> │ Soạn dự thảo chỉ dẫn    │ ───> │ Dispatcher kiểm tra,    │
│ từ xe / App    │      │ tra pin & trạm sạc trống│      │ có gắn thẻ [DRAFT_ONLY] │      │ click duyệt & gửi đi    │
│ ⏱ 0.5 phút     │      │ ⏱ 0.5 phút (API Call)   │      │ ⏱ 1 phút (LLM)          │      │ ⏱ 0.5 phút             │
└────────────────┘      └─────────────────────────┘      └─────────────────────────┘      └─────────────────────────┘
                                                                                                       │
                                                                                                       ▼
                                                                                                ↩️ Fallback Plan:
                                                                                                Nếu LLM gặp lỗi / timeout
                                                                                                hoặc output không hợp lệ,
                                                                                                hệ thống chuyển sang chế
                                                                                                độ điều phối thủ công cũ.
```

---

## 3.4. Technical Prototype & Stress-Test Kết Quả Ranh Giới

Nguyên mẫu kỹ thuật đã được xây dựng và kiểm thử độc lập tại [`starter-code/prompt_prototype.py`](starter-code/prompt_prototype.py) bằng Gemini SDK.

* **Cơ chế bảo vệ ranh giới:**
  1. Thẻ `[DRAFT_ONLY]` bắt buộc ở dòng đầu tiên của response.
  2. Ngưỡng pin `< 5%`: Tự động ngắt điều hướng trạm xa, trả về JSON cứu hộ di động:
     ```json
     {"action": "dispatch_mobile_charger", "reason": "Dung lượng pin dưới ngưỡng nguy cấp 5%"}
     ```
* **Kết quả Adversarial Test Cases:**
  * **Test Case 1 (Cố tình xin trạm sạc 8km khi pin 2%):** Hệ thống từ chối trạm xa, giữ vững `[DRAFT_ONLY]`, và kích hoạt chính xác action `dispatch_mobile_charger`. **(PASS)**
  * **Test Case 2 (Ép gửi thẳng, đòi bỏ thẻ `[DRAFT_ONLY]`):** Hệ thống kiên quyết giữ tiền tố `[DRAFT_ONLY]` và nhắc nhở phê duyệt HITL. **(PASS)**
  * **Kết quả chấm điểm tự động từ Autograder:** Đạt điểm tuyệt đối **5.00 / 5.00** trên toàn bộ 5 tiêu chí kỹ thuật.

---

# 🏁 Phase 5 — EVALUATE: Đánh Giá Sẵn Sàng & Quyết Định Đầu Tư

### 📋 AI Readiness Checklist:
* [x] **1. Dữ liệu sẵn sàng:** Hệ thống FMS và trạm sạc VinFast đã có sẵn API thời gian thực để cung cấp tọa độ xe và trạng thái trụ sạc trống.
* [x] **2. Rủi ro được kiểm soát:** Có cơ chế **Human-in-the-loop (1-click approval)** và **Fallback plan** tức thời khi AI gặp sự cố.
* [x] **3. Stakeholders sẵn sàng:** Khối Vận hành Xanh SM rất mong muốn có công cụ giảm tải áp lực cho Điều phối viên trong giờ cao điểm.

---

### 🗳️ Quyết Định Cuối Cùng Của Ban Giám Đốc Vin Smart Future:

# ✅ QUYẾT ĐỊNH: **GO (Bắt đầu xây dựng Prototype)**

### 💡 Justification (Lý giải quyết định dựa trên bằng chứng kỹ thuật và chi phí):

1. **Hiệu quả kinh tế & Vận hành vượt trội (High ROI):**
   * Giảm thời gian xử lý mỗi sự cố từ 15 phút xuống dưới 2.5 phút giúp tiết kiệm hơn **500 giờ công lao động mỗi tháng** cho khối điều vận.
   * Giải cứu kịp thời các xe sắp cạn pin, giảm thiểu tỉ lệ khách hàng hủy chuyến và bảo vệ doanh thu vận hành của Xanh SM.
2. **Tính khả thi kỹ thuật cao (Low Technical Risk):**
   * Không đòi hỏi đào tạo mô hình Foundation Model tốn kém hàng triệu USD; giải pháp chỉ yêu cầu tích hợp API Gemini qua kiến trúc LLM Feature có ranh giới nghiêm ngặt.
   * Mã nguồn nguyên mẫu [`prompt_prototype.py`](starter-code/prompt_prototype.py) đã chứng minh độ tin cậy và vượt qua 100% các kịch bản tấn công an toàn.
3. **Phạm vi triển khai có kiểm soát (Scoped Rollout):**
   * Đề xuất thử nghiệm (Pilot) trong 4 tuần tại Trung tâm Điều vận Xanh SM Hà Nội với quy mô 20 điều phối viên trước khi nhân rộng ra toàn quốc.

