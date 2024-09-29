---
Created at: 2024-07-14
Source:
  - "[[Deep_learning_foundation.pdf#page=62|Deelp_learning_foundation - 2.4]]"
---
# 1. Biến đổi một biến số:
- Khi biến số x được biến đổi phi tuyến tính thành y bằng hàm $x = g(y)$, mật độ xác suất $p_x(x)$ sẽ chuyển thành $p_y(y)$.
- Công thức để biến đổi mật độ là:
  $$p_y(y) = p_x(x) \left| \frac{dx}{dy} \right| = p_x(g(y)) \left| \frac{dg}{dy} \right|$$

# 2. Hệ quả của biến đổi:
- Đỉnh của mật độ xác suất phụ thuộc vào biến số được chọn. Nếu hàm f(x) có cực đại tại $x̂$, thì đỉnh tương ứng của $\tilde{f}(y)$ sẽ nằm tại giá trị $ŷ$ được xác định bằng cách biến đổi trở lại x.
- Tuy nhiên, khi thực hiện biến đổi phi tuyến tính, vị trí của đỉnh mật độ không còn bảo toàn. Đối với biến đổi tuyến tính, vị trí của cực đại sẽ bảo toàn.

# 3. Ví dụ minh họa:
- Xem xét biến đổi Gaussian $p_x(x)$ thành $y$ qua hàm:
  $$x = g(y) = \ln(y) - \ln(1 - y) + 5$$
  và ngược lại:
  $$y = g^{-1}(x) = \frac{1}{1 + \exp(-x + 5)}$$
  Khi biến đổi $p_x(x)$ như một hàm của x, ta được đường cong màu xanh. Tuy nhiên, mật độ $p_y(y)$ theo công thức trên sẽ là đường cong màu tím [[Deep_learning_foundation.pdf#page=64|Deelp_learning_foundation, p.44]]

# 4. Biến đổi đa biến:
- Kết quả trên được mở rộng cho các mật độ định nghĩa trên nhiều biến số bằng cách sử dụng ma trận Jacobian, với công thức:
  $$p_y(y) = p_x(x) \left| \det J \right|$$
  trong đó J là [[Ma trận Jacobian]], biểu diễn các đạo hàm riêng phần của $g(y)$.

Biến đổi mật độ có thể giúp ta thu được mật độ mới từ một mật độ cố định bằng cách thay đổi biến số phi tuyến tính.