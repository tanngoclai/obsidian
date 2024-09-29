---
Created at: 2024-08-11
Source:
---

Ma trận Jacobian là một ma trận các đạo hàm riêng từng phần, mô tả sự biến thiên của một vector hàm khi các biến đầu vào thay đổi. Nếu ta có một hàm vector $\mathbf{f}: \mathbb{R}^n \rightarrow \mathbb{R}^m$, trong đó $\mathbf{f}(\mathbf{x}) = [f_1(\mathbf{x}), f_2(\mathbf{x}), \ldots, f_m(\mathbf{x})]^\top$, thì ma trận Jacobian của hàm này là ma trận $m \times n$ được định nghĩa bởi:

$$
\mathbf{J}(\mathbf{x}) = \begin{pmatrix}
\frac{\partial f_1}{\partial x_1} & \frac{\partial f_1}{\partial x_2} & \cdots & \frac{\partial f_1}{\partial x_n} \\
\frac{\partial f_2}{\partial x_1} & \frac{\partial f_2}{\partial x_2} & \cdots & \frac{\partial f_2}{\partial x_n} \\
\vdots & \vdots & \ddots & \vdots \\
\frac{\partial f_m}{\partial x_1} & \frac{\partial f_m}{\partial x_2} & \cdots & \frac{\partial f_m}{\partial x_n}
\end{pmatrix}
$$