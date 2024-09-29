---
Created at: 2024-08-29
Source:
---

# 1. Ma trận Embedding
Quá trình embedding được định nghĩa bởi một ma trận $E$ có kích thước $D \times K$, trong đó $D$ là số chiều của không gian embedding và $K$ là kích thước của từ điển. 
Mỗi vector đầu vào được mã hóa one-hot (tương tự [[Single layer networks - Classification#1.3. 1-of-K coding|1-of-K coding]]) có thể được chuyển thành vector embedding tương ứng bằng cách nhân với ma trận $E$.

# 2. Mô hình Word2Vec
Tài liệu giới thiệu kỹ thuật Word2Vec, một mô hình mạng nơ-ron hai lớp, để học ma trận embedding từ một corpus lớn của văn bản. Word2Vec có hai biến thể:

   - **Continuous Bag of Words (CBOW)**: Dự đoán từ trung tâm dựa trên các từ ngữ cảnh xung quanh.

   - **Skip-Grams**: Ngược lại với CBOW, dự đoán các từ ngữ cảnh xung quanh dựa trên từ trung tâm.

# 3. Mối quan hệ ngữ nghĩa
Các từ có mối quan hệ ngữ nghĩa được ánh xạ đến các vị trí gần nhau trong không gian embedding. 
Ví dụ, các từ như "city" và "capital" có thể xuất hiện với tần suất cao hơn như bối cảnh cho các từ mục tiêu như "Paris" hoặc "London".