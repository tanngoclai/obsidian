---
Created at: 2024-08-12
Source:
  - "[[Deep_learning_foundation.pdf#page=261|Deep_learning_foundation, p.244]]"
---
automatic differentiation (AD), also known as *autodiff* or *algorithmic differentiation*

# 1. Định nghĩa
AD là một kỹ thuật giúp tính toán gradient một cách hiệu quả và chính xác. Có hai phương pháp chính trong AD:
- **Forward Mode AD**: Dùng để tính đạo hàm của một biến đầu vào duy nhất ảnh hưởng đến nhiều biến đầu ra.
- **Reverse Mode AD**: Dùng để tính đạo hàm của một hàm số có nhiều biến đầu vào ảnh hưởng đến một biến đầu ra duy nhất. Phương pháp này rất phổ biến trong các mô hình học sâu (deep learning), vì trong các mạng nơ-ron, số lượng tham số (biến đầu vào) thường lớn hơn nhiều so với số lượng đầu ra (mất mát là một số duy nhất).

# 2. Lợi ích
- **Chính xác**: AD tính toán gradient một cách chính xác tới mức máy, khác với các phương pháp xấp xỉ.
- **Hiệu quả**: AD có thể tính toán gradient với chi phí tương tự như việc tính toán giá trị của chính hàm số đó.
- **Tự động**: Người dùng không cần phải viết các biểu thức đạo hàm thủ công, giảm thiểu sai sót và tiết kiệm thời gian.

# 3. Forward-mode
Forward Mode AD tính đạo hàm của một hàm số thông qua việc áp dụng quy tắc chuỗi (chain rule) trong đạo hàm, theo hướng từ đầu vào đến đầu ra. Điều này có nghĩa là khi tính đạo hàm, Forward Mode sẽ đi qua từng biến đầu vào của hàm số, tính toán và giữ lại cả giá trị của hàm và đạo hàm của nó tại mỗi bước.

## 3.1. Cấu trúc dữ liệu của Forward Mode AD
Forward Mode AD sử dụng một cấu trúc dữ liệu gọi là **dual number**. Một số dual có dạng:

$$ \tilde{x} = x + \epsilon \dot{x} $$

Trong đó:
- $x$ là giá trị thực của biến.
- $\dot{x}$ là giá trị đạo hàm của biến $x$ đối với một biến đầu vào cụ thể.
- $\epsilon$ là một phần tử vô cùng bé với đặc tính $\epsilon^2 = 0$.

Khi thực hiện các phép toán với các số dual này, ta sẽ tự động tính được cả giá trị và đạo hàm.

##  3.2. Cơ chế hoạt động của Forward Mode AD
Forward Mode AD thực hiện việc tính đạo hàm bằng cách "theo dõi" từng bước của hàm số khi nó thực hiện các phép toán cơ bản. Ta đi qua từng bước tính toán để lấy ra cả giá trị của hàm số và đạo hàm của nó.

Ví dụ, giả sử ta có hàm $f(x, y) = \sin(x) + xy$. Ta muốn tính đạo hàm của hàm số này với $x$ trong khi giữ $y$ cố định.

#### Bước 1: Khởi tạo số dual cho biến $x$
- Ta khởi tạo $\tilde{x} = x + \epsilon$.
- Ta khởi tạo $\tilde{y} = y$, vì ta không cần tính đạo hàm với $y$.

#### Bước 2: Theo dõi các phép toán
- **Tính $\sin(x)$**:
  $$
  \sin(\tilde{x}) = \sin(x) + \epsilon \cos(x)
  $$
  Ta nhận được giá trị $\sin(x)$ và đạo hàm là $\cos(x)$.

- **Tính $xy$**:
  $$
  \tilde{x} \tilde{y} = (x + \epsilon) \cdot y = xy + \epsilon y
  $$
  Ta nhận được giá trị $xy$ và đạo hàm là $y$.

- **Cộng các kết quả lại**:
  $$
  f(\tilde{x}, \tilde{y}) = \sin(x) + xy + \epsilon (\cos(x) + y)
  $$

Trong đó, $\cos(x) + y$ là đạo hàm của hàm $f(x, y)$ với $x$.

## 3.3. Đặc điểm và ưu điểm của Forward Mode AD
- **Ưu điểm**:
  - **Hiệu quả** khi số biến đầu vào ít và số biến đầu ra nhiều, vì chỉ cần một phép tính cho mỗi biến đầu vào.
  - **Chính xác** vì không bị ảnh hưởng bởi các lỗi số học như trong phương pháp sai phân hữu hạn.
  
- **Nhược điểm**:
  - **Không hiệu quả** khi số biến đầu vào lớn hơn nhiều so với số biến đầu ra, vì mỗi biến đầu vào cần tính toán riêng biệt.
# 4. Reverse-mode

Reverse-Mode AD dựa trên quy tắc chuỗi (chain rule) để tính đạo hàm, nhưng theo hướng ngược lại so với Forward-Mode AD. Thay vì tính toán giá trị và đạo hàm từng bước từ đầu vào đến đầu ra như Forward-Mode, Reverse-Mode AD bắt đầu từ đầu ra và lần lượt tính toán đạo hàm ngược trở về đầu vào.

## 4.1. Quá trình Reverse-Mode AD

Giả sử ta có một hàm $y = f(x_1, x_2, \dots, x_n)$ với nhiều biến đầu vào $x_1, x_2, \dots, x_n$ và một biến đầu ra $y$. Reverse-Mode AD sẽ thực hiện các bước sau:

#### Bước 1: Tính giá trị của hàm số (Forward Pass)
- Trong bước này, Reverse-Mode AD sẽ tính giá trị của hàm số $f(x_1, x_2, \dots, x_n)$ bằng cách thực hiện các phép toán theo thứ tự từ đầu vào đến đầu ra. Trong quá trình này, ta sẽ lưu lại các giá trị trung gian cần thiết cho bước tiếp theo.

#### Bước 2: Tính đạo hàm ngược (Backward Pass)
- Sau khi đã có giá trị đầu ra $y$, Reverse-Mode AD sẽ tính đạo hàm của $y$ theo từng biến đầu vào bằng cách áp dụng quy tắc chuỗi ngược từ đầu ra về các biến đầu vào. Ta sẽ tính đạo hàm của $y$ theo từng biến trung gian trong quá trình, cuối cùng tính ra được đạo hàm của $y$ theo từng biến đầu vào.

## 4.2. Ví dụ chi tiết về Reverse-Mode AD

Xét một hàm đơn giản: $f(x_1, x_2) = (x_1 + x_2) \cdot x_2$.

#### Bước 1: Forward Pass
- Tính các giá trị trung gian:
  $$
  v_1 = x_1 + x_2
  $$
  $$
  y = v_1 \cdot x_2
  $$
  
- Giá trị đầu ra $y$ phụ thuộc vào giá trị của $v_1$ và $x_2$.

#### Bước 2: Backward Pass
- Bắt đầu từ đạo hàm của $y$ theo chính nó, ta có:
  $$
  \frac{\partial y}{\partial y} = 1
  $$
  
- Tính đạo hàm của $y$ theo $v_1$ và $x_2$:
  $$
  \frac{\partial y}{\partial v_1} = \frac{\partial y}{\partial y} \cdot \frac{\partial y}{\partial v_1} = 1 \cdot x_2 = x_2
  $$
  $$
  \frac{\partial y}{\partial x_2} = \frac{\partial y}{\partial y} \cdot \frac{\partial y}{\partial x_2} = 1 \cdot v_1
  $$
  
- Cuối cùng, tính đạo hàm của $y$ theo $x_1$ và $x_2$ (dùng quy tắc chuỗi):
  $$
  \frac{\partial y}{\partial x_1} = \frac{\partial y}{\partial v_1} \cdot \frac{\partial v_1}{\partial x_1} = x_2 \cdot 1 = x_2
  $$
  $$
  \frac{\partial y}{\partial x_2} = \frac{\partial y}{\partial v_1} \cdot \frac{\partial v_1}{\partial x_2} + \frac{\partial y}{\partial x_2} \cdot 1 = x_2 + v_1 = x_2 + (x_1 + x_2)
  $$

- Vậy, các đạo hàm cuối cùng là:
  $$
  \frac{\partial y}{\partial x_1} = x_2
  $$
  $$
  \frac{\partial y}{\partial x_2} = x_1 + 2x_2
  $$

## 4.3. Đặc điểm và ưu điểm của Reverse-Mode AD
- **Ưu điểm**:
  - **Hiệu quả cao** khi số biến đầu vào nhiều và số biến đầu ra ít, vì tất cả các đạo hàm theo từng biến đầu vào được tính đồng thời trong một lần backward pass.
  - **Phù hợp cho các bài toán học sâu**: Reverse-Mode AD là nền tảng cho việc huấn luyện các mô hình học sâu, đặc biệt là việc tính gradient của hàm mất mát với rất nhiều tham số.

- **Nhược điểm**:
  - **Bộ nhớ yêu cầu cao**: Reverse-Mode AD cần lưu lại các giá trị trung gian trong quá trình forward pass, dẫn đến việc tiêu tốn bộ nhớ, đặc biệt khi hàm số phức tạp.




