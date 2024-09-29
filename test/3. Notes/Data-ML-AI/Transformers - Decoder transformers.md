
Decoder-only Transformers, một dạng kiến trúc được sử dụng phổ biến trong các mô hình ngôn ngữ như GPT (Generative Pre-trained Transformer).

 Sử dụng kiến trúc Transformer để xây dựng một mô hình tự hồi quy ([[Autoregressive models - NLP]]) nhằm dự đoán phân phối điều kiện của mỗi token dựa trên các token trước đó trong chuỗi.

1. **Chức năng chính:** Decoder Transformers được thiết kế để tạo ra đầu ra tuần tự, thường là văn bản, dựa trên một đầu vào đã được mã hóa.

2. **Cấu trúc:**
   - Gồm nhiều lớp decoder được xếp chồng lên nhau.
   - Mỗi lớp decoder có ba thành phần chính: self-attention, cross-attention, và feedforward neural network.

3. **[[Transformers - Attention#3. Self-attention|Self-attention]]**: Cho phép mô hình tập trung vào các phần khác nhau của chuỗi đầu ra đã được tạo ra.

4. **Masked attention (mask [[Transformers - Attention#6. Multi-head attention|multi-head attention]])**: Sử dụng kỹ thuật masked attention để đảm bảo rằng mỗi token chỉ có thể chú ý đến các token trước đó trong chuỗi đầu ra, ẩn đi các phần chưa dịch đến.

**Ứng dụng**: Được sử dụng trong nhiều mô hình ngôn ngữ như GPT (chỉ sử dụng decoder) và trong các mô hình dịch máy như phần decoder của BERT.