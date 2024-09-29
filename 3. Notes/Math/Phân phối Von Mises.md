---
Created at: 2024-07-22
Source:
  - "[[Deep_learning_foundation.pdf#page=108|Deelp_learning_foundation - 3.3]]"
---

# 1 Định nghĩa
Phân phối Von Mises, hay còn gọi là phân phối chuẩn tròn, là một phân phối xác suất trên đường tròn. 
Nó được đặc trưng bởi hai tham số chính: $\theta_0$ (góc trung bình) và $m$ (tham số tập trung). Công thức của phân phối Von Mises là:

$$ p(\theta | \theta_0, m) = \frac{1}{2\pi I_0(m)} \exp \{ m \cos (\theta - \theta_0) \} $$

Trong đó, $I_0(m)$ là [[Hàm Bassel|hàm Bessel bậc 0 của loại I]]. Khi $m$ lớn, phân phối Von Mises gần giống dạng của[[Phân phối chuẩn (Gaussian)]].

# 2 Maximum Likelihood Estimation

Logarithm của hàm khả năng cho phân phối Von Mises được cho bởi:

$$ \ln p(D | \theta_0, m) = -N \ln(2\pi) - N \ln I_0(m) + m \sum_{n=1}^{N} \cos(\theta_n - \theta_0) $$

Để tìm giá trị $\theta_0$ tối đa, ta giải phương trình:

$$ \sum_{n=1}^{N} \sin(\theta_n - \theta_0) = 0 $$

Sử dụng định lý lượng giác:

$$ \sin(A - B) = \cos B \sin A - \cos A \sin B $$

Giải phương trình trên ta được:

$$ \theta_{ML_0} = \tan^{-1} \left( \frac{\sum_{n} \sin \theta_n}{\sum_{n} \cos \theta_n} \right) $$

Tương tự, để tìm giá trị $m$ tối đa, ta có:

$$ A(m_{ML}) = \frac{1}{N} \sum_{n=1}^{N} \cos(\theta_n - \theta_{ML_0}) $$

trong đó, $A(m)$ được định nghĩa là:

$$ A(m) = \frac{I_1(m)}{I_0(m)} $$

Phương trình này có thể được giải bằng cách đảo ngược hàm $A(m)$ một cách số học.

# 3 Đặc điểm của phân phối Von Mises

Phân phối Von Mises có đặc điểm là đơn đỉnh. Để mô hình hóa các biến tuần hoàn có nhiều đỉnh, ta có thể sử dụng hỗn hợp của các phân phối Von Mises. Cách đơn giản nhất để xây dựng các phân phối tuần hoàn là sử dụng biểu đồ tần suất (histogram) chia tọa độ góc thành các ô cố định.

Phân phối Von Mises là một công cụ mạnh mẽ trong việc xử lý các biến tuần hoàn, đặc biệt hữu ích trong các lĩnh vực như thống kê tròn (circular statistics) và phân tích tín hiệu tuần hoàn.
