- PoisonPill:
	- Put poison sau khi update config (afterSave), dùng PoisonPillPutInterface
	- Dùng PoisonPillReadInterface::getLatestVersion() và PoisonPillCompareInterface::isLatestVersion để check xem là nếu không phải lastest thì reject queue.

![[Pasted image 20240405171653.png]]

#### 1. Flow:
- Producer nhận message, format message -> đẩy message vào exchange -> exchange dựa theo sự trùng khớp các key mà đẩy message vào queue tương ứng -> consumer lấy message ra (dequeue) và xử lý.
- Topic hay topic exchange: có thể hiểu là 1 group các queue.
- Trong Magento 2: 
	- `communication.xml` để định nghĩa topic và input/output của message.
	- Dùng `\Magento\Framework\MessageQueue\PublisherInterface::publish(...)` để đẩy message đi (publisher).
	- File `queue_publisher.xml` để link publisher với exchange.
	- File `queue_topology.xml` để đẩy message từ exchange vào queue nếu topic name match với điều kiện.
	- File `queue_consumer.xml` dequeue.
#### 2. Cụ thể:
- communication.xml - Định nghĩa topic, input và output của message queue trong topic đấy.
	- `handler` tương đương consumer (dequeue và process message).
	- `topic.response` (test) của topic là bắt buộc nếu là queue đồng bộ, không khai báo nếu là queue không đồng bộ. Hoặc `is_synchronous="false"` nếu không đồng bộ.
	- `topic.schema` validate và xử lí cấu trúc của message trước khi đưa vào queue.
- queue_publisher.xml - Xác định connection để push message từ topic nào vào exchange nào. 
- queue_topology.xml - Tạo queue thuộc topic nào đó. Sau khi push message vào exchange thì đẩy tiếp message vào queue dựa theo tên topic có match với điều kiện không. 1 Exchange có thể đẩy message đến nhiều queue miễn là topic name thỏa mãn điều kiện.
- queue_consumer.xml - Định nghĩa consumer:
	- `queue`: tên queue mà consumer sẽ xử lí.
	- `handler`: xử lý message sau khi dequeue. Nếu có handler ở đây thì không cần handler ở communication.xml nữa, không cái này thì dùng cái kia.
	- `consumerInstance`: default value là `Magento\Framework\MessageQueue\Consumer`.
	- `onlySpawnWhenMessageAvailable` vs `consumers-wait-for-messages`:
		- `onlySpawnWhenMessageAvailable` -> check message có trong queue không, có thì mới chạy. Scope queue.
		- `consumers-wait-for-messages` -> chạy rồi mới check message có trong queue không, không có thì exit. Scope global.
		- Cả 2 đều có thể dùng với `maxIdleTime`.
	- Dùng `Magento\AsynchronousOperations\Model\MassConsumer` thì handler ở communication và consumer đều được thực thi. Ngoài trường hợp này ra thì handler ở communication chỉ chạy khi consumer không có handler.