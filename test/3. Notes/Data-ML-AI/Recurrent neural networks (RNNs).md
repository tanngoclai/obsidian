
# 1. Giới thiệu về RNN
   - RNN được phát triển để giải quyết vấn đề của [[Autoregressive models - NLP]] bằng cách sử dụng các mô hình tham số hóa dựa trên mạng nơ-ron. 

   - RNN có khả năng xử lý các chuỗi có độ dài thay đổi trong các bộ huấn luyện và kiểm tra, không giống như mạng nơ-ron truyền thẳng tiêu chuẩn với số đầu vào và đầu ra cố định.
   
# 2. Hoạt động của RNN
   - RNN hoạt động bằng cách lấy đầu vào hiện tại $x_n$ và trạng thái ẩn $z_{n-1}$ hiện tại, rồi tạo ra đầu ra $y_n$ cũng như trạng thái tiếp theo $z_n$.

   - Các bản sao của mạng này có thể được liên kết với nhau, trong đó các giá trị trọng số được chia sẻ giữa các bản sao, tạo ra kiến trúc được gọi là mạng nơ-ron hồi quy.
