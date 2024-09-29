---
Created at: 2024-07-31
Source:
  - "[[Deep_learning_foundation.pdf#page=150|Deep_learning_foundation - 5]]"
---
Giới thiệu về các mạng đơn lớp được sử dụng cho phân loại, cụ thể là các hàm phân biệt. Hàm phân biệt là một hàm nhận đầu vào là một vector và gán nó vào một trong các lớp. Trọng tâm của chương này là các hàm phân biệt tuyến tính, tức là các bề mặt quyết định là các siêu phẳng.
# 1. Discriminant function
Phần này tập trung vào các hàm phân biệt tuyến tính, được sử dụng để phân loại các đối tượng vào các lớp khác nhau. Các hàm phân biệt này xác định bề mặt quyết định phân chia không gian đầu vào thành các vùng tương ứng với các lớp.
## 1.1. Hai lớp
**Hàm phân biệt tuyến tính cho phân loại nhị phân:**
  $$ y(x) = w^T x + w_0 $$
  Trong đó, $w$ là vector trọng số và $w_0$ là hệ số tự do. Nếu $y(x) \geq  0$, $x$ được gán vào lớp $C_1$, ngược lại, $x$ được gán vào lớp $C_2$. Bề mặt quyết định là một siêu phẳng trong không gian đầu vào.
## 1.2. Nhiều lớp
- Với nhiều lớp, mỗi lớp $C_k$ có một hàm phân biệt tuyến tính riêng $y_k(x) = w_k^T x + w_{k0}$.
- Điểm $x$ được gán vào lớp $C_k$ nếu $y_k(x) > y_j(x)$ cho mọi $j \neq k$.
- Bề mặt quyết định giữa hai lớp $C_k$ và $C_j$ là siêu phẳng $y_k(x) = y_j(x)$.
## 1.3. 1-of-K coding
- Mỗi lớp $C_k$ được mã hóa thành một vector nhị phân với một phần tử là 1 và các phần tử còn lại là 0.
- Ví dụ, với 3 lớp, các vector mã hóa có thể là: $C_1 = [1, 0, 0]$, $C_2 = [0, 1, 0]$, $C_3 = [0, 0, 1]$.
## 1.4. Least squares for classification
- Sử dụng phương pháp này để tìm trọng số $w$:
  $$ \min_w \sum_{i=1}^N (y_i - w^T x_i)^2 $$
  Trong đó, $y_i$ là nhãn của điểm dữ liệu $x_i$.
- Phương pháp này có thể không tối ưu cho phân loại vì không tối ưu hóa xác suất có điều kiện của các lớp, mà chỉ tối thiểu hóa sai số dự đoán.

# 2. Decision theory
## 2.1. Misclassification rate (tỉ lệ sai)
-  **Quy tắc quyết định và các vùng quyết định**:
	- Quy tắc quyết định gán mỗi đầu vào $x$ cho một trong các lớp có sẵn.
	- Không gian đầu vào được chia thành các vùng $R_k$ gọi là các vùng quyết định, mỗi vùng tương ứng với một lớp cụ thể $C_k$.
	- Ranh giới giữa các vùng này được gọi là ranh giới quyết định hoặc bề mặt quyết định.
- **Quy tắc quyết định tối ưu cho hai lớp**:
	- Xét một vấn đề với hai lớp, $C_1$ và $C_2$.
	- Một lỗi phân loại xảy ra khi một vector đầu vào thuộc lớp $C_1$ được gán cho lớp $C_2$ và ngược lại.
	- Xác suất phân loại sai được cho bởi: $$
     p(\text{mistake}) = p(x \in R_1, C_2) + p(x \in R_2, C_1) = \int_{R_1} p(x, C_2) \, dx + \int_{R_2} p(x, C_1) \, dx
     $$

- **Giảm thiểu tỷ lệ phân loại sai**:
	- Để giảm thiểu xác suất mắc lỗi, mỗi đầu vào $x$ nên được gán cho lớp có xác suất hậu nghiệm $p(C_k | x)$ lớn nhất.
	- Điều này tuân theo quy tắc tích xác suất: $p(x, C_k) = p(C_k | x)p(x)$. Thuật ngữ $p(x)$ là chung cho cả hai lớp và không ảnh hưởng đến quyết định, vì vậy quyết định chỉ phụ thuộc vào việc tối đa hóa $p(C_k | x)$.

- **Trường hợp tổng quát cho $K$ lớp**:
	- Cách tiếp cận có thể được mở rộng cho $K$ lớp, trong đó mục tiêu là tối đa hóa xác suất đúng:
	 $$
	 p(\text{correct}) = \sum_{k=1}^{K} p(x \in R_k, C_k)
	 $$
	- Quy tắc quyết định tối ưu gán mỗi $x$ cho lớp có xác suất hậu nghiệm lớn nhất.
## 2.2. Expected loss
#### Hàm mất mát

Để mô tả những vấn đề này, chúng ta giới thiệu một hàm mất mát (loss function), còn được gọi là hàm chi phí (cost function), là một thước đo tổng thể duy nhất về mất mát khi thực hiện bất kỳ quyết định hoặc hành động nào có sẵn. Mục tiêu của chúng ta là giảm thiểu tổng mất mát.

Trong ngữ cảnh phân loại, chúng ta định nghĩa hàm mất mát $L_{kj}$ là mất mát phát sinh khi quyết định phân loại một mẫu thuộc lớp $C_k$ thành lớp $C_j$. Ví dụ, trong vấn đề chẩn đoán ung thư, ta có thể sử dụng một ma trận mất mát như sau:

```
               | normal | cancer
   ------------|--------|--------
   normal      |   0    |    1
   cancer      |  100   |    0
```

Trong đó, giá trị 0 nghĩa là không có mất mát khi phân loại đúng, giá trị 1 và 100 thể hiện mức độ mất mát khác nhau khi phân loại sai.

#### Mất mát kỳ vọng

Để giảm thiểu mất mát kỳ vọng, ta cần tính toán tổng mất mát kỳ vọng $E[L]$ bằng cách trung bình mất mát qua tất cả các khả năng phân loại sai và đúng, cân nhắc theo xác suất xuất hiện của các mẫu. Công thức tính toán mất mát kỳ vọng được mô tả như sau:

$$ E[L] = \sum_{k,j} L_{kj} p(C_k, C_j) $$

Trong đó $p(C_k, C_j)$ là xác suất một mẫu thực sự thuộc lớp $C_k$ nhưng bị phân loại thành lớp $C_j$.

Để tối ưu hoá hàm mất mát kỳ vọng, ta sẽ sử dụng các kỹ thuật như phương pháp gradient descent hoặc các thuật toán tối ưu khác để tìm ra các tham số của mô hình sao cho tổng mất mát kỳ vọng là nhỏ nhất.

## 2.3. Reject option
- Ta có thể giới thiệu ngưỡng $\theta$ và từ chối những đầu vào $x$ mà xác suất hậu nghiệm lớn nhất $p(C_k|x)$ nhỏ hơn hoặc bằng $\theta$. 
- Ta cũng có thể mở rộng tiêu chí từ chối để giảm thiểu mất mát kỳ vọng, khi một ma trận mất mát được cung cấp, bằng cách tính đến mất mát xảy ra khi quyết định từ chối được thực hiện.

Khi các xác suất hậu nghiệm cao nhất $p(C_k|x)$ không đạt đến mức gần với 1, hoặc các phân phối đồng thời $p(x, C_k)$ có giá trị tương đương nhau, thì xảy ra lỗi phân loại. Đây là các vùng mà chúng ta không chắc chắn về thành viên lớp.

## 2.4. Inference và Decision
Phương pháp phân loại thông qua hai giai đoạn chính: giai đoạn suy luận (inference) và giai đoạn quyết định (decision).
- **Giai đoạn Suy luận**: Sử dụng dữ liệu huấn luyện để học một mô hình xác suất hậu nghiệm $p(C_k|x)$.
- **Giai đoạn Quyết định**: Sử dụng các xác suất hậu nghiệm này để đưa ra các quyết định phân loại tối ưu.

Có ba cách tiếp cận chính để giải quyết các vấn đề quyết định:
#### Tiếp cận Generative Models (Mô hình tạo sinh):
- Xác định các mật độ xác suất điều kiện lớp $p(x|C_k)$ cho từng lớp riêng lẻ.
- Suy luận các xác suất tiên nghiệm của lớp $p(C_k)$.
- Sử dụng định lý Bayes để tính toán xác suất hậu nghiệm $p(C_k|x)$.
- Sử dụng lý thuyết quyết định để xác định lớp cho từng đầu vào mới $x$.
#### Tiếp cận Discriminative Models (Mô hình phân biệt):
- Xác định trực tiếp các xác suất hậu nghiệm $p(C_k|x)$.
- Sử dụng decision theory để phân loại đầu vào $x$ vào các lớp.
#### Tiếp cận Discriminant Functions (Hàm phân biệt):
- Tìm một hàm $f(x)$ trực tiếp ánh xạ đầu vào $x$ tới một nhãn lớp.
- Trong các vấn đề hai lớp, $f(\cdot)$ có thể nhận giá trị nhị phân, với $f = 0$ đại diện cho lớp $C_1$ và $f = 1$ đại diện cho lớp $C_2$.

#### Lợi ích và Hạn chế:
- **Tiếp cận [[Generative Classifier | Generative Models]]**:
    - Yêu cầu xác định phân phối chung trên cả $x$ và $C_k$, đòi hỏi một tập dữ liệu huấn luyện lớn nếu $x$ có nhiều chiều.
    - Ưu điểm là có thể xác định mật độ biên $p(x)$ để phát hiện các điểm dữ liệu mới có xác suất thấp (outlier detection).
- **Tiếp cận Discriminative Models**:
    - Mô hình trực tiếp xác suất hậu nghiệm, dễ thực hiện hơn khi không cần xác định phân phối chung.
- **Tiếp cận Discriminant Functions**:
    - Trực tiếp ánh xạ đầu vào tới nhãn lớp, không cần xác suất, phù hợp cho các bài toán đơn giản.

 Phương pháp Generative phù hợp cho các ứng dụng yêu cầu phát hiện điểm ngoại lai, trong khi phương pháp Discriminative và Discriminant Functions phù hợp cho các ứng dụng phân loại trực tiếp và đơn giản.

## 2.5. Classifier accuracy
   Độ chính xác (accuracy) là tỷ lệ số điểm trong tập kiểm tra được phân loại đúng.
$$ \text{Accuracy} = \frac{N_{TP} + N_{TN}}{N_{TP} + N_{FP} + N_{TN} + N_{FN}} $$
   - **True Positive (TP)**: Dự đoán đúng là có bệnh.
   - **False Positive (FP)**: Dự đoán sai là có bệnh (không có bệnh nhưng dự đoán có).
   - **True Negative (TN)**: Dự đoán đúng là không có bệnh.
   - **False Negative (FN)**: Dự đoán sai là không có bệnh (có bệnh nhưng dự đoán không có).
   - **Confusion Matrix**: Ma trận này biểu diễn các giá trị TP, FP, TN và FN.

**Các chỉ số khác**:
   - **Precision** (Độ chính xác của dương tính): $\text{Precision} = \frac{N_{TP}}{N_{TP} + N_{FP}}$
   - **Recall** (Độ nhạy): $\text{Recall} = \frac{N_{TP}}{N_{TP} + N_{FN}}$
   - **False Positive Rate (FPR)** (Tỷ lệ dương tính giả): $\text{FPR} = \frac{N_{FP}}{N_{FP} + N_{TN}}$
   - **False Discovery Rate (FDR)** (Tỷ lệ khám phá giả): $\text{FDR} = \frac{N_{FP}}{N_{FP} + N_{TP}}$

## 2.6. ROC curve
![[Pasted image 20240801065701.png]]
ROC Curve là đồ thị thể hiện mối quan hệ giữa Tỷ lệ Dương tính thật (True Positive Rate - TPR) và Tỷ lệ Dương tính giả (False Positive Rate - FPR).
- Mỗi confusion matrix đại diện cho một điểm trên đường cong ROC.
- Điểm tốt nhất trên ROC là góc trên bên trái của biểu đồ (TPR cao và FPR thấp).
- Đường chéo trong biểu đồ ROC đại diện cho bộ phân loại ngẫu nhiên, nơi xác suất đúng và sai là như nhau.

# 3. Generative Classifiers
## 3.1. Continuous input
### 5.3.1. Đầu vào liên tục

**Các giả định về Mật độ Điều kiện Lớp và Gaussian:**
- Mật độ điều kiện cho lớp $C_k$ được mô hình hóa như một phân phối Gaussian với ma trận hiệp phương sai chung $\Sigma$ cho tất cả các lớp. Hàm mật độ xác suất được biểu diễn bởi:
  $$
  p(x|C_k) = \frac{1}{(2\pi)^{D/2} |\Sigma|^{1/2}} \exp \left( -\frac{1}{2} (x - \mu_k)^T \Sigma^{-1} (x - \mu_k) \right)
  $$
- Đối với hai lớp, xác suất hậu nghiệm $p(C_1|x)$ có thể được biểu thị bằng hàm sigmoid logistic:
  $$
  p(C_1|x) = \sigma(w^T x + w_0)
  $$
  với $w$ và $w_0$ được định nghĩa là:
  $$
  w = \Sigma^{-1} (\mu_1 - \mu_2)
  $$
  $$
  w_0 = -\frac{1}{2} \mu_1^T \Sigma^{-1} \mu_1 + \frac{1}{2} \mu_2^T \Sigma^{-1} \mu_2 + \ln \frac{p(C_1)}{p(C_2)}
  $$

**Trường hợp tổng quát với $K$ lớp:**
- Đối với trường hợp tổng quát với $K$ lớp, xác suất hậu nghiệm được xác định bằng hàm softmax:
  $$
  a_k(x) = w_k^T x + w_{k0}
  $$
  với $w_k$ và $w_{k0}$ được biểu diễn là:
  $$
  w_k = \Sigma^{-1} \mu_k
  $$
  $$
  w_{k0} = -\frac{1}{2} \mu_k^T \Sigma^{-1} \mu_k + \ln p(C_k)
  $$

## 3.2. Maximum likelihood 
### Tóm tắt Chương 5.3.2: Maximum Likelihood Solution
  $$
  p(t, X | \pi, \mu_1, \mu_2, \Sigma) = \prod_{n=1}^{N} [\pi N(x_n|\mu_1, \Sigma)]^{t_n} [(1 - \pi) N(x_n|\mu_2, \Sigma)]^{1 - t_n}
  $$

- Tối ưu hóa hàm hợp lý logarit:
  $$
  \ln p(t, X | \pi, \mu_1, \mu_2, \Sigma) = \sum_{n=1}^{N} \{ t_n \ln \pi + (1 - t_n) \ln (1 - \pi) \} + \sum_{n=1}^{N} \{ t_n \ln N(x_n|\mu_1, \Sigma) + (1 - t_n) \ln N(x_n|\mu_2, \Sigma) \}
  $$
- Đặt đạo hàm theo $\pi = 0$  và giải ra được:
  $$
  \pi = \frac{1}{N} \sum_{n=1}^{N} t_n
  $$
## 3.4. [[Phân phối mũ (The Exponential Family)|Exponential Family]]
Đây là các trường hợp đặc biệt của một kết quả tổng quát hơn thu được bằng cách giả định rằng các mật độ điều kiện lớp $p(x|C_k)$ là thành viên của tập hợp các phân phối họ mũ:
$$ p(x|\lambda_k, s) = \frac{1}{s} h\left(\frac{x}{s}\right) g(\lambda_k) \exp\left(\frac{1}{s} \lambda_k^T x\right) $$
Với tham số tỷ lệ $s$ chia sẻ giữa tất cả các lớp.

Đối với bài toán hai lớp, xác suất hậu nghiệm của lớp lại được cho bởi hàm logistic sigmoid hoạt động trên một hàm tuyến tính $a(x)$:
$$ a(x) = (\lambda_1 - \lambda_2)^T x + \ln g(\lambda_1) - \ln g(\lambda_2) + \ln p(C_1) - \ln p(C_2) $$

Tương tự, đối với bài toán $K$ lớp, ta có:
$$ a_k(x) = \lambda_k^T x + \ln g(\lambda_k) + \ln p(C_k) $$
# 4. Discriminative Classifiers
Phần 5.4.4 trong tài liệu "Deep Learning Foundation" đề cập đến "Multi-class logistic regression". Dưới đây là tóm tắt:

## 4.1. Multi-class Logistic Regression
- **Giới thiệu:** Multi-class logistic regression, còn được gọi là softmax regression, là một mở rộng của logistic regression để xử lý các vấn đề phân loại với nhiều lớp.
- **Softmax Function:** Chức năng chính của mô hình này là hàm softmax, dùng để tính xác suất của từng lớp. Công thức của hàm softmax cho đầu ra của lớp $k$ là:
  $$
  P(y=k|x) = \frac{e^{\theta_k^T x}}{\sum_{j=1}^{K} e^{\theta_j^T x}}
  $$
  Trong đó, $\theta_k$ là vector trọng số của lớp $k$ và $K$ là tổng số lớp.
- **Loss Function:** Hàm mất mát cho multi-class logistic regression là negative log-likelihood, hay cross-entropy loss. Công thức của nó là:
  $$
  L(\theta) = -\sum_{i=1}^{N} \log P(y^{(i)}|x^{(i)}; \theta)
  $$
  Trong đó, $N$ là số lượng mẫu, $y^{(i)}$ là nhãn thực tế của mẫu $i$, và $x^{(i)}$ là đầu vào của mẫu $i$.
- **Optimization:** Việc tối ưu hóa mô hình thường được thực hiện bằng cách sử dụng các thuật toán gradient descent hoặc các biến thể của nó, chẳng hạn như stochastic gradient descent (SGD).
- **Applications:** Mô hình này được sử dụng rộng rãi trong nhiều ứng dụng như nhận dạng chữ viết tay, phân loại văn bản, và nhận diện hình ảnh.
## 4.2 Hồi quy Probit (Probit regression)

- **Giới thiệu:** Hồi quy Probit được giới thiệu như một phương pháp thay thế cho hồi quy logistic cho các bài toán phân loại nhị phân. Nó hoạt động trong khung của các mô hình tuyến tính tổng quát và cung cấp một hàm liên kết khác.

- **Hàm Probit:** Hàm probit là hàm phân phối tích lũy (CDF) của phân phối chuẩn. Nó được sử dụng trong mô hình hồi quy probit để xác định xác suất của biến đầu ra nhị phân dựa trên tổ hợp tuyến tính của các biến đầu vào. Công thức của hàm probit là:
$$
\Phi(a) = \int_{-\infty}^{a} N(\theta|0, 1) d\theta
$$
	Trong đó:
	- $\Phi(a)$ là giá trị của hàm probit tại điểm $a$.
	- $N(\theta|0, 1)$ là mật độ xác suất của phân phối chuẩn với giá trị trung bình bằng 0 và độ lệch chuẩn bằng 1.
	- $a$ là tổ hợp tuyến tính của các biến đầu vào (ví dụ: $a = w^T x$ với $w$ là vector trọng số và $x$ là vector các biến đầu vào).
	Hàm probit có dạng sigmoid, tương tự như hàm sigmoid logistic, nhưng có phần đuôi giảm nhanh hơn, do đó mô hình probit có thể nhạy cảm hơn với các giá trị ngoại lai so với mô hình logistic.

- **Hàm kích hoạt:** Trong mô hình probit, hàm kích hoạt là CDF của phân phối Gaussian. Với tổ hợp tuyến tính của các đầu vào, $a = w^T\phi$, hàm kích hoạt được cho bởi tích phân của mật độ Gaussian:
  $$
  f(a) = \int_{-\infty}^{a} p(\theta) d\theta
  $$

- **Hàm lỗi:** Các tham số của mô hình hồi quy probit có thể được xác định bằng phương pháp ước lượng hợp lý tối đa, tương tự như hồi quy logistic. Sự khác biệt chính nằm ở độ nhạy với các giá trị ngoại lai, nơi mà phần đuôi của mô hình probit suy giảm nhanh hơn so với mô hình logistic.

- **So sánh với hồi quy Logistic:** Hồi quy probit có thể nhạy cảm hơn với các giá trị ngoại lai do sự khác biệt ở phần đuôi. Đuôi của hàm logistic suy giảm theo $\exp(-x)$, trong khi đuôi của hàm probit suy giảm theo $\exp(-x^2)$.

- **Ứng dụng:** Hồi quy probit hữu ích trong các tình huống mà giả định về tính chuẩn của phân phối cơ sở là hợp lý và khi độ nhạy với các giá trị ngoại lai là một yếu tố cần cân nhắc.

## 4.3 [[Canonical Link Functions]]