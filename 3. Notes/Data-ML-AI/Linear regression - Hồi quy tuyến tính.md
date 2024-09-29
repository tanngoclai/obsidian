---
Created at: 2024-07-03
Source:
  - "[[ML cơ bản.pdf#page=95|book_ML_color, Chương 7]]"
  - "[[Deep_learning_foundation.pdf#page=131|Deep_learning_foundation - 4.1]]"
tags: 
---
# 1 Giới thiệu

- **Hồi quy tuyến tính (Linear Regression)** là một phương pháp cơ bản và phổ biến trong thống kê và học máy, được sử dụng để mô hình hóa mối quan hệ giữa một biến phụ thuộc (output) và một hoặc nhiều biến độc lập (input).
- Mục tiêu của hồi quy tuyến tính là tìm một đường thẳng hoặc một siêu phẳng trong không gian nhiều chiều sao cho nó mô tả tốt nhất mối quan hệ giữa các biến này.

# 2 Xây dựng và tối ưu hàm mất mát

- **Mô hình hồi quy tuyến tính**: Mô hình hồi quy tuyến tính có dạng:
    - $y = X W + \epsilon = w_0 + w_1 x_1 + ... + w_D x_D$ 
    - Trong đó, $y$ là vector kết quả, $X$ là **vector** hoặc **ma trận** đặc trưng, $W$ là vector hệ số, và $\epsilon$ là nhiễu.
- **Hàm mất mát**: Hàm mất mát phổ biến cho hồi quy tuyến tính là tổng bình phương sai số (Sum of Squared Errors, SSE):
    - $L(\beta) = \frac{1}{2}\sum_{i=1}^{n} (y_i - X_i \beta)^2$
    - Hàm mất mát này đo lường độ sai lệch giữa giá trị dự đoán và giá trị thực tế.
- **Tối ưu hàm mất mát**: Mục tiêu là tìm các giá trị của $\beta$ sao cho hàm mất mát $L(\beta)$ đạt giá trị nhỏ nhất. Điều này có thể được thực hiện bằng các phương pháp như:
    - Giải phương trình tối ưu (Normal Equation)
    - Phương pháp gradient descent

# 3 Sequential Learning (Học Tuần Tự)

**Mô tả:**
Học tuần tự là một phương pháp trong đó mô hình cập nhật các tham số của mình từng bước một khi từng mẫu dữ liệu mới được quan sát. Điều này đặc biệt hữu ích trong các tình huống mà dữ liệu đến theo thời gian thực hoặc khi toàn bộ tập dữ liệu không có sẵn cùng một lúc.

**Công thức:**
Quá trình cập nhật tham số trong học tuần tự có thể được thực hiện thông qua thuật toán Gradient Descent hoặc các biến thể của nó như Stochastic Gradient Descent (SGD). Cụ thể, với mỗi mẫu dữ liệu mới $(x_n, t_n)$, tham số $w$ được cập nhật như sau:
$$
w^{(t+1)} = w^{(t)} - \eta \nabla E(w^{(t)})
$$
Trong đó:
- $\eta$ là tốc độ học (learning rate).
- $\nabla E(w^{(t)})$ là gradient của hàm lỗi tại thời điểm $t$.

**Ưu điểm:**
- Khả năng xử lý dữ liệu lớn bằng cách chỉ cần lưu trữ một mẫu hoặc một lô mẫu nhỏ tại một thời điểm.
- Linh hoạt và có khả năng thích ứng với các thay đổi trong dữ liệu theo thời gian.

**Nhược điểm:**
- Có thể yêu cầu nhiều lần duyệt qua dữ liệu để hội tụ.
- Lựa chọn tốc độ học phù hợp là một thách thức để đảm bảo hội tụ nhanh và ổn định.

# 4 Regularized Least Squares (Ridge Regression)

**Mô tả:**
Phương pháp bình phương cực tiểu có điều chuẩn (còn gọi là Ridge Regression) được sử dụng để tránh hiện tượng quá khớp (overfitting) bằng cách thêm một hệ số phạt vào hàm lỗi. Nó giúp giới hạn kích thước của các tham số $w$, giúp mô hình trở nên mượt mà hơn và có khả năng tổng quát tốt hơn.

**Công thức:**
Hàm lỗi trong Ridge Regression bao gồm hai phần: lỗi bình phương và hệ số điều chuẩn:
$$
E(w) = \frac{1}{2} \sum_{n=1}^N (t_n - y(x_n, w))^2 + \frac{\lambda}{2} \|w\|^2
$$
Trong đó:
- $\lambda$ là hệ số điều chuẩn, điều chỉnh mức độ phạt áp dụng cho các tham số $w$.
- $\|w\|^2$ là bình phương của norm L2 của vector trọng số $w$.

**Ưu điểm:**
- Giúp giảm thiểu hiện tượng quá khớp bằng cách giới hạn độ lớn của các trọng số $w$.
- Cải thiện khả năng tổng quát hóa của mô hình.

**Nhược điểm:**
- Lựa chọn giá trị $\lambda$ phù hợp có thể khó khăn và thường yêu cầu kỹ thuật như Cross-Validation để tìm giá trị tối ưu.
- Thuật ngữ điều chuẩn có thể làm giảm độ chính xác nếu không được điều chỉnh đúng cách.

**Phương pháp giải:**
Để tìm $w$ tối ưu, ta có thể giải hệ phương trình tuyến tính mở rộng:
$$
w = (X^T X + \lambda I)^{-1} X^T t
$$
Trong đó:
- $X$ là ma trận dữ liệu với các hàng là các vector đặc trưng $x_n$.
- $t$ là vector các giá trị mục tiêu $t_n$.
- $I$ là ma trận đơn vị.

Như vậy, Regularized Least Squares là một phương pháp mạnh mẽ để cải thiện độ tin cậy và khả năng tổng quát hóa của mô hình hồi quy tuyến tính bằng cách kiểm soát kích thước của các tham số mô hình.
## 4 Thảo luận

- **Ưu điểm của hồi quy tuyến tính**: Đơn giản, dễ hiểu, dễ triển khai, và có thể mở rộng để áp dụng vào các bài toán có nhiều biến đầu vào.
- **Nhược điểm**: Không phù hợp với các dữ liệu có quan hệ phi tuyến tính, nhạy cảm với các outlier và giả định rằng các biến đầu vào phải không tương quan.