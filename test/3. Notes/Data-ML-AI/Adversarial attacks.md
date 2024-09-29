---
Created at: 2024-08-25
Source:
---

Adversarial attacks trong CNN (Convolutional Neural Networks) là những kỹ thuật được thiết kế để đánh lừa một mô hình học máy bằng cách đưa ra các đầu vào được thay đổi tinh vi, nhưng vẫn giống với dữ liệu thực tế đối với con người. Các đầu vào này thường được gọi là "adversarial examples".

### Mục đích của Adversarial Attacks
Mục tiêu của các cuộc tấn công này là làm cho mô hình CNN dự đoán sai lệch hoặc phân loại sai đầu vào, mặc dù sự thay đổi trong dữ liệu đầu vào rất nhỏ và không đáng chú ý đối với con người. Các loại tấn công này thường được sử dụng để kiểm tra độ an toàn và độ bền vững của các hệ thống học máy, đặc biệt là trong các ứng dụng nhạy cảm như nhận diện khuôn mặt, xe tự lái, hay bảo mật.

### Các loại Adversarial Attacks phổ biến
1. **FGSM (Fast Gradient Sign Method):** Đây là một phương pháp tấn công đơn giản nhưng hiệu quả. Bằng cách tính toán gradient của hàm mất mát liên quan đến đầu vào và thực hiện một bước nhỏ theo hướng gradient này, phương pháp này tạo ra một biến thể của đầu vào mà mạng CNN có thể dễ dàng bị đánh lừa.

2. **PGD (Projected Gradient Descent):** Đây là một phiên bản mở rộng của FGSM, trong đó tấn công được thực hiện nhiều bước thay vì chỉ một bước. Mỗi bước sẽ thực hiện một thay đổi nhỏ theo hướng gradient và sau đó chiếu lại đầu vào vào một miền giới hạn.

3. **DeepFool:** Một thuật toán tấn công khác được thiết kế để tìm ra các thay đổi nhỏ nhất cần thiết để chuyển đầu vào qua biên phân lớp của mô hình.

4. **Carlini & Wagner (C&W) Attack:** Đây là một trong những kỹ thuật tấn công tiên tiến hơn, với mục tiêu tối ưu hóa một hàm chi phí để tạo ra các adversarial examples với sự khác biệt tối thiểu so với đầu vào ban đầu.

![[Pasted image 20240825064502.png]]