---
Date: 2024-09-16
Source: 
aliases:
  - Tích vô hướng
---
Cho 2 vector:
$$
\vec{a} = (a_1, a_2, \dots, a_n), \quad \vec{b} = (b_1, b_2, \dots, b_n)
$$

Tích vô hướng được định nghĩa là:

$$
\vec{a} \cdot \vec{b} = |\vec{a}| |\vec{b}| \cos(\theta)
$$

Định nghĩa này giúp đo mối quan hệ giữa hai vector, đặc biệt là góc $\theta$ giữa chúng. Tuy nhiên, việc tính toán này trực tiếp trong các trường hợp thực tế là không dễ dàng, do phải tính cả độ dài của vector và góc giữa chúng.

Ngoài ra, tích vô hướng của hai vector $\vec{a}$ và $\vec{b}$  có thể tính bằng công thức:

$$
\vec{a} \cdot \vec{b} = a_1b_1 + a_2b_2 + \dots + a_nb_n
$$

# 1. Ý tưởng chính
Tích vô hướng $\vec{a} \cdot \vec{b}$  biểu diễn phép chiếu vector $\vec{a}$ lên đường thẳng đi qua vector $\vec{b}$, sau đó nhân theo tỉ lệ.

Việc chiếu này tương đương với đổi hệ tọa độ của vector $\vec{a}$, từ nhiều chiều thành 1 chiều. đổi hệ tọa độ bằng cách chiếu các điểm trong không gian nhiều chiều lên trục tọa độ đi qua vector $\vec{b}$.

Đây là nguyên nhân khiến kết quả của tích vô hướng là 1 số (do tính trên hệ tọa độ 1 chiều).

# 2. Biến đổi toán học
Giả sử trên không gian 2 chiều (nhiều chiều hơn cũng tương tự), ta có 2 vector đơn vị $\hat{i} = (1,0)$ và $\hat{j} = (0,1)$

Biển diễn 2 vector: $\vec{a} = x . \hat{i} + y . \hat{j}$  và  $\vec{b} = z . \hat{i} + t . \hat{j}$

Khi đó: $$\vec{a} \cdot \vec{b} = xz . \hat{i}^2 + yt . \hat{j}^2 + (xt+yz) . \hat{i} . \hat{j} = xz + yt$$ 