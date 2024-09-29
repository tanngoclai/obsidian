---
Created at: 2024-08-06
Source:
  - "[[Deep_learning_foundation.pdf#page=200|Deep_learning_foundation - 6,2,3]]"
---

# 1. Tổng quan

Các hàm kích hoạt cho các đơn vị ẩn trong mạng nơron được chọn dựa trên tính khả vi của chúng, cho phép một loạt các khả năng. Các lựa chọn phổ biến bao gồm các hàm tuyến tính và phi tuyến, mỗi loại có đặc điểm và ứng dụng riêng.

# 2. Hàm kích hoạt tuyến tính

Hàm kích hoạt tuyến tính chỉ đơn giản là xuất ra giá trị đầu vào. Mặc dù đơn giản, mạng chỉ sử dụng hàm kích hoạt tuyến tính có thể được giảm xuống một lớp duy nhất, vì sự kết hợp của các biến đổi tuyến tính vẫn là tuyến tính. Điều này làm cho các mạng tuyến tính thuần túy ít biểu diễn hơn so với các mạng sử dụng hàm kích hoạt phi tuyến.

# 3. Hàm kích hoạt phi tuyến

Các hàm kích hoạt phi tuyến rất quan trọng vì chúng cho phép mạng nơron mô hình hóa các hàm phức tạp. Các hàm kích hoạt phi tuyến phổ biến bao gồm:

## 3.1. Hàm sigmoid logistic
   $$
   \sigma(a) = \frac{1}{1 + e^{-a}}
   $$
   Hàm sigmoid logistic được sử dụng rộng rãi trong các mạng nơron sớm. Nó nén các giá trị đầu vào về khoảng từ 0 đến 1.

## 3.2. Hàm tangent hyperbolic (tanh)
   $$
   \tanh(a) = \frac{e^a - e^{-a}}{e^a + e^{-a}}
   $$
   Hàm tanh xuất ra các giá trị từ -1 đến 1, cung cấp gradient mạnh hơn và hội tụ nhanh hơn so với hàm sigmoid logistic.

## 3.3. Hàm ReLU (ReLU)
   $$
   \text{ReLU}(a) = \max(0, a)
   $$
   ReLU phổ biến trong các mạng nơron hiện đại do tính đơn giản và hiệu quả của nó trong việc giảm thiểu vấn đề gradient biến mất. Nó xuất ra giá trị 0 cho đầu vào âm và giá trị đầu vào cho đầu vào dương.

## 3.4. Softplus
   $$
   \text{Softplus}(a) = \log(1 + e^a)
   $$
   Hàm softplus là một xấp xỉ mượt mà của ReLU.
