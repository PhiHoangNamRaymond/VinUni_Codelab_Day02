# 🔍 Phase 1 — SCAN (Cá nhân, 20 min)

Tôi rà soát các tác vụ vận hành của các công ty thành viên Vingroup qua bốn lens. Các quy trình và mốc thời gian dưới đây là giả định cần kiểm chứng với người vận hành. Các ngưỡng trong từng thẻ là mục tiêu thử nghiệm.

### 4 Lenses tìm bài toán AI cho Vingroup

1. **Lặp lại (Repetitive)** — Tác vụ được thực hiện nhiều lần.
2. **Tốn thời gian (Time-consuming)** — Tác vụ cần nhiều thời gian xử lý thủ công.
3. **AI có thể tốt hơn (AI-upgrade)** — Dịch vụ phản hồi chậm hoặc dùng câu trả lời mẫu thiếu ngữ cảnh.
4. **Pain từ người khác (Stakeholder Pain)** — Điểm nghẽn ảnh hưởng trực tiếp đến khách hàng hoặc nhân viên.

### 📝 List bài toán của tôi

| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
|---|---|---|---|
| 1 | Vinpearl | Tốn thời gian | Ca trưởng đọc từng đánh giá để lọc phản ánh về vệ sinh phòng trước khi chuyển cho bộ phận buồng phòng. |
| 2 | Vinhomes | Pain từ người khác | Cư dân phải giải thích lại sự cố khi yêu cầu bảo trì bị chuyển nhầm bộ phận. |
| 3 | VinFast | Lặp lại | Nhân viên đối soát rà từng bảng kê sạc để tìm các dòng có thể bị tính trùng. |
| 4 | Vinpearl | AI có thể tốt hơn | Khách phải hỏi lại khi câu trả lời mẫu về vé thiếu thông tin theo ngày đi hoặc loại vé. |
| 5 | Xanh SM | Tốn thời gian | Nhân viên phải đọc ghi chú của tài xế và tổng đài để tổng hợp lý do hủy chuyến. |

---

# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

Ba thẻ được chọn từ bảng SCAN là **#1 Vinpearl**, **#2 Vinhomes** và **#3 VinFast**.

```text
┌────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                                      │
│                                                                            │
│ Bài toán (1 câu): Ca trưởng mất thời gian đọc các đánh giá để tìm phản ánh │
│ về vệ sinh phòng và chuyển cho bộ phận buồng phòng.                        │
│ Công ty thành viên: [ ] VinFast   [ ] Xanh SM   [ ] Vinhomes               │
│                     [ ] Vinmec    [x] Khác (Vinpearl)                      │
│                                                                            │
│ Ai đang đau (Actor)? Ca trưởng phụ trách rà soát phản hồi của khách.       │
│                                                                            │
│ Workflow thủ công hiện tại (4 bước):                                       │
│   1. Mở danh sách đánh giá                                                 │
│   2. Đọc từng đánh giá và xác định có phản ánh về vệ sinh phòng hay không  │
│   3. Ghi lại câu phản ánh và mã đánh giá                                   │
│   4. Chuyển danh sách cho bộ phận buồng phòng.                             │
│                                                                            │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2–3, ước tính 10 phút cho 30 đánh    │
│ giá. Một phản ánh có thể nằm trong đoạn nhận xét về nhiều chủ đề hoặc được │
│ diễn đạt gián tiếp.                                                        │
│                                                                            │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                                      │
│ Ở bước 2–3, LLM gắn nhãn và trích nguyên văn câu liên quan kèm mã đánh     │
│ giá. Ca trưởng đối chiếu bản gốc, bổ sung mục bị sót và duyệt danh sách    │
│ trước khi chuyển. Nếu công cụ lỗi, ca trưởng rà thủ công.                  │
│                                                                            │
│ Đo thành công bằng gì (Metric có số)?                                      │
│ Giảm ít nhất 30% thời gian rà soát so với đọc tay, tính cả thời gian ca    │
│ trưởng duyệt và sửa. Với mốc giả định 10 phút/lô, mục tiêu tương ứng là    │
│ tối đa 7 phút/lô. Đầu ra của công cụ trước khi duyệt phải phát hiện ít     │
│ nhất 90% đánh giá có phản ánh vệ sinh phòng theo nhãn do người chấm xác    │
│ nhận. Đo cả thời gian và tỷ lệ phát hiện trên cùng bộ mẫu cho ba cách: đọc │
│ tay, lọc từ khóa và dùng LLM.                                              │
│                                                                            │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent                │
│ Với rule từ khóa làm mốc so sánh.                                          │
└────────────────────────────────────────────────────────────────────────────┘
```

```text
┌────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                                      │
│                                                                            │
│ Bài toán (1 câu): Yêu cầu bảo trì có mô tả mơ hồ dễ bị chuyển nhầm bộ      │
│ phận, khiến cư dân phải giải thích lại.                                    │
│ Công ty thành viên: [ ] VinFast   [ ] Xanh SM   [x] Vinhomes               │
│                     [ ] Vinmec    [ ] Khác                                 │
│                                                                            │
│ Ai đang đau (Actor)? Nhân viên tiếp nhận yêu cầu bảo trì. Cư dân chịu ảnh  │
│ hưởng khi yêu cầu bị chuyển nhầm.                                          │
│                                                                            │
│ Workflow thủ công hiện tại (4 bước):                                       │
│   1. Nhận yêu cầu                                                          │
│   2. Đọc mô tả sự cố                                                       │
│   3. Xác định bộ phận phụ trách hoặc hỏi thêm cư dân                       │
│   4. Chuyển yêu cầu đến bộ phận đã xác nhận.                               │
│                                                                            │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3, ước tính 3 phút thao tác cho mỗi  │
│ yêu cầu mơ hồ, chưa tính thời gian chờ cư dân trả lời.                     │
│                                                                            │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                                      │
│ Ở bước 3, LLM gợi ý nhóm điện, nước, thiết bị chung hoặc cần làm rõ dựa    │
│ trên mô tả. Nhân viên kiểm tra gợi ý, hỏi thêm khi thiếu thông tin và xác  │
│ nhận bộ phận trước khi chuyển.                                             │
│                                                                            │
│ Đo thành công bằng gì (Metric có số)?                                      │
│ Gợi ý đúng bộ phận cho ít nhất 18/20 yêu cầu có đủ thông tin. Trên 10 mẫu  │
│ thiếu thông tin, gắn nhãn cần làm rõ cho ít nhất 9/10 mẫu. Chấm gợi ý      │
│ trước khi nhân viên sửa, theo nhãn đã được xác nhận.                       │
│                                                                            │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent                │
│ Để phân loại mô tả tự do.                                                  │
└────────────────────────────────────────────────────────────────────────────┘
```

```text
┌────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                                      │
│                                                                            │
│ Bài toán (1 câu): Nhân viên đối soát phải rà từng dòng bảng kê để phát     │
│ hiện phiên sạc có thể bị tính hai lần.                                     │
│ Công ty thành viên: [x] VinFast   [ ] Xanh SM   [ ] Vinhomes               │
│                     [ ] Vinmec    [ ] Khác                                 │
│                                                                            │
│ Ai đang đau (Actor)? Nhân viên đối soát hóa đơn sạc.                       │
│                                                                            │
│ Workflow thủ công hiện tại (4 bước):                                       │
│   1. Nhận bảng kê                                                          │
│   2. Rà mã phiên sạc                                                       │
│   3. Đối chiếu thời gian và số tiền                                        │
│   4. Đánh dấu dòng nghi trùng để xác minh.                                 │
│                                                                            │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2–3, ước tính 10 phút cho bảng kê 50 │
│ dòng.                                                                      │
│                                                                            │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                                      │
│ Ở bước 2–3, rule đánh dấu dòng có cùng mã phiên và số tiền với một dòng    │
│ trước đó trong cùng bảng kê. Dòng thiếu mã phiên được đưa vào danh sách    │
│ kiểm tra thủ công. Nhân viên đối chiếu thời gian và chứng từ trước khi     │
│ quyết định điều chỉnh.                                                     │
│                                                                            │
│ Đo thành công bằng gì (Metric có số)?                                      │
│ Trên bảng mẫu 50 dòng có 10 dòng trùng đã được đánh dấu, phát hiện ít nhất │
│ 9/10 dòng trùng và cảnh báo nhầm tối đa 2 trong 40 dòng còn lại. Mỗi bản   │
│ sao phát sinh được tính là một dòng trùng.                                 │
│                                                                            │
│ Quick Architecture: [ ] No AI  [x] Rule  [ ] LLM  [ ] Agent                │
│ Vì bảng kê đã có trường dữ liệu để so khớp.                                │
└────────────────────────────────────────────────────────────────────────────┘
```

---

### Đề xuất chọn bài toán cho Deep-Dive

**Chọn Card #1 — Vinpearl.** Có thể dùng một bộ đánh giá ẩn danh đã gán nhãn để so sánh công bằng giữa đọc tay, lọc từ khóa và LLM. Bài thử đo được cả thời gian sau khi ca trưởng duyệt và tỷ lệ phát hiện các phản ánh viết gián tiếp.

- **Card #2 — Vinhomes:** Cần xác nhận danh mục sự cố và bộ phận phụ trách trước khi chấm đề xuất phân loại.
- **Card #3 — VinFast:** Mã phiên và số tiền cho phép thử ngay cách so khớp bằng rule. Bài toán phù hợp để đánh giá tự động hóa đối soát.
