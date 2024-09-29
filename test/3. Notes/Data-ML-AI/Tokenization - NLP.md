---
Created at: 2024-08-29
Source:
---


# 1. Vấn đề của từ điển cố định
   Sử dụng từ điển cố định có thể gặp phải nhiều vấn đề, như không thể xử lý các từ không có trong từ điển hoặc các từ viết sai chính tả. Nó cũng không xử lý được các ký tự đặc biệt, ký hiệu, hoặc các chuỗi ký tự như mã máy tính.

# 2. Tokenization dựa trên ký tự
   Một cách tiếp cận để giải quyết vấn đề trên là làm việc ở mức ký tự thay vì từ. Tuy nhiên, điều này làm mất cấu trúc ngữ nghĩa quan trọng của ngôn ngữ và yêu cầu mạng neural học cách tái cấu trúc từ từ các ký tự cơ bản, làm tăng chi phí tính toán.

# 3. Lợi ích của kết hợp mức ký tự và mức từ
 Kết hợp lợi ích của biểu diễn ở mức ký tự và mức từ bằng cách sử dụng bước tiền xử lý để chuyển đổi chuỗi từ và ký hiệu thành chuỗi các token. Các token này có thể bao gồm từ thông thường, các đoạn của từ dài hơn, và các ký tự đơn lẻ để tạo thành các từ ít phổ biến hơn.

# 4. Byte Pair Encoding (BPE)
Một kỹ thuật được gọi là **byte pair encoding** (BPE) được sử dụng để nén dữ liệu, có thể được điều chỉnh cho việc token hóa văn bản. Quá trình này bắt đầu với các ký tự riêng lẻ và liên tục kết hợp chúng thành các chuỗi dài hơn dựa trên tần suất xuất hiện của cặp ký tự liền kề. Quá trình này dừng lại khi đạt đến số lượng token cố định trước.

![[Pasted image 20240829065726.png]]