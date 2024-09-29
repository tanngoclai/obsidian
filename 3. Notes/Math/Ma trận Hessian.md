---
Created at: 2024-08-11
Source:
---
Ma trận Hessian là một công cụ toán học quan trọng trong giải tích, được sử dụng để nghiên cứu các tính chất của hàm số nhiều biến. Nó là một ma trận vuông bao gồm các đạo hàm bậc hai của một hàm số theo các biến của nó, giúp chúng ta hiểu được sự biến thiên và độ cong của hàm số xung quanh một điểm.

# 1. Định nghĩa Ma trận Hessian:

Giả sử ta có một hàm số $f: \mathbb{R}^n \rightarrow \mathbb{R}$ khả vi hai lần liên tục. Ma trận Hessian của hàm $f$ tại một điểm $\mathbf{x} \in \mathbb{R}^n$ là ma trận vuông $n \times n$ chứa các đạo hàm bậc hai của $f$, được định nghĩa như sau:

$$
\mathbf{H}(\mathbf{x}) = \begin{pmatrix}
\frac{\partial^2 f}{\partial x_1^2} & \frac{\partial^2 f}{\partial x_1 \partial x_2} & \cdots & \frac{\partial^2 f}{\partial x_1 \partial x_n} \\
\frac{\partial^2 f}{\partial x_2 \partial x_1} & \frac{\partial^2 f}{\partial x_2^2} & \cdots & \frac{\partial^2 f}{\partial x_2 \partial x_n} \\
\vdots & \vdots & \ddots & \vdots \\
\frac{\partial^2 f}{\partial x_n \partial x_1} & \frac{\partial^2 f}{\partial x_n \partial x_2} & \cdots & \frac{\partial^2 f}{\partial x_n^2}
\end{pmatrix}
$$

# 2. Ý nghĩa của Ma trận Hessian:

- **Độ cong của hàm số:** Ma trận Hessian cung cấp thông tin về độ cong của hàm số $f$ tại một điểm nhất định. Điều này liên quan đến hình dạng của đồ thị hàm số trong vùng lân cận của điểm đó (chẳng hạn như là điểm yên ngựa, cực đại, hay cực tiểu).

- **Phân loại điểm tới hạn:** Tại một điểm tới hạn $\mathbf{x}_0$ (nơi gradient bằng không, tức là $\nabla f(\mathbf{x}_0) = 0$), ma trận Hessian có thể được sử dụng để xác định bản chất của điểm đó:
  - Nếu ma trận Hessian là xác định dương (tất cả các giá trị riêng đều dương), $\mathbf{x}_0$ là một điểm cực tiểu cục bộ.
  - Nếu ma trận Hessian là xác định âm (tất cả các giá trị riêng đều âm), $\mathbf{x}_0$ là một điểm cực đại cục bộ.
  - Nếu ma trận Hessian không xác định (có cả giá trị riêng dương và âm), $\mathbf{x}_0$ là một điểm yên ngựa.

- **Sự ổn định:** Ma trận Hessian cũng liên quan đến độ ổn định của một hàm số. Trong một số bài toán tối ưu hóa, ma trận Hessian giúp đánh giá liệu giải pháp tìm được có ổn định hay không.