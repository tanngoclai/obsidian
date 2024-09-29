Large Language Models (LLMs), các mô hình ngôn ngữ lớn dựa trên mạng nơ-ron Transformer với số lượng tham số khổng lồ, lên tới hàng nghìn tỷ.

# 1. Kích thước mô hình
   - Các LLMs được gọi là "lớn" vì số lượng tham số (trọng số và bias) rất lớn, có thể lên tới khoảng một nghìn tỷ tham số.

   - Các mô hình này tốn kém để huấn luyện, nhưng đem lại khả năng vượt trội trong xử lý ngôn ngữ tự nhiên (NLP).

# 2. Khả năng và sự phát triển
   - Sự phát triển của LLMs được thúc đẩy bởi khả năng xử lý song song của phần cứng, đặc biệt là các GPU và các bộ xử lý tương tự được kết hợp chặt chẽ trong các cụm lớn với kết nối nhanh và bộ nhớ tích hợp.

   - Kiến trúc Transformer đóng vai trò quan trọng trong việc phát triển các mô hình này bởi vì nó sử dụng hiệu quả phần cứng này.

# 3. Phương pháp huấn luyện
   - **Huấn luyện tự giám sát**: Thay vì dựa vào học có giám sát, đòi hỏi dữ liệu được gán nhãn, LLMs sử dụng học tự giám sát trên các bộ dữ liệu văn bản rất lớn, và có thể cả các chuỗi token khác như mã máy tính. Điều này cho phép mô hình tận dụng lượng dữ liệu huấn luyện lớn hơn rất nhiều.

   - Mô hình học phân phối xác suất có điều kiện bằng cách sử dụng các chuỗi token mà mỗi token đóng vai trò như một ví dụ mục tiêu có gán nhãn, với chuỗi trước đó làm đầu vào.

# 4. Sự cải tiến trong hiệu suất
   - Thường thì việc tăng kích thước của tập dữ liệu huấn luyện, cùng với sự tăng tương ứng trong số lượng tham số mô hình, dẫn đến cải thiện hiệu suất vượt xa so với cải tiến kiến trúc hoặc các cách khác để tích hợp nhiều kiến thức miền hơn.

   - Ví dụ, sự tăng cường đáng kể về hiệu suất của các thế hệ mô hình GPT chủ yếu đến từ sự tăng kích thước của mô hình.

# 5. Học chuyển giao và mô hình nền tảng
   - LLMs cũng thúc đẩy sự chuyển đổi trong phương pháp học máy, nơi một mô hình lớn đầu tiên được huấn luyện trước bằng dữ liệu không gán nhãn và sau đó được điều chỉnh lại (fine-tuned) bằng dữ liệu gán nhãn cho các nhiệm vụ cụ thể. Điều này hiệu quả như một hình thức học chuyển giao, và cùng một mô hình đã được huấn luyện trước có thể được sử dụng cho nhiều ứng dụng "hạ nguồn" khác nhau.

   - Một mô hình với khả năng rộng rãi có thể được điều chỉnh lại cho các tác vụ cụ thể được gọi là mô hình nền tảng.
