---
Created at: 2024-08-15
Source:
  - "[[Deep_learning_foundation.pdf#page=291|Deep_learning_foundation, p.274]]"
---
**Residual Connections**, còn được gọi là **skip connections**, là một kỹ thuật trong học sâu (deep learning) được giới thiệu trong mô hình mạng nơ-ron Residual Networks (ResNet). Kỹ thuật này giúp giải quyết vấn đề suy giảm độ chính xác (degradation problem) khi mạng nơ-ron sâu trở nên quá phức tạp (có thể do [[Gradient descent#5. Normalization|Vanishing Gradient]] hoặc dữ liệu bị suy giảm thông tin quan trọng sau khi truyền qua nhiều lớp)

### Vấn đề được giải quyết
Khi các mạng nơ-ron ngày càng sâu hơn (tức là có nhiều lớp hơn), người ta nhận thấy rằng việc thêm nhiều lớp không nhất thiết làm tăng độ chính xác, mà đôi khi còn làm giảm hiệu suất mô hình. Điều này không phải do overfitting, mà là do các lớp sâu hơn gặp khó khăn trong việc học một cách hiệu quả.

### Cách hoạt động của Residual Connections
Residual connections hoạt động bằng cộng đầu ra của một hoặc nhiều lớp trực tiếp vào đầu ra của một lớp sâu hơn. Công thức của một residual block thường như sau:

$$
y = F(x, \{W_i\}) + x
$$

Trong đó:
- $x$ là đầu vào của block.
- $F(x, \{W_i\})$ là hàm biểu diễn các lớp mà block đó học được.
- $y$ là đầu ra của block.

Thay vì học trực tiếp ánh xạ từ $x$ đến $y$, mô hình chỉ học phần dư $F(x) = y - x$. Điều này giúp mô hình dễ học hơn vì việc học phần dư (residual) thường dễ hơn so với việc học một ánh xạ phức tạp trực tiếp.

Ta có thể thấy việc đầu vào $x$ được bảo toàn ở đầu ra của block.

### Ưu điểm của Residual Connections
1. **Giảm thiểu vấn đề biến mất gradient**: Khi các mạng sâu hơn, gradient có thể trở nên rất nhỏ và làm chậm quá trình học tập. Residual connections giúp gradient lan truyền dễ dàng hơn qua các lớp, giảm thiểu vấn đề này.
2. **Học nhanh hơn**: Các mô hình với residual connections thường hội tụ nhanh hơn vì mô hình không cần phải học toàn bộ ánh xạ phức tạp mà chỉ cần học phần dư.
3. **Cải thiện độ chính xác**: Bằng cách làm cho việc học trở nên dễ dàng hơn, residual connections giúp các mạng nơ-ron sâu hơn có thể đạt được độ chính xác cao hơn mà không gặp phải vấn đề suy giảm.

![[Pasted image 20240815070941.png]]
