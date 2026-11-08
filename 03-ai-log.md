# 03 – AI LOG: NHẬT KÝ TƯƠNG TÁC VỚI AI

## 1. Mục đích sử dụng AI

Trong buổi học, tôi sử dụng ChatGPT và Gemini như hai công cụ hỗ trợ tìm kiếm và phân tích Business Problem trong hệ sinh thái doanh nghiệp VinGroup.

Mục tiêu ban đầu là tìm hiểu các vấn đề nghiệp vụ có thể tồn tại trong những công ty thành viên, xác định đối tượng chịu ảnh hưởng (Actor), các điểm nghẽn (Pain Point) và tác động kinh doanh (Business Impact). Tôi sử dụng AI để mở rộng góc nhìn và tham khảo nhiều hướng tiếp cận khác nhau, chứ không yêu cầu AI quyết định thay mình nên lựa chọn bài toán nào.

Sau quá trình tìm hiểu, tôi lựa chọn bài toán ứng dụng AI hỗ trợ bác sĩ chẩn đoán hình ảnh tại Vinmec/VRIC trong việc phát hiện các dấu hiệu bất thường trên ảnh X-quang và MRI. Đây là ý tưởng xuất phát từ định hướng và sự quan tâm của cá nhân tôi, không phải ý tưởng do ChatGPT hoặc Gemini đề xuất.

## 2. AI đã hỗ trợ tôi như thế nào?

**Thứ nhất, hỗ trợ tìm kiếm và khám phá các Business Problem.**

Tôi sử dụng ChatGPT và Gemini để tìm kiếm những vấn đề nghiệp vụ có thể phát sinh trong các công ty thành viên. Hai công cụ giúp tôi tiếp cận nhiều lĩnh vực và góc nhìn khác nhau, từ hoạt động vận hành, quản lý đến cung cấp dịch vụ.

Việc tham khảo nhiều gợi ý giúp tôi có thêm cơ sở để so sánh, đánh giá và lựa chọn vấn đề phù hợp với định hướng của bản thân.

**Thứ hai, hỗ trợ phân tích Business Impact.**

Sau khi có các vấn đề cần xem xét, tôi sử dụng AI để phân tích những tác động có thể xảy ra đối với doanh nghiệp, chẳng hạn:
- Ảnh hưởng đến thời gian và hiệu quả vận hành.
- Ảnh hưởng đến chi phí và năng suất nhân sự.
- Ảnh hưởng đến chất lượng dịch vụ và trải nghiệm khách hàng.
- Những rủi ro có thể phát sinh nếu vấn đề không được giải quyết.

AI giúp tôi hệ thống hóa các tác động theo góc nhìn kinh doanh, thay vì chỉ mô tả vấn đề ở khía cạnh kỹ thuật.

**Thứ ba, hỗ trợ hoàn thiện và cấu trúc hóa bài toán do tôi lựa chọn.**

Sau khi lựa chọn bài toán hỗ trợ bác sĩ phân tích hình ảnh y tế, tôi tiếp tục sử dụng ChatGPT để:
- Chuẩn hóa Problem Statement theo sáu thành phần.
- Phân tích Current Workflow và xác định Bottleneck.
- Làm rõ Business Impact và đề xuất Success Metrics.
- Xác định Operational Boundary để giới hạn quyền quyết định của AI.
- Phân tích mức độ phù hợp của Rule/Workflow, LLM Feature và Agent.

Như vậy, AI hỗ trợ tôi trong quá trình tìm kiếm thông tin, phân tích và hoàn thiện cấu trúc bài toán; còn việc lựa chọn vấn đề cuối cùng xuất phát từ định hướng của cá nhân tôi.

## 3. Hạn chế và nguy cơ Hallucination

Trong quá trình sử dụng, tôi nhận thấy câu trả lời của AI cần được đánh giá và kiểm chứng trước khi sử dụng.

**Một là, AI có thể đưa ra Business Impact mang tính suy luận nhưng diễn đạt như kết quả đã được xác thực.**

Ví dụ, các nhận định như giảm thời gian xử lý, tăng năng suất hoặc giảm chi phí có thể hợp lý về mặt kỳ vọng, nhưng không thể mặc định đó là kết quả thực tế của doanh nghiệp nếu chưa có dữ liệu vận hành chứng minh.

**Hai là, các gợi ý Business Problem có thể còn chung chung.**

Khi câu hỏi chưa giới hạn rõ phạm vi doanh nghiệp, đối tượng và hoạt động nghiệp vụ, AI có thể đưa ra những vấn đề phổ biến nhưng chưa chắc phản ánh đúng tình hình thực tế của công ty. Vì vậy, tôi không sử dụng các gợi ý đó như những sự thật đã được xác nhận.

**Ba là, AI có thể khái quát hóa tài liệu nghiên cứu vượt quá phạm vi ban đầu.**

Trong quá trình phân tích bài toán y tế, tôi nhận thấy cần thận trọng khi sử dụng nghiên cứu về AI trong sàng lọc ung thư vú để lập luận cho toàn bộ bài toán phân tích ảnh X-quang và MRI. Hiệu quả trên một tác vụ cụ thể không đồng nghĩa mô hình có hiệu quả tương tự trên các phương thức hình ảnh và bệnh lý khác.

**Bốn là, AI có thể đề xuất hoặc phân loại công nghệ chưa sát với bản chất bài toán.**

Tôi nhận thấy cần phân biệt mô hình Medical Imaging AI/Computer Vision chuyên phân tích hình ảnh y tế với LLM dùng để xử lý ngôn ngữ. Không nên mặc định LLM có thể trực tiếp thay thế mô hình chuyên biệt trong việc phát hiện và định vị tổn thương trên ảnh y khoa.

## 4. Tôi đã điều chỉnh Prompt và thiết lập ranh giới như thế nào?

Để cải thiện chất lượng kết quả, tôi điều chỉnh cách tương tác với AI theo các hướng sau:

- **Thu hẹp phạm vi câu hỏi:** Nêu rõ công ty thành viên, lĩnh vực hoạt động và đối tượng chịu ảnh hưởng để tránh nhận được các gợi ý quá rộng.
- **Yêu cầu phân tích theo cấu trúc:** Đề nghị AI phân tích riêng Actor, Current Workflow, Bottleneck và Business Impact thay vì chỉ đưa ra danh sách ý tưởng.
- **Phân biệt dữ kiện và giả định:** Yêu cầu làm rõ thông tin nào có nguồn tham khảo và thông tin nào chỉ là giả thuyết cần xác minh.
- **Kiểm tra phạm vi tài liệu tham khảo:** Không sử dụng một nghiên cứu trên một loại hình ảnh hoặc bệnh lý để khẳng định hiệu quả cho tất cả các tác vụ chẩn đoán hình ảnh.
- **Giới hạn quyền quyết định của AI:** Tôi tự lựa chọn Business Problem cuối cùng và sử dụng AI như công cụ hỗ trợ phân tích, không giao cho AI quyết định thay mình.

Đối với bài toán y tế, tôi cũng xác định rõ ranh giới vận hành: AI chỉ đóng vai trò hỗ trợ bác sĩ phát hiện và định vị vùng nghi ngờ; bác sĩ phải kiểm tra, xác nhận và ký duyệt báo cáo cuối cùng.

## 5. Bài học rút ra

Qua quá trình sử dụng ChatGPT và Gemini, tôi nhận thấy AI có giá trị trong việc mở rộng góc nhìn, tìm kiếm các hướng tiếp cận và hệ thống hóa thông tin. Tuy nhiên, chất lượng đầu ra phụ thuộc đáng kể vào cách đặt câu hỏi, phạm vi thông tin cung cấp và khả năng kiểm chứng của người sử dụng.

Một bài học quan trọng đối với tôi là cần phân biệt giữa việc sử dụng AI để tìm kiếm ý tưởng và việc tự mình xác định vấn đề cần giải quyết. AI có thể đưa ra nhiều gợi ý, nhưng không phải gợi ý nào cũng phù hợp với bối cảnh doanh nghiệp hoặc định hướng cá nhân.

Tôi cũng nhận ra rằng không nên bắt đầu từ câu hỏi "Có thể dùng AI nào?" mà cần bắt đầu từ "Vấn đề nghiệp vụ nào cần được giải quyết, ai đang chịu ảnh hưởng và tác động kinh doanh là gì?".

**Kết luận:** Tôi xem ChatGPT và Gemini là những trợ lý đồng hành trong quá trình tìm kiếm và phân tích, không phải nguồn thông tin tuyệt đối hay công cụ quyết định thay mình. Tôi chịu trách nhiệm lựa chọn Business Problem, xác minh thông tin và đánh giá tính khả thi của giải pháp cuối cùng.