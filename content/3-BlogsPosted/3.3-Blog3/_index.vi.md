---

title: "Blog 3"
date: 2026-08-04
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
----------------------

#  Upload tài liệu thành công nhưng AI vẫn trả lời sai – Bài học về RAG và Knowledge Base khi xây dựng AI Learning Assistant

Xin chào mọi người! 

Trong quá trình phát triển dự án **AI Learning Assistant** mình muốn tạo ra một trợ lý AI có thể trả lời câu hỏi dựa trên tài liệu học tập của người dùng thay vì chỉ dựa vào kiến thức chung của mô hình AI.

Mình đã triển khai thành công chức năng tải tài liệu lên hệ thống và quá trình xử lý tài liệu cũng diễn ra bình thường. Tuy nhiên, khi bắt đầu đặt câu hỏi, AI lại đưa ra những câu trả lời khá bất ngờ.

Có những câu hỏi đã được trình bày rất rõ trong tài liệu nhưng AI vẫn trả lời sai, hoặc thậm chí trả lời dựa trên kiến thức chung thay vì nội dung mà mình đã cung cấp.

Ban đầu, mình nghĩ rằng mô hình AI hoạt động chưa tốt. Nhưng sau khi tìm hiểu sâu hơn, mình nhận ra nguyên nhân thực sự nằm ở **Knowledge Base** và cơ chế **Retrieval-Augmented Generation (RAG)**.

---

## Kiến trúc của hệ thống

Khi người dùng tải tài liệu lên, hệ thống không chuyển trực tiếp toàn bộ tài liệu đến mô hình AI. Thay vào đó, tài liệu phải trải qua nhiều bước xử lý trước khi có thể được sử dụng để trả lời câu hỏi.

Quy trình tổng quát :

### Hình 1. Kiến trúc RAG của AI Learning Assistant

![Kiến trúc RAG của AI Learning Assistant](/images/h1bl3.png)

---

## Vấn đề mình gặp phải

Sau khi tải tài liệu lên, mình thử đặt câu hỏi:

> **Amazon EC2 là gì?**

Mặc dù nội dung này đã có trong tài liệu nhưng AI lại trả lời rất chung chung, giống như đang sử dụng kiến thức được huấn luyện trước đó thay vì đọc tài liệu của mình.

Thậm chí, với một số câu hỏi khác, AI còn trả lời:

> *“Tôi không tìm thấy thông tin trong tài liệu.”*

Trong khi nội dung đó thực sự tồn tại trong tài liệu đã tải lên.

### Hình 2. AI trả lời không đúng với nội dung trong tài liệu

![AI trả lời sai dù tài liệu đã được tải lên](/images/h2bl3bl3.png)

---

## Nguyên nhân

Sau khi kiểm tra toàn bộ quy trình, mình phát hiện rằng **tải tài liệu lên thành công không đồng nghĩa với việc AI đã có thể sử dụng tài liệu đó để trả lời câu hỏi**.

Trong một hệ thống RAG, sau khi người dùng tải tài liệu lên, hệ thống còn phải thực hiện nhiều bước xử lý:

* Trích xuất văn bản từ tài liệu.
* Chia nội dung thành các đoạn nhỏ, còn được gọi là **chunks**.
* Chuyển từng đoạn thành vector bằng mô hình **Embedding**.
* Lưu các vector vào cơ sở dữ liệu vector.
* Chuyển câu hỏi của người dùng thành vector.
* Tìm kiếm những đoạn tài liệu có nội dung liên quan nhất.
* Gửi câu hỏi và các đoạn tài liệu liên quan đến mô hình AI.

Nếu một trong các bước trên chưa hoàn thành hoặc được cấu hình chưa phù hợp, AI sẽ không tìm được đúng ngữ cảnh và có thể trả lời dựa trên kiến thức chung.

Ngoài ra, mình nhận thấy prompt hệ thống chưa đủ chặt chẽ. AI không được yêu cầu chỉ sử dụng nội dung trong tài liệu nên đôi khi mô hình tự suy luận và tạo ra thông tin không xuất hiện trong tài liệu. Hiện tượng này thường được gọi là **hallucination**.

---

## Giải pháp

Để khắc phục vấn đề, mình thực hiện các bước sau:

* Kiểm tra trạng thái xử lý của Knowledge Base.
* Chỉ đặt câu hỏi sau khi tài liệu đã được lập chỉ mục hoàn tất.
* Xác nhận tài liệu đã được chia thành các chunks phù hợp.
* Kiểm tra các chunks đã được chuyển thành vector và lưu thành công trong vector database.
* Kiểm tra lại mô hình Embedding đang được sử dụng.
* Điều chỉnh prompt để yêu cầu AI chỉ trả lời dựa trên tài liệu đã cung cấp.
* Yêu cầu AI thông báo rõ nếu không tìm thấy thông tin thay vì tự tạo câu trả lời.
* Kiểm tra cơ chế Retrieval để bảo đảm hệ thống truy xuất đúng các đoạn tài liệu liên quan.
* Điều chỉnh số lượng chunks được truy xuất và ngưỡng tương đồng nếu cần thiết.

Prompt hệ thống có thể được điều chỉnh theo hướng:

> **Chỉ trả lời câu hỏi dựa trên nội dung được cung cấp trong Knowledge Base. Nếu không tìm thấy thông tin phù hợp, hãy thông báo rằng tài liệu hiện tại chưa cung cấp nội dung cần thiết. Không tự tạo hoặc suy đoán câu trả lời.**

---

## Quy trình RAG sau khi tối ưu

Khi người dùng đặt câu hỏi, hệ thống sẽ chuyển câu hỏi thành vector và tìm kiếm những đoạn tài liệu có độ tương đồng cao nhất.

Các đoạn liên quan sau đó được gửi cùng câu hỏi đến mô hình AI để tạo câu trả lời.


### Hình 3. Quy trình Retrieval-Augmented Generation sau khi tối ưu

![Quy trình Retrieval-Augmented Generation](/images/h3bl3.png)

Sau khi tối ưu quy trình trên, AI đã trả lời chính xác hơn, có thể dựa vào nội dung trong tài liệu và giảm đáng kể các câu trả lời không liên quan.

---

## Bài học mình rút ra

Qua sự cố này, mình nhận ra rằng **chất lượng của một ứng dụng AI không chỉ phụ thuộc vào mô hình ngôn ngữ lớn (LLM)**.

Trong các hệ thống sử dụng RAG, chất lượng câu trả lời còn phụ thuộc vào:

* Chất lượng tài liệu đầu vào.
* Khả năng trích xuất nội dung từ tài liệu.
* Quá trình chia tài liệu thành các đoạn nhỏ.
* Kích thước và mức độ chồng lặp giữa các chunks.
* Mô hình tạo Embedding.
* Cơ sở dữ liệu vector.
* Cơ chế truy xuất dữ liệu.
* Prompt hướng dẫn mô hình AI.

Một mô hình AI mạnh vẫn không thể trả lời chính xác nếu không được cung cấp đúng ngữ cảnh.

---

## Kết luận

RAG là một kỹ thuật hiệu quả để xây dựng các ứng dụng AI dựa trên dữ liệu riêng của doanh nghiệp hoặc người dùng. Tuy nhiên, để hệ thống hoạt động chính xác, cần bảo đảm toàn bộ quy trình từ xử lý tài liệu, tạo Embedding đến truy xuất dữ liệu đều được cấu hình đúng.

Qua trải nghiệm này, mình hiểu rằng việc tối ưu **Knowledge Base** và **Retrieval** quan trọng không kém việc lựa chọn mô hình AI.

Hy vọng bài viết sẽ giúp những bạn đang xây dựng chatbot AI hoặc ứng dụng RAG trên AWS tránh được lỗi mà mình đã gặp phải.

---

## Tài liệu tham khảo

 **Tài liệu AWS mình tham khảo:**

1. **Amazon Bedrock Knowledge Bases**
   https://docs.aws.amazon.com/bedrock/latest/userguide/knowledge-base.html

2. **What is Retrieval-Augmented Generation (RAG)?**
   https://aws.amazon.com/what-is/retrieval-augmented-generation/

3. **Amazon Bedrock User Guide**
   https://docs.aws.amazon.com/bedrock/latest/userguide/what-is-bedrock.html

4. **Build a Knowledge Base by Connecting to a Data Source**
   https://docs.aws.amazon.com/bedrock/latest/userguide/knowledge-base-create.html

---

## Link bài viết

https://www.facebook.com/groups/awsstudygroupfcj/?multi_permalinks=2233469244084702&notif_id=1785773605274872&notif_t=feedback_reaction_generic&ref=notif