---
Created at: 2024-07-16
Source:
  - "[[Deep_learning_foundation.pdf#page=78|Deelp_learning_foundation, excercise 2.3]]"
---
Tích chập (convolution) của hai hàm số là một phép toán quan trọng trong toán học và xử lý tín hiệu, đặc biệt là trong học máy và xử lý ảnh. Để giải thích khái niệm này, chúng ta sẽ sử dụng hai hàm số $f(t)$ và $g(t)$. Tích chập của hai hàm số này được ký hiệu là $(f * g)(t)$ và được định nghĩa bởi công thức:

$$(f * g)(t) = \int_{-\infty}^{\infty} f(\tau) g(t - \tau) \, d\tau$$

Trong đó:

- $f(t)$ và $g(t)$ là hai hàm số thực hoặc phức.
- $\tau$ là biến tích phân giả định.
- $t$ là biến độc lập của hàm kết quả.

Để hiểu rõ hơn, chúng ta hãy xét các bước sau:

1. **Lấy một hàm số và lật ngược nó:** Giả sử $g(t)$, chúng ta tạo hàm $g(-\tau)$.
2. **Dịch chuyển hàm số đã lật:** Dịch chuyển $g(-\tau)$ thành $g(t - \tau)$.
3. **Nhân với hàm số ban đầu:** Nhân hàm số đã dịch chuyển với hàm số thứ hai $f(\tau)$.
4. **Tính tích phân:** Tính tích phân của kết quả nhân này trên toàn bộ không gian.

### Ví dụ Minh Họa

Giả sử hai hàm số đơn giản $f(t) = e^{-t}$ và $g(t) = u(t)$, trong đó $u(t)$ là hàm bước Heaviside. Tích chập của hai hàm số này là:

$$(f * g)(t) = \int_{-\infty}^{\infty} e^{-\tau} u(t - \tau) \, d\tau$$

Do hàm bước Heaviside $u(t - \tau)$ bằng 0 khi $t - \tau < 0$, nên giới hạn tích phân sẽ thay đổi:

$$(f * g)(t) = \int_{0}^{t} e^{-\tau} \, d\tau$$

Kết quả của tích phân này là:

$$(f * g)(t) = \left[ -e^{-\tau} \right]_{0}^{t} = 1 - e^{-t}$$

### Ứng Dụng của Tích Chập

- **Xử lý tín hiệu:** Tích chập được sử dụng để lọc tín hiệu, như làm mượt hoặc phát hiện biên trong hình ảnh.
- **Mạng nơ-ron tích chập (CNN):** Trong học sâu, CNN sử dụng tích chập để trích xuất đặc trưng từ dữ liệu hình ảnh.
- **Hệ thống điều khiển:** Tích chập mô tả đáp ứng của hệ thống với các tín hiệu đầu vào khác nhau.

### Kết luận

Tích chập là một phép toán mạnh mẽ và linh hoạt, được sử dụng rộng rãi trong nhiều lĩnh vực khoa học và kỹ thuật. Hiểu và áp dụng đúng tích chập có thể giúp giải quyết nhiều bài toán phức tạp trong thực tế.