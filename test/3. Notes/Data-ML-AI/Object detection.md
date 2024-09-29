---
Created at: 2024-08-25
Source:
  - "[[Deep_learning_foundation.pdf#page=324|Deep_learning_foundation, p.308]]"
---

# 1. Bounding boxes
**Bounding boxes** trong CNN (Convolutional Neural Networks) là các khung hình chữ nhật được sử dụng để xác định vị trí của các đối tượng trong một hình ảnh. Bounding boxes chứa các tọa độ biểu thị vùng giới hạn của đối tượng mà mô hình cần nhận diện, thường được sử dụng trong các tác vụ như phát hiện đối tượng (object detection) và phân đoạn ảnh (image segmentation).

### Mục đích của Bounding Boxes trong CNN

1. **Xác định vị trí của đối tượng:** Bounding boxes được sử dụng để chỉ ra vùng trong hình ảnh mà một đối tượng cụ thể đang tồn tại. Điều này giúp mô hình không chỉ phân loại đối tượng mà còn xác định vị trí chính xác của nó trong hình ảnh.

2. **Phát hiện đối tượng (Object Detection):** Trong các tác vụ phát hiện đối tượng, CNN được huấn luyện để không chỉ nhận diện các loại đối tượng khác nhau mà còn xác định vị trí của chúng thông qua các bounding boxes. Ví dụ, trong một hình ảnh chứa nhiều đối tượng như ô tô, người, và chó, mô hình phải xác định tất cả các đối tượng và đặt một bounding box xung quanh mỗi đối tượng đó.

3. **Hỗ trợ phân đoạn ảnh:** Bounding boxes có thể được sử dụng như một bước đầu tiên để phân đoạn ảnh, giúp xác định vùng quan tâm trước khi áp dụng các kỹ thuật phân đoạn chi tiết hơn.

### Cách Hoạt Động của Bounding Boxes trong CNN

1. **Dự đoán Bounding Boxes:** Trong các mô hình phát hiện đối tượng, CNN được thiết kế để dự đoán các bounding boxes cho mỗi đối tượng trong một hình ảnh. Mô hình sẽ học các đặc trưng của hình ảnh và dự đoán các tọa độ (thường là x, y của góc trên bên trái và chiều rộng, chiều cao của khung) cho mỗi đối tượng.

2. **Loss Function cho Bounding Boxes:** Để huấn luyện mô hình phát hiện đối tượng, hàm mất mát (loss function) phải tính đến cả độ chính xác của phân loại đối tượng và độ chính xác của bounding boxes được dự đoán. Thông thường, các hàm mất mát như **Intersection over Union (IoU)** được sử dụng để đo lường mức độ trùng khớp giữa bounding box dự đoán và bounding box thực tế.

3. **Non-Maximum Suppression (NMS):** Khi một hình ảnh có nhiều đối tượng hoặc một đối tượng có thể được dự đoán nhiều lần với các bounding boxes khác nhau, kỹ thuật Non-Maximum Suppression được sử dụng để giữ lại bounding box có độ tin cậy cao nhất và loại bỏ các bounding boxes chồng chéo khác.

### Các Mô Hình Sử Dụng Bounding Boxes

1. **YOLO (You Only Look Once):** Là một trong những mô hình phát hiện đối tượng phổ biến nhất, YOLO dự đoán các bounding boxes và các nhãn lớp đối tượng đồng thời, giúp nó hoạt động nhanh và hiệu quả.

2. **SSD (Single Shot MultiBox Detector):** SSD hoạt động bằng cách sử dụng nhiều feature maps ở các cấp độ khác nhau để phát hiện đối tượng, cho phép phát hiện các đối tượng có kích thước khác nhau.

3. **Faster R-CNN:** Một phiên bản cải tiến của R-CNN, sử dụng mạng nơ-ron để tạo ra các vùng quan tâm (region proposals) và sau đó phân loại các đối tượng trong những vùng đó.

# 2. Sliding window
**Sliding windows** là một kỹ thuật cơ bản được sử dụng trong phát hiện đối tượng (object detection) bằng CNN (Convolutional Neural Networks). Kỹ thuật này giúp xác định và phân loại các đối tượng trong một hình ảnh bằng cách di chuyển một cửa sổ cố định (window) qua các vùng khác nhau của hình ảnh.

### Cách Hoạt Động của Sliding Windows trong Object Detection

1. **Chia Hình Ảnh Thành Các Cửa Sổ Nhỏ:**
   - Một hình ảnh đầu vào được chia thành các vùng nhỏ hơn (cửa sổ) bằng cách sử dụng một cửa sổ hình chữ nhật cố định, gọi là sliding window. Kích thước của cửa sổ này có thể thay đổi tùy theo yêu cầu của ứng dụng.
   
2. **Di Chuyển Cửa Sổ Qua Hình Ảnh:**
   - Cửa sổ được di chuyển (trượt) từ trái sang phải và từ trên xuống dưới qua toàn bộ hình ảnh với một bước di chuyển (stride) xác định. Với mỗi vị trí của cửa sổ, một phần nhỏ của hình ảnh được cắt ra để tạo thành một "patch" (mảnh hình ảnh).

3. **Phân Loại Các Patch:**
   - Mỗi patch được đưa vào mô hình CNN để xác định xem nó có chứa đối tượng mong muốn hay không. CNN thực hiện quá trình này bằng cách sử dụng các lớp convolutional và pooling để trích xuất các đặc trưng, sau đó các lớp fully connected cuối cùng sẽ quyết định xem patch đó thuộc về lớp đối tượng nào.

4. **Xử Lý Đa Tỷ Lệ (Multi-Scale Detection):**
   - Để phát hiện các đối tượng có kích thước khác nhau, hình ảnh có thể được thay đổi kích thước (resized) nhiều lần, và kỹ thuật sliding windows được áp dụng trên mỗi kích thước hình ảnh. Điều này giúp mô hình nhận diện được cả những đối tượng lớn và nhỏ trong cùng một hình ảnh.

### Ưu Điểm của Kỹ Thuật Sliding Windows

- **Đơn Giản và Hiệu Quả:** Sliding windows là một phương pháp đơn giản và trực tiếp để áp dụng phát hiện đối tượng, không đòi hỏi các kỹ thuật phức tạp ban đầu.
- **Khả Năng Phát Hiện Tổng Quát:** Bằng cách di chuyển cửa sổ qua toàn bộ hình ảnh, phương pháp này đảm bảo rằng tất cả các vùng của hình ảnh đều được kiểm tra.

### Hạn Chế của Kỹ Thuật Sliding Windows

1. **Tính Toán Tốn Kém:** Do phải thực hiện rất nhiều lần tính toán CNN trên mỗi patch của hình ảnh và trên nhiều kích thước khác nhau, kỹ thuật này yêu cầu nhiều thời gian xử lý và tài nguyên tính toán, làm cho nó trở nên chậm và không hiệu quả đối với các ứng dụng yêu cầu xử lý thời gian thực.

2. **Chồng Chéo Các Cửa Sổ:** Các cửa sổ có thể chồng chéo lên nhau nhiều lần, dẫn đến việc một đối tượng có thể được phát hiện nhiều lần, làm tăng tỷ lệ lỗi và cần các kỹ thuật bổ sung để loại bỏ các phát hiện dư thừa.

3. **Khó Tối Ưu Hóa:** Việc chọn kích thước cửa sổ và bước di chuyển (stride) tối ưu có thể là một thách thức, và các giá trị không phù hợp có thể dẫn đến việc bỏ sót các đối tượng hoặc phát hiện sai.

# 3. Detection across scales
Khi cần detect object trong nhiều trạng thái (đứng, nằm, ngồi...), thay vì tạo ra nhiều hình dạng tương ứng của detector, thì ta tạo ra nhiều bản sao của hình ảnh.

![[Pasted image 20240825072753.png]]