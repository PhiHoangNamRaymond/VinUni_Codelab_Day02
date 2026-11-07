# 01 — Problem Scan & Quick Assess (Cá nhân)

> **Lab 02: AI Product Scoping — Vin Smart Future**
> **Học viên:** Vũ Xuân Trường — Mã SV: 2A202603433
> **Vai trò:** AI Product Engineer, Vin Smart Future (Vingroup)

---

# 🔍 Phase 1 — SCAN: Bảng quét cơ hội (5 bài toán thực tế)

Quét bằng **4 Lenses** (Lặp lại · Tốn thời gian · AI-upgrade · Pain từ người khác) qua vận hành của các công ty thành viên Vingroup. Các bài toán được thu thập từ phản ánh thực tế của chủ xe, tài xế, cư dân, khách hàng trên diễn đàn chủ xe, Trustpilot, Google Reviews, nhóm Facebook và báo chí giai đoạn 2023–2025.

| # | Subsidiary | Lens | Mô tả ngắn bài toán (kèm chứng cứ thực tế) |
|---|------------|------|---------------------------------------------|
| 1 | **VinFast** | Pain từ người khác | **Lỗi phiên sạc gián đoạn:** Chủ xe VF8 phản ánh xe tự dừng sạc khi mới vào 3–5% pin, lỗi giao tiếp giữa xe và trụ sạc công cộng phải thử nhiều lần; VinFast phải phát hành firmware 8.3.10.11 (5/2025) để khắc phục. Kỹ thuật viên L1 phải tra log từng phiên sạc thủ công để chẩn đoán, chủ xe chờ lâu, phải gọi lại nhiều lần. |
| 2 | **VinFast** | Tốn thời gian | **Xử lý khiếu nại CSKH chậm, thiếu minh bạch:** Khiếu nại về lỗi sạc/xe qua hotline, app, fanpage được đọc — ghi log — phân loại — soạn phản hồi hoàn toàn thủ công (15–20 phút/ticket, case phức tạp kéo dài nhiều ngày; bài viral "Day 12 of VinFast EV Nightmare" và TrustScore ~3/5 trên Trustpilot cho thấy khách leo thang khiếu nại lên mạng xã hội). |
| 3 | **VinFast** | AI-upgrade | **Bảo trì xe phản ứng bị động (Reactive maintenance):** Lỗi pin/phan mềm xe chỉ được xử lý sau khi chủ xe báo, chưa khai thác dữ liệu telemetry sẵn có để dự báo hư hỏng; firmware bị lỗi phải chờ bản vá đại trà thay vì cảnh báo từng xe theo dấu hiệu sớm. |
| 4 | **Xanh SM** | Pain từ người khác | **Gợi ý điểm đón không chính xác:** Tài xế phàn nàn hệ thống gợi ý điểm đón sai/không tối ưu, phải gọi điện hỏi khách vị trí thật, khách chờ lâu giờ cao điểm, phát sinh hủy chuyến do "tài xế không tìm thấy khách". |
| 5 | **Vinpearl / VinWonders** | Lặp lại + Tốn thời gian | **Ùn tắc check-in mùa cao điểm & trả lời review thủ công:** Lễ tân quá tải lúc check-in cao điểm (Vinpearl phải tung check-in online + nhận diện gương mặt để giảm ùn — chứng tỏ pain có thật); đội marketing trả lời tay từng review đa ngôn ngữ trên TripAdvisor/Google Reviews. |

---

# 🃏 Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards

Chọn top 3 từ bảng SCAN: **#2 (VinFast CSKH), #4 (Xanh SM điểm đón), #1 (VinFast lỗi sạc).**

> 📌 *Phần quyết định chọn bài toán Deep-Dive và phân tích sâu nằm ở file riêng: [`02-deep-dive-report.md`](02-deep-dive-report.md).*

## Card #1 — VinFast: Phân loại & Soạn phản hồi khiếu nại CSKH

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1 (SCAN #2)                             │
│                                                             │
│ Bài toán: CSKH VinFast xử lý thủ công luồng khiếu nại về    │
│ lỗi sạc/xe (đọc, tra cứu, phân loại, soạn phản hồi) gây    │
│ chậm trễ, khách hàng leo thang khiếu nại lên mạng xã hội.  │
│ Công ty thành viên: [x] VinFast                             │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│ Chuyên viên CSKH L1 (quá tải ticket), Giám sát CSKH         │
│ (phê duyệt chậm), Chủ xe VF (chờ phản hồi nhiều ngày).     │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Tiếp nhận khiếu nại qua hotline/app/fanpage            │
│   ──> 2. Đọc và ghi log tay vào ticket hệ thống             │
│   ──> 3. Tra cứu lịch sử xe + phiên sạc trên nhiều hệ thống │
│   ──> 4. Phân loại mức độ nghiêm trọng (severity) tay       │
│   ──> 5. Soạn phản hồi và chờ cấp trên duyệt rồi gửi        │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3–5                   │
│ (⏱ 15–20 phút/ticket; case phức tạp kéo dài 12+ ngày)       │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2–5              │
│ (tự tổng hợp lịch sử xe + phân loại severity + soạn draft)  │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ - Thời gian phản hồi đầu tiên: 45 phút ──> dưới 5 phút      │
│ - 100% bản thảo AI gắn thẻ [DRAFT_ONLY] chờ duyệt (HITL)    │
│ - Giảm 50% số case leo thang khiếu nại lên mạng xã hội      │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

## Card #2 — Xanh SM: Gợi ý điểm đón thông minh (Smart Pickup)

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2 (SCAN #4)                             │
│                                                             │
│ Bài toán: Hệ thống gán điểm đón mặc định không chính xác,   │
│ tài xế phải gọi điện hỏi khách vị trí thật, làm khách chờ   │
│ lâu và tăng tỷ lệ hủy chuyến giờ cao điểm.                  │
│ Công ty thành viên: [ ] VinFast  [x] Xanh SM                │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│ Tài xế Xanh SM (mất giờ lượn tìm khách, bị khách trách),    │
│ Khách hàng (chờ đợi, hủy chuyến), Điều phối viên (chửi).    │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Khách đặt xe qua app SM                                │
│   ──> 2. Hệ thống gán điểm đón mặc định (pin/auto, sai)     │
│   ──> 3. Tài xế gọi điện xác nhận vị trí với khách          │
│   ──> 4. Khách mô tả vị trí bằng lời (khó định vị)          │
│   ──> 5. Tài xế nhập lại địa chỉ vào app để tìm đường       │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2–4                   │
│ (⏱ 3–5 phút/chuyến vào giờ cao điểm)                        │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2 & 4            │
│ (gợi ý điểm đón tối ưu theo POI + lịch sử đón + giao        │
│ thông thời gian thực; soạn draft tin xác nhận cho tài xế)   │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ - Giảm 70% cuộc gọi xác nhận điểm đón tài xế–khách          │
│ - Thời gian tiếp cận điểm đón: 6 phút ──> 3 phút            │
│ - Giảm 30% tỷ lệ hủy chuyến do không tìm thấy nhau          │
│                                                             │
│ Quick Architecture: [ ] No AI  [x] Rule  [x] LLM  [ ] Agent │
│ (Rule-geocoding + LLM soạn tin nhắn xác nhận)               │
└─────────────────────────────────────────────────────────────┘
```

## Card #3 — VinFast: Trợ lý chẩn đoán lỗi phiên sạc (Charging Diagnostic Co-pilot)

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3 (SCAN #1)                             │
│                                                             │
│ Bài toán: Chủ xe VF báo lỗi sạc (tự dừng sau 3–5% pin, lỗi  │
│ giao tiếp xe–trụ sạc) nhưng kỹ thuật viên L1 phải tra log   │
│ phiên sạc thủ công từng case để chẩn đoán nguyên nhân.      │
│ Công ty thành viên: [x] VinFast                             │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│ Kỹ thuật viên L1 hotline (mò log từng case), Chủ xe VF      │
│ (chờ chẩn đoán, phải gọi lại nhiều lần).                    │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Chủ xe gọi hotline/app báo lỗi sạc                     │
│   ──> 2. NV ghi lại mô tả lỗi bằng lời của khách            │
│   ──> 3. Kỹ thuật tra log phiên sạc trên dashboard nội bộ   │
│   ──> 4. Đối chiếu tay với bảng mã lỗi & phiên bản firmware │
│   ──> 5. Hướng dẫn khắc phục hoặc đặt lịch bảo dưỡng        │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3–4                   │
│ (⏱ 15–20 phút/case; mã lỗi mới chưa có trong bảng)          │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 3–5              │
│ (AI đọc log + mô tả lỗi ──> phân loại nguyên nhân ──>       │
│  draft hướng dẫn khắc phục/đặt lịch cho NV duyệt)           │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ - Thời gian chẩn đoán: 20 phút ──> dưới 3 phút              │
│ - 80% case phổ biến xử lý xong ở L1, không chuyển kỹ sư     │
│ - Tỷ lệ nhận diện đúng nguyên nhân ≥ 90% (đối chiếu NVKT)   │
│                                                             │
│ Quick Architecture: [ ] No AI  [x] Rule  [x] LLM  [ ] Agent │
│ (Rule cho mã lỗi đã biết + LLM cho mô tả tiếng Việt)        │
└─────────────────────────────────────────────────────────────┘
```
