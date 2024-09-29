

1. **Mục đích và Ứng dụng**:
   - Encoder transformers được sử dụng để mã hóa thông tin từ chuỗi đầu vào thành một vector có độ dài cố định.
   - Ví dụ tiêu biểu là mô hình BERT (Bidirectional Encoder Representations from Transformers).

2. **Kiến trúc:
   - Mô hình bắt đầu với một token đầu tiên đặc biệt được gọi là `<class>`, và đầu ra tương ứng của mô hình trong quá trình huấn luyện trước sẽ bị bỏ qua. Token này sẽ trở nên quan trọng khi chúng ta thảo luận về việc điều chỉnh mô hình.
   - Mô hình được huấn luyện trước bằng cách trình bày các chuỗi token tại đầu vào. Một tập hợp con các token được chọn ngẫu nhiên (khoảng 15%) sẽ được thay thế bằng một token đặc biệt gọi là `<mask>`. Mô hình được huấn luyện để dự đoán các token bị thiếu tại các nút đầu ra tương ứng.

3. **Khái niệm Bidirectional trong BERT**:
   - Thuật ngữ "bidirectional" (hai chiều) trong BERT đề cập đến khả năng của mô hình trong việc xem xét các từ ở cả trước và sau từ bị che khuất (masked) để đưa ra dự đoán chính xác. Điều này khác biệt so với các mô hình chỉ sử dụng phần giải mã, nơi mà chỉ có thể sử dụng các token trước đó trong chuỗi để đưa ra dự đoán.
   - Vì vậy, không cần phải dịch chuyển các đầu vào sang phải một vị trí và không cần phải che giấu đầu ra của mỗi lớp để ngăn chúng nhìn thấy các token đầu vào xuất hiện sau trong chuỗi.

4. **So sánh với [[Transformers - Decoder transformers]]**:
   - Mô hình mã hóa (encoder) kém hiệu quả hơn so với mô hình giải mã (decoder) vì chỉ có một phần nhỏ các token trong chuỗi được sử dụng làm nhãn huấn luyện. 
   - Hơn nữa, mô hình mã hóa không thể tạo ra các chuỗi, điều này làm giảm tính linh hoạt của nó so với các mô hình giải mã có khả năng tạo ra các chuỗi văn bản mới.