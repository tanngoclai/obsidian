---
Created at: 2024-08-15
Source:
  - "[[Deep_learning_foundation.pdf#page=296|Deep_learning_foundation, p.279]]"
---
**Dropout** là một kỹ thuật thường được sử dụng trong học sâu (deep learning) để ngăn chặn việc quá khớp (overfitting) của mô hình. Overfitting xảy ra khi mô hình học quá kỹ lưỡng các chi tiết của tập dữ liệu huấn luyện, dẫn đến khả năng tổng quát hóa kém khi xử lý dữ liệu mới.

### Cách hoạt động của Dropout
Trong quá trình huấn luyện mô hình, Dropout ngẫu nhiên loại bỏ (tạm thời) một số lượng các nơ-ron trong một lớp với một xác suất nhất định. Điều này có nghĩa là trong mỗi bước huấn luyện, một phần của mạng nơ-ron sẽ không hoạt động, và các nơ-ron khác sẽ phải gánh vác công việc của những nơ-ron bị bỏ đi. Xác suất bỏ đi các nơ-ron thường là một tham số hyperparameter, thường được đặt trong khoảng từ 0.2 đến 0.5.

### Ý nghĩa của Dropout
- **Giảm quá khớp**: Vì các nơ-ron không thể phụ thuộc quá mức vào một số nơ-ron cụ thể, Dropout giúp mạng học cách phân phối trọng số đều hơn, từ đó làm giảm nguy cơ quá khớp.
- **Cải thiện khả năng tổng quát hóa**: Khi các nơ-ron không được sử dụng trong một số bước huấn luyện, mô hình sẽ học được các đại diện (representations) mạnh mẽ và đa dạng hơn, từ đó cải thiện khả năng dự đoán với dữ liệu mới.

### Dropout trong thực tế
Dropout thường được sử dụng trong các lớp ẩn (hidden layers) của mạng nơ-ron. Sau khi huấn luyện xong, khi mô hình được sử dụng để dự đoán, tất cả các nơ-ron đều hoạt động, nhưng các trọng số của chúng được nhân với xác suất dropout để đảm bảo rằng tổng đầu ra của lớp vẫn được duy trì tương đương với quá trình huấn luyện.

Tóm lại, Dropout là một kỹ thuật mạnh mẽ giúp tăng cường khả năng tổng quát hóa của mô hình học sâu bằng cách giảm thiểu nguy cơ quá khớp.