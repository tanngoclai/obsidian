**Sampling Strategies** (chiến lược lấy mẫu) là những kỹ thuật được sử dụng trong mô hình Transformer để tạo ra các chuỗi đầu ra đa dạng và sáng tạo. Khi huấn luyện một mô hình Transformer, mô hình học được xác suất phân phối của các từ tiếp theo dựa trên các từ trước đó. Sampling Strategies giúp chúng ta tận dụng xác suất phân phối này để tạo ra các kết quả khác nhau, thay vì chỉ chọn từ có xác suất cao nhất.

# 1. Mục đích

- **Đa dạng hóa đầu ra:** Thay vì luôn chọn từ có xác suất cao nhất, sampling giúp tạo ra nhiều kết quả khác nhau, tăng tính sáng tạo và tự nhiên của văn bản.

- **Điều khiển mức độ ngẫu nhiên:** Các chiến lược sampling khác nhau cho phép chúng ta điều chỉnh mức độ ngẫu nhiên của đầu ra, từ rất ngẫu nhiên đến rất xác định.

- **Khám phá không gian tiềm ẩn:** Sampling giúp chúng ta khám phá không gian tiềm ẩn của mô hình, tìm ra những kết quả bất ngờ và thú vị.
# 2. Một số chiến lược sampling

## 2.1. Greedy Search:
   - Chiến lược này chọn token có xác suất cao nhất tại mỗi bước. 
   - Ưu điểm: đơn giản và nhanh chóng.
   - Nhược điểm: dễ dẫn đến việc thiếu đa dạng trong kết quả đầu ra và có thể gây ra các vòng lặp vô tận, nơi một đoạn văn bản ngắn được lặp đi lặp lại.

## 2.2. Beam Search:
   - Giữ lại một số lượng giới hạn các giả thuyết (chuỗi token) có xác suất cao nhất tại mỗi bước.
   - Tại mỗi bước, các giả thuyết này được mở rộng thêm với các token có xác suất cao nhất và chỉ giữ lại một số lượng giới hạn các giả thuyết tốt nhất.
   - Ưu điểm: tạo ra các chuỗi có xác suất cao hơn so với Greedy Search và giảm nguy cơ lặp lại.
   - Nhược điểm: tăng chi phí tính toán, đặc biệt đối với các mô hình ngôn ngữ lớn.

## 2.3. Nucleus Sampling:
   - Thay vì chỉ chọn token có xác suất cao nhất, phương pháp này chọn token dựa trên một phân phối xác suất được cắt ngưỡng để giữ lại một tập hợp các token có xác suất tổng cộng bằng một giá trị xác định (thường là 0.9 hoặc 0.95).
   - Ưu điểm: giữ lại sự ngẫu nhiên trong việc chọn token mà vẫn đảm bảo rằng các token được chọn có xác suất tương đối cao.
   - Nhược điểm: có thể tạo ra các chuỗi có xác suất thấp hơn so với Greedy Search hoặc Beam Search.

## 2.4. Top-k Sampling:
   - Giới hạn việc chọn token trong số k token có xác suất cao nhất.
   - Cho phép tạo ra các chuỗi văn bản đa dạng hơn so với Greedy Search mà không đòi hỏi nhiều tài nguyên tính toán như Beam Search.