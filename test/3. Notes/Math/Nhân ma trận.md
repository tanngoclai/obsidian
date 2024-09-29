---
~
---

Phép nhân ma trận **A** với **B**
- Thực chất là 1 phép ánh xạ (phép biển đổi tuyến tính) ma trận **B**, các biến đổi tuyến tính được biển diễn bằng ma trận **A** (phép xoay, cắt, tịnh tiến...)

$$ \begin{bmatrix}
a & b \\
c & d \\
\end{bmatrix} \times \begin{bmatrix}
x \\ y
\end{bmatrix} 
= x \times \begin{bmatrix} a \\ c \end{bmatrix} 
+ y \times \begin{bmatrix} b \\ d \end{bmatrix} = \begin{bmatrix}
ax + by \\
cx + dy \\
\end{bmatrix}$$

-> Tóm lại, đây là 1 ánh xạ tuyến tính của các vector trong ma trận **B**. 

- Đôi khi, phép nhân ma trận còn biểu diễn sự kết hợp của nhiều phép ánh xạ, trong đó mỗi nhân tử là 1 phép ánh xạ.

# Non-square matrix
Phép nhân 2 ma trận: $A_{m \times n} \times B_{n \times r}$ tương đương với biến đổi tuyến tính $r$ vector từ không gian $n$ chiều sang không gian $m$ chiều.

# Kí hiệu
Nếu áp dụng thêm các phép biến đổi khác thì ta thêm ma trận khác vào **bên trái** của phép nhân ma trận. Lí do ta thêm phép ánh xạ (chính là ma trận) vào bên trái là điều đó **tương tự với kí hiệu hàm số** (ánh xạ). VD $f(x)$ có kí hiệu $f$ nằm bên trái của biến $x$.

# Related:
1. [[Dot products|Tích vô hướng]]
2. [[Ma trận]]