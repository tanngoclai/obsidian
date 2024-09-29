---
Created at: 2024-08-22
Source:
---


**Pooling** trong CNN là một kỹ thuật giảm chiều dữ liệu, giúp giảm kích thước của các bản đồ đặc trưng (feature maps) mà không làm mất đi các thông tin quan trọng. Mục đích của pooling là giảm số lượng tham số và tính toán trong mạng, đồng thời kiểm soát hiện tượng quá khớp (overfitting) bằng cách làm cho mô hình trở nên bất biến với các thay đổi nhỏ của dữ liệu đầu vào.

### Các loại Pooling phổ biến
1. **Max Pooling**:
   - Max pooling lấy giá trị lớn nhất từ mỗi vùng nhỏ (thường là 2x2) trong bản đồ đặc trưng.
   - Điều này giúp giữ lại những đặc trưng quan trọng nhất, như các cạnh hoặc chi tiết nổi bật trong ảnh.
   - Max pooling rất phổ biến vì nó thường cho hiệu quả tốt trong việc nhận diện các đặc trưng mạnh nhất của dữ liệu.

2. **Average Pooling**:
   - Average pooling tính giá trị trung bình của các giá trị trong mỗi vùng nhỏ.
   - Thay vì chỉ giữ lại giá trị lớn nhất, average pooling mang lại một đại diện trung bình của vùng đó.
   - Average pooling có thể được sử dụng khi muốn giữ lại nhiều thông tin hơn và giảm thiểu mất mát chi tiết, nhưng nó thường ít hiệu quả hơn max pooling trong nhiều ứng dụng thị giác máy tính.

3. **Global Pooling**:
   - Global pooling lấy giá trị lớn nhất (trong global max pooling) hoặc giá trị trung bình (trong global average pooling) trên toàn bộ bản đồ đặc trưng, thay vì chỉ trong các vùng nhỏ.
   - Kết quả là một bản đồ đặc trưng có kích thước rất nhỏ (thường là 1x1), thường được sử dụng trong các lớp cuối cùng của mạng để tổng hợp toàn bộ thông tin trước khi đưa vào lớp fully connected.

### Ưu điểm của Pooling
- **Giảm kích thước đầu ra**: Pooling giúp giảm số lượng đơn vị tính toán, từ đó giảm chi phí tính toán và bộ nhớ.
- **Giảm hiện tượng quá khớp**: Bằng cách giảm độ chi tiết của bản đồ đặc trưng, pooling giúp mạng tập trung vào các đặc trưng quan trọng và tránh việc học quá chi tiết, giúp mô hình tổng quát hóa tốt hơn.
- **Tính bất biến với dịch chuyển**: Pooling làm cho mô hình trở nên bất biến với các dịch chuyển nhỏ trong dữ liệu đầu vào, tức là một đối tượng có thể được nhận diện dù nó bị dịch chuyển một chút trong ảnh.