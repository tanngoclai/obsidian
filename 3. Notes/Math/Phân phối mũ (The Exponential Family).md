---
Created at: 2024-07-23
Source:
  - "[[Deep_learning_foundation.pdf#page=113|Deep_learning_foundation - 3.4 ]]"
---
# 1 Định nghĩa:
Họ mũ của các phân phối trên $x$, với tham số $\eta$, được định nghĩa là tập hợp các phân phối dưới dạng:
$$ p(x|\eta) = h(x)g(\eta)\exp\{\eta^T u(x)\} $$

Trong đó:
- $x$ có thể là số vô hướng hoặc vector, và có thể là biến rời rạc hoặc liên tục.
- $\eta$ được gọi là các tham số tự nhiên của phân phối.
- $u(x)$ là một hàm của $x$.
- $g(\eta)$ đảm bảo phân phối được chuẩn hóa.

# 2 Ví dụ minh họa

## 2.1 Phân phối Bernoulli
$$ p(x|\mu) = Bern(x|\mu) = \mu^x (1 - \mu)^{1-x} $$
Biểu diễn lại dưới dạng họ mũ thông qua [[Hàm sigmoid]]:
$$ p(x|\eta) = \sigma(-\eta) \exp(\eta x) $$
Với:
$$ \eta = \ln \left( \frac{\mu}{1 - \mu} \right) $$
$$ \sigma(\eta) = \frac{1}{1 + \exp(-\eta)} $$

## 2.2 Phân phối đa thức (Multinomial)
$$ p(x|\mu) = \prod_{k=1}^{M} \mu_k^{x_k} = \exp\left( \sum_{k=1}^{M} x_k \ln \mu_k \right) $$
Biểu diễn lại dưới dạng họ mũ:
$$ p(x|\eta) = \exp(\eta^T x) $$
Với:
$$ \eta_k = \ln \mu_k $$

## 2.3 Phân phối Gaussian
$$ p(x|\mu, \sigma^2) = \frac{1}{\sqrt{2\pi\sigma^2}} \exp\left( -\frac{(x - \mu)^2}{2\sigma^2} \right) $$
Biểu diễn lại dưới dạng họ mũ:
$$ p(x|\eta) = \frac{1}{\sqrt{2\pi}} \exp\left( \eta_1 x + \eta_2 x^2 \right) $$
Với:
$$ \eta_1 = \frac{\mu}{\sigma^2} $$
$$ \eta_2 = -\frac{1}{2\sigma^2} $$