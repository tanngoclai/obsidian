---
Created at: 2024-07-19
Source:
  - "[[Deep_learning_foundation.pdf#page=85|Deelp_learning_foundation - 3.1]]"
---

# 1 Bernoulli Distribution
- Phân phối Bernoulli mô tả một biến nhị phân $x \in \{0, 1\}$, như việc tung một đồng xu với $x = 1$ đại diện cho 'mặt ngửa' và $x = 0$ đại diện cho 'mặt sấp'.
- Xác suất của $x = 1$ được ký hiệu là $\mu \ (0 \leq \mu \leq 1)$, do đó xác suất của $x = 0$ là $1 - \mu$.
- Công thức cho phân phối Bernoulli là:$$\text{Bern}(x|\mu) = \mu^x(1 - \mu)^{1 - x}$$
- Phân phối này có trung bình $E[x] = \mu$ và phương sai $$\text{var}[x] = \mu(1 - \mu)$$
# 2 Binomial Distribution
- Phân phối nhị thức (Binomial distribution) mở rộng phân phối Bernoulli cho một số lần thử $N$.
- Xác suất của $m$ lần thành công trong $N$ lần thử được mô tả bởi:$$\text{Bin}(m|N, \mu) = \binom{N}{m} \mu^m (1 - \mu)^{N - m}$$.
- Trung bình và phương sai của phân phối nhị thức lần lượt là:$$E[m] = N\mu$$$$\text{var}[m] = N\mu(1 - \mu)$$
# 3 Multinomial Distribution
- Biến rời rạc có thể có nhiều hơn hai trạng thái, mô tả bởi phân phối đa thức (Multinomial distribution).
- Biến có thể được biểu diễn bằng một vector $K$ - chiều $x$, trong đó một phần tử $x_k = 1$ và các phần tử còn lại bằng 0.
- Xác suất của $x_k = 1$ được ký hiệu là $\mu_k$, và phân phối của $x$ là:$$p(x|\mu) = \prod_{k=1}^K \mu_k^{x_k}$$.
- Các tham số $\mu_k$ phải thỏa mãn: $\sum_{k=1}^K \mu_k = 1$.
- Phân phối này là một sự mở rộng của phân phối Bernoulli cho nhiều kết quả.