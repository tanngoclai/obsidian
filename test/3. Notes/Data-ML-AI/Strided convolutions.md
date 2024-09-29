---
Created at: 2024-08-22
Source:
---


**Strided convolutions** là một kỹ thuật được sử dụng trong các mạng nơ-ron tích chập (Convolutional Neural Networks - CNN) để giảm kích thước của bản đồ đặc trưng (feature map) mà không cần phải sử dụng các lớp pooling riêng biệt. 

Thông thường, trong một phép tích chập, bộ lọc (kernel) được di chuyển qua ảnh đầu vào từng bước một, tức là stride bằng 1. Tuy nhiên, nếu bạn tăng stride lên, ví dụ như stride = 2, thì bộ lọc sẽ di chuyển qua ảnh đầu vào với bước nhảy là 2 pixel thay vì 1 pixel. Điều này dẫn đến việc giảm kích thước của bản đồ đặc trưng bởi vì bộ lọc sẽ "nhảy" qua một số vị trí và do đó giảm số lượng vị trí mà nó tính toán.

### Một số điểm quan trọng về strided convolutions:
- **Stride = 1**: Tạo ra bản đồ đặc trưng có kích thước gần giống với kích thước của ảnh đầu vào (tùy thuộc vào việc có sử dụng padding hay không).
- **Stride > 1**: Giảm kích thước của bản đồ đặc trưng vì bộ lọc bỏ qua một số vị trí trong ảnh đầu vào.
- **Hiệu ứng tương tự pooling**: Strided convolutions cũng có tác dụng tương tự như các lớp pooling trong việc giảm kích thước, nhưng với strided convolutions, quá trình này là một phần của quá trình học đặc trưng chứ không phải là một lớp tách biệt.

Sử dụng strided convolutions có thể giúp mô hình giảm số lượng tham số và tính toán, đồng thời giúp mô hình dễ dàng xử lý các dữ liệu lớn hơn bằng cách giảm dần kích thước của các bản đồ đặc trưng qua các lớp tích chập.