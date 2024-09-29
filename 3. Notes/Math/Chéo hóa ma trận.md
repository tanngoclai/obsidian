---
Date: 2024-09-29
Source: 
aliases:
  - Eigenbasis
  - Diagonal matrices
---

**Chéo hóa ma trận** là quá trình biến đổi một ma trận vuông thành một ma trận đường chéo, tức là một ma trận mà tất cả các phần tử ngoài đường chéo chính đều bằng 0. Điều này có nghĩa là, nếu một ma trận $A$ là ma trận vuông $n \times n$, chúng ta tìm một ma trận khả nghịch $P$ sao cho:

$$
P^{-1}AP = D
$$

trong đó $D$ là một ma trận đường chéo.

### Điều kiện để chéo hóa ma trận
Không phải ma trận nào cũng có thể chéo hóa. Để một ma trận có thể chéo hóa, cần thoả mãn các điều kiện sau:

1. **Tồn tại đủ số trị riêng**: Ma trận $A$ phải có đủ $n$ trị riêng khác nhau (hoặc bội số đại số của trị riêng bằng bội số hình học của trị riêng). Điều này có nghĩa là ma trận $A$ phải có đủ số vec-tơ riêng độc lập tuyến tính để tạo thành cơ sở.

2. **Độc lập tuyến tính của các vec-tơ riêng**: Các vec-tơ riêng tương ứng với các trị riêng phải độc lập tuyến tính để có thể tạo thành ma trận $P$.

### Các tính chất của chéo hóa ma trận

1. **Tương đương với việc biểu diễn ma trận theo cơ sở vec-tơ riêng**: Chéo hóa ma trận có thể được hiểu là việc biến đổi ma trận sang cơ sở các vec-tơ riêng. Ma trận đường chéo $D$ sẽ có các trị riêng của ma trận $A$ trên đường chéo.

2. **Trị riêng là các phần tử trên đường chéo**: Sau khi chéo hóa, các phần tử trên đường chéo của ma trận $D$ chính là các trị riêng của ma trận $A$.

3. **Dễ dàng tính toán lũy thừa của ma trận**: Nếu ma trận $A$ có thể chéo hóa thành ma trận đường chéo $D$, việc tính lũy thừa của ma trận $A$ trở nên đơn giản hơn. Cụ thể, $A^k = P D^k P^{-1}$, và lũy thừa của một ma trận đường chéo chỉ là lũy thừa của các phần tử trên đường chéo.

4. **Bảo toàn định thức và giá trị riêng**: Định thức của ma trận $A$ và ma trận đường chéo $D$ là như nhau, tức là $\text{det}(A) = \text{det}(D)$, và các trị riêng của $A$ cũng chính là các phần tử trên đường chéo của $D$.

Tóm lại, chéo hóa ma trận giúp đơn giản hóa các phép toán với ma trận, đặc biệt trong việc tính lũy thừa và phân tích các tính chất nội tại của ma trận đó, như trị riêng và vec-tơ riêng.

---
# Related
1. [[Trị riêng và vector riêng]]
2. [[Định thức]]
