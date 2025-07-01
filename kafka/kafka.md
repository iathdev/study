# Các khái niệm cơ bản

## 1. Kafka topic
- Là luồng dữ liệu cụ thể trong kafka
- Không giới hạn số lượng topic
- Hỗ trợ nhiều dạng message format
- Dữ liệu trong topic là dạng binary

Producer > Kafka (Topic) > Consumer

Một producer quyết định gửi message đến topic nào dựa trên các chiến lược sau:
- Dựa vào tên topic (Hardcoded topic name)
- Dựa vào loại dữ liệu/message type
- Dựa vào routing key hoặc logic tùy chỉnh
- Dựa vào cấu hình từ database hoặc config service

## 1.1. Kafka message
- Bao gồm key - value, compression type (phương thức nén của dữ liệu), headers, partition + offset, timestamps (thời gian truyền tải)
- value: là giá trị message truyền tải
- key: 

- Message serializer: để encode message trong quá trình gửi publish message sang dạng binary
- Key serializer, Value serializer để consumer decode lại dữ liệu

Khi nào message bị xoá?
- Khi hết thời gian retention time
- Khi tổng dung lượng topic đạt giới hạn (Log Retention Size)
- Xóa log segment cũ (Log Segment Cleanup)
- Topic có policy xóa dữ liệu (Delete hoặc Compact)

## 1.2. Kafka partition
- Mỗi topic được chia thành nhiều partition
- Mỗi messgae trong partition được đảm bảo tính tuần tự theo thời gian (nhưng trong nhiều partition của topic thì ko) 
- Dữ liệu trong kafka topic là dữ liệu không thể thay đổi (imutable)
- Dữ liệu được kafka lưu trữ trong khoảng thời gian nhất định - có thể cấu hình (retention time)

## 1.3 Producers
- Là thành phần gửi data (message) vào trong kafka topic 
- Message bao gồm key - value

- Nếu key = null: message được gửi vào partition RoundRobin
- Nếu key <> null: các message có cùng key sẽ được gửi vào chung 1 partition (theo thuật toán hasing)

### RoundRobin trong Kafka:
- RoundRobin là một chiến lược phân phối message của Kafka Producer tới các partition của một topic một cách tuần tự, luân phiên.

➡️ Nếu không có key trong message, thì Kafka Producer mặc định sẽ dùng RoundRobin (tuần tự từng partition).
#### Cơ chế hoạt động
- Giả sử topic có 3 partitions: P0, P1, P2
- Producer gửi 6 message không có key, thì Kafka sẽ gửi theo vòng tròn như sau:

| Message | Partition được chọn |
| ------- | ------------------- |
| M1      | P0                  |
| M2      | P1                  |
| M3      | P2                  |
| M4      | P0                  |
| M5      | P1                  |
| M6      | P2                  |
Cân bằng tải tốt, nhưng không đảm bảo thứ tự cho cùng 1 entity (vì không có key)

#### So sánh: RoundRobin vs Sticky vs Keyed
| Strategy       | Phân phối như thế nào                                                                   | Giữ được thứ tự theo key? | Load balance?    |
| -------------- | --------------------------------------------------------------------------------------- | ------------------------- | ---------------- |
| **RoundRobin** | Mỗi message gửi vào partition khác nhau (luân phiên)                                    | ❌ Không                   | ✅ Tốt            |
| **Keyed**      | Dựa trên `hash(key)` để chọn partition                                                  | ✅ Có                      | ❌ (nếu key skew) |
| **Sticky**     | Gửi nhiều message vào **cùng 1 partition** trong khoảng thời gian ngắn để giảm overhead | ❌ Không                   | ✅ Rất tốt        |

###  Có nên dùng RoundRobin?
| Câu hỏi                                         | Trả lời                 |
| ----------------------------------------------- | ----------------------- |
| Có cần giữ thứ tự theo key không?               | ❌ Không → dùng được     |
| Muốn phân phối message đồng đều?                | ✅ Dùng tốt              |
| Dữ liệu quan trọng theo nhóm (userId, orderId)? | ❌ KHÔNG dùng RoundRobin |


Tóm lại:
- Không cần thứ tự cố định của message theo key.
- Cần phân phối đều dữ liệu giữa các partition để tận dụng tài nguyên.
- Tránh partition bị quá tải khi một số key có nhiều message hơn.

### DefaultPartitioin:
- Dự trên hasing key để đảm bảo các message có cùng key sẽ luôn đi vào 1 partition
- Vì chỉ đi vào 1 partition nên đảm bảo tính tuần tự. Consumer sẽ đọc theo thứ tự FIFO

## 1.4 Consumer
- Đọc data từ topic theo thứ tự tuần tự

## 1.5 Consumer group
Trường hợp producers gửi rất nhiều dữ liệu vào trong topic và chỉ có 1 consumer để xử lý => consumer không có đủ khả năng để xử lý
-> Cần tăng số lượng consumer
-> Để đảm bảo mỗi message trong 1 topic được xử lý một lần duy nhất -> sinh ra khái niệm consumer group

Có 2 trường hợp cần lưu ý:
- Số lượng consumer trong group < số lượng partition: một consumer đọc nhiều hơn một partition
- Số lượng consumer trong group > số lượng partition: có consumer bị inactive


- Có một topic mặc định của kafka là _consumer_offsets để lưu thông tin offset(vị trí) nào đã được đọc
Khi một consumer đọc message từ Kafka, nó cần ghi nhớ offset (vị trí) cuối cùng mà nó đã đọc, để khi khởi động lại có thể tiếp tục từ đúng điểm đó.
_consumer_offsets là một internal topic trong Apache Kafka, được sử dụng để lưu trữ offset của consumer groups. Đây là nơi Kafka lưu lại thông tin về vị trí đọc của từng consumer trong từng partition, giúp đảm bảo rằng consumer có thể tiếp tục đọc dữ liệu từ đúng vị trí nếu bị restart hoặc có lỗi xảy ra.
Tóm lại, _consumer_offsets là trái tim của Kafka Consumer Group, giúp quản lý offset, tránh mất dữ liệu, và tối ưu hiệu suất của hệ thống.


## 1.6 Serializer trong Kafka
- Là quá trình dữ liệu được chuyển thành byte (để kafka xử lý) và ngược lại (DeSerializer) chuyển dữ liệu của kafka về dạng mà ứng dụng có thể xử lý
- Các loại serializer phổ biến: String, Integer, JSON, Avro...

Tóm lại:
Serializer hoạt động ở Producer để chuyển đổi dữ liệu thành byte array.
Deserializer hoạt động ở Consumer để chuyển byte array ngược lại thành object.

