---
Date: 2024-09-22
Source: 
aliases:
  - Expectation
  - Expected value
---
 # 1. Định nghĩa
Kỳ vọng của một biến ngẫu nhiên $x$ được tính bằng (mang ý nghĩa *tương tự* giá trị trung bình):
- Rời rạc: $E[X] = \sum_x x p(x)$
- Liên tục: $E[X] = \int x p(x) dx$
Với:
- $x$ là giá trị trên không gian xác suất của $X$.
- $p(x)$ là hàm phân phối xác suất của $X$.
- Kí hiệu: $\mu = E[X]$
# 2. Các tính chất
## 2.1 Tuyến tính
Với 2 biến ngẫu nhiên bất kì $X$ và $Y$ (xác định trên cùng không gian xác suất):
$$E[aX+bY]=aE[X]+bE[Y]$$
## 2.2 Tính nhân
Nếu $X$ và $Y$ **độc lập tuyến tính**:
$$E[XY] = E[X]E[Y]$$
## 2.3 Giá trị của hàm
$$E[g(X)] = \int g(x) p(x) dx$$
Nhân với $p(x)dx$ do vẫn sử dụng biến ngẫu nhiên $X$, vẫn cần nhân với hàm phân phối xác suất của $X$