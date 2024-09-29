---
Date: 2024-09-22
Source: 
aliases:
  - SVD
---
# 1. Định nghĩa
Một ma trận $A_{m×n}$ **bất kỳ** đều có thể phân tích thành dạng: $$A_{m×n} = U_{m×n}Σ_{m×n}V_{m×n}^T$$ 
Trong đó:
- $U, V$ là các ma trận trực giao, $U$ gồm các [[Trị riêng và vector riêng|vector riêng]] của $AA^T$,  $V$ gồm các [[Trị riêng và vector riêng|vector riêng]] của $A^TA$,
- $Σ$ là một ma trận đường chéo cùng kích thước với $A$. 
- Các phần tử trên đường chéo chính của $Σ$ là không âm và được theo thứ tự giảm dần $σ_1 ≥ σ_2 ≥ · · · ≥ σ_r ≥ 0 = 0 = · · · = 0$. Số lượng các phần tử khác $0$ trong $Σ$ chính là rank của ma trận $A$: $r = rank(A)$, $\sigma_i$ là căn bậc 2 của [[Trị riêng và vector riêng|trị riêng]] của $A^TA$.

Chứng minh: https://goo.gl/TdtWDQ

![[Pasted image 20240925065807.png]]