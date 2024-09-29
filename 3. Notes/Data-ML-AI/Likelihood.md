## 1 Giới thiệu

- **Maximum Likelihood Estimation (MLE)**: Đây là phương pháp ước lượng các [[Tham số mô hình|tham số của mô hình]] dựa trên việc tối đa hóa xác suất của dữ liệu quan sát được. Mục tiêu của MLE là tìm tham số $\theta$ mà làm cho xác suất của dữ liệu $X$ lớn nhất.
- **Maximum A Posteriori (MAP)**: Phương pháp này cũng nhằm ước lượng các [[Tham số mô hình|tham số của mô hình]] nhưng có thêm thông tin tiên nghiệm về tham số. MAP tối đa hóa xác suất hậu nghiệm của tham số $\theta$.

## 2 Maximum Likelihood Estimation

- **Xác suất của dữ liệu**: Được cho bởi hàm likelihood $L(\theta) = p(X|\theta)$, tức là xác suất của dữ liệu $X$ biết tham số $\theta$.
- **Tối đa hóa hàm likelihood**: MLE tìm $\theta$ bằng cách giải phương trình tối đa hóa:
    - $\theta_{MLE} = \arg\max_{\theta} L(\theta) = \arg\max_{\theta} p(X|\theta)$
- **Hàm log-likelihood**: Trong thực tế, thường tính log của hàm likelihood để đơn giản hóa tính toán:
    - $\log L(\theta) = \sum_{i=1}^n \log p(x_i|\theta)$
- **Ví dụ**: Đối với phân phối chuẩn một chiều với dữ liệu $X = {x_1, x_2, ..., x_n}$, ta có thể ước lượng $\mu$ và $\sigma^2$ bằng cách tìm giá trị $\mu$ và $\sigma^2$ mà tối đa hóa hàm log-likelihood của phân phối chuẩn.

## 3 Maximum A Posteriori

- **Xác suất hậu nghiệm**: Được tính theo quy tắc Bayes, xác suất hậu nghiệm của $\theta$ biết dữ liệu $X$ là:
    - $p(\theta|X) = \frac{p(X|\theta) p(\theta)}{p(X)}$
- **Tối đa hóa xác suất hậu nghiệm**: MAP tìm $\theta$ bằng cách giải phương trình tối đa hóa:
    - $\theta_{MAP} = \arg\max_{\theta} p(\theta|X) = \arg\max_{\theta} \frac{p(X|\theta) p(\theta)}{p(X)}$
- **Ưu điểm**: MAP có thể sử dụng thông tin tiên nghiệm về tham số để cải thiện kết quả ước lượng, đặc biệt khi có ít dữ liệu hoặc dữ liệu nhiễu.

## 4 Tóm tắt

- **MLE**: Là phương pháp ước lượng phổ biến nhất trong thống kê, tối đa hóa xác suất của dữ liệu quan sát được mà không cần thông tin tiên nghiệm.
- **MAP**: Là phương pháp cải tiến của MLE, sử dụng thêm thông tin tiên nghiệm để tối đa hóa xác suất hậu nghiệm của tham số.