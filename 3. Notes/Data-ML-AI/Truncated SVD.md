---
Date: 2024-09-29
Source: 
aliases:
---
# 1. Định nghĩa

Giả sử bạn có một ma trận $A$ kích thước $m \times n$ và phân tích SVD đầy đủ của nó là:

$$
A = U \Sigma V^T
$$

Trong đó:

- $U$ là ma trận trực giao kích thước $m \times m$,
- $\Sigma$ là ma trận đường chéo $m \times n$, chứa các giá trị kỳ dị (singular values), sắp xếp theo thứ tự giảm dần: $\sigma_1 \geq \sigma_2 \geq \dots \geq \sigma_r \geq 0$, trong đó $r = \min(m, n)$ ($r$ = $rank(A)$)
- $V^T$ là ma trận trực giao kích thước $n \times n$.

Trong **Truncated SVD**, thay vì giữ toàn bộ các ma trận này, ta chỉ giữ lại $k$ giá trị kỳ dị lớn nhất và tương ứng với các cột đầu tiên của $U$ và $V$, dẫn đến một phiên bản rút gọn của SVD:

$$
A_k \approx U_k \Sigma_k V_k^T
$$

Trong đó:

- $U_k$ là ma trận $m \times k$,
- $\Sigma_k$ là ma trận đường chéo $k \times k$,
- $V_k^T$ là ma trận $k \times n$.

Với $k$ là số lượng giá trị kỳ dị lớn nhất mà bạn muốn giữ lại, và thông thường $k \ll \min(m, n)$.

Sai số của **Truncated SVD** (SVD rút gọn) phát sinh khi ta chỉ giữ lại một số lượng giới hạn các giá trị kỳ dị lớn nhất của ma trận gốc, và loại bỏ các giá trị kỳ dị nhỏ hơn. Việc này dẫn đến việc xấp xỉ ma trận ban đầu bởi một ma trận hạng thấp hơn, và do đó có thể gây ra sai số. Tuy nhiên, theo lý thuyết, truncated SVD mang lại xấp xỉ tốt nhất cho ma trận theo cả chuẩn Frobenius và chuẩn 2.

# 2. Sai số của Truncated SVD

Khi áp dụng **Truncated SVD** với $k$ giá trị kỳ dị lớn nhất, ta có:

$$
A_k = U_k \Sigma_k V_k^T
$$

1. Sai số trong **Chuẩn Frobenius**: Sai số xấp xỉ theo chuẩn Frobenius, hay còn gọi là sai số bình phương của các phần tử ma trận, được tính bằng:

$$
\| A - A_k \|_F = \sqrt{\sum_{i=k+1}^{r} \sigma_i^2}
$$

Nghĩa là sai số bình phương tổng của ma trận xấp xỉ $A_k$ so với ma trận gốc $A$ chính là tổng bình phương các giá trị kỳ dị bị loại bỏ, tức là từ $\sigma_{k+1}$ đến $\sigma_r$.

2. **Chuẩn 2 (Spectral norm)**: Sai số xấp xỉ trong chuẩn 2, hay còn gọi là chuẩn phổ (spectral norm), được tính bằng:

$$
\| A - A_k \|_2 = \sigma_{k+1}
$$

Nghĩa là sai số lớn nhất (sai số phổ) giữa ma trận gốc và ma trận xấp xỉ bằng giá trị kỳ dị lớn nhất bị loại bỏ, tức là $\sigma_{k+1}$.

### Tính chất của sai số

- **Xấp xỉ tốt nhất**: Theo định lý Eckart-Young, truncated SVD cung cấp xấp xỉ hạng thấp tốt nhất cho ma trận $A$ về chuẩn Frobenius và chuẩn 2. Điều này có nghĩa là nếu bạn chỉ giữ lại $k$ thành phần chính của SVD, truncated SVD sẽ cho bạn xấp xỉ tốt nhất có thể trong các ma trận có hạng $k$.

- **Giảm dần độ chính xác**: Khi giảm số lượng giá trị kỳ dị $k$, sai số xấp xỉ sẽ tăng lên. Tuy nhiên, trong nhiều trường hợp thực tế, các giá trị kỳ dị nhỏ thường không chứa nhiều thông tin quan trọng, vì vậy việc loại bỏ chúng không gây ra sự suy giảm đáng kể về chất lượng của ma trận xấp xỉ.

### Ví dụ về sai số trong thực tế

Nếu các giá trị kỳ dị của một ma trận $A$ giảm nhanh chóng (ví dụ: $\sigma_1 \gg \sigma_2 \gg \dots \gg \sigma_r$), thì việc giữ lại chỉ một vài giá trị kỳ dị lớn nhất có thể vẫn giữ được phần lớn thông tin quan trọng của ma trận, và sai số xấp xỉ sẽ nhỏ.

Tuy nhiên, nếu các giá trị kỳ dị giảm chậm hoặc phân bố đồng đều, việc giữ lại ít giá trị kỳ dị có thể dẫn đến sai số xấp xỉ lớn hơn và mất nhiều thông tin.

### Tóm tắt

- **Sai số trong truncated SVD** là tổng bình phương các giá trị kỳ dị bị loại bỏ (đối với chuẩn Frobenius) hoặc giá trị kỳ dị lớn nhất bị loại bỏ (đối với chuẩn 2).
- **Truncated SVD** cung cấp xấp xỉ hạng thấp tốt nhất cho ma trận theo cả hai chuẩn Frobenius và chuẩn 2.
- Trong thực tế, sai số phụ thuộc vào tốc độ suy giảm của các giá trị kỳ dị: nếu các giá trị kỳ dị giảm nhanh, sai số có thể nhỏ ngay cả khi chỉ giữ lại vài giá trị kỳ dị lớn nhất.
---
# Related
1. [[Singular Value Decomposition|SVD]]
