# N-layer:
Chia thành nhiều layer
Thông thường sẽ gồm 4 layer:
+ User Interface: tương tác với người dùng
+ Business layer: Xử lý logic của hệ thông
+ Repository layer: Nhiệm vụ tương tác với tầng data access
+ Database layer: tầng dữ liệu: database,..

——————————————————————————————

# Hexagonal architecture:
Port -Adapter
Kiến trúc hình lục giác:
Bên trong là application core
Bên ngoài là những gì mà ứng dụng tương tác: UI, user, DB,...
Bên trong & bên ngoài tương tác với nhau thông qua adapter
Các thành phần bên ngoài phụ thuộc vào bên trong nhưng không ngược lại
Dễ dàng thay đổi công nghệ sử dụng

Port: Interface
Adapter: Implement của interface, có thể dễ dàng thay đổi

Một port có nhiều adapter implement
Sử dụng DI để giao tiếp giữa port & adapter
Ví dụ:
Port: service
Adapter: laravel
=> Có thể thay đổi adapter sang ngôn ngữ khác

——————————————————————————————

# Clean architecture:
Là kiểu kiến trúc layer
Triết lý:
- Cô lập business logic: entities + use case
- Tương tự hexagonal: cô lập business logic và giao tiếp với bên ngoài thông qua port & adapter
- Sử dụng Dependency inversion: High level & low level ko phụ thuộc lẫn nhau, Chúng phụ
thuộc vào interface
- Chiều phụ thuộc đi từ trong ra ngoài. Bên ngoài phụ thuộc vào bên trong & không ngược lại
- Kiến trúc gồm 4 layer đi từ trong ra ngoài:

1. Entities: là khái niệm miêu tả business logic chính và là tâng quan trọng nhất, trong OOP nó
chính là object
2. Use case: các rule liên quan trực tiếp đến ứng dụng. Chứa logic liên quan đến từng use case
VD: Use Case đăng ký tài khoản (tạo mới một Person/Account) sẽ cần tổ hợp một hoặc nhiều
Entities tuỳ vào độ phức tạp của Use Case.
3. Interface Adapter: tập hợp các adapter tương tác với các công nghệ, chuyển đối dữ liệu để
phù hợp với từng use case

4. Framework & Driver: DB, UI, ...
Ưu điểm:
+ Chia để trị, tầng nào làm nhiệm vụ của tầng đấy
+ Dễ maintance, scale
+ Dễ unit test
Nhược:
+ Kông kềnh phức tạp
+ Tính trừu tượng cao

——————————————————————————————

# Domains:
+ Use case: là một phần business logic, biểu diễn một nhiệm vụ duy nhất mà hệ thống cần thực
hiện
==> Các use case cần độc lập và tách biệt với nhau hoàn toàn. Giống Single Responsibility
trong SOLID
Tại sao cần thiết kế ứng dụng xoay quanh use case:
- Đảm bảo code có thể tái sử dụng
- Đảm bảo nguyên tắc Single Responsibility trong SOLID
- Dễ dàng nắm bắt business hơn là phải tập trung vào Controller hay Model
- Dễ dàng kiểm thử

+ Action:

Ví dụ:
Thay vì có một OrderService bao gồm: index, create, edit, ...
Thì chi thành các use case (Action)
- Use case (action): tạo order
- Sẽ có các action nhỏ hơn:
+ Kiểm tra thời gian hợp lệ (ở cart & order)
+ Kiểm tra tồn kho (ở cart & order)
+ Kiểm tra các logic khác
+ Tính toán giá
+ Lưu trữ đơn hàng và các thông tin liên quan vào DB
- Mỗi action - repository sẽ giao tiếp thông qua repository & các biến truyền vào là DTO (Data)
khi cần một object
- Gồm các entities:
+ item: đại diện cho thông tin sản phẩm
+ order: đại diện cho một đơn hàng
+ order_product: lưu order mua những item nào
Các action được khỏi tạo thông qua phương thức app() của Laravel: là một helper function: trả
về instance của app container
Giúp truy cập vào các dependencies mà container quản lý

```
trait AsAction
{
/**

* @return static
*/
public static function make(): static
{
return app(static::class);
}
}
```

make(): factory method khỏi tạo instance. Gọi đến helper app() của Laravel
Sử dụng:
Khi sử dụng sẽ gọi đến make để làm việc
Tại sao lại sử dụng trait mà ko đủ dụng abstract class:
+ Giải quyết vấn đề đa kế thừa
+ Tái sử dụng: sử dụng trait action có thể ở data hoặc bất kì đâu

