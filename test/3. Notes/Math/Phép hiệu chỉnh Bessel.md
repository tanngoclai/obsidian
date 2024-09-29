---
Created at: 2024-07-12
Source: 
tags:
---
# 1. Hiệu chỉnh Bessel
Hiệu chỉnh Bessel là một phương pháp được sử dụng để điều chỉnh độ chệch trong ước lượng phương sai của mẫu. Trong thống kê, khi chúng ta ước lượng phương sai của tổng thể từ một mẫu dữ liệu, nếu chúng ta sử dụng công thức chuẩn để tính phương sai, phương sai sẽ bị ước lượng thấp hơn thực tế. Điều này xảy ra vì mẫu chỉ là một phần của tổng thể và không bao quát được toàn bộ biến động của dữ liệu.

Để khắc phục điều này, hiệu chỉnh Bessel được áp dụng. Thay vì chia tổng bình phương sai lệch so với trung bình mẫu cho số lượng mẫu $n$, ta chia cho $n - 1$. Điều này giúp ước lượng phương sai không bị chệch.

Công thức của phương sai mẫu có hiệu chỉnh Bessel là:
$$s^2 = \frac{1}{n-1} \sum_{i=1}^{n} (x_i - \bar{x})^2$$

Trong đó:
- $n$ là kích thước mẫu.
- $x_i$ là từng giá trị dữ liệu trong mẫu.
- $\bar{x}$ là giá trị trung bình của mẫu.

Hiệu chỉnh Bessel được áp dụng trong nhiều trường hợp, đặc biệt là khi kích thước mẫu nhỏ, để đảm bảo rằng ước lượng phương sai gần đúng hơn với phương sai thật sự của tổng thể.

# 2. Bậc tự do trong phương sai
Bậc tự do trong phương sai là số lượng giá trị trong mẫu có thể thay đổi một cách độc lập khi tính toán một thống kê, trong khi vẫn duy trì các ràng buộc đã biết (chẳng hạn như trung bình của mẫu).

Cụ thể, khi tính phương sai mẫu, chúng ta cần biết trung bình mẫu $\bar{x}$. Trung bình mẫu này được tính từ tất cả các giá trị trong mẫu. Một khi chúng ta biết trung bình mẫu, chỉ $n-1$ giá trị trong mẫu có thể thay đổi độc lập, vì giá trị cuối cùng phải đảm bảo rằng tổng các giá trị chia cho số lượng giá trị bằng trung bình mẫu.

Ví dụ, giả sử chúng ta có một mẫu gồm 4 giá trị: $x_1, x_2, x_3, x_4$.

- Trung bình mẫu $\bar{x}$ được tính là:
$$\bar{x} = \frac{x_1 + x_2 + x_3 + x_4}{4}$$

- Một khi biết $\bar{x}$, chỉ có 3 giá trị $x_1, x_2, x_3$ có thể thay đổi tự do. Giá trị $x_4$ phải được tính sao cho tổng của tất cả 4 giá trị vẫn bằng $4 \cdot \bar{x}$.

Vì lý do này, số bậc tự do trong mẫu là $n-1$, với $n$ là số lượng giá trị trong mẫu. Điều này được thể hiện trong công thức tính phương sai mẫu:

$$s^2 = \frac{1}{n-1} \sum_{i=1}^{n} (x_i - \bar{x})^2$$

Trong đó:
- $n-1$ là số bậc tự do.
- $(x_i - \bar{x})^2$ là bình phương độ lệch của từng giá trị so với trung bình mẫu.

Tóm lại, bậc tự do trong phương sai phản ánh số lượng giá trị có thể thay đổi một cách độc lập, đảm bảo rằng ước lượng phương sai là không chệch.

# 3. Giải thích ý nghĩa hiệu chỉnh Bessel
Số bậc tự do là $n-1$ khi tính phương sai mẫu vì việc sử dụng giá trị trung bình mẫu $\bar{x}$ làm mất một bậc tự do. Khi tính phương sai mẫu, chúng ta muốn ước lượng phương sai của tổng thể từ một mẫu. Tuy nhiên, vì chúng ta sử dụng trung bình mẫu (một ước lượng của trung bình tổng thể), chúng ta cần điều chỉnh để đảm bảo rằng phương sai mẫu không bị chệch.

Để hiểu rõ hơn, hãy xem xét quá trình tính phương sai mẫu:

1. **Tính trung bình mẫu ($\bar{x}$)**:
   $$\bar{x} = \frac{1}{n} \sum_{i=1}^{n} x_i$$

2. **Tính tổng bình phương sai lệch so với trung bình mẫu**:
   $$\sum_{i=1}^{n} (x_i - \bar{x})^2$$

Khi tính trung bình mẫu, chúng ta đã sử dụng toàn bộ $n$ giá trị trong mẫu để xác định một giá trị duy nhất là $\bar{x}$. Điều này tạo ra một ràng buộc: tổng các sai lệch so với trung bình mẫu phải bằng 0. Do đó, chỉ có $n-1$ giá trị có thể thay đổi tự do, và giá trị cuối cùng phải tuân theo ràng buộc đó.

Vì chúng ta đã "mất" một bậc tự do khi tính trung bình mẫu, số bậc tự do còn lại cho việc tính phương sai là $n-1$. Để đảm bảo ước lượng phương sai không bị chệch, chúng ta cần chia tổng bình phương sai lệch cho $n-1$ thay vì $n$. Điều này đảm bảo rằng phương sai mẫu là một ước lượng không chệch của phương sai tổng thể.

Nếu chúng ta chia cho $n$ (thay vì $n-1$), ước lượng phương sai sẽ bị chệch thấp, tức là nhỏ hơn giá trị thực của phương sai tổng thể. Chia cho $n-1$ điều chỉnh sự thiên lệch này, làm cho phương sai mẫu trở thành một ước lượng tốt hơn cho phương sai tổng thể.