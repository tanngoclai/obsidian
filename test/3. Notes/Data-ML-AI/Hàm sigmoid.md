---
Created at: 2024-07-23
Source:
---

# 1 Định nghĩa

Hàm sigmoid, còn được gọi là hàm logistic, là một hàm toán học phi tuyến thường được sử dụng trong mạng nơ-ron nhân tạo và học máy. Nó được biểu diễn bằng công thức sau: $$f(x) = \frac{1}{(1+\exp(-x))}$$
# 2 Đặc điểm:

- **Đường cong hình chữ S:** Hàm sigmoid có dạng đường cong hình chữ S, với giá trị đầu ra nằm trong khoảng 0 và 1.
- **Giới hạn:** Hàm sigmoid có giá trị hội tụ về 0 khi x tiến về âm vô cùng và hội tụ về 1 khi x tiến về dương vô cùng.
- **Đạo hàm:** Đạo hàm của hàm sigmoid có thể được tính dễ dàng: $$f'(x) = f(x)  (1 - f(x))$$

# 3 Ứng dụng

- **Mạng nơ-ron nhân tạo:** Hàm sigmoid được sử dụng như hàm kích hoạt cho các nơ-ron trong mạng nơ-ron nhân tạo. Nó giúp giới hạn giá trị đầu ra của nơ-ron và tạo ra tính phi tuyến cho mạng.
- **Phân loại nhị phân:** Hàm sigmoid thường được sử dụng trong các mô hình phân loại nhị phân, nơi đầu ra cần được giải thích như xác suất. Ví dụ, trong mô hình logistic regression, hàm sigmoid được sử dụng để dự đoán xác suất một mẫu dữ liệu thuộc về một lớp cụ thể.
- **Mạng nơ-ron tuần hoàn:** Hàm sigmoid cũng có thể được sử dụng trong mạng nơ-ron tuần hoàn (RNN) để mô hình hóa các chuỗi dữ liệu phụ thuộc thời gian.