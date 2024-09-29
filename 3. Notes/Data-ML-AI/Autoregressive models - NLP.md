
# 1. Giới hạn của mô hình [[Bag of words - NLP|Bag of words]]
   - Mô hình Bag-of-Words hoàn toàn bỏ qua thứ tự từ, điều này dẫn đến việc mất thông tin quan trọng về ngữ cảnh và ý nghĩa của câu. \
   
   - Để khắc phục hạn chế này, các mô hình tự hồi quy được sử dụng.

# 2. Tiếp cận tự hồi quy
   - Tính toán xác suất của mỗi từ dựa trên tất cả các từ trước đó trong câu. Biểu thức toán học của nó là:
     $$
     p(x_1, x_2, ..., x_N) = p(x_1) \cdot p(x_2|x_1) \cdot p(x_3|x_1, x_2) \cdot ... \cdot p(x_N|x_1, ..., x_{N-1})
     $$
   
   - Mô hình này có thể được biểu diễn dưới dạng mô hình đồ thị xác suất, trong đó mỗi nút trong chuỗi có một liên kết từ mọi nút trước đó.

# 3. Thách thức của mô hình tự hồi quy
   - Kích thước của các bảng biểu diễn xác suất điều kiện trong mô hình này tăng theo cấp số nhân với độ dài của chuỗi, làm cho việc lưu trữ và tính toán trở nên rất tốn kém. 
   
# 4. Mô hình n-gram
   - Để giải quyết vấn đề này, người ta giả định rằng mỗi phân phối điều kiện chỉ phụ thuộc vào một số từ gần nhất thay vì tất cả các từ trước đó.

   - Để đơn giản hóa mô hình, chúng ta giả định rằng mỗi phân phối điều kiện chỉ phụ thuộc vào $L$ từ gần nhất. Ví dụ, nếu $L = 2$, mô hình này được gọi là mô hình tri-gram. Với $L = 1$, mô hình được gọi là bi-gram.