---
Date: 2024-09-22
Source: 
aliases:
  - Covariance
  - Covariance matrix
---
# 1. Định nghĩa
1. Xét trận 1 tập hợp biến ngẫu nhiên $X_i$, biểu diễn dưới dạng vector $X$ 
$$X=\begin{bmatrix}X_{1} \\\vdots \\X_{n} \end{bmatrix}$$
2. Khi đó, ma trận hiệp phương sai tính như sau:
$$\Sigma =\begin{bmatrix}\mathrm {E} [(X_{1}-\mu _{1})(X_{1}-\mu _{1})]&\mathrm {E} [(X_{1}-\mu _{1})(X_{2}-\mu _{2})]&\cdots &\mathrm {E} [(X_{1}-\mu _{1})(X_{n}-\mu _{n})]\\\\\mathrm {E} [(X_{2}-\mu _{2})(X_{1}-\mu _{1})]&\mathrm {E} [(X_{2}-\mu _{2})(X_{2}-\mu _{2})]&\cdots &\mathrm {E} [(X_{2}-\mu _{2})(X_{n}-\mu _{n})]\\\\\vdots &\vdots &\ddots &\vdots \\\\\mathrm {E} [(X_{n}-\mu _{n})(X_{1}-\mu _{1})]&\mathrm {E} [(X_{n}-\mu _{n})(X_{2}-\mu _{2})]&\cdots &\mathrm {E} [(X_{n}-\mu _{n})(X_{n}-\mu _{n})]\end{bmatrix}$$

$$\Sigma =\begin{bmatrix} var(X_{1}) & cov(X_{1},X_{2})&\cdots &cov(X_{1},X_{n})\\\\\ cov(X_{2},X_{1}) & var(X_{2})&\cdots &cov(X_{1},X_{n})\\\\\vdots &\vdots &\ddots &\vdots \\\\ cov(X_{n},X_{1})&cov(X_{n},X_{2})&\cdots &\mathrm var(X_{n})\end{bmatrix}$$

	Với [[Kỳ vọng]] $\mu_i = E[X_i]$

3. Hoặc viết gọn lại thành:
$$\Sigma = E[(x - \mu)(x - \mu)^T]$$

# 2. Tính chất
- $X_i$ có thể không phải 1 chiều. Nếu $X_i$ nhiều chiều thì:
	- $X$ tổng quát có dạng 1 ma trận bình thường.
	- $\mu_i$ là phương sai của các phần tử trong vector $X_i$.
- Ma trận hiệp phương sai là ma trận đối xứng:
	- Phần tử trên đường chéo chính là phương sai của các biến ngẫu nhiêu $X_i$ ban đầu.
- Các phần tử khác thể hiện tương quan về độ lệch giữa 2 biến:
	- Khi $cov(X,Y)>0$: 2 biến X và Y có quan hệ tuyến tính thuận, X tăng, Y tăng.
	- Khi $cov(X,Y)<0$: 2 biến X và Y có quan hệ tuyến tính nghịch, X tăng, Y giảm và ngược lại.
	- Khi $cov(X,Y)=0:$ 2 biến X và Y không có mối quan hệ với nhau.
- Phương sai và hiệp phương sai khác nhau. Phương sai dành cho 1 biến, hiệp phương sai dành cho 2 biến.