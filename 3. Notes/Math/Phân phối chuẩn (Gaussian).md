---
Created at: 2024-07-11
Source: 
tags:
---

# **1. Phân phối Gaussian**
Phân phối Gaussian, còn gọi là phân phối chuẩn, có hàm mật độ xác suất (PDF) được biểu diễn như sau:
$$
f(x|\mu, \sigma^2) = \frac{1}{\sqrt{2\pi\sigma^2}} exp\left\{ -\frac{(x - \mu)^2}{2\sigma^2} \right\}
$$
Trong đó:
- $x$ là biến ngẫu nhiên.
- $\mu$ là giá trị trung bình của phân phối.
- $\sigma^2$ là phương sai của phân phối.

# **2. Hàm [[Likelihood]]**
Giả sử bạn có một tập hợp dữ liệu $X = \{x_1, x_2, ..., x_n\}$ bao gồm $n$ quan sát độc lập từ một phân phối Gaussian với các tham số chưa biết $\mu$ và $\sigma^2$. Hàm Likelihood cho dữ liệu này được định nghĩa như sau:

$$
\mathcal{L}(\mu, \sigma^2 | X) = \prod_{i=1}^n f(x_i | \mu, \sigma^2)
$$

Ở đây, $f(x_i | \mu, \sigma^2)$ là hàm mật độ xác suất của phân phối Gaussian tại mỗi điểm dữ liệu $x_i$.

# **3. Log-Likelihood**
Để tính toán dễ dàng hơn, người ta thường sử dụng log-likelihood, là logarit tự nhiên của hàm Likelihood. Việc sử dụng log-likelihood giúp chuyển tích thành tổng và tránh các vấn đề số học với các giá trị nhỏ. Log-likelihood của phân phối Gaussian được biểu diễn như sau:

$$
\log \mathcal{L}(\mu, \sigma^2 | X) = \sum_{i=1}^n \log f(x_i | \mu, \sigma^2)
$$

Thay thế hàm mật độ xác suất của phân phối Gaussian vào phương trình log-likelihood, ta có:

$$
\log \mathcal{L}(\mu, \sigma^2 | X) = \sum_{i=1}^n \left[ -\frac{1}{2} \log (2\pi\sigma^2) - \frac{(x_i - \mu)^2}{2\sigma^2} \right]
$$

Đơn giản hóa hơn:

$$
\log \mathcal{L}(\mu, \sigma^2 | X) = -\frac{n}{2} \log (2\pi\sigma^2) - \frac{1}{2\sigma^2} \sum_{i=1}^n (x_i - \mu)^2
$$
# 4 Phân phối chuẩn nhiều chiều
## 4.1 Định nghĩa
Phân phối Gaussian (hay còn gọi là phân phối chuẩn) được định nghĩa cho một vector $D$ chiều $\mathbf{x}$ có dạng:

$$
N(\mathbf{x}|\boldsymbol{\mu}, \mathbf{\Sigma}) = \frac{1}{(2\pi)^{D/2} |\mathbf{\Sigma}|^{1/2}} \exp \left( -\frac{1}{2} (\mathbf{x} - \boldsymbol{\mu})^T \mathbf{\Sigma}^{-1} (\mathbf{x} - \boldsymbol{\mu}) \right)
$$

- $\boldsymbol{\mu}$ là vector trung bình D chiều.
- $\mathbf{\Sigma}$ là [[Xác suất#3 Tính chất của các biến ngẫu nhiên |ma trận hiệp phương sai]] $D \times D$.
- $|\mathbf{\Sigma}|$ là định thức của $\mathbf{\Sigma}$.
## 4.2 Đặc tính hình học của Gaussian
Phụ thuộc hàm số của Gaussian lên $\mathbf{x}$ thông qua dạng bậc hai:

$$
\Delta^2 = (\mathbf{x} - \boldsymbol{\mu})^T \mathbf{\Sigma}^{-1} (\mathbf{x} - \boldsymbol{\mu})
$$

## 4.3 Một số đặc điểm quan trọng
- **Trung bình và Hiệp phương sai:** Phân phối Gaussian có trung bình $\boldsymbol{\mu}$ và ma trận hiệp phương sai $\mathbf{\Sigma}$.
- **Tính chất chuẩn hóa:** Gaussian phân phối được chuẩn hóa, có nghĩa là tổng xác suất trên toàn bộ không gian bằng 1.
- **Các tính chất ma trận:** Ma trận hiệp phương sai $\mathbf{\Sigma}$ là đối xứng và không âm, và ma trận này có thể được phân rã thành các giá trị riêng.

## 4.4 Phân phối chuẩn nhiều chiều có điều kiện
#### **Phân vùng và tính toán****
Giả sử $\mathbf{x}$ là vector có chiều $D$ với phân phối Gaussian $\mathcal{N}(\mathbf{x}|\boldsymbol{\mu}, \mathbf{\Sigma})$ và ta phân vùng $\mathbf{x}$ thành hai tập con rời nhau $\mathbf{x}_a$ và $\mathbf{x}_b$. Không mất tổng quát, ta có thể chọn $\mathbf{x}_a$ là $M$ thành phần đầu tiên của $\mathbf{x}$ và $\mathbf{x}_b$ gồm $D - M$ thành phần còn lại:
$$
\mathbf{x} = \begin{pmatrix} \mathbf{x}_a \\ \mathbf{x}_b \end{pmatrix}
$$

Với các vector trung bình tương ứng:
$$
\boldsymbol{\mu} = \begin{pmatrix} \boldsymbol{\mu}_a \\ \boldsymbol{\mu}_b \end{pmatrix}
$$

Và ma trận hiệp phương sai:
$$
\mathbf{\Sigma} = \begin{pmatrix} \mathbf{\Sigma}_{aa} & \mathbf{\Sigma}_{ab} \\ \mathbf{\Sigma}_{ba} & \mathbf{\Sigma}_{bb} \end{pmatrix}
$$
#### **Ma trận nghịch đảo**
Trong nhiều tình huống, sẽ thuận tiện hơn khi làm việc với ma trận nghịch đảo của ma trận hiệp phương sai, gọi là ma trận độ chính xác (precision matrix):
$$
\mathbf{\Lambda} \equiv \mathbf{\Sigma}^{-1}
$$
Và phân vùng tương ứng của ma trận độ chính xác:
$$
\mathbf{\Lambda} = \begin{pmatrix} \mathbf{\Lambda}_{aa} & \mathbf{\Lambda}_{ab} \\ \mathbf{\Lambda}_{ba} & \mathbf{\Lambda}_{bb} \end{pmatrix}
$$
#### **Phân phối điều kiện**
Phân phối điều kiện của $\mathbf{x}_a$ khi biết $\mathbf{x}_b$ là:
$$
p(\mathbf{x}_a|\mathbf{x}_b) = \mathcal{N}(\mathbf{x}_a|\boldsymbol{\mu}_{a|b}, \mathbf{\Lambda}_{aa}^{-1})
$$
Với: $$\boldsymbol{\mu}_{a|b} = \boldsymbol{\mu}_a - \mathbf{\Lambda}_{aa}^{-1} \mathbf{\Lambda}_{ab} (\mathbf{x}_b - \boldsymbol{\mu}_b)$$
(Coi như bỏ qua $x_b$)

# 5 Mixtures of Gaussians
## 5.1 Giới thiệu và ví dụ
  Phân phối Gaussian có những thuộc tính toán học quan trọng nhưng gặp hạn chế khi mô hình hóa các tập dữ liệu thực tế phức tạp. Ví dụ, dữ liệu "Old Faithful" bao gồm 272 lần đo lường thời gian phun trào của mạch nước nóng Old Faithful ở Yellowstone. Dữ liệu này có hai cụm rõ rệt mà một phân phối Gaussian đơn không thể nắm bắt được. Tuy nhiên, sự kết hợp của hai phân phối Gaussian sẽ mô tả chính xác hơn cấu trúc của dữ liệu này.

## 5.2. Hỗn hợp Gaussian:
   Hỗn hợp Gaussian được hình thành bằng cách kết hợp tuyến tính của nhiều phân phối Gaussian cơ bản. Công thức tổng quát của hỗn hợp Gaussian là:
    $$p(x) = \sum_{k=1}^{K} \pi_k N(x|\mu_k, \Sigma_k)$$
   Trong đó, $\pi_k$ là các hệ số trộn, $N(x|\mu_k, \Sigma_k)$ là các phân phối Gaussian thành phần với trung bình $\mu_k$ và hiệp phương sai $\Sigma_k$.
## 5.3 Các thành phần của hỗn hợp:
   - Mỗi phân phối Gaussian trong hỗn hợp được gọi là một thành phần của hỗn hợp và có các tham số riêng: trung bình $\mu_k$ và hiệp phương sai $\Sigma_k$.
   - Các hệ số trộn $\pi_k$ phải thỏa mãn điều kiện $\sum_{k=1}^{K} \pi_k = 1$ và $0 \leq \pi_k \leq 1$.
## 5.4 Ưu điểm:
   - Sự kết hợp tuyến tính của các phân phối Gaussian có thể tạo ra các mật độ phức tạp hơn nhiều. Bằng cách sử dụng đủ số lượng Gaussian và điều chỉnh các tham số của chúng, hầu như mọi phân phối liên tục đều có thể được xấp xỉ với độ chính xác tùy ý.