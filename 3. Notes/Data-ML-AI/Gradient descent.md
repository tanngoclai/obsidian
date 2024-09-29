---
Created at: 2024-08-08
Source:
  - "[[Deep_learning_foundation.pdf#page=226|Deep_learning_foundation, p.209]]"
---
# 1. Xấp xỉ cục bộ (Local quadratic approximation)
## 1.1. [[Ma trận Hessian]] và Gradient:
   - Xét điểm $\hat{w}$ gần điểm cực tiểu của hàm lỗi $E$.
   - Gradient của hàm lỗi tại $\hat{w}$ được ký hiệu là $b$, tức là:
     $$
     b \equiv \nabla E|_{w=\hat{w}}
     $$
   - Ma trận Hessian $H(\hat{w})$ là ma trận các đạo hàm bậc hai tại $\hat{w}$:
     $$
     H(\hat{w}) = \nabla\nabla E(w)|_{w=\hat{w}}
     $$

## 1.2. Xấp xỉ bậc hai cục bộ:
   - Nếu điểm $\hat{w}$ là cực tiểu của hàm lỗi, thì biểu thức bậc hai cho hàm lỗi là:
     $$
     E(w) = E(\hat{w}) + \frac{1}{2}(w - \hat{w})^T H (w - \hat{w})
     $$
   - Các đường đồng mức của hàm lỗi là các elip mà các trục của chúng tương ứng với các vector riêng của ma trận Hessian.

## 1.3. Giải thích hình học:
   - Phương trình giá trị riêng của ma trận Hessian là:
     $$
     Hui = \lambda_i ui
     $$
     trong đó $ui$ là các vector riêng và $\lambda_i$ là các giá trị riêng.
   - Nếu tất cả các giá trị riêng $\lambda_i$ đều dương, thì điểm $\hat{w}$ là cực tiểu cục bộ của hàm lỗi. Nếu có giá trị riêng âm, $\hat{w}$ là điểm yên ngựa.

## 1.4. Đổi hệ tọa độ:
   - Biểu diễn $w - \hat{w}$ dưới dạng tổ hợp tuyến tính của các vector riêng:
     $$
     w - \hat{w} = \sum_i \alpha_i ui
     $$
   - Hàm lỗi có thể được viết dưới dạng:
     $$
     E(w) = E(\hat{w}) + \frac{1}{2} \sum_i \lambda_i \alpha_i^2
     $$
   - Độ tăng của hàm lỗi phụ thuộc vào giá trị $\lambda_i$: nếu dương thì tăng, nếu âm thì giảm.

---
# 2. Gradient descent optimize
## 2.1. Batch gradient descent
- Trong phương pháp này, hàm lỗi xác định theo training set, nên mỗi step gradient đều phải xử lí trên toàn bộ dữ liệu (nên gọi là batch methods).
- Chọn trọng số theo hướng gradient âm: 
$$w(τ ) = w^{(τ −1)} − η∇E(w^{(τ −1)})$$
	Trong đó $η$ là learning rate  
## 2.2. Stochastic gradient descent
- Đặc điểm và cách hoạt động
	- Hoạt động trên từng điểm dữ liệu một cách tuần tự, thay vì trên toàn bộ tập dữ liệu như trong batch gradient descent.
	- Trọng số được cập nhật bằng công thức:
	     $$
	     w^{(\tau)} = w^{(\tau-1)} - \eta \nabla E_n(w^{(\tau-1)})
	     $$
	     trong đó $\eta$ là tham số learning rate, và $E_n(w)$ là hàm lỗi cho từng điểm dữ liệu.
	
	- **Khả năng thoát khỏi cực tiểu cục bộ:** Do tính chất ngẫu nhiên, SGD có khả năng thoát khỏi các điểm cực tiểu cục bộ, mà các phương pháp khác có thể bị mắc kẹt.

		![[Pasted image 20240808071057.png]]

- **Hạn chế và cách khắc phục:**
	- Gradient tính từ một điểm dữ liệu có thể rất nhiễu, dẫn đến độ chính xác của hướng di chuyển kém.
	- Một cách khắc phục là sử dụng mini-batches, tức là lấy một nhóm nhỏ điểm dữ liệu để tính toán gradient, giúp giảm độ nhiễu và tăng hiệu quả.
## 2.3. Mini-batches
- Thay vì sử dụng toàn bộ tập dữ liệu hoặc một mẫu duy nhất để tính toán gradient, phương pháp Mini-batch Gradient Descent sử dụng một nhóm nhỏ các mẫu, gọi là mini-batch. Điều này giúp cân bằng giữa Batch Gradient Descent (sử dụng toàn bộ dữ liệu) và Stochastic Gradient Descent (sử dụng một mẫu duy nhất).
- **Lợi ích của Mini-batches**:
    - **Hiệu quả Tính toán**: Việc tính toán trên mini-batches có thể được tối ưu hóa bằng cách sử dụng các công cụ tính toán song song, đặc biệt trên GPU.
    - **Hội tụ nhanh hơn**: Mini-batches giúp cập nhật các tham số thường xuyên hơn so với Batch Gradient Descent, điều này có thể dẫn đến hội tụ nhanh hơn.
    - **Ổn định hơn so với SGD**: So với Stochastic Gradient Descent, mini-batches cung cấp một sự ổn định hơn trong việc ước lượng gradient và giúp giảm sự dao động trong việc cập nhật tham số.
- **Kích thước Mini-batch**: Việc chọn kích thước của mini-batch là một yếu tố quan trọng và thường được xác định thông qua thử nghiệm. Kích thước phổ biến thường là 32, 64, hoặc 128, tùy thuộc vào kích thước tập dữ liệu và khả năng tính toán.
		![[Pasted image 20240808071759.png]]


---
# 3. Parameter initialization
Khởi tạo tham số trong các thuật toán học lặp lại như gradient descent là rất quan trọng vì nó ảnh hưởng đến thời gian hội tụ và khả năng tổng quát hóa của mô hình đã được huấn luyện. Đặc biệt, việc khởi tạo có thể phá vỡ tính đối xứng, giúp tránh các đơn vị ẩn tính toán cùng một hàm và trở nên dư thừa. Để phá vỡ tính đối xứng, các tham số nên được khởi tạo ngẫu nhiên từ một phân phối nhất định.
## 3.1. Phân phối Khởi tạo
- Các trọng số thường được khởi tạo từ phân phối đều trong khoảng $[-ε, ε]$ hoặc Gaussian với $N(0, \epsilon^2)$. 
- Giá trị của $\epsilon$ là rất quan trọng, và một cách khởi tạo phổ biến là *He initialization*. Đối với một lớp $l$ sử dụng hàm kích hoạt [[Activation function#3.3. Hàm ReLU (ReLU)|ReLU]], nếu các trọng số được khởi tạo từ Gaussian $N(0, ε^2)$, và đầu ra của các đơn vị ở lớp $l-1$ có phương sai $\lambda^2$, thì:

$$
E[a_i^{(l)}] = 0
$$

$$
\text{var}[z_j^{(l)}] = \frac{M}{2}ε^2λ^2
$$

Để duy trì phương sai không đổi qua các lớp, lựa chọn tiêu chuẩn cho độ lệch chuẩn của Gaussian dùng để khởi tạo trọng số là:

$$
ε = \sqrt{\frac{2}{M}}
$$

trong đó $M$ là số đầu vào tới một đơn vị.

## 3.2. Khởi tạo Bias
Các tham số bias thường được đặt ở giá trị dương nhỏ để đảm bảo rằng hầu hết các pre-activation ban đầu đều hoạt động. Điều này hữu ích cho ReLU, giúp duy trì gradient không bằng 0 trong quá trình học.

## 3.3. Kỹ thuật Khởi tạo Khác
Ngoài ra, khởi tạo có thể thực hiện bằng cách sử dụng các giá trị từ việc huấn luyện mô hình trên một tác vụ khác hoặc thông qua các kỹ thuật huấn luyện không giám sát, thuộc phạm trù các kỹ thuật học chuyển giao.

# 4. Convergence (hội tụ)
Delta của vector trọng số:
$$\Delta w = \sum^{}_{i}\Delta\alpha_{i}u_{i}$$
Dùng ma trận Hessian với vector riêng $\lambda_i$ :
$$\Delta\alpha_{i} = -\eta \lambda_{i} \alpha_{i} \leftrightarrow \alpha_{i}^{new} = (1-\eta \lambda_{i})\alpha_{i}^{old}$$ 
$$\to \alpha_{i}^{(T)} = (1-\eta \lambda_{i})^T\alpha_{i}^{(0)}$$
## 4.1 Momentum
- Ý tưởng chính để áp dụng momentum trong gradient descent là:
	1. Mô phỏng quán tính: Momentum mô phỏng quán tính của một vật chuyển động. Nó giúp thuật toán "tăng tốc" theo các hướng ổn định và "giảm tốc" khi gặp dao động.
	2. Tích lũy các cập nhật trước đó: Momentum lưu trữ một phần của cập nhật trước đó (thông qua tham số μ) và thêm nó vào cập nhật hiện tại. Điều này tạo ra một "ký ức" về các bước di chuyển trước đó.
	3. Làm mượt dao động: Trong các vùng có độ cong cao của hàm mất mát, gradient descent thường dao động qua lại. Momentum giúp làm mượt những dao động này bằng cách trung bình hóa các cập nhật qua thời gian.
	4. Tăng tốc hội tụ: Trong các vùng có độ dốc thấp (như thung lũng dài), momentum giúp tăng tốc độ hội tụ bằng cách tích lũy các bước nhỏ theo cùng một hướng.
	5. Vượt qua các điểm yên ngựa: Momentum có thể giúp thuật toán vượt qua các điểm yên ngựa (saddle points) bằng cách duy trì một lượng động lượng đủ lớn để không bị mắc kẹt.
	6. Điều chỉnh kích thước bước: Momentum tự động điều chỉnh kích thước bước dựa trên lịch sử gradient. Nó tăng kích thước bước khi các gradient liên tiếp cùng hướng và giảm khi chúng đổi hướng.
	7. Giảm sự phụ thuộc vào learning rate: Bằng cách sử dụng thông tin từ các bước trước, momentum giúp giảm độ nhạy cảm của thuật toán đối với việc chọn learning rate.
- Công thức: 
$$\Delta w^{(T)} = - \eta \nabla E(w^{(T)}) + \mu \Delta w^{(T-1)}$$
		Với $\mu$ là tham số momentum, thường chọn 0.9
- Minh họa thuật toán
![[Pasted image 20240811084339.png]]

## 4.2 Learning rate schedule
- Mục đích:
    - Điều chỉnh learning rate $\eta$ theo thời gian trong quá trình huấn luyện.
- Lý do:
    - $\eta$ lớn ban đầu giúp học nhanh
    - $\eta$ nhỏ dần giúp ổn định và hội tụ tốt hơn
- Các cách schedule phổ biến: 
	- Tuyến tính: $$ \eta^{(\tau)} = (1 - \frac{\tau}{K})\eta^{(0)} + \frac{\tau}{K}\eta^{(K)} $$
	- Lũy thừa: $$ \eta^{(\tau)} = \frac{\eta^{(0)}}{(1 + \tau/s)^c}$$
	- Hàm mũ: $$ \eta^{(\tau)} = \eta^{(0)}\cdot c^{\tau/s} $$ Trong đó:
		- $\tau$: bước lặp hiện tại
		- $K$, $s$, $c$: hyperparameters cần điều chỉnh
		- $\eta^{(0)}$: learning rate ban đầu
		- $\eta^{(K)}$: learning rate cuối cùng (cho lịch trình tuyến tính)
- Ưu điểm:
    - Cải thiện tốc độ hội tụ
    - Giúp tránh bị mắc kẹt ở cực tiểu cục bộ
    - Tăng khả năng tìm được nghiệm tốt hơn
## 4.3 AdaGrad
AdaGrad điều chỉnh learning rate (learning rate) cho mỗi tham số của mô hình một cách tự động, giúp cải thiện quá trình hội tụ, đặc biệt khi dữ liệu có các tính năng hiếm gặp hoặc không đồng nhất.
### Nguyên lý cơ bản của AdaGrad:
AdaGrad dựa trên việc điều chỉnh learning rate của từng tham số dựa trên lịch sử của gradient của chúng. Các bước chính của AdaGrad có thể tóm tắt như sau:

1. **Khởi tạo**:
   - Ban đầu, tất cả các tham số của mô hình được khởi tạo với giá trị ban đầu (thường là ngẫu nhiên).
   - learning rate (learning rate) toàn cục $\eta$ cũng được thiết lập.

2. **Tính toán Gradient**:
   - Ở mỗi bước huấn luyện, tính gradient của hàm mất mát (loss function) theo từng tham số.

3. **Cập nhật tham số với gradient tích lũy**:
   - AdaGrad tích lũy bình phương của gradient cho mỗi tham số theo thời gian. Cụ thể, với mỗi tham số $w_i$, một giá trị tích lũy $G_i$ được cập nhật:
     $$
     G^{(\tau)}_i = G^{(\tau-1)}_i + g_{i}^2
     $$
     ở đây $g_i$ là gradient tại thời điểm hiện tại.
   - Sau đó, learning rate hiệu quả cho mỗi tham số sẽ được điều chỉnh dựa trên giá trị $G_i$:
     $$
     w^{(\tau)}_i = w^{(\tau -1)}_i - \frac{\eta}{\sqrt{G^{(\tau)}_i} + \epsilon} \cdot g_i
     $$
     ở đây $\epsilon$ là một giá trị rất nhỏ (ví dụ $10^{-8}$) để tránh chia cho 0.

4. **Hiệu ứng điều chỉnh**:
   - Với những tham số có gradient lớn, $G_i$ sẽ tăng nhanh, làm giảm learning rate cho những tham số này, ngăn chặn việc cập nhật quá mức.
   - Ngược lại, với những tham số có gradient nhỏ, learning rate sẽ chậm hơn, giúp các tham số này có cơ hội hội tụ.

### Ưu điểm của AdaGrad:
- **Tự động điều chỉnh learning rate**: AdaGrad tự động điều chỉnh learning rate cho mỗi tham số một cách thích hợp dựa trên lịch sử của gradient, giúp tối ưu hóa hiệu quả hơn, đặc biệt khi có sự không đồng đều trong dữ liệu.
- **Hiệu quả với các tính năng hiếm gặp**: AdaGrad đặc biệt hữu ích khi làm việc với dữ liệu có tính năng hiếm gặp (sparse data), vì nó giúp các tham số liên quan đến những tính năng này học với tốc độ thích hợp.

### Nhược điểm của AdaGrad:
- **learning rate giảm dần quá nhiều**: Một nhược điểm lớn của AdaGrad là learning rate giảm dần quá nhiều qua thời gian, có thể khiến thuật toán hội tụ quá chậm hoặc không thể đạt đến tối ưu toàn cục.
  
Để giải quyết vấn đề này, các biến thể như **RMSProp** hay **Adam** đã được phát triển, duy trì các ưu điểm của AdaGrad trong khi cải thiện nhược điểm về learning rate giảm dần.

## 4.4 RMSProp
Thuật toán RMSProp (Root Mean Square Propagation) là một biến thể của AdaGrad, được thiết kế để giải quyết một trong những nhược điểm chính của AdaGrad, đó là learning rate giảm quá nhanh. RMSProp giúp duy trì một learning rate ổn định qua thời gian, cho phép mô hình hội tụ nhanh hơn và hiệu quả hơn.

### Nguyên lý cơ bản của RMSProp:

1. **Khởi tạo**:
   - Khởi tạo tất cả các tham số của mô hình với giá trị ban đầu.
   - Thiết lập learning rate $\eta$ và hệ số giảm dần $\beta$ (thường là 0.9).

2. **Tính toán Gradient**:
   - Tại mỗi bước huấn luyện, tính gradient của hàm mất mát theo từng tham số $g_i$.

3. **Tính toán trung bình bình phương của Gradient**:
   - RMSProp duy trì một trung bình động (moving average) của bình phương gradient. Giá trị này được cập nhật tại mỗi bước như sau:
     $$
     G^{(\tau)}_i = \beta G^{(\tau-1)}_i + (1-\beta)g_i^2
     $$
		Trong đó $g_i$ là gradient ở thời điểm hiện tại.
1. **Cập nhật tham số**:
   - Các tham số của mô hình được cập nhật bằng cách điều chỉnh gradient theo trung bình động của bình phương gradient:
     $$
     w^{(\tau)}_i = w^{(\tau -1)}_i - \frac{\eta}{\sqrt{G^{(\tau)}_i} + \epsilon} \cdot g_i
     $$
     ở đây $\epsilon$ là một giá trị rất nhỏ (ví dụ $10^{-8}$) để tránh chia cho 0.

RMSProp thường được sử dụng kết hợp với các thuật toán khác, như **Adam** (Adaptive Moment Estimation), để tối ưu hóa quá trình huấn luyện. Adam kết hợp lợi ích của RMSProp và AdaGrad, giúp cải thiện hiệu quả trong việc tối ưu hóa các mô hình học sâu.
## 4.5 Adam

Thuật toán **Adam** (viết tắt của **Adaptive Moment Estimation**) là một trong những thuật toán tối ưu hóa phổ biến nhất hiện nay trong học sâu (deep learning). Adam kết hợp các ưu điểm của hai thuật toán trước đó là AdaGrad và RMSProp, đồng thời bổ sung thêm các tính năng giúp cải thiện tốc độ hội tụ và độ ổn định trong quá trình huấn luyện mô hình.

### Nguyên lý cơ bản của Adam:

Adam sử dụng hai thành phần chính: **momentum** (mô-men động lượng) và **RMSProp** (Root Mean Square Propagation). Cụ thể, nó ước tính cả giá trị trung bình lẫn phương sai của gradient để điều chỉnh tốc độ học cho từng tham số.
#### Các bước chính của Adam:

1. **Khởi tạo**:
   - Tất cả các tham số của mô hình được khởi tạo với giá trị ban đầu.
   - Thiết lập tốc độ học $\eta$ (thường là 0.001) và hai hệ số giảm dần $\beta_1$ (thường là 0.9) và $\beta_2$ (thường là 0.999).
   - Khởi tạo hai giá trị trung bình động cho mô-men bậc nhất $m_0$ và bậc hai $v_0$ đều bằng 0.

2. **Tính toán Gradient**:
   - Ở mỗi bước huấn luyện, tính gradient $g_t$ của hàm mất mát theo từng tham số tại thời điểm $t$.

3. **Cập nhật mô-men bậc nhất và bậc hai**:
   - Cập nhật mô-men bậc nhất (ước lượng trung bình của gradient):
     $$
     m_t = \beta_1 m_{t-1} + (1 - \beta_1) g_t
     $$
   - Cập nhật mô-men bậc hai (ước lượng phương sai của gradient):
     $$
     v_t = \beta_2 v_{t-1} + (1 - \beta_2) g_t^2
     $$

4. **Hiệu chỉnh mô-men**:
   - Do $m_t$ và $v_t$ ban đầu được khởi tạo bằng 0, nên để tránh bias (thiên vị) trong các bước đầu tiên, ta áp dụng hiệu chỉnh bias cho chúng:
     $$
     \hat{m}_t = \frac{m_t}{1 - \beta_1^t}
     $$
     $$
     \hat{v}_t = \frac{v_t}{1 - \beta_2^t}
     $$

5. **Cập nhật tham số**:
   - Cuối cùng, tham số $\theta_t$ được cập nhật bằng cách sử dụng giá trị trung bình có hiệu chỉnh và tốc độ học:
     $$
     \theta_t = \theta_{t-1} - \frac{\eta}{\sqrt{\hat{v}_t} + \epsilon} \cdot \hat{m}_t
     $$
     ở đây $\epsilon$ là một giá trị rất nhỏ (ví dụ $10^{-8}$) để tránh chia cho 0.
### Ưu điểm của Adam:
- **Tốc độ hội tụ nhanh**: Adam thường hội tụ nhanh hơn so với các thuật toán tối ưu khác, giúp mô hình đạt được kết quả tốt hơn trong thời gian ngắn hơn.
- **Ổn định**: Adam sử dụng mô-men bậc nhất và bậc hai để điều chỉnh tốc độ học, giúp việc cập nhật tham số ổn định hơn, tránh được các dao động lớn.
- **Không cần điều chỉnh tốc độ học quá nhiều**: Adam thường hoạt động tốt với tốc độ học mặc định (0.001), giúp giảm bớt công việc điều chỉnh siêu tham số.
### Nhược điểm của Adam:
- **Tính tổng quát**: Adam có thể không tổng quát hóa tốt như các phương pháp khác trên một số bài toán cụ thể. Có những trường hợp, các thuật toán như SGD với momentum lại hoạt động tốt hơn.
- **Lệch bias trong ước lượng gradient**: Mặc dù Adam đã hiệu chỉnh bias, nhưng trong một số trường hợp, lệch bias này vẫn có thể ảnh hưởng đến kết quả cuối cùng.

Adam hiện là một trong những lựa chọn hàng đầu cho việc tối ưu hóa trong học sâu, đặc biệt khi huấn luyện các mạng nơ-ron sâu phức tạp với số lượng tham số lớn.
![[Pasted image 20240811150733.png]]

# 5. Normalization
## 5.1. Data normalization
- Mỗi chiều dữ liệu có thể chứa 1 range khác nhau trong tập dữ liệu nhiều chiều. Dẫn đến các trọng số bị biến đổi không phù hợp trong tất cả các chiều.
- Chuẩn hóa bằng cách:
	- Tính trung bình và phương sai của từng chiều.
	- Convert sang dữ liệu mới: $$x^{normalized}_{ni} = \frac{x^{original}_{ni} - \mu_{i}}{\sigma_{i}}$$
## 5.2. Batch normalization
Khi huấn luyện mạng nhiều lớp, các gradient có xu hướng tiến về 0 hoặc dương vô cùng (do đạo hàm qua nhiều lớp), dẫn đến hiện tượng *vanishing gradients* và *exploding gradients*.
### Các bước thực hiện Batch Normalization:
1. **Tính toán trung bình và độ lệch chuẩn trên từng batch**:
   - Đối với mỗi batch dữ liệu trong quá trình huấn luyện, ta tính toán giá trị trung bình $\mu_B$ và độ lệch chuẩn $\sigma_B^2$ của các đầu vào cho mỗi lớp:
     $$
     \mu_B = \frac{1}{m} \sum_{i=1}^{m} x_i
     $$
     $$
     \sigma_B^2 = \frac{1}{m} \sum_{i=1}^{m} (x_i - \mu_B)^2
     $$
     ở đây $m$ là số lượng mẫu trong batch, và $x_i$ là giá trị đầu vào của một nơ-ron cụ thể.
2. **Chuẩn hóa đầu vào**:
   - Chuẩn hóa đầu vào dựa trên trung bình và độ lệch chuẩn đã tính:
     $$
     \hat{x}_i = \frac{x_i - \mu_B}{\sqrt{\sigma_B^2 + \epsilon}}
     $$
     $\epsilon$ là một số rất nhỏ để tránh chia cho 0.
3. **Tính đầu ra đã chuẩn hóa**:
   - Sau khi chuẩn hóa, đầu ra được điều chỉnh thông qua các tham số học được $\gamma$ và $\beta$ để đưa giá trị đầu ra về một khoảng giá trị thích hợp:
     $$
     y_i = \gamma \hat{x}_i + \beta
     $$
     $\gamma$ và $\beta$ là các tham số có thể học được, cho phép mô hình điều chỉnh lại quy mô và vị trí của đầu vào sau khi chuẩn hóa.
### Lợi ích của Batch Normalization:
1. **Tăng tốc độ hội tụ**:
   - Batch normalization cho phép sử dụng tốc độ học cao hơn mà không gây ra các vấn đề về ổn định, giúp mô hình hội tụ nhanh hơn.
2. **Giảm sự phụ thuộc vào khởi tạo tham số**:
   - Việc chuẩn hóa các đầu vào của mỗi lớp giúp giảm độ nhạy cảm của mô hình đối với các giá trị khởi tạo ban đầu của tham số.
3. **Giảm hiện tượng "internal covariate shift"**:
   - Bằng cách chuẩn hóa đầu vào của mỗi lớp, batch normalization giúp giảm thiểu sự thay đổi của phân phối đầu vào qua các lớp, giúp quá trình huấn luyện trở nên ổn định hơn.
4. **Giảm sự cần thiết của các kỹ thuật regularization khác**:
   - Batch normalization có thể giảm bớt sự cần thiết phải sử dụng các kỹ thuật regularization như dropout, vì nó đã góp phần làm giảm overfitting.
### Nhược điểm của Batch Normalization:
1. **Phụ thuộc vào batch size**:
   - Hiệu quả của batch normalization phụ thuộc vào kích thước batch được sử dụng trong quá trình huấn luyện. Batch size quá nhỏ có thể làm giảm độ chính xác của việc ước lượng trung bình và độ lệch chuẩn, gây ra biến động trong quá trình huấn luyện.
2. **Độ phức tạp tăng thêm**:
   - Batch normalization thêm các bước tính toán trong quá trình huấn luyện, làm tăng độ phức tạp và yêu cầu tài nguyên tính toán.
3. **Không hoạt động tốt trong một số trường hợp**:
   - Trong một số trường hợp như mạng hồi quy (RNN), batch normalization có thể không hoạt động hiệu quả, và các kỹ thuật khác như layer normalization có thể phù hợp hơn.
## 5.3 Layer normalization
Thay vì chuẩn hóa dữ liệu theo từng batch, Layer normalization chuẩn hóa các đầu vào trong một lớp (layer) bằng cách tính toán giá trị trung bình và độ lệch chuẩn cho mỗi mẫu đơn lẻ. Điều này có nghĩa là mọi nơ-ron trong cùng một lớp sẽ được chuẩn hóa cùng nhau, mà không cần xem xét đến các mẫu khác trong batch.

### Các bước thực hiện Layer Normalization:
1. **Tính toán giá trị trung bình và độ lệch chuẩn**:
   - Đối với mỗi mẫu $x$ trong một lớp với $H$ nơron, tính giá trị trung bình $\mu$ và độ lệch chuẩn $\sigma$ của tất cả các nơ-ron trong lớp đó:
     $$
     \mu = \frac{1}{H} \sum_{i=1}^{H} x_i
     $$$$
     \sigma^2 = \frac{1}{H} \sum_{i=1}^{H} (x_i - \mu)^2
     $$
     Trong đó $H$ là số lượng nơ-ron trong lớp.
2. **Chuẩn hóa đầu vào**:
   - Chuẩn hóa đầu vào dựa trên giá trị trung bình và độ lệch chuẩn đã tính:
     $$
     \hat{x}_i = \frac{x_i - \mu}{\sqrt{\sigma^2 + \epsilon}}
     $$
     ở đây $\epsilon$ là một giá trị nhỏ để tránh chia cho 0.
3. **Tính đầu ra đã chuẩn hóa**:
   - Sau khi chuẩn hóa, đầu ra của mỗi nơ-ron được điều chỉnh thông qua các tham số học được $\gamma$ và $\beta$ để đưa giá trị đầu ra về khoảng giá trị thích hợp:
     $$
     y_i = \gamma \hat{x}_i + \beta
     $$
     $\gamma$ và $\beta$ là các tham số có thể học được, cho phép mô hình điều chỉnh lại quy mô và vị trí của đầu vào sau khi chuẩn hóa.
### Ưu điểm của Layer Normalization:
1. **Độc lập với batch size**:
   - Vì Layer normalization không dựa trên các batch dữ liệu, nó hoạt động ổn định ngay cả khi batch size nhỏ, hoặc khi chỉ có một mẫu trong batch.
2. **Hiệu quả cho mô hình RNN**:
   - Layer normalization đặc biệt hữu ích trong các mô hình hồi quy (RNN), nơi mà sự phụ thuộc tuần tự giữa các bước thời gian có thể gây ra vấn đề cho Batch normalization.
3. **Giảm hiện tượng "internal covariate shift"**:
   - Giống như Batch normalization, Layer normalization giúp giảm thiểu sự thay đổi trong phân phối đầu vào qua các lớp, giúp quá trình huấn luyện ổn định hơn.
4. **Không phụ thuộc vào việc xáo trộn dữ liệu**:
   - Batch normalization yêu cầu dữ liệu được xáo trộn để tránh các mẫu trong một batch có tương quan cao. Layer normalization không gặp phải vấn đề này, vì nó hoạt động trên từng mẫu riêng lẻ.
### Nhược điểm của Layer Normalization:
1. **Hiệu quả có thể kém hơn trong một số tình huống**:
   - Trong các mô hình với các batch lớn và không có sự phụ thuộc tuần tự giữa các mẫu, Batch normalization thường hoạt động tốt hơn Layer normalization.
2. **Tăng độ phức tạp tính toán**:
   - Mặc dù Layer normalization có thể linh hoạt hơn, nhưng nó cũng đòi hỏi tính toán nhiều hơn so với việc không chuẩn hóa.