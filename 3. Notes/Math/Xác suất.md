
## 1 Xác suất
- **Xác suất cơ bản:** 
	- Xác suất của một biến ngẫu nhiên rời rạc $p(x)$ phải thoả mãn: $$\sum_x p(x) = 1$$
	- Với biến ngẫu nhiên liên tục, hàm mật độ xác suất $p(x)$ phải thoả mãn: $$\int p(x) dx = 1$$.
- **Xác suất đồng thời:** Xác suất đồng thời của hai biến ngẫu nhiên $x$ và $y$ được ký hiệu là $p(x, y)$, và tổng của nó phải bằng 1.
- **Xác suất biên:** Xác suất của một biến có thể được tính từ xác suất đồng thời bằng cách tổng (hoặc tích phân) theo các biến còn lại.
    - Rời rạc: $p(x) = \sum_y p(x, y)$
    - Liên tục: $p(x) = \int p(x, y) dy$
- **Xác suất có điều kiện:** Xác suất của $x$ biết $y$ được ký hiệu là $p(x|y)$ và có thể được tính từ xác suất đồng thời $p(x, y)$.
    - $p(x|y) = \frac{p(x, y)}{p(y)}$
- **Quy tắc Bayes:** Dùng để tính xác suất có điều kiện theo cách khác.
    - $p(y|x) = \frac{p(x|y)p(y)}{p(x)}$
## 2 Một vài phân phối thường gặp
- **[[Phân phối chuẩn (Gaussian) | Phân phối chuẩn]] một chiều:** Được mô tả bởi kỳ vọng $\mu$ và phương sai $\sigma^2$. Hàm mật độ xác suất là: 
	- $\mu$ là trung bình (mean)
	- $\sigma$ là độ lệch chuẩn, $\sigma^2$ là phương sai
	$$p(x) = \frac{1}{\sqrt{2\pi\sigma^2}} \exp\left(-\frac{(x - \mu)^2}{2\sigma^2}\right)$$
![Biểu đồ phân phối Gaussian](https://upload.wikimedia.org/wikipedia/commons/thumb/8/8c/Standard_deviation_diagram.svg/1200px-Standard_deviation_diagram.svg.png)
- **[[Phân phối chuẩn (Gaussian) | Phân phối chuẩn]] nhiều chiều:** Tổng quát hoá từ phân phối chuẩn một chiều với vector kỳ vọng $\mu$ và ma trận hiệp phương sai $\Sigma$.
    $$p(x) = \frac{1}{(2\pi)^{D/2}|\Sigma|^{1/2}} \exp\left(-\frac{1}{2}(x - \mu)^T \Sigma^{-1} (x - \mu)\right)$$
- **Phân phối Beta:** Được định nghĩa trên đoạn $[0, 1]$ với hai tham số $\alpha$ và $\beta$.
 $$p(\lambda) = \frac{\Gamma(\alpha + \beta)}{\Gamma(\alpha)\Gamma(\beta)} \lambda^{\alpha-1} (1-\lambda)^{\beta-1}$$
- **Phân phối mũ**: thường được dùng để mô hình thời gian giữa các biến cố xảy ra theo một tỷ lệ trung bình là hằng số: $$ f(x|λ)=λe^{−λx}, x≥0 $$
	- ***Ví dụ:*** Giả sử trung bình có 10 cuộc gọi đến trung tâm hỗ trợ khách hàng mỗi giờ. Sự kiện này có thể được mô hình hóa bằng phân phối mũ với tham số $\lambda = 10$. Ta có thể tính toán xác suất rằng sẽ không có cuộc gọi nào trong 5 phút đầu tiên (1/12 giờ) như sau:

$$P(X>\frac{1}{12})=e^{−10⋅\frac{1}{12}}≈0.434$$
- **Phân phối Laplace**: thường được sử dụng để mô hình hóa dữ liệu có những sự thay đổi đột ngột hoặc có những điểm bất thường (outliers)
$$f(x|μ,\gamma)=\frac{1}{2\gamma}exp\left(-\frac{|x−μ|}{\gamma} \right)$$

## 3 Tính chất của các biến ngẫu nhiên

- **[[Kỳ vọng]] (Expectation):** Kỳ vọng của một biến ngẫu nhiên $x$ được tính bằng (ý nghĩa tương tự như trung bình):
    - Rời rạc: $E[x] = \sum_x x p(x)$
    - Liên tục: $E[x] = \int x p(x) dx$
- **[[Phương sai]] (Variance):** Đo lường độ phân tán của biến ngẫu nhiên quanh kỳ vọng: $$cov(x) = E[(x - E[x])^2] = E(x^2)−(E(x))^2$$ $$cov(x,y) = E(xy)−E(x)E(y)$$
 - **[[Ma trận hiệp phương sai]] (Covariance Matrix):** Đo lường sự tương quan giữa các biến ngẫu nhiên trong không gian nhiều chiều.
    - $\Sigma = E[(x - \mu)(x - \mu)^T]$

## 4 Ứng dụng trong Machine Learning
- **Quy tắc Bayes và xác suất có điều kiện** được sử dụng rộng rãi trong các mô hình phân loại, giúp dự đoán xác suất của các nhãn dựa trên các đặc trưng đầu vào.
- **Phân phối chuẩn** được sử dụng trong nhiều thuật toán thống kê và học máy để mô hình hoá dữ liệu liên tục.

---