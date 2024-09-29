---
Created at: 2024-07-23
Source:
---
![[Pasted image 20240723071400.png]]
### Mô tả:
- Histogram là phương pháp đơn giản, chia dữ liệu thành các khoảng (bins) và đếm số lượng điểm dữ liệu trong mỗi khoảng đó.

### Công thức:
- Mật độ ước lượng tại điểm $x$ được tính như sau:
  $$
  p(x) = \frac{n}{N \cdot \Delta x}
  $$
  Trong đó:
  - $n$ là số lượng điểm dữ liệu trong khoảng $x$.
  - $N$ là tổng số điểm dữ liệu.
  - $\Delta x$ là chiều rộng của mỗi khoảng.

### Ưu điểm:
- Dễ hiểu và dễ thực hiện.

### Nhược điểm:
- Kết quả phụ thuộc vào việc chọn số lượng khoảng (bins) và chiều rộng của mỗi khoảng.
- Không mượt mà, có thể dẫn đến hiện tượng "biên độ" (boundary effects).