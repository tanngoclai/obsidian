---
Created at: 2024-08-11
Source:
  - "[[Deep_learning_foundation.pdf#page=250|Deep_learning_foundation, p.233]]"
---
![[Pasted image 20240811160228.png]]
# 1. Ý tưởng
**Thuật toán Backpropagation** (Lan truyền ngược) là một trong những thuật toán cơ bản và quan trọng nhất trong học sâu (deep learning). Nó được sử dụng để huấn luyện các mạng nơ-ron bằng cách tối ưu hóa các trọng số của mô hình dựa trên hàm mất mát (loss function). Thuật toán này tính toán gradient của hàm mất mát với các trọng số của mạng nơ-ron và điều chỉnh các trọng số này bằng cách sử dụng một phương pháp tối ưu hóa như gradient descent.
## 1.1. Nhắc lại về mạng nơ-ron:
Trước khi đi vào chi tiết của backpropagation, hãy hiểu rằng một mạng nơ-ron bao gồm các lớp (layer) liên kết với nhau:
- **Lớp đầu vào (Input Layer)**: Nhận đầu vào từ dữ liệu.
- **Lớp ẩn (Hidden Layer)**: Xử lý các đầu vào thông qua các trọng số và hàm kích hoạt (activation function).
- **Lớp đầu ra (Output Layer)**: Tạo ra kết quả dự đoán.
Mỗi kết nối giữa các nơ-ron trong các lớp khác nhau có trọng số $w$ và các nơ-ron có thể có thêm một bias $b$.

### 1.2. Quy trình tổng quát của Backpropagation:

1. **Forward Propagation**:
   - Đầu tiên, đầu vào từ dữ liệu được chuyển qua mạng nơ-ron, tính toán đầu ra của mỗi nơ-ron dựa trên trọng số và bias hiện tại.
   - Kết quả dự đoán cuối cùng được so sánh với giá trị mục tiêu (label) để tính toán hàm mất mát (loss function). Hàm mất mát đo lường mức độ sai lệch giữa dự đoán và thực tế.

2. **Tính toán Gradient**:
   - Để giảm hàm mất mát, cần phải điều chỉnh các trọng số sao cho dự đoán chính xác hơn.
   - Backpropagation thực hiện điều này bằng cách tính toán gradient của hàm mất mát theo từng trọng số trong mạng. Gradient này cho biết mức độ thay đổi của hàm mất mát nếu một trọng số cụ thể thay đổi.

3. **Lan truyền ngược lỗi (Error Backpropagation)**:
   - Thuật toán bắt đầu từ lớp đầu ra, tính toán lỗi (error) cho từng nơ-ron và lan truyền ngược qua các lớp ẩn về lớp đầu vào.
   - Trong mỗi lớp, lỗi được chia nhỏ và truyền ngược lại để tính toán gradient cho các trọng số kết nối giữa các nơ-ron.

4. **Cập nhật Trọng số**:
   - Sau khi tính toán gradient cho tất cả các trọng số, thuật toán sử dụng một phương pháp tối ưu hóa (ví dụ: gradient descent) để điều chỉnh các trọng số nhằm giảm hàm mất mát.
   - Trọng số được cập nhật theo công thức: $$
     w_{new} = w_{old} - \eta \cdot \frac{\partial L}{\partial w}
     $$
     trong đó $\eta$ là tốc độ học (learning rate) và $\frac{\partial L}{\partial w}$ là gradient của hàm mất mát theo trọng số $w$.

5. **Lặp lại**:
   - Quá trình này được lặp lại cho đến khi hàm mất mát đạt đến một giá trị tối ưu hoặc mô hình hội tụ (không cải thiện thêm).

# 2. Công thức tính
Giả sử mạng nơ-ron có:
- $L$ là hàm mất mát (loss function).
- $w$ là trọng số của mạng.
- $b$ là bias của mạng.
- $z = wx + b$ là tổng trọng số trước khi đưa qua hàm kích hoạt.
- $a$ là đầu ra của hàm kích hoạt.
- $y$ là giá trị thực tế.

## 2.1. Tính toán lỗi ở lớp đầu ra:
Đối với một mạng nơ-ron với hàm kích hoạt sigmoid hoặc softmax ở lớp đầu ra, gradient của hàm mất mát đối với đầu ra $a_L$ (của lớp cuối cùng) là:
$$
\delta_L = \frac{\partial L}{\partial a_L} \cdot \frac{\partial a_L}{\partial z_L}
$$
Trong đó:
- $\frac{\partial L}{\partial a_L} = a_L - y$ nếu sử dụng hàm mất mát là cross-entropy.
- $\frac{\partial a_L}{\partial z_L}$ là đạo hàm của hàm kích hoạt tại lớp đầu ra.

## 2.2. Lan truyền ngược lỗi qua các lớp:
Lỗi tại lớp $l$ (với $l$ là chỉ số của lớp) có thể được tính bằng cách sử dụng lỗi của lớp kế tiếp $l+1$:
$$
\delta_l = \left( w_{l+1}^T \delta_{l+1} \right) \cdot f'(z_l)
$$
Trong đó:
- $\delta_{l+1}$ là lỗi của lớp kế tiếp $l+1$.
- $w_{l+1}^T$ là ma trận trọng số đã chuyển vị của lớp $l+1$.
- $f'(z_l)$ là đạo hàm của hàm kích hoạt tại lớp $l$.

## 2.3. Cập nhật trọng số và bias:

Sau khi tính được gradient, trọng số và bias được cập nhật bằng cách sử dụng gradient descent:
$$
w_l = w_l - \eta \cdot \frac{\partial L}{\partial w_l} = w_l - \eta \cdot (\delta_l \cdot a_{l-1}^T)
$$
$$
b_l = b_l - \eta \cdot \frac{\partial L}{\partial b_l} = b_l - \eta \cdot \delta_l
$$
Trong đó:
- $\eta$ là tốc độ học (learning rate).
- $\frac{\partial L}{\partial w_l}$ và $\frac{\partial L}{\partial b_l}$ lần lượt là gradient của hàm mất mát theo trọng số và bias tại lớp $l$.
- $a_{l-1}$ là đầu ra của lớp $l-1$.

# 3. Ứng dụng khác của backpropagation
## 3.1. [[Ma trận Jacobian]]
Dùng để tính gradient của $Loss \ function$ và input $x$.
Giả sử ta có một lớp mạng với đầu vào là $\mathbf{x}$, đầu ra là $\mathbf{y}$, và $\mathbf{f}$ là activation function:
$$
\mathbf{y} = \mathbf{f}(\mathbf{x})
$$

Trong quá trình backpropagation, để tính gradient của hàm lỗi $L$ theo $\mathbf{x}$, ta cần sử dụng ma trận Jacobian $\mathbf{J}(\mathbf{x})$ của $\mathbf{f}$ theo $\mathbf{x}$:

$$
\frac{\partial L}{\partial \mathbf{x}} = \mathbf{J}(\mathbf{x})^\top \cdot \frac{\partial L}{\partial \mathbf{y}}
$$

Trong đó:
- $\mathbf{J}(\mathbf{x})$ là ma trận Jacobian của $\mathbf{y}$ theo $\mathbf{x}$, mô tả sự thay đổi của đầu ra $\mathbf{y}$ khi thay đổi đầu vào $\mathbf{x}$.
- $\frac{\partial L}{\partial \mathbf{y}}$ là gradient của hàm lỗi $L$ theo đầu ra $\mathbf{y}$.

## 3.2. [[Ma trận Hessian]]
Sử dụng ma trận Hessian để đánh giá đạo hàm bậc hai của hàm lỗi trong thuật toán backpropagation có thể cải thiện việc tối ưu hóa, giúp hiểu rõ hơn về cấu trúc của hàm lỗi và làm cho quá trình huấn luyện trở nên hiệu quả hơn. Dưới đây là cách ma trận Hessian được áp dụng trong ngữ cảnh này:

### 3.2.1. Định nghĩa

Ma trận Hessian là ma trận các đạo hàm bậc hai của hàm lỗi $L$ với các tham số của mô hình. Nếu hàm lỗi là $L(\mathbf{w})$ với $\mathbf{w}$ là vector các tham số (trọng số và bias của mạng), thì ma trận Hessian $\mathbf{H}$ tại điểm $\mathbf{w}$ được định nghĩa như sau:

$$
\mathbf{H}_{ij} = \frac{\partial^2 L}{\partial w_i \partial w_j}
$$
### 3.2.2. Ứng dụng

- **Tính toán Ma trận Hessian**: Để tính ma trận Hessian, trước tiên, bạn cần tính gradient của hàm lỗi $\nabla L(\mathbf{w})$ bằng phương pháp backpropagation. Sau đó, để có ma trận Hessian, bạn tính đạo hàm bậc hai của $L$ đối với các tham số. Việc này yêu cầu tính toán thêm một bước đạo hàm đối với mỗi phần tử của gradient.

  Ví dụ, nếu bạn đã tính gradient $\frac{\partial L}{\partial w_i}$, bạn sẽ cần tính đạo hàm của $\frac{\partial L}{\partial w_i}$ theo từng trọng số khác $w_j$:
  $$
  \mathbf{H}_{ij} = \frac{\partial}{\partial w_j} \left( \frac{\partial L}{\partial w_i} \right)
  $$

### 3.2.3. Hạn chế

- **Chi phí Tính Toán**: Tính toán ma trận Hessian đầy đủ là tốn kém về mặt tính toán và bộ nhớ, đặc biệt với mạng nơ-ron có nhiều tham số. Do đó, việc sử dụng ma trận Hessian thường không khả thi trong các mạng lớn.
### 3.2.4. Levenberg-Marquardt approximation (LMA)

Levenberg-Marquardt approximation sử dụng một ma trận cập nhật cải tiến, kết hợp giữa ma trận Hessian và một ma trận điều chỉnh để tạo ra một bước cập nhật hiệu quả. Công thức cập nhật trong LMA được cho bởi:

$$
\mathbf{w}_{new} = \mathbf{w}_{old} - (\mathbf{J}^\top \mathbf{J} + \lambda \mathbf{I})^{-1} \mathbf{J}^\top \mathbf{r}
$$

Trong đó:

- $\mathbf{w}_{old}$ và $\mathbf{w}_{new}$ là các tham số trước và sau cập nhật.
- $\mathbf{J}$ là ma trận Jacobian của hàm mục tiêu.
- $\mathbf{r} = \mathbf{y} - \hat{\mathbf{y}}$.
- $\lambda$ là tham số điều chỉnh (damping factor) giúp điều chỉnh giữa gradient descent và phương pháp Newton.
- $\mathbf{I}$ là ma trận đơn vị.