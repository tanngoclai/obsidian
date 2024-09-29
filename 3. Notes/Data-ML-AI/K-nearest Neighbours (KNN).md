---
Created at: 2024-07-23
Source:
---
![[Pasted image 20240723071319.png]]
### Mô tả:
- Phương pháp này xác định mật độ tại điểm $x$ dựa trên số lượng điểm dữ liệu trong K lân cận gần nhất của $x$.

### Công thức:
- Mật độ ước lượng tại điểm $x$ được tính bằng cách chia số lượng điểm trong K lân cận cho thể tích của hình cầu chứa các điểm này:
  $$
  p(x) = \frac{K}{N \cdot V}
  $$
  Trong đó:
  - $K$ là số lượng điểm dữ liệu trong K lân cận.
  - $N$ là tổng số điểm dữ liệu.
  - $V$ là thể tích của hình cầu có bán kính $r$, với $r$ là khoảng cách giữa $x$ và điểm dữ liệu xa nhất trong K lân cận.

### Ưu điểm:
- Đơn giản, dễ hiểu và dễ áp dụng cho phân loại.

### Nhược điểm:
- Kết quả phụ thuộc vào việc chọn K, với K quá nhỏ có thể dẫn đến quá nhiễu, và K quá lớn có thể làm mất các đặc điểm quan trọng của dữ liệu.