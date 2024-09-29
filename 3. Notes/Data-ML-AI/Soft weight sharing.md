---
Created at: 2024-08-15
Source:
---

# 1. Định nghĩa
**Soft weight sharing** là một kỹ thuật trong học sâu (deep learning) nhằm giảm số lượng tham số của mô hình bằng cách khuyến khích các trọng số (weights) trong mạng nơ-ron có giá trị gần nhau.

### Cách thức hoạt động:
- **Chia nhóm trọng số**: Trước hết, các trọng số của mô hình được chia thành nhiều nhóm. Mỗi nhóm có một giá trị trọng số trung bình, gọi là **trọng số chung**.
- **Regularization**: Trong quá trình huấn luyện, một thành phần regularization (phạt) được thêm vào hàm mất mát (loss function) để khuyến khích các trọng số cá nhân của mô hình tiến gần hơn với trọng số chung của nhóm mà nó thuộc về. Điều này giúp các trọng số trong cùng một nhóm có xu hướng "chia sẻ" giá trị với nhau một cách mềm dẻo (soft), thay vì bị ép buộc phải giống nhau hoàn toàn.

### Ưu điểm của soft weight sharing:
- **Giảm độ phức tạp của mô hình**: Bằng cách khuyến khích các trọng số chia sẻ giá trị, số lượng trọng số hiệu quả cần phải học được giảm xuống, giúp mô hình tổng quát hóa tốt hơn và tránh overfitting.
- **Tăng cường khả năng khái quát**: Do có ít tham số hơn, mô hình trở nên ít phụ thuộc vào dữ liệu huấn luyện cụ thể và có khả năng áp dụng tốt hơn trên dữ liệu mới.

### Ứng dụng:
Soft weight sharing thường được sử dụng trong các bài toán mà số lượng tham số quá lớn có thể dẫn đến overfitting hoặc khi ta muốn tăng khả năng tổng quát hóa của mô hình mà không cần phải giảm kích thước mạng nơ-ron.

# 2. Công thức và Ví dụ

**Soft weight sharing** được hiện thực bằng cách thêm một hàm phạt (regularization term) vào hàm mất mát của mô hình. Mục tiêu của kỹ thuật này là khuyến khích các trọng số của mạng nơ-ron có giá trị gần nhau, trong khi vẫn duy trì tính linh hoạt của mô hình.

### Công thức

Giả sử chúng ta có một mạng nơ-ron với tập hợp các trọng số $W = \{w_1, w_2, \dots, w_n\}$. Các trọng số này được chia thành $k$ nhóm, với mỗi nhóm $j$ có một trọng số chung $\mu_j$.

Hàm mất mát gốc là $L(\theta)$, trong đó $\theta$ là các tham số của mô hình, bao gồm cả các trọng số $W$.

Khi áp dụng soft weight sharing, chúng ta thêm vào một hàm phạt $R(W)$ dựa trên khoảng cách giữa các trọng số cá nhân $w_i$ và trọng số chung $\mu_j$ của nhóm tương ứng. Hàm phạt này thường có dạng:

$$
R(W) = \sum_{i=1}^{n} \sum_{j=1}^{k} \gamma_{ij} \cdot d(w_i, \mu_j)
$$

- $d(w_i, \mu_j)$ là khoảng cách giữa trọng số $w_i$ và trọng số chung $\mu_j$ của nhóm tương ứng. Khoảng cách này có thể được định nghĩa bằng nhiều cách, nhưng thường sử dụng là **khoảng cách Euclidean**: $d(w_i, \mu_j) = (w_i - \mu_j)^2$.
- $\gamma_{ij}$ là hệ số xác định trọng số $w_i$ thuộc về nhóm nào, thường được thiết kế sao cho tổng tất cả các $\gamma_{ij}$ bằng 1.

Hàm mất mát tổng hợp mới sẽ là:

$$
L'(\theta) = L(\theta) + \lambda \cdot R(W)
$$

Trong đó, $\lambda$ là hệ số regularization, kiểm soát mức độ quan trọng của hàm phạt.

### Ví dụ cụ thể

Giả sử bạn có một mạng nơ-ron đơn giản với 4 trọng số $w_1, w_2, w_3, w_4$ và bạn chia chúng thành 2 nhóm:

- Nhóm 1 với trọng số chung $\mu_1$ gồm $w_1, w_2$
- Nhóm 2 với trọng số chung $\mu_2$ gồm $w_3, w_4$

Giả sử hàm phạt $R(W)$ là:

$$
R(W) = (w_1 - \mu_1)^2 + (w_2 - \mu_1)^2 + (w_3 - \mu_2)^2 + (w_4 - \mu_2)^2
$$

Hàm mất mát cuối cùng sẽ là:

$$
L'(\theta) = L(\theta) + \lambda \left[ (w_1 - \mu_1)^2 + (w_2 - \mu_1)^2 + (w_3 - \mu_2)^2 + (w_4 - \mu_2)^2 \right]
$$

Trong quá trình huấn luyện, mô hình sẽ không chỉ cố gắng tối ưu hóa hàm mất mát $L(\theta)$ mà còn cố gắng giảm thiểu sự khác biệt giữa các trọng số $w_i$ và trọng số chung $\mu_j$ của nhóm tương ứng.

### Hiệu quả của Soft Weight Sharing

Giả sử bạn huấn luyện mô hình trên một tập dữ liệu cụ thể, kỹ thuật này sẽ giúp các trọng số tiến tới các giá trị chung (trọng số trung bình), giảm số lượng tham số thực sự độc lập, từ đó giúp mô hình tổng quát hóa tốt hơn.

Ví dụ, nếu bạn có một mạng nơ-ron sâu với hàng triệu trọng số, việc áp dụng soft weight sharing có thể giảm thiểu sự phụ thuộc vào từng trọng số cụ thể, thay vào đó, mô hình sẽ học được các đặc trưng tổng quát hơn, giúp mô hình hoạt động tốt hơn trên dữ liệu mới.