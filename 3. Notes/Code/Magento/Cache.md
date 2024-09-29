
Public content -> Cache. 
- Ngoài URL, cần dùng các biến như language, currency, customer group, store, logged in or not để lấy cached content -> dữ liệu này lấy trong biến HTTP Context.
- Hàm \\Magento\\Framework\\App\\Http\\Context::getVaryString sẽ hash biến context cùng với URL để lưu cache. Kết quả hash được lưu trong `X-Magento-Vary` - biến nằm trong cookie.
- Cache tag: 
	- Entity cần extend  `Magento/Framework/DataObject/IdentityInterface`.
	- Ở block cũng implement `Magento/Framework/DataObject/IdentityInterface`, hàm getIdentities() sẽ gọi getIdentities của entity -> Khi entity có thay đổi thì block cũng thay đổi theo.
	- Càng nhiều cache tag thì cache càng lớn, càng chậm.
