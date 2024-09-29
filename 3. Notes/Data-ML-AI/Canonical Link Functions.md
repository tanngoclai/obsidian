---
Created at: 2024-08-06
Source:
---
# 1. Link functions
Hàm liên kết (link function) trong ngữ cảnh của các mô hình tuyến tính tổng quát (Generalized Linear Models - GLMs) là một hàm toán học được sử dụng để thiết lập mối quan hệ giữa giá trị kỳ vọng của biến đáp ứng (response variable) và hàm tuyến tính của các biến dự đoán (predictor variables).
### Tác dụng của hàm liên kết:

1. **Chuyển đổi giá trị kỳ vọng**:
    - Hàm liên kết chuyển đổi giá trị kỳ vọng của biến đáp ứng (thường ký hiệu là $\mu$) từ không gian phân phối của nó sang không gian tuyến tính của các biến dự đoán. Điều này rất hữu ích khi giá trị kỳ vọng không phải lúc nào cũng phù hợp để mô hình hóa trực tiếp.
    
2. **Tạo sự tương thích**:
    - Hàm liên kết cho phép sử dụng các mô hình tuyến tính để mô hình hóa các biến đáp ứng có phân phối không chuẩn. Bằng cách này, ta có thể áp dụng các phương pháp hồi quy tuyến tính cho các loại dữ liệu khác nhau.
    
3. **Đảm bảo giới hạn của biến đáp ứng**:
    - Một số hàm liên kết giúp đảm bảo rằng giá trị kỳ vọng $\mu$ nằm trong một khoảng hợp lý. Ví dụ, hàm liên kết logit đảm bảo rằng xác suất (giá trị kỳ vọng) nằm trong khoảng $[0, 1]$.
### Các loại hàm liên kết phổ biến:

1. **Hàm nhận dạng (Identity Link Function)**:
    - $\eta = g(\mu) = \mu$
    - Ứng dụng: Hồi quy tuyến tính (biến đáp ứng có phân phối chuẩn).

2. **Hàm logit (Logit Link Function)**:
    - $\eta = g(\mu) = \log\left(\frac{\mu}{1 - \mu}\right)$
    - Ứng dụng: Hồi quy logistic (biến đáp ứng nhị phân).

3. **Hàm log (Log Link Function)**:
    - $\eta = g(\mu) = \log(\mu)$
    - Ứng dụng: Hồi quy Poisson (biến đáp ứng là số đếm).

4. **Hàm nghịch đảo (Inverse Link Function)**:
    - $\eta = g(\mu) = \frac{1}{\mu}$
    - Ứng dụng: Các mô hình với biến đáp ứng có phân phối Gamma.

5. **Hàm probit (Probit Link Function)**:
    - $\eta = g(\mu) = \Phi^{-1}(\mu)$, với $\Phi$ là hàm phân phối chuẩn tích lũy.
    - Ứng dụng: Các mô hình hồi quy probit.

### Ví dụ minh họa:

Để cung cấp ví dụ chi tiết hơn về cách sử dụng hàm liên kết trong mô hình tuyến tính tổng quát (GLM), hãy xem xét hai ví dụ phổ biến: hồi quy logistic và hồi quy Poisson.
### Ví dụ 1: Hồi quy Logistic

Giả sử bạn muốn dự đoán xác suất của một sự kiện dựa trên một biến dự đoán $X$. Hồi quy logistic là phương pháp thích hợp để giải quyết bài toán này. Xác suất của sự kiện $Y = 1$ được mô hình hóa bằng một hàm logistic:
$$ P(Y = 1 \mid X) = \frac{1}{1 + e^{-\eta}} $$
Trong đó $\eta$ là một hàm tuyến tính của $X$:
$$ \eta = \beta_0 + \beta_1 X $$
$\beta_0$ và $\beta_1$ là các hệ số hồi quy cần ước lượng.

Hàm liên kết logit (logistic) được sử dụng để kết nối giữa giá trị kỳ vọng $\mu = P(Y = 1 \mid X)$ và hàm tuyến tính $\eta$:
$$ \eta = \log\left(\frac{\mu}{1 - \mu}\right) $$

Do đó, mô hình hồi quy logistic được xây dựng như sau:
$$ \log\left(\frac{\mu}{1 - \mu}\right) = \beta_0 + \beta_1 X $$

Trong đó:
- $\mu = P(Y = 1 \mid X)$ là xác suất dự đoán của sự kiện $Y = 1$.
- Hàm liên kết logit đảm bảo rằng giá trị dự đoán của xác suất $\mu$ nằm trong khoảng $[0, 1]$.

### Ví dụ 2: Hồi quy Poisson

Giả sử bạn muốn mô hình hóa số lần xảy ra của một sự kiện (ví dụ: số lần các cuộc gọi điện thoại nhận được trong một ngày) dựa trên các biến dự đoán $X$. Trong trường hợp này, phân phối Poisson thường được sử dụng vì nó phù hợp với các biến đếm.

Giả sử $Y$ là số lần xảy ra của sự kiện và có giá trị kỳ vọng $\mu$. Mô hình hồi quy Poisson giả định rằng:
$$ E(Y \mid X) = \mu $$
Và hàm liên kết log được sử dụng để kết nối giữa giá trị kỳ vọng $\mu$ và hàm tuyến tính $\eta$:
$$ \eta = \log(\mu) $$

Do đó, mô hình hồi quy Poisson có dạng:
$$ \log(\mu) = \beta_0 + \beta_1 X $$

Trong đó:
- $\mu$ là giá trị kỳ vọng của biến đáp ứng $Y$, tức là số lần xảy ra của sự kiện.
- Hàm liên kết log đảm bảo rằng $\mu$ là một số dương, phù hợp với tính chất của phân phối Poisson.
# 2. Canonical link functions
Dưới đây là một số ví dụ về các hàm liên kết chính tắc phổ biến và ứng dụng của chúng:

1. **Hàm liên kết Logit (Logit Link Function)**:
    - **Mô hình**: Hồi quy Logistic.
    - **Ứng dụng**: Dùng để mô hình hóa xác suất của biến nhị phân (binary outcome).
    - **Hàm liên kết**: $\eta = \log \left(\frac{\mu}{1 - \mu}\right)$, trong đó $\mu$ là xác suất của biến đáp ứng bằng 1.

2. **Hàm liên kết Log (Log Link Function)**:
    - **Mô hình**: Hồi quy Poisson.
    - **Ứng dụng**: Dùng cho các biến đáp ứng là số đếm (count data).
    - **Hàm liên kết**: $\eta = \log(\mu)$, trong đó $\mu$ là giá trị kỳ vọng của biến đáp ứng.

3. **Hàm liên kết Nhận dạng (Identity Link Function)**:
    - **Mô hình**: Hồi quy tuyến tính.
    - **Ứng dụng**: Dùng khi biến đáp ứng có phân phối chuẩn.
    - **Hàm liên kết**: $\eta = \mu$.

4. **Hàm liên kết Log-log (Log-log Link Function)**:
    - **Mô hình**: Dùng trong các mô hình tỷ lệ nguy cơ (hazard models) hoặc các biến nhị phân.
    - **Hàm liên kết**: $\eta = \log(-\log(1 - \mu))$.

Trong đó, $\eta$ là hàm tuyến tính của các biến độc lập và $\mu$ là giá trị kỳ vọng của biến đáp ứng.