---
Created at: 2024-08-25
Source:
---
**Up sampling** (tạm dịch là "lấy mẫu lên" hoặc "tăng cỡ mẫu") là một kỹ thuật trong xử lý tín hiệu và học sâu, đặc biệt trong các mạng nơ-ron nhân tạo như CNNs, để tăng kích thước không gian của dữ liệu. Trong ngữ cảnh của mạng nơ-ron tích chập (CNN), up sampling thường được sử dụng để mở rộng kích thước của các feature maps (bản đồ đặc trưng) để khôi phục hoặc tái tạo lại độ phân giải ban đầu của hình ảnh đầu vào.

### Mục Đích của Up Sampling

Up sampling được sử dụng trong nhiều trường hợp, nhưng phổ biến nhất trong các tác vụ như:

1. **[[Image Segmentation]]:** Trong các mô hình segmentation như U-Net, việc mở rộng kích thước của feature maps cho phép mạng tạo ra một bản đồ phân đoạn có cùng kích thước với hình ảnh đầu vào, giúp phân loại từng pixel trong hình ảnh.

2. **Image Super-Resolution:** Up sampling được sử dụng để tăng độ phân giải của hình ảnh, tức là từ một hình ảnh có độ phân giải thấp tạo ra một phiên bản có độ phân giải cao hơn.

3. **Autoencoders và Generative Models:** Trong các mạng autoencoder hoặc generative models (ví dụ: GANs), up sampling được sử dụng để tạo ra dữ liệu đầu ra từ một không gian tiềm ẩn (latent space) có kích thước nhỏ hơn.

### Các Phương Pháp Up Sampling

Có nhiều phương pháp khác nhau để thực hiện up sampling, tùy thuộc vào ứng dụng cụ thể và yêu cầu của mô hình:

1. **Nearest Neighbor Up Sampling (Lấy mẫu gần nhất):**
   - Đây là phương pháp đơn giản nhất để tăng kích thước của feature maps. Mỗi giá trị pixel được sao chép sang các vị trí lân cận để mở rộng kích thước. Ví dụ, một pixel duy nhất có thể được sao chép để tạo thành một khối 2x2 pixel trong hình ảnh mở rộng.
   - Phương pháp này nhanh và đơn giản, nhưng thường dẫn đến hình ảnh có răng cưa và chất lượng kém hơn vì nó không giới thiệu thêm thông tin mới.

2. **Bilinear hoặc Bicubic Interpolation:**
   - Bilinear interpolation tính toán giá trị của pixel mới bằng cách lấy trung bình có trọng số của các pixel lân cận trong ảnh gốc. Bicubic interpolation là một phương pháp phức tạp hơn, sử dụng nhiều pixel xung quanh hơn để tính toán giá trị mới.
   - Những phương pháp này tạo ra hình ảnh mịn hơn so với nearest neighbor nhưng vẫn chỉ là ước lượng dựa trên thông tin sẵn có, không thể tạo ra chi tiết mới.

3. **Transposed Convolution (Deconvolution):**
   - Transposed convolution, còn gọi là deconvolution hoặc up convolution, là một kỹ thuật phổ biến trong học sâu để thực hiện up sampling. Thay vì thực hiện phép convolution với bộ lọc trên hình ảnh đầu vào để giảm kích thước, nó sử dụng các bộ lọc để "tăng kích thước" của feature maps.
   - Transposed convolution hoạt động bằng cách chèn các giá trị 0 giữa các pixel trong feature map gốc, sau đó áp dụng một phép convolution bình thường. Kết quả là một feature map lớn hơn với các đặc trưng được "giãn nở".

4. **Unpooling (Ngược với Pooling):**
   - Unpooling là quá trình ngược với pooling (như max pooling) để tái tạo lại kích thước ban đầu của feature maps. Unpooling giữ lại các vị trí được chọn trong quá trình pooling và đặt các giá trị tại các vị trí đó, trong khi đặt các giá trị còn lại thành 0 hoặc các giá trị đặc biệt khác.
   - Phương pháp này được sử dụng trong các kiến trúc như SegNet, nơi thông tin vị trí từ max pooling được lưu trữ và sử dụng lại để tái tạo hình ảnh trong giai đoạn up sampling.

5. **Sub-pixel Convolution:**
   - Đây là một phương pháp khác thường được sử dụng trong các mô hình super-resolution. Thay vì thực hiện một phép convolution chuẩn, sub-pixel convolution thay đổi cách sắp xếp đầu ra của các phép convolution bình thường để tạo ra hình ảnh có độ phân giải cao hơn.
   - Phương pháp này đã được chứng minh là hiệu quả trong việc tạo ra hình ảnh sắc nét hơn cho các ứng dụng siêu phân giải.