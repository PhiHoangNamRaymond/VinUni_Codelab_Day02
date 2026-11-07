# 📝 Phase 6 — AI Log & Reflection (Cá nhân)

Trong Lab 02, tôi dùng ChatGPT để phát triển bài toán Vinpearl: ca trưởng phải đọc các đánh giá của khách, tìm phản ánh về vệ sinh phòng và chuyển danh sách cho bộ phận buồng phòng. Tôi đưa README, worksheet và bài mẫu để AI hiểu yêu cầu. ChatGPT giúp tôi sắp xếp năm ý tưởng theo bốn lens, hoàn thiện ba Quick Problem Card và mở rộng thẻ Vinpearl thành báo cáo Deep-Dive. Phần hỗ trợ có ích nhất là biến mục tiêu “rà nhanh hơn” thành phép so sánh cụ thể giữa đọc tay, lọc từ khóa và LLM trên cùng một bộ đánh giá.

### AI làm chưa đúng ở đâu?

Khi tôi yêu cầu trình bày Phase 3 theo ví dụ, ChatGPT xếp bốn hộp trên cùng một hàng. Các dòng quá rộng và phần nối giữa các bước khó theo dõi trong Markdown. Tôi phản hồi “lỗi trình bày rồi phần các bước”. Sau đó, ChatGPT chuyển sơ đồ thành hai hàng, mỗi hàng hai hộp, và nối theo thứ tự 1 → 2 → 3 → 4. Khi tôi nói rõ cần một mẫu để vẽ lại trên giấy, AI tạo ảnh PNG có màu riêng cho điểm chuyển giao và điểm nghẽn, kèm thời gian từng bước.

Về nội dung, tôi chưa có dữ liệu vận hành để xác nhận các mốc thời gian. Báo cáo dùng **12 phút/lô** cho toàn bộ quy trình và **10 phút/lô** cho riêng hai bước đọc và ghi nhận. Nếu dùng lẫn hai mốc, mục tiêu **7 phút/lô** sẽ dễ bị hiểu là thời gian cho cả quy trình. Vì vậy, tôi ghi rõ 7 phút chỉ là mục tiêu cho phần rà soát nếu đo được mốc đọc tay là 10 phút. Mức giảm **30%** và tỷ lệ phát hiện **90%** cũng là ngưỡng cần kiểm chứng khi thử nghiệm.

### Tôi đã điều chỉnh yêu cầu và ranh giới thế nào?

Thay vì chỉ yêu cầu hoàn thiện báo cáo theo README, tôi gửi trực tiếp mẫu Phase 3 để làm rõ cách trình bày. Sau khi phát hiện lỗi bố cục, tôi chỉ rõ phần cần sửa là sơ đồ các bước. Lần sau, tôi sẽ ghi ngay trong yêu cầu rằng mỗi hộp phải có số bước, người thực hiện, thời gian, đầu vào và đầu ra, đồng thời yêu cầu hai hộp mỗi hàng để dễ đọc trên trang Markdown.

Với bài toán Vinpearl, tôi giới hạn LLM ở việc tạo bản nháp từ đánh giá đã ẩn danh. Mỗi đề xuất chỉ gồm mã đánh giá, nhãn và trích đoạn có thể đối chiếu với văn bản nguồn. Ca trưởng kiểm tra, bổ sung phản ánh bị sót và duyệt trước khi bàn giao. Trường hợp mô hình lỗi hoặc kết quả không hợp lệ sẽ quay về rà soát thủ công. Thời gian duyệt, sửa và rà lại đều phải tính vào phép đo.

Tôi chọn **NOT YET** vì vẫn cần bộ đánh giá được phép sử dụng, số đo đọc tay và xác nhận quy trình duyệt từ người vận hành. Qua bài này, tôi học được cách dùng AI để cụ thể hóa một giả thuyết, rồi kiểm tra lại phạm vi đo và những việc con người vẫn phải làm trước khi kết luận giải pháp có hiệu quả.
