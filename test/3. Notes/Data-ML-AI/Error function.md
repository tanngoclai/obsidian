---
Created at: 2024-08-07
Source:
  - "[[Deep_learning_foundation.pdf#page=212|Deep_learning_foundation, p.194]]"
---

# 1. [[Linear regression - Hồi quy tuyến tính|Regression]]
Trong các mô hình hồi quy, mục tiêu là dự đoán một giá trị thực từ các biến đầu vào. Hàm lỗi phổ biến nhất được sử dụng trong bối cảnh này là hàm bình phương lỗi (mean squared error - MSE), được định nghĩa như sau:
$$ E(\mathbf{w}) = \frac{1}{2N} \sum_{n=1}^{N} (y_n - \mathbf{w}^T \mathbf{x}_n)^2 $$

   Trong đó $y_n$ là giá trị mục tiêu, $\mathbf{x}_n$ là vector đầu vào, và $\mathbf{w}$ là vector trọng số của mô hình.

# 2. Binary classification
Sử dụng phân phối [[Phân phối mũ (The Exponential Family)#2.1 Phân phối Bernoulli|Bernoulli]], đầu ra của mô hình cho một đầu vào cụ thể có thể được xem như một biến ngẫu nhiên với phân phối Bernoulli, được xác định bởi xác suất $y(x, w)$. 
Hàm mất mát cho mô hình này thường là hàm *cross-entropy*, dùng để đo lường sự khác biệt giữa xác suất dự đoán và giá trị thực của lớp.
$$
   E(w) = -\sum_{n=1}^{N} \{ t_n \ln y(x_n, w) + (1 - t_n) \ln (1 - y(x_n, w)) \}
$$
# 3. Multiclass classification
Hàm xác suất:
$$
  y_{k}=p(C_k|x) = \frac{p(x|C_k)p(C_k)}{\sum_j p(x|C_j)p(C_j)} = \frac{\exp(a_k)}{\sum_j \exp(a_j)}
  $$
Error function:
   $$
   E = -\sum_{n=1}^{N} \sum_{k=1}^{K} t_{nk} \ln y_{nk}
   $$

   Trong đó $N$ là số mẫu trong dữ liệu, và $t_{nk}$ là phần tử của vector [[Single layer networks - Classification#1.3. 1-of-K coding|1-of-K coding]] cho mẫu thứ $n$ và lớp $k$.
