---
Created at: 2024-08-25
Source:
  - "[[Deep_learning_foundation.pdf#page=331|Deep_learning_foundation, p.315]]"
---

**Image segmentation** trong CNN (Convolutional Neural Networks) là quá trình phân chia một hình ảnh thành nhiều phần (segments) hoặc vùng khác nhau dựa trên các đặc trưng nhất định. Mục tiêu của image segmentation là gán một nhãn cho mỗi pixel trong hình ảnh để mỗi vùng đại diện cho một đối tượng cụ thể hoặc một phần của đối tượng. Đây là một bước quan trọng trong thị giác máy tính, giúp máy tính hiểu và phân tích nội dung của hình ảnh một cách chi tiết hơn.

# 1. Các Loại Image Segmentation

## 1.1 Semantic Segmentation (Phân đoạn ngữ nghĩa)
   - **Semantic segmentation** gán một nhãn lớp cho mỗi pixel trong hình ảnh, sao cho tất cả các pixel thuộc cùng một loại đối tượng được gán cùng một nhãn. Ví dụ, trong một bức ảnh có người, xe cộ, và cây cối, tất cả các pixel thuộc về người sẽ được gán nhãn là "người", các pixel thuộc về xe cộ được gán nhãn "xe cộ", và v.v.
   - Semantic segmentation không phân biệt giữa các đối tượng riêng lẻ cùng loại. Ví dụ, tất cả các ô tô trong hình ảnh sẽ được gán cùng một nhãn "ô tô", không phân biệt chúng là các ô tô khác nhau.

## 1.2. Instance Segmentation (Phân đoạn đối tượng riêng lẻ)
   - **Instance segmentation** là một bước nâng cao hơn so với semantic segmentation. Nó không chỉ gán nhãn cho các loại đối tượng mà còn phân biệt giữa các đối tượng khác nhau cùng loại trong hình ảnh. Ví dụ, nếu có hai người trong một hình ảnh, instance segmentation sẽ gán nhãn "người 1" cho người đầu tiên và "người 2" cho người thứ hai.
   - Đây là một sự kết hợp giữa phát hiện đối tượng (object detection) và semantic segmentation, vì nó xác định cả vùng chứa đối tượng và các pixel cụ thể tạo nên đối tượng đó.

## 1.3. Panoptic Segmentation
   - **Panoptic segmentation** là một sự kết hợp giữa semantic và instance segmentation, nó phân đoạn tất cả các pixel trong hình ảnh thành các nhãn lớp, bao gồm cả đối tượng và nền (background). Mỗi pixel được gán một nhãn duy nhất, dù nó là một phần của đối tượng nào đó hay chỉ là nền của hình ảnh.

# 2. Cách Hoạt Động của Image Segmentation trong CNN

CNN là công cụ mạnh mẽ để thực hiện image segmentation nhờ khả năng trích xuất các đặc trưng đa cấp từ hình ảnh. Các mô hình CNN cho image segmentation thường có một số thành phần và kỹ thuật đặc biệt để xử lý và phân đoạn hình ảnh:

## 2.1. Fully Convolutional Networks (FCNs)
   - FCNs là các mạng CNN mà trong đó tất cả các lớp fully connected (lớp kết nối hoàn toàn) được thay thế bằng các lớp convolutional. Điều này cho phép FCN nhận đầu vào là hình ảnh có kích thước bất kỳ và tạo ra đầu ra là một bản đồ đặc trưng (feature map) với kích thước tương ứng.
   - FCNs áp dụng một loạt các lớp convolutional để trích xuất đặc trưng và một bộ các lớp convolutional ngược (transposed convolution hoặc deconvolution) để xây dựng lại bản đồ đặc trưng thành phân đoạn có cùng kích thước với hình ảnh đầu vào.

## 2.2. U-Net
   - U-Net là một kiến trúc CNN phổ biến cho image segmentation, ban đầu được thiết kế cho phân đoạn ảnh y tế. Nó có một phần "encoder" để trích xuất đặc trưng (tương tự như FCN) và một phần "decoder" để tái tạo lại hình ảnh phân đoạn.
   - U-Net sử dụng các skip connections (kết nối bỏ qua) để kết nối các lớp tương ứng trong phần encoder và decoder, giúp mô hình học được cả đặc trưng chi tiết và ngữ cảnh tổng quát.

## 2.3. SegNet
   - SegNet là một kiến trúc CNN khác dành cho phân đoạn ngữ nghĩa. Nó sử dụng một encoder-decoder giống như U-Net, nhưng với các kỹ thuật khác nhau để giải mã các đặc trưng và tạo ra phân đoạn đầu ra. ([[Up-sampling]])
   - SegNet lưu trữ các chỉ số pooling từ quá trình trích xuất đặc trưng và sử dụng chúng trong quá trình tái tạo để giúp xác định vị trí chính xác của các đặc trưng.


## 2.4. Mask R-CNN
   - Mask R-CNN là một mở rộng của Faster R-CNN, thêm một nhánh cho segmentation vào mạng. Nó thực hiện instance segmentation bằng cách sử dụng các bounding boxes được phát hiện để tạo ra các mặt nạ nhị phân (binary masks) cho từng đối tượng trong hình ảnh.
