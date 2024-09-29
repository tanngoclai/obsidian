---
Created at: 2024-08-14
Source:
  - "[[Deep_learning_foundation.pdf#page=285|Deep_learning_foundation, p.268]]"
---
**Double descent** là một hiện tượng quan sát được trong việc huấn luyện mô hình học máy, đặc biệt là trong các mô hình có nhiều tham số như mạng neural (neural networks). Nó mô tả một mối quan hệ không tuyến tính giữa độ phức tạp của mô hình và lỗi trên tập kiểm tra (test error). Đây là một trong những hiện tượng mới được khám phá và thu hút sự chú ý vì nó thách thức hiểu biết truyền thống về overfitting.

### Mô hình Truyền thống (Bias-Variance Tradeoff):

Trước khi giải thích về double descent, cần hiểu qua về mối quan hệ giữa bias (độ thiên lệch) và variance (độ biến thiên) trong học máy:

- **Bias**: Là sai số xuất hiện khi mô hình đơn giản hóa quá mức (underfitting). Mô hình có bias cao sẽ không thể nắm bắt hết các mối quan hệ phức tạp trong dữ liệu.
  
- **Variance**: Là sai số xuất hiện khi mô hình phức tạp hóa quá mức (overfitting). Mô hình có variance cao sẽ học quá mức chi tiết từ dữ liệu huấn luyện, dẫn đến việc không tổng quát hóa tốt trên dữ liệu mới.

Theo cách hiểu truyền thống, khi tăng độ phức tạp của mô hình:
- Ban đầu, test error giảm vì mô hình có thể học tốt hơn các mẫu dữ liệu.
- Tuy nhiên, sau một điểm nào đó, test error bắt đầu tăng trở lại vì mô hình bắt đầu overfitting (đây là điểm "uốn" trong đồ thị, tạo nên hình chữ U).

### Double Descent:

Hiện tượng **double descent** mở rộng hiểu biết này bằng cách chỉ ra rằng test error không chỉ đơn giản là tăng khi mô hình phức tạp hơn sau điểm uốn. Thay vào đó, sau khi đạt đỉnh tại điểm overfitting, test error có thể giảm xuống một lần nữa khi độ phức tạp của mô hình tiếp tục tăng.

#### Cụ thể:

1. **Vùng đầu tiên (Bias-dominant region)**: Khi mô hình còn đơn giản, test error giảm dần khi độ phức tạp của mô hình tăng lên, do mô hình có thể học thêm các mẫu dữ liệu.

2. **Điểm uốn (Traditional overfitting)**: Khi mô hình trở nên đủ phức tạp để vừa khít với dữ liệu huấn luyện, test error đạt đỉnh. Đây là điểm overfitting trong cách hiểu truyền thống.

3. **Vùng thứ hai (Variance-dominant region)**: Khi tiếp tục tăng độ phức tạp (chẳng hạn tăng số lượng tham số của mô hình), test error bắt đầu giảm lại. Điều này xảy ra do mô hình quá phức tạp, nhưng thay vì chỉ đơn giản hóa các mẫu dữ liệu huấn luyện, mô hình có thể học các mẫu phức tạp hơn và tổng quát hóa tốt hơn trên dữ liệu mới.

4. **Double Descent**: Đồ thị test error không chỉ có một điểm uốn mà có hai điểm uốn, tạo nên hai pha giảm và tăng, dẫn đến hình dạng "double descent" (chữ "W" hoặc "U kép").

### Ý nghĩa của Double Descent:

Hiện tượng này chỉ ra rằng tăng thêm độ phức tạp của mô hình có thể dẫn đến một hiệu suất tốt hơn, thậm chí sau khi mô hình đã bị overfitting. Điều này đặc biệt quan trọng trong thời đại của các mô hình lớn như mạng neural sâu, nơi mà việc tăng số lượng tham số (ví dụ: số lớp, số neuron) có thể cải thiện hiệu suất, thay vì làm giảm nó như cách hiểu truyền thống.

Hiện tượng double descent thách thức các lý thuyết cổ điển về bias-variance tradeoff và mở ra hướng nghiên cứu mới về cách chọn và huấn luyện các mô hình phức tạp trong học máy.

![[Pasted image 20240814071222.png]]