---
Created at: 2024-07-04
Source:
  - "[[ML cơ bản.pdf#page=103|book_ML_color, Chương 8]]"
tags: 
---
## 1 Giới thiệu

- **Overfitting (quá khớp)**: Là hiện tượng mà mô hình học quá chi tiết từ dữ liệu huấn luyện (training set) đến mức nó không thể tổng quát hóa tốt cho dữ liệu mới (test set). Điều này dẫn đến hiệu suất kém trên dữ liệu kiểm tra hoặc dữ liệu thực tế.
- **Nguyên nhân**: Thường xảy ra khi mô hình quá phức tạp so với lượng dữ liệu hoặc không có đủ dữ liệu để huấn luyện mô hình.

## 2 Validation

- **Validation (xác thực)**: Là quá trình đánh giá mô hình trên một tập dữ liệu riêng biệt (validation set) không được sử dụng trong quá trình huấn luyện. Mục đích là để ước lượng hiệu suất của mô hình trên dữ liệu chưa thấy trước. Tập dữ liệu này được tách từ tập training ra.
- **K-fold cross-validation**: Dữ liệu được chia thành $k$ phần. Mỗi phần sẽ lần lượt được sử dụng làm tập kiểm tra, trong khi $k-1$ phần còn lại được sử dụng làm tập huấn luyện. Kết quả được lấy trung bình để ước lượng hiệu suất của mô hình.
    - **Ưu điểm**: Giúp đánh giá mô hình một cách toàn diện hơn và giảm thiểu nguy cơ overfitting.

## 3 Regularization

- **Regularization (điều chuẩn)**: Là kỹ thuật thêm các ràng buộc hoặc điều kiện vào quá trình huấn luyện để ngăn chặn overfitting. Điều này được thực hiện bằng cách thêm các điều khoản phạt vào hàm mất mát.
- **Các kỹ thuật điều chuẩn phổ biến**:
    - **L1 Regularization (Lasso)**: Thêm thêm hệ số tỉ lệ với tổng trị tuyệt đối của các trọng số. Kết quả là một số trọng số có thể trở về 0, giúp mô hình đơn giản hơn.
        - $L_{L1} = \lambda \sum |w|$
    - **L2 Regularization**: Thêm hệ số tỷ lệ với tổng bình phương của các trọng số. Điều này giúp làm giảm biên độ của các trọng số nhưng không làm cho chúng trở về 0.
        - $L_{L2} = \lambda \sum w^2$
- **Early Stopping**: Là kỹ thuật dừng quá trình huấn luyện khi hiệu suất trên tập validation không cải thiện nữa, tránh việc mô hình học quá nhiều từ dữ liệu huấn luyện.
- **Dropout**: Kỹ thuật thường được sử dụng trong mạng nơ-ron để ngẫu nhiên loại bỏ một số đơn vị trong quá trình huấn luyện, giúp mô hình trở nên linh hoạt và tổng quát hơn.