---
Created at: 2024-08-26
Source:
  - "[[Deep_learning_foundation.pdf#page=374|Deep_learning_foundation, p.358]]"
---
Attention cho phép mạng tập trung vào các phần quan trọng của đầu vào, dựa trên ngữ cảnh cụ thể, và tự động xác định những từ nào cần chú ý nhiều hơn dựa vào ngữ cảnh đó.

# 1. Cách hoạt động
**Dữ liệu:**
- Transformer xử lý dữ liệu đầu vào dưới dạng một tập hợp các vector (gọi là tokens). Mỗi token có thể đại diện cho một từ trong câu, một phần trong ảnh, hoặc một axit amin trong protein. 
- Dữ liệu đầu vào này được tổ chức thành một ma trận $X$ có kích thước $N \times D$, với $N$ là số lượng tokens và $D$ là số lượng đặc trưng (features).

**Cấu trúc:**
- Transformer được xây dựng từ nhiều lớp (layers), mỗi lớp nhận vào một ma trận dữ liệu và tạo ra một ma trận mới cùng kích thước. 
- Một lớp transformer gồm hai giai đoạn: giai đoạn đầu tiên thực hiện cơ chế attention, trộn các đặc trưng từ các token khác nhau; giai đoạn thứ hai tác động lên từng token một cách độc lập và biến đổi các đặc trưng bên trong mỗi token. 

Mục tiêu của các lớp transformer là tạo ra một không gian biểu diễn mới có cấu trúc ngữ nghĩa phong phú hơn, giúp giải quyết hiệu quả các nhiệm vụ khác nhau.

# 2. Attention coefficients
- Biểu diễn output tokens, $Y_n$, được tính toán như là một tổ hợp tuyến tính của các input tokens, $X_i$, $a_{nm}$ là các hệ số:
    $$Y_n = ∑ a_{nm} X_m$$
     Trong đó:
	- $a_{nm} ≥ 0$: Các tokens không có ảnh hưởng đến $Y_n$ nên có trọng số gần bằng 0.
	- $∑ a_{nm} = 1:$ Nếu một tokens quan trọng đối với $Y_n$, các tokens khác nên ít quan trọng hơn.

Về bản chất, quy trình này gán trọng số cho mỗi input tokens dựa trên sự tương đồng của nó với output tokens mục tiêu. Sau đó, các trọng số này được sử dụng để kết hợp các input tokens thành biểu diễn output tokens, cho phép Transformer tập trung vào thông tin có liên quan.

# 3. Self-attention
Self-attention cho phép mô hình nhìn nhận và cân nhắc mọi phần tử trong một chuỗi (sequence) để tạo ra một biểu diễn ngữ nghĩa sâu sắc hơn cho mỗi từ trong chuỗi đó. Điều này giúp mô hình hiểu rõ hơn về ngữ cảnh của từ, từ đó cải thiện khả năng dự đoán và hiểu biết.

Ví dụ, trong câu "I walked across the road to get cash from the bank", mạng Transformer cần tập trung vào từ "cash" và "bank" để hiểu được "bank" ở đây là ngân hàng tài chính chứ không phải bờ sông.
### Cách hoạt động của Self-Attention

Self-attention hoạt động theo các bước sau:

1. **Tạo Queries, Keys và Values**:
   - Mỗi từ trong chuỗi đầu vào được biến đổi thành ba vector khác nhau: Query (Q), Key (K), và Value (V). Các vector này được tạo ra bằng cách nhân từ đó với ba ma trận trọng số đã được huấn luyện trước.

2. **Tính toán điểm số Attention**:
   - Điểm số attention cho một từ được tính bằng cách lấy tích vô hướng (dot product) giữa query của từ đó và key của tất cả các từ khác trong chuỗi. Điều này giúp xác định mức độ liên quan của từ đó đối với các từ khác.

3. **Áp dụng Softmax**:
   - Softmax được áp dụng trên các điểm số này để chuyển đổi chúng thành các xác suất. Những xác suất này biểu thị mức độ chú ý mà mỗi từ trong chuỗi đầu vào nên có với từ đang được xét.
  $$a_{nm} = \frac{exp(X_n^T X_m)}{\sum_{m'=1}^N exp(X_n^T X_{m'})}$$
	    Công thức này sử dụng hàm Softmax để chuẩn hóa các tích vô hướng giữa vectơ "Truy vấn" (Query) $X_n$, và mỗi vectơ "Khóa" (Key) $X_m$.

4. **Tạo ra đầu ra attention**:
   - Cuối cùng, mỗi vector Value (V) được nhân với xác suất attention tương ứng và cộng lại để tạo ra vector đầu ra mới cho từ đó. Vector này kết hợp thông tin từ tất cả các từ trong chuỗi dựa trên mức độ liên quan đã được tính toán.

# 4. Network Parameter

* **Giới hạn của cơ chế chú ý ban đầu:** Phiên bản đơn giản của attention không có khả năng học hỏi từ dữ liệu do thiếu các tham số điều chỉnh được. Hơn nữa, tất cả các giá trị đặc trưng (feature values) trong một vector mã thông báo (token vector) đóng vai trò như nhau trong việc xác định hệ số chú ý (attention coefficient). Điều này hạn chế sự linh hoạt của mô hình vì chúng ta mong muốn mạng có thể tập trung vào một số đặc trưng nhất định hơn những đặc trưng khác.

* **Giải pháp bằng biến đổi tuyến tính:** Để khắc phục những giới hạn này, tài liệu đề xuất việc sử dụng các biến đổi tuyến tính (linear transformations) đối với các vector mã thông báo ban đầu. Cụ thể:

    * **Ma trận trọng số:** Giới thiệu các ma trận trọng số học được $W^{(q)}$, $W^{(k)}$ và $W^{(v)}$ tương ứng cho các vector truy vấn (query), khóa (key) và giá trị (value). 

    * **Biến đổi tuyến tính:** Áp dụng các biến đổi tuyến tính lên các vector đầu vào X để tạo ra các vector truy vấn Q, khóa K và giá trị V:
        * $Q = XW^{(q)}$
        * $K = XW^{(k)}$
        * $V = XW^{(v)}$
    * Dựa vào đó, ta sử dụng cách tính output Y bằng [[Softmax function]]:
$$Y = Softmax \ [QK^T] \ V$$

![[Pasted image 20240828071946.png]]
![[Pasted image 20240828071959.png]]

# 5. Scaled self-attention
$$
 Y = \text{attention}(Q, K, V) = Softmax \ \left[\frac{Q \cdot K^T}{\sqrt{D_k}}\right] V
 $$
Trong đó:
- $Q$ là vector truy vấn của từ hiện tại.
- $K$ là vector khóa của các từ khác.
- $D_k$ là chiều dài vector khóa.

# 6. Multi-head attention
**Multi-head attention** là một mở rộng của cơ chế self-attention được sử dụng trong các mô hình Transformer, nhằm cải thiện khả năng học hỏi và biểu diễn thông tin của mô hình. Nó cho phép mô hình tập trung vào các khía cạnh khác nhau của dữ liệu đầu vào bằng cách sử dụng nhiều "đầu chú ý" (attention heads) thay vì chỉ một.

### Cơ chế hoạt động của Multi-head Attention:

1. **Chia nhỏ không gian embedding:**
   - Đầu tiên, embedding đầu vào được chia thành nhiều phần nhỏ, mỗi phần tương ứng với một "đầu chú ý". Mỗi đầu chú ý này sẽ làm việc với các vectors truy vấn $Q$, khóa $K$, và giá trị $V$ của riêng mình.

2. **Tính toán attention cho từng head:**
   - Với mỗi đầu chú ý, mô hình thực hiện cơ chế self-attention theo cách thông thường:
     $$
     \text{Attention}(Q_i, K_i, V_i) = \text{softmax}\left(\frac{Q_i \cdot K_i^T}{\sqrt{d_k}}\right) \cdot V_i
     $$
   - Ở đây, $Q_i$, $K_i$, và $V_i$ là các vectors tương ứng cho đầu chú ý thứ $i$, và $d_k$ là kích thước của mỗi vector truy vấn (sau khi chia nhỏ).

3. **Ghép nối và kết hợp thông tin:**
   - Sau khi tính toán xong attention cho từng head, kết quả từ các đầu chú ý này được ghép nối lại với nhau để tạo thành một vector đầu ra duy nhất.
   - Vector đầu ra này sau đó được biến đổi thông qua một ma trận trọng số để tạo ra đầu ra cuối cùng cho lớp multi-head attention.

4. **Tăng cường khả năng biểu diễn:**
   - Bằng cách sử dụng nhiều đầu chú ý, multi-head attention cho phép mô hình học và biểu diễn các khía cạnh khác nhau của thông tin trong câu. Ví dụ, một đầu chú ý có thể tập trung vào cấu trúc ngữ pháp, trong khi một đầu khác có thể tập trung vào các mối liên kết ngữ nghĩa giữa các từ.

![[Pasted image 20240828160055.png]]
![[Pasted image 20240828160208.png]]

# 7. Transformer layers
![[Pasted image 20240828162050.png]]
![[Pasted image 20240828162137.png]]

# 8. Positional encoding

- **Vấn đề vị trí trong Transformer**: Transformer xử lý dữ liệu đầu vào dưới dạng một tập hợp các token và do đó *không tự động ghi nhận được thứ tự của các token trong chuỗi*. Việc này dẫn đến một hạn chế lớn khi xử lý dữ liệu tuần tự, như văn bản tự nhiên, nơi thứ tự của các từ là cực kỳ quan trọng.

- **Kỹ thuật mã hóa sinusoidal**:
	Giả sử $n$ là vị trí của một token trong chuỗi, và $i$ là chỉ số của chiều trong vector, các thành phần của vector mã hóa vị trí $r_{ni}$ được tính như sau:
$$
r_{ni} =
\begin{cases}
\sin\left(\frac{n}{L^{i/D}}\right), & \text{nếu } i \text{ chẵn}, \\
\cos\left(\frac{n}{L^{(i-1)/D}}\right), & \text{nếu } i \text{ lẻ}.
\end{cases}
$$
	Trong đó:
	- $D$ là chiều của vector mã hóa vị trí.
	- $L=10000$
