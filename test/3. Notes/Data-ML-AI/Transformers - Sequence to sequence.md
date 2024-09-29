
# 1. Kiến trúc tổng thể
   - Mô hình Sequence-to-sequence Transformer sử dụng [[Transformers - Encoder transformers]] để chuyển đổi chuỗi đầu vào thành một biểu diễn trung gian (vector ẩn) và sau đó sử dụng [[Transformers - Decoder transformers]] để tạo ra chuỗi đầu ra từ biểu diễn này.

   - Một ví dụ điển hình là nhiệm vụ dịch máy, nơi mô hình chuyển đổi một câu tiếng Anh sang câu tiếng Hà Lan. Bộ mã hóa xử lý câu tiếng Anh để tạo ra một biểu diễn trung gian, sau đó bộ giải mã sử dụng biểu diễn này để tạo ra câu tiếng Hà Lan.

# 2. Cross-Attention
   - Cross-attention, khác với [[Transformers - Attention#3. Self-attention|self-attention]], nơi mà các truy vấn (queries), khóa (keys), và giá trị (values) đều đến từ cùng một chuỗi, cross-attention sử dụng các truy vấn từ chuỗi đầu ra đang được tạo, trong khi các khóa và giá trị đến từ biểu diễn trung gian của chuỗi đầu vào.

   - Điều này cho phép mô hình học cách liên kết các phần của chuỗi đầu vào với các phần tương ứng trong chuỗi đầu ra.

# 3. Quy trình huấn luyện
   - Mô hình được huấn luyện sử dụng các cặp câu đầu vào-đầu ra. Bộ mã hóa và bộ giải mã học cách chuyển đổi chuỗi đầu vào thành đầu ra mong muốn thông qua quá trình tối ưu hóa các trọng số bằng cách sử dụng gradient descent.

![[Pasted image 20240901083817.png]]