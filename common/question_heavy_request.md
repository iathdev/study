1. Nếu web có một request rất nặng như export file hay gen audio. Thiết kế sao để không ảnh hưởng đến người dùng khác?

Ảnh hưởng:
- Làm nghẽ worker, queue, hoặc connection pool
- Trải nghiệm người dùng tệ

Giải pháp:
- Xử lý trong background: Heavy tasks → Background jobs

| Vấn đề                             | Giải pháp                                |
| ---------------------------------- | ---------------------------------------- |
| Request timeout                    | Đừng xử lý trực tiếp — đưa vào queue     |
| Tài nguyên CPU cao                 | Tách service export riêng (microservice) |
| Nhiều user export cùng lúc         | Dùng throttle / giới hạn / pagination    |
| Người dùng cần theo dõi tiến trình | Tạo jobId + status check API             |


2. Distributed Task Queue là gì?
(Hàng đợi tác vụ phân tán)

Đây là một kiến trúc nơi mà:

- Web server chỉ nhận request và đẩy nó vào một hàng đợi
- Worker (có thể chạy riêng biệt hoặc phân tán nhiều máy) sẽ xử lý công việc thực sự ở hậu trường

Mục tiêu:
- Giải phóng web server khỏi các tác vụ nặng
- Tăng khả năng scale theo chiều ngang
- Giảm latency cho người dùng
- Tăng độ bền (task retry, theo dõi job...)

| Thành phần       | Vai trò                                                   |
| ---------------- | --------------------------------------------------------- |
| Web Server       | Nhận HTTP request, đẩy job vào queue                      |
| Message Broker   | Trung gian truyền job (RabbitMQ, Kafka, Redis, SQS...)    |
| Worker           | Tiến trình độc lập, tiêu thụ job từ queue để xử lý        |
| Storage/Database | Ghi trạng thái job, lưu file sinh ra                      |
| Notify/Callback  | Gửi kết quả về client (email, WebSocket, API callback...) |

3. Nếu một worker 1 nhận task tuy nhiên đang làm dở thì mất mạng. Vậy làm sao để retry message cho worker 2 xử lý lại

- retry / re-delivery task phụ thuộc vào message broker (RabbitMQ, Kafka, Redis, SQS...).
- Hầu hết các broker đều hỗ trợ đảm bảo độ bền (durability) và xác nhận ACK (acknowledgement)

=> 
+ Hệ thống cần có cơ chế ACK. Task sẽ không được xoá khỏi queue cho đến khi worker gửi tín hiệu ACK cho broker là task đã xong
+ Hệ thống cần có cơ chế retry. Có thể cần đẩy vào DLQ nếu vượt quá

Với RabbitMQ (Spring AMQP hoặc raw):
- Task được gửi vào hàng đợi (queue)
- Worker 1 nhận task (consumer)
- Chưa ack (xác nhận) thì message vẫn chưa mất
- Nếu worker chết hoặc timeout → RabbitMQ sẽ requeue message
- Worker 2 có thể nhận lại và xử lý

Với Kafka:
- Kafka lưu message theo offset
- Worker (consumer) sẽ commit offset sau khi xử lý thành công
- Nếu chưa commit mà worker sập → consumer khác sẽ reprocess message từ offset cũ







