Code structure
1. Layer Architecture
Phụ thuộc vào các lớp bên dưới nó
Không biết và không phụ thuộc vào các lớp bên trên sử dụng nó
Ưu điểm:
+ Đơn giản, dễ implement
+ Dễ test
Nhược điểm:
+ Khó scale khi hệ thống càng ngày càng lớn
+ Các tầng trên phụ thuộc vào tầng dưới

2. Hexagonal
Port - Adapter
Port: Interface
Adapter: Implementation
Tách biệt app không phụ thuộc vào môi trường bên ngoài
Ưu điểm:
+ Loose coupling (coupling: là nói đến sự liên kết chặt chẽ giữa các module, thay đổi một
module sẽ ảnh hưởng đến các module khác liên quan): Các phần của ứng dụng độc lập hơn.
+ Dễ dàng kiểm tra core logic của application một các độc lập và dễ dàng
+ Dễ dàng thay đổi adapter (Ví dụ: có thể thay đổi từ mysql sang postgresql, hoặc email ,
upload file) mà không làm ảnh hưởng đến application.
Nhược điểm:
+ Chưa làm quen được thì khó áp dụng
==> Bất kể sự giao tiếp nào với bên ngoài nên tạo ra các interface để phần application không
phụ thuộc vào bên ngoài.

3. Onion
Giải 2 quyết vấn đề của layer:
+ Các layer phụ thuộc lẫn nhau
+ Phần code vẫn phụ thuộc vào infrastructure (VD: Database layer)
The database (infrastructure) is not the center. It is external. Business Domain is the center:
=> DB không là trung tâm của ứng dung. Trung tâm của ứng dụng là business domain
Tuân theo Dependency Inversion:
+ Layer bên trong không biết bất kì điều gì của layer bên ngoài. Tầng bên ngoài import code
của tầng bên trong
+ Các tâng tách biệt nhau, thay đổi ở một layer sẽ ko ảnh hưởng đến những layer khác (cả
layer trước và sau)
Ưu điểm:
Domain làm trọng tâm, nên app có sự linh hoạt, không phụ thuộc vào bên ngoài. Có thể thay
đổi phần hạ tầng.
Các layer chia rõ ràng nên dễ test
Lose coupling

4. Clean
Đề cao Dependency Inversion
Số lượng layer không cố định
Domain (Entities) > Use cases > ... > ....
Ưu điểm:
Không phụ thuộc vào framework
Dễ maintance
Test
Flexible
Scale - mở rộng
Nhược điểm:
Mất thời gian làm quen, học hỏi, code

5. DDD:
Là cách thiết kế phần mềm tập trung vào việc mô hình hoá, phản ánh nghiệp vụ business.
Không quan tâm sử dụng công nghệ gì, infrastrature gì
Đặt tên class, method, vả phải phù hợp với business domain
5.1 Bounded Context:
Nhóm chức năng, thành phần & concepts.
Trông một context, sẽ có common language (Ubiquitous Language)
==> Các ngữ cảnh khác nhau sẽ chạy một cách độc lập
5.2 Collaborative Modeling:
Dev sẽ phải làm việc với domain experts để đưa ra Domain Model
Khuyến khích mn cùng hợp tác tra đổi
Để hợp tác tốt thì cần ngôn ngữ dùng chung gọi là Ubiquitous Language. Tất cả thành viên đều
phải hiểu được ngôn ngữ này. Ngôn ngữ này đẽ được phản ánh vào code
Ví dụ: Mình gọi tài khoản nhận tiền là credit account thì trong code cũng phải đặt là
creaditAccount

5.3 Tactical Design:
Entity:
Là đối tượng có id, lifecycle (thể hiện qua trường status)
Bản thân của ứng dụng sẽ phản ánh vòng đời của một tập các entity.
VD: ở luồng use cases có thể sẽ thay đổi vòng đời của một số entity. Vẽ ra được sự thay đổi
này quan trọng trong việc phát triển phần mềm (diagram)
5.4 Value Object:
Là đối tượng để mô tả tính chất hỗ trợ entity
Không có ID,
Không thể thay đổi
VD:
Address: Street, Postal Code
Money: Currency, Amount
5.5 Aggregate:
Là tập các entity
Dùng để hạn chế ảnh hưởng từ bên ngoài vào entity

Nếu không có lớp này thì những tác động bên ngoài có thể làm thay đổi các entity. Giúp làm
giảm độ phức tạp của hệ thống.
Entity yêu cầu sự thống nhất về mặt dữ liệu thì có thể đưa vào. Aggregate
Giống như một người quản lý
Service:
Repository:
5.6 Layer