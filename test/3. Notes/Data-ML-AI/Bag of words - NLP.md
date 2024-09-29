
- Mô hình BOW giả định rằng các từ trong một câu hoặc đoạn văn bản **được chọn độc lập** từ cùng một phân phối xác suất. 

- **Thứ tự của các từ bị bỏ qua** hoàn toàn, và chỉ có tần suất xuất hiện của từ trong văn bản là quan trọng.

- Được sử dụng để xây dựng bộ phân loại văn bản đơn giản, ví dụ như trong phân tích cảm xúc.

- Hạn chế: Một hạn chế lớn của mô hình BOW là nó bỏ qua hoàn toàn thứ tự từ, điều này có thể làm mất đi ngữ cảnh và ý nghĩa của văn bản. Ngoài ra, nếu có từ trong bộ kiểm tra mà không có trong bộ huấn luyện, xác suất ước lượng cho từ đó sẽ là 0. Do đó, các ước lượng này thường được "làm mịn" bằng cách phân phối một mức xác suất nhỏ đồng đều cho tất cả các từ để tránh giá trị 0.