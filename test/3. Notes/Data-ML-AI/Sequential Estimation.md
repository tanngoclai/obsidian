---
Created at: 2024-07-21
Source:
  - "[[Deep_learning_foundation.pdf#page=104|Deelp_learning_foundation - 3.2.8]]"
---
# 1. Tổng quan 
Phương pháp ước lượng tuần tự là một lựa chọn khác so với phương pháp ước lượng lớn nhất (maximum likelihood estimation) truyền thống (thường được gọi là phương pháp batch - xử lý toàn bộ dữ liệu cùng một lúc).
# 2. Ưu điểm 
Phương pháp tuần tự cho phép xử lý từng điểm dữ liệu một và sau đó loại bỏ chúng. Điều này rất quan trọng đối với các ứng dụng trực tuyến (online applications) và dữ liệu lớn khi xử lý batch toàn bộ điểm dữ liệu cùng một lúc là không khả thi.
# 3. Công thức ước lượng tuần tự: 
Công thức cho ước lượng lớn nhất của giá trị trung bình (mean) $\mu_{ML}$ được cập nhật khi dựa trên $N$ quan sát. Công thức này có thể tách riêng đóng góp của điểm dữ liệu cuối cùng $x_N$ và biểu diễn dưới dạng:
$$ \mu_{ML}^{(N)} = \frac{1}{N} x_N + \frac{N-1}{N} \mu_{ML}^{(N-1)} = \mu_{ML}^{(N-1)} + \frac{1}{N} (x_N - \mu_{ML}^{(N-1)}) $$
# 4. Giải thích
Kết quả này có thể được diễn giải rằng sau khi quan sát $N-1$ điểm dữ liệu, chúng ta ước lượng $\mu$ bởi $\mu_{ML}^{(N-1)}$. Khi quan sát điểm dữ liệu $x_N$, ước lượng được cập nhật bằng cách di chuyển ước lượng cũ một lượng nhỏ, tỷ lệ với $\frac{1}{N}$, theo hướng của sai số $(x_N - \mu_{ML}^{(N-1)})$.


Tóm lại, phương pháp ước lượng tuần tự cho phép cập nhật liên tục ước lượng khi nhận thêm dữ liệu mới, phù hợp cho các ứng dụng yêu cầu xử lý dữ liệu trực tuyến và dữ liệu lớn.