---
Created at: 2024-07-22
Source:
---

# 1 Định nghĩa
Hàm Bessel thường xuất hiện trong các bài toán vật lý và kỹ thuật liên quan đến các phương trình vi phân, đặc biệt là trong các tình huống có đối xứng tròn.

Hàm Bessel giải quyết phương trình vi phân Bessel, mà phương trình này có dạng:

$$ x^2 \frac{d^2y}{dx^2} + x \frac{dy}{dx} + (x^2 - \nu^2) y = 0, $$

trong đó $\nu$ là tham số của hàm Bessel, còn  $x$ là biến độc lập.

Hàm Bessel được chia thành hai loại chính:

1. **Hàm Bessel bậc $\nu$ (hoặc hàm Bessel loại I):** Được ký hiệu là $J_\nu(x)$. Đây là giải pháp chính của phương trình Bessel có thể được định nghĩa qua tích phân:

   $$ J_\nu(x) = \frac{1}{\pi} \int_0^\pi \cos(x \sin \theta - \nu \theta) \, d\theta. $$

2. **Hàm Bessel loại II (hoặc hàm Bessel của thứ hai):** Được ký hiệu là $Y_\nu(x)$. Đây là giải pháp phụ của phương trình Bessel và có thể được định nghĩa qua hàm $J_\nu(x)$ và hàm logarithm:

   $$ Y_\nu(x) = \frac{J_\nu(x) \cos(\nu \pi) - J_{-\nu}(x)}{\sin(\nu \pi)}. $$

Hàm Bessel thường xuất hiện trong các bài toán liên quan đến sóng, truyền nhiệt và các vấn đề vật lý khác có đối xứng hình tròn. Chúng đặc biệt hữu ích trong việc mô tả các hiện tượng vật lý trong các không gian đối xứng hình tròn hoặc silinder.

# 2 Hàm Bassel bậc 0 của loại I

Công thức tổng quát của hàm Bessel bậc 0 là:

$$J_0(x) = \frac{1}{\pi} \int_0^\pi \cos(x \sin \theta) \, d\theta.$$

Hàm này có một số đặc điểm quan trọng:

- **Đối xứng:** $J_0(x)$ là hàm đối xứng với trục $y$, tức là $J_0(-x) = J_0(x)$.
- **Chu kỳ:** Hàm Bessel bậc 0 có dạng dao động và giảm dần khi $x$ tăng.
- **Giá trị tại $x = 0$:** $J_0(0) = 1$.

Hàm Bessel thường xuất hiện trong các phương trình vi phân liên quan đến các hệ thống có hình dạng đối xứng tròn, chẳng hạn như trong giải quyết các bài toán về sóng trong mặt phẳng tròn hoặc trong các bài toán về truyền nhiệt.