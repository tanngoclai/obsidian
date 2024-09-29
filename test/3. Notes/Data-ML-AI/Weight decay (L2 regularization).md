---
Created at: 2024-08-13
Source:
  - "[[Deep_learning_foundation.pdf#page=277|Deep_learning_foundation, p.260]]"
---
**Weight Decay** là một kỹ thuật phổ biến trong deep learning, được sử dụng để ngăn chặn hiện tượng overfitting, giúp mô hình tổng quát hóa tốt hơn. Nó thực chất là một dạng của regularization, đặc biệt là **L2 regularization**.

# 1. Định nghĩa
### Cách Hoạt Động:
Trong quá trình huấn luyện mô hình deep learning, mục tiêu của ta là tối ưu hàm mất mát (loss function), chẳng hạn như hàm mất mát MSE (Mean Squared Error) hoặc Cross-Entropy. Để làm điều này, ta sử dụng các thuật toán tối ưu hóa như **[[Gradient descent#2.2. Stochastic gradient descent|Stochastic Gradient Descent (SGD)]]** để cập nhật trọng số (weights) của mô hình.

Weight decay làm cho quá trình tối ưu hóa "trừng phạt" các giá trị trọng số lớn bằng cách thêm một thuật ngữ vào hàm mất mát, biểu diễn tổng bình phương của tất cả các trọng số nhân với một hệ số nhỏ gọi là **hệ số weight decay (λ)**.

### Công Thức:
Giả sử hàm mất mát ban đầu là $L(w)$, với $w$ là các trọng số của mô hình. Sau khi áp dụng weight decay, hàm mất mát mới sẽ là:

$$
L'(w) = L(w) + \frac{\lambda}{2} \sum_{i} w_i^2
$$

Trong đó:
- $\lambda$ là hệ số weight decay, điều chỉnh mức độ regularization.
- $\sum_{i} w_i^2$ là tổng bình phương của các trọng số.

### Ảnh Hưởng:
- **Regularization**: Weight decay giúp làm giảm overfitting bằng cách làm giảm độ phức tạp của mô hình. Các trọng số lớn có xu hướng được giảm xuống, dẫn đến một mô hình đơn giản hơn và ít phụ thuộc vào dữ liệu huấn luyện cụ thể.
- **Gradient Descent**: Trong quá trình huấn luyện, trọng số sẽ bị giảm bớt một lượng tỷ lệ với giá trị của chúng, tức là:

$$
w_{new} = w_{old} - \eta \cdot \frac{\partial L(w)}{\partial w} - \eta \cdot \lambda \cdot w_{old}
$$

Ở đây, $\eta$ là learning rate, và $\lambda \cdot w_{old}$ là thành phần giảm weight do weight decay.

### Kết Quả:
Weight decay giúp các trọng số của mô hình không trở nên quá lớn, giảm thiểu nguy cơ overfitting, và giúp mô hình có khả năng tổng quát hóa tốt hơn trên dữ liệu chưa thấy trước.

# 2. Cải tiến
## 2.1. Consistent regularizers
$$
L'(w) = L(w) + \sum_{j} \left( \frac{\lambda_{j}}{2} \sum_{w \in W_{j}} w_i^2 \right)
$$
Trong đó $W_j$ là tập hợp trọng số của mỗi layer.
## 2.2. Tổng quát hóa
$$\Omega(\boldsymbol{w}) = \frac{\lambda}{2} \sum_{i} |w_i|^q$$
$$L'(w) = L(w) + \frac{\lambda}{2} \sum_{i} |w_i|^q$$
Điều này tương đương với việc điều chỉnh $L(w)$ theo điều kiện: $$\sum_{i} |w_i|^q \leq \eta$$