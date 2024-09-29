---
Created at: ""
Source:
  - "[[Deep_learning_foundation.pdf#page=283|Deep_learning_foundation, p.266]]"
---
**Early stopping** là một kỹ thuật phổ biến trong huấn luyện mô hình học máy, đặc biệt là trong các mô hình học sâu (deep learning). Mục tiêu của kỹ thuật này là ngăn chặn mô hình trở nên quá khớp (overfitting) với dữ liệu huấn luyện, tức là mô hình học quá kỹ trên dữ liệu huấn luyện và không tổng quát hóa tốt trên dữ liệu kiểm tra.

### Cách hoạt động của Early Stopping:

1. **Chia dữ liệu**: Khi huấn luyện mô hình, dữ liệu thường được chia thành ba phần: dữ liệu huấn luyện (training set), dữ liệu kiểm tra (validation set), và dữ liệu kiểm định (test set).

2. **Theo dõi hiệu suất**: Trong quá trình huấn luyện, mô hình sẽ được đánh giá không chỉ trên dữ liệu huấn luyện mà còn trên dữ liệu kiểm tra sau mỗi epoch (một lượt huấn luyện trên toàn bộ dữ liệu).

3. **Điều kiện dừng**: Early stopping theo dõi lỗi (loss) hoặc độ chính xác (accuracy) trên dữ liệu kiểm tra. Nếu hiệu suất trên dữ liệu kiểm tra không cải thiện sau một số lượng epoch liên tiếp (được gọi là `patience`), quá trình huấn luyện sẽ dừng lại, ngay cả khi mô hình có thể tiếp tục học thêm trên dữ liệu huấn luyện.

4. **Tránh overfitting**: Mục tiêu của early stopping là dừng quá trình huấn luyện trước khi mô hình bắt đầu học quá mức từ dữ liệu huấn luyện, dẫn đến hiệu suất kém trên dữ liệu mới (tức là, mô hình bị overfitting).

### Lợi ích của Early Stopping:

- **Ngăn chặn overfitting**: Giúp mô hình có thể tổng quát hóa tốt hơn trên dữ liệu mới.
- **Tiết kiệm tài nguyên**: Dừng quá trình huấn luyện sớm có thể giúp tiết kiệm thời gian và tài nguyên tính toán, đặc biệt khi mô hình cần nhiều thời gian để huấn luyện.
- **Tự động hóa**: Với kỹ thuật này, người dùng không cần phải theo dõi quá trình huấn luyện một cách liên tục để xác định thời điểm dừng.

### Thực hiện Early Stopping:
Trong nhiều thư viện học máy như TensorFlow hoặc PyTorch, early stopping có thể được thực hiện một cách dễ dàng bằng cách sử dụng các callback tích hợp sẵn.

Ví dụ trong Keras (một thư viện của TensorFlow):

```python
from tensorflow.keras.callbacks import EarlyStopping

# Tạo callback cho early stopping
early_stopping = EarlyStopping(monitor='val_loss', patience=3)

# Huấn luyện mô hình với early stopping
model.fit(X_train, y_train, validation_data=(X_val, y_val), epochs=100, callbacks=[early_stopping])
```

Trong ví dụ trên, huấn luyện sẽ dừng lại nếu `val_loss` không được cải thiện sau 3 epoch liên tiếp.

![[Pasted image 20240814070223.png]] Trong hình này, việc training nên dừng lại ở nét đứt dọc