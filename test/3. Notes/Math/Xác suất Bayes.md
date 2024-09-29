---
Created at: 2024-07-15
Source:
  - "[[Deep_learning_foundation.pdf#page=74|Deelp_learning_foundation - 2.6]]"
---




# 1. Tham số mô hình
   - Tham số mô hình có thể được chọn bằng cách sử dụng ước lượng hợp lý tối đa (maximum likelihood), trong đó giá trị của tham số $w$ được chọn sao cho hàm hợp lý $p(D|w)$ là lớn nhất.
   - Xác suất hậu nghiệm cho $w$ sau khi quan sát dữ liệu $D$ được tính bằng định lý Bayes: 
     $$ p(w|D) = \frac{p(D|w)p(w)}{p(D)} $$
$$− ln \ p(w|D) = − ln \ p(D|w) − ln \ p(w) + ln \ p(D)$$