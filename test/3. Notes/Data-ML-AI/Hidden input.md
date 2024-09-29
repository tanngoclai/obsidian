---
Created at: 2024-08-06
Source:
---

Trong deep learning, "hidden input" thường ám chỉ đầu vào của các lớp ẩn (hidden layers) trong một mạng nơ-ron. Đây là các lớp nằm giữa lớp đầu vào (input layer) và lớp đầu ra (output layer). Cụ thể:

1. **Hidden Layers (Lớp ẩn)**: Lớp ẩn là các lớp nằm giữa lớp đầu vào và lớp đầu ra. Chúng chứa các nơ-ron (neurons) mà tại đó các phép biến đổi và tính toán phức tạp diễn ra. Mục đích của các lớp ẩn là trích xuất các đặc trưng (features) từ dữ liệu đầu vào để dự đoán chính xác hơn ở lớp đầu ra.

2. **Hidden Input (Đầu vào của lớp ẩn)**: Đầu vào của lớp ẩn là các giá trị (thường là các vectơ) được truyền từ lớp trước đó. Ví dụ, đầu vào của lớp ẩn đầu tiên chính là đầu ra của lớp đầu vào, và đầu vào của các lớp ẩn tiếp theo là đầu ra của lớp ẩn trước đó.

Quá trình tính toán trong mỗi nơ-ron của lớp ẩn thường bao gồm:

- **Linear Transformation (Biến đổi tuyến tính)**: Tính tổng có trọng số của các đầu vào và cộng thêm một hằng số gọi là bias (độ chệch).
- **Activation Function (Hàm kích hoạt)**: Áp dụng một hàm phi tuyến (như ReLU, sigmoid, tanh, v.v.) để quyết định xem nơ-ron có kích hoạt hay không. 

Công thức cơ bản của một nơ-ron trong lớp ẩn có thể viết như sau:

$$ h = f(Wx + b) $$

Trong đó:
- $h$ là đầu ra của nơ-ron (hidden output),
- $W$ là ma trận trọng số,
- $x$ là đầu vào của nơ-ron,
- $b$ là bias,
- $f$ là hàm kích hoạt.

Hiểu rõ về hidden input và cách nó được xử lý trong các lớp ẩn là rất quan trọng để nắm vững cách hoạt động của các mạng nơ-ron sâu và cải thiện hiệu suất của các mô hình deep learning.