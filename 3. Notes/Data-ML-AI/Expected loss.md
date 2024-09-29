---
Created at: 2024-07-26
Source:
  - "[[Deep_learning_foundation.pdf#page=144|Deep_learning_foundation - 4.3]]"
---

# 1. Sự đánh đổi giữa Bias và Variance (Bias-Variance Trade-off):
   - Khi xây dựng mô hình, mục tiêu là giảm thiểu sai số dự đoán tổng thể. Sai số này có thể được chia thành ba thành phần: bias, variance, và noise.
   - **Bias** đo lường sự khác biệt giữa giá trị trung bình của các dự đoán của mô hình và giá trị thực. Bias cao thường xảy ra khi mô hình quá đơn giản và không thể nắm bắt được xu hướng dữ liệu (underfitting).
   - **Variance** đo lường sự thay đổi của các dự đoán của mô hình khi áp dụng trên các tập dữ liệu khác nhau. Variance cao thường xảy ra khi mô hình quá phức tạp và nhạy cảm với nhiễu của dữ liệu huấn luyện (overfitting).
   - **Noise** là thành phần lỗi không thể giảm được do sự ngẫu nhiên trong dữ liệu.
   - Mô hình đơn giản có bias cao và variance thấp, trong khi mô hình phức tạp có bias thấp và variance cao.
# 2. Biểu diễn toán học:
   - Sai số dự đoán kỳ vọng có thể được biểu diễn như sau:
     $$
     E[L] = (bias)^2 + variance + noise
     $$
   - Trong đó:
     $$
     (bias)^2 = \int \left( \mathbb{E}_D[f(x;D)] - h(x) \right)^2 p(x) dx
     $$
     $$
     variance = \int \mathbb{E}_D \left[ \left( f(x;D) - \mathbb{E}_D[f(x;D)] \right)^2 \right] p(x) dx
     $$
     $$
     noise = \int \int \left( h(x) - t \right)^2 p(x, t) dx dt
     $$
   $$h(x) = \mathbb{E}\left[t|x \right] = \int tp(t|x)dt$$
   $$\mathbb{E}_D[f(x;D)] = \int f(x,D)p(D)dD $$
   - $t$ là giá trị thực tế
   - Nhân với $p(x)$ để thể hiện trọng số của xác suất.