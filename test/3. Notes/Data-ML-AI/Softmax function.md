---
Created at: 2024-07-23
Source:
---
Hàm softmax là một hàm được sử dụng phổ biến trong học máy, đặc biệt là trong các mô hình phân loại. Hàm này chuyển đổi một vector các giá trị thành một vector xác suất mà tổng của chúng bằng 1. Điều này rất hữu ích trong các mô hình phân loại đa lớp, nơi ta cần xác suất để xác định lớp nào một mẫu thuộc về.

Công thức của hàm softmax cho một vector đầu vào $\mathbf{z} = [z_1, z_2, \ldots, z_K]$ được định nghĩa như sau:

$$\text{softmax}(z_i) = \frac{e^{z_i}}{\sum_{j=1}^{K} e^{z_j}} $$

Trong đó:
- $z_i$ là giá trị tại vị trí $i$ trong vector đầu vào.
- $K$ là số lượng phần tử trong vector đầu vào.
- $e$ là cơ số của logarithm tự nhiên, xấp xỉ 2.718.

Kết quả của hàm softmax là một vector các xác suất, với tổng các phần tử của vector này bằng 1. 

Ví dụ, nếu vector đầu vào là \([1.0, 2.0, 3.0]\), thì vector đầu ra sau khi áp dụng hàm softmax sẽ là \([0.090, 0.244, 0.665]\). Tổng các giá trị này là 1.0, và giá trị lớn nhất (0.665) tương ứng với giá trị đầu vào lớn nhất (3.0), cho thấy lớp 3 là lớp có xác suất cao nhất.

Hàm softmax thường được sử dụng trong lớp đầu ra của mạng nơ-ron khi giải quyết bài toán phân loại đa lớp.