---
Created at: 2024-07-23
Source:
---
![[Pasted image 20240723071241.png]]
### Mô tả:
- KDE ước lượng mật độ bằng cách sử dụng các hàm kernel (ví dụ, hàm Gauss) để tạo ra một "bản đồ nhiệt" của mật độ.

### Công thức:
- Mật độ ước lượng tại điểm $x$ là tổng của các hàm kernel xung quanh tất cả các điểm dữ liệu khác:
  $$
  p(x) = \frac{1}{n h} \sum_{i=1}^{n} K\left(\frac{x - x_i}{h}\right)
  $$
  Trong đó:
  - $n$ là số lượng điểm dữ liệu.
  - $h$ là băng thông (bandwidth), điều chỉnh độ rộng của hàm kernel.
  - $K(\cdot)$ là hàm kernel, thường là hàm Gauss với công thức:
    $$
    K(z) = \frac{1}{\sqrt{2\pi}} \exp\left(-\frac{z^2}{2}\right)
    $$

### Ưu điểm:
- Mượt mà, không phụ thuộc vào việc chọn số lượng khoảng.
- Có thể điều chỉnh độ mịn của đồ thị bằng cách thay đổi băng thông $h$.

### Nhược điểm:
- Chi phí tính toán cao, đặc biệt với dữ liệu lớn.
