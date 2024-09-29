
## 1 Đạo hàm của hàm trả về một số vô hướng 
- Đạo hàm bậc nhất của một hàm số $f(x): \mathbb{R}^n \rightarrow \mathbb{R}$ theo $x$ được định nghĩa là: $$ \nabla_x f(x) = \left[ \frac{\partial f(x)}{\partial x_1}, \frac{\partial f(x)}{\partial x_2}, \ldots, \frac{\partial f(x)}{\partial x_n} \right]^T $$ - Đạo hàm của một hàm số trả về một số vô hướng là một vector có cùng chiều với vector đang được lấy đạo hàm. 
## 2 Đạo hàm của hàm trả về một vector 
- Đạo hàm của hàm số $f(X): \mathbb{R}^{n \times m} \rightarrow \mathbb{R}$ theo ma trận $X$ được định nghĩa là: $$\nabla f(X) = \left[ \frac{\partial f(X)}{\partial x_{11}}, \frac{\partial f(X)}{\partial x_{12}}, \ldots, \frac{\partial f(X)}{\partial x_{1m}}, \ldots, \frac{\partial f(X)}{\partial x_{n1}}, \frac{\partial f(X)}{\partial x_{n2}}, \ldots, \frac{\partial f(X)}{\partial x_{nm}} \right]$$
## 3 Tính chất quan trọng của đạo hàm 
- **Quy tắc tích (Product Rule)**:  $$\nabla (f(X) g(X)) = (\nabla f(X)) g(X) + (\nabla g(X)) f(X) $$
- **Quy tắc chuỗi (Chain Rule)**: $$\nabla_X g(f(X)) = (\nabla_X f)^T (\nabla_f g) $$