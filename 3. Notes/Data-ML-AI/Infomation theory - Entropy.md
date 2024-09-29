---
Created at: 2024-07-14
Source:
  - "[[Deep_learning_foundation.pdf#page=66|Deelp_learning_foundation - 2.5]]"
---
Chương 2.5 của cuốn sách "Deep Learning: Foundations and Concepts" của Christopher M. Bishop và Hugh Bishop tập trung vào Lý thuyết Thông tin. Dưới đây là tóm tắt của chương này:
# 1 Entropy
- **Entropy**: Đây là một khái niệm quan trọng trong lý thuyết thông tin. Entropy đo lường lượng thông tin trung bình mà ta có thể nhận được khi quan sát giá trị của một biến ngẫu nhiên.
- **Định nghĩa**: Được xác định bởi công thức $$H[x] = -\sum_x p(x) \log_2 p(x)$$trong đó $p(x)$ là xác suất của biến ngẫu nhiên $x$.
- **Ví dụ**: Đối với một biến có tám trạng thái có xác suất bằng nhau, entropy là 3 bit.
# 2 Relative Entropy and Mutual Information
- **Relative Entropy (Kullback–Leibler divergence)**: Là thước đo sự khác biệt giữa hai phân phối xác suất $p(x)$ và $q(x)$. Được xác định bởi công thức $$KL(p \| q) = \sum_x p(x) \log \frac{p(x)}{q(x)}$$
- **Mutual Information**: Đo lường lượng thông tin mà một biến ngẫu nhiên có về một biến ngẫu nhiên khác. Được xác định bởi công thức $$I(x; y) = H[x] - H[x | y] = H[y] - H[y | x]$$
# 3 Data Compression and Coding
- **Noiseless Coding Theorem**: Entropy là giới hạn dưới của số bit cần thiết để truyền trạng thái của một biến ngẫu nhiên.
- **Ví dụ**: Đối với một biến có phân phối không đồng đều, ta có thể sử dụng mã ngắn hơn cho các sự kiện có xác suất cao hơn để giảm chiều dài mã trung bình.

# 4 Practical Applications
- **Data Compression**: Sử dụng lý thuyết thông tin để tối ưu hóa quá trình nén dữ liệu.
- **Density Estimation**: Ước lượng phân phối xác suất của dữ liệu thông qua mô hình hóa.

# 5 Conditional Entropy
- **Conditional Entropy**: Đo lường lượng thông tin cần thiết để xác định giá trị của một biến khi đã biết giá trị của biến khác. Được xác định bởi công thức $$H[y|x] = -\int \int p(y,x) \log p(y|x) dy dx$$