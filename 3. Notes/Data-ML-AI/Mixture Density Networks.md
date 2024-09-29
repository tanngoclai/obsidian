---
Created at: 2024-08-07
Source:
  - "[[Deep_learning_foundation.pdf#page=216|Deep_learning_foundation, p.198]]"
---
# Conditional mixture distributions
Có thể kết hợp nhiều dạng mô hình xác suất để biểu diễn các phân phối phức tạp.
Ví dụ:

   - Sử dụng các thành phần Gaussian cho mô hình, biểu thức cho phân phối có điều kiện $p(t|x)$ là: $$
     p(t|x) = \sum_{k=1}^{K} \pi_k(x) N(t|\mu_k(x), \sigma_k^2(x))
     $$
   - Các tham số của mô hình hỗn hợp, bao gồm các hệ số trộn $\pi_k(x)$, các trung bình $\mu_k(x)$, và phương sai $\sigma_k^2(x)$, được điều khiển bởi đầu ra của mạng nơron.
   - Các hệ số trộn phải thỏa mãn điều kiện tổng bằng 1 và giá trị nằm trong khoảng từ 0 đến 1, điều này có thể đạt được bằng cách sử dụng các đầu ra softmax:$$
     \pi_k(x) = \frac{\exp(a_{\pi_k})}{\sum_{l=1}^{K} \exp(a_{\pi_l})}
     $$
   - Phương sai được biểu diễn thông qua các hàm số mũ: $$
     \sigma_k(x) = \exp(a_{\sigma_k})
     $$
   - Trung bình có thể được biểu diễn trực tiếp bằng các đầu ra của mạng: $$
     \mu_{kj}(x) = a_{\mu_{kj}}
     $$