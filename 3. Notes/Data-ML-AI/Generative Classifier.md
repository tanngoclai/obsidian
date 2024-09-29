---
Created at: 2024-08-01
Source:
  - "[[Deep_learning_foundation.pdf#page=169|Deep_learning_foundation - 5.3]]"
---
**Xác suất hậu nghiệm (áp dụng [[Xác suất Bayes]]):**
- Hai lớp (Two classes): 
  $$
  p(C_1|x) = \frac{p(x|C_1)p(C_1)}{p(x|C_1)p(C_1) + p(x|C_2)p(C_2)} = \frac{1}{1 + \exp(-a)} = \sigma(a)
  $$
	  với $a = \ln \left( \frac{p(x|C_1)p(C_1)}{p(x|C_2)p(C_2)} \right)$.

-  Nhiều lớp (Multiple classes):
$$
  p(C_k|x) = \frac{p(x|C_k)p(C_k)}{\sum_j p(x|C_j)p(C_j)} = \frac{\exp(a_k)}{\sum_j \exp(a_j)}
  $$
		  với $a_k = \ln (p(x|C_k)p(C_k))$.


# 1 Continuous Inputs
Phần này mô tả cách xử lý các đầu vào liên tục trong các bộ phân loại sinh. Đặc biệt, khi các đầu vào được phân phối Gaussian, xác suất hậu nghiệm của lớp có thể được biểu diễn dưới dạng mô hình tuyến tính tổng quát với các hàm kích hoạt sigmoid logistic hoặc softmax. Điều này cho phép tính toán xác suất lớp một cách hiệu quả.

**Các giả định về Mật độ Điều kiện Lớp và Gaussian:**
- Mật độ điều kiện cho lớp $C_k$ được mô hình hóa như một phân phối Gaussian với ma trận hiệp phương sai chung $\Sigma$ cho tất cả các lớp. Hàm mật độ xác suất được biểu diễn bởi:
  $$
  p(x|C_k) = \frac{1}{(2\pi)^{D/2} |\Sigma|^{1/2}} \exp \left( -\frac{1}{2} (x - \mu_k)^T \Sigma^{-1} (x - \mu_k) \right)
  $$
- Đối với hai lớp, xác suất hậu nghiệm $p(C_1|x)$ có thể được biểu thị bằng hàm sigmoid logistic: $$
  p(C_1|x) = \sigma(w^T x + w_0)
  $$
  với $w$ và $w_0$ được định nghĩa là:  $$
  w = \Sigma^{-1} (\mu_1 - \mu_2)
  $$$$
  w_0 = -\frac{1}{2} \mu_1^T \Sigma^{-1} \mu_1 + \frac{1}{2} \mu_2^T \Sigma^{-1} \mu_2 + \ln \frac{p(C_1)}{p(C_2)}
  $$
- Đối với trường hợp tổng quát với $K$ lớp, xác suất hậu nghiệm được xác định bằng hàm softmax: $$
  a_k(x) = w_k^T x + w_{k0}
  $$
  với $w_k$ và $w_{k0}$ được biểu diễn là: $$
  w_k = \Sigma^{-1} \mu_k
  $$$$
  w_{k0} = -\frac{1}{2} \mu_k^T \Sigma^{-1} \mu_k + \ln p(C_k)
  $$
# 2 Maximum Likelihood Solution
Phần này thảo luận về cách tìm giải pháp hợp lý cực đại cho các tham số của các phân phối điều kiện lớp. Bắt đầu với các lớp có phân phối Gaussian và ma trận hiệp phương sai chung, phần này mô tả cách tính toán xác suất hợp lý của các tham số và xác suất lớp từ một tập dữ liệu đã quan sát. Tối đa hóa log-likelihood để tìm các tham số tối ưu là một phương pháp chính được sử dụng.

# 3 Discrete Features
Phần này xem xét các giá trị đầu vào rời rạc, bắt đầu với các giá trị nhị phân và mở rộng đến các tính năng rời rạc chung. Sử dụng giả định Naive Bayes, các giá trị tính năng được xử lý như độc lập và có điều kiện trên lớp. Điều này dẫn đến các phân phối điều kiện lớp dưới dạng tích của các tham số độc lập cho mỗi lớp.

# 4 Exponential Family
Phần này trình bày cách xác suất hậu nghiệm của lớp có thể được biểu diễn bằng các mô hình tuyến tính tổng quát khi các mật độ điều kiện lớp thuộc về một tập hợp con của họ phân phối exponential family. Điều này bao gồm cả trường hợp có hai lớp và nhiều lớp, với các xác suất hậu nghiệm được tính toán bằng cách sử dụng hàm sigmoid logistic hoặc hàm softmax.