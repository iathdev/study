# 🧩 Dependency Injection (DI)

## 1. Khái niệm

**Dependency Injection (DI)** là kỹ thuật trong lập trình dùng để **giảm sự phụ thuộc chặt chẽ (tight coupling)** giữa các class và **tăng tính mở rộng, dễ test** của hệ thống.

---

## 2. Ví dụ đơn giản

### ❌ Không dùng DI

```php
class A {
    private $b;
    public function __construct() {
        $this->b = new B();  // A tự tạo B
    }
}
```

### ✅ Dùng DI

```php
class A {
    private $b;
    public function __construct(B $b) {
        $this->b = $b;  // B được tiêm từ bên ngoài
    }
}
```
## 3. Lợi ích của Dependency Injection

- ✅ **Tăng khả năng tái sử dụng**
- ✅ **Dễ test hơn** (có thể mock các dependency)
- ✅ **Giảm coupling (phụ thuộc chặt)**
- ✅ **Tuân thủ nguyên lý SOLID** (đặc biệt là chữ D: Dependency Inversion)

---

## 4. Các loại Dependency Injection

| Kiểu DI              | Mô tả                                                           |
|----------------------|------------------------------------------------------------------|
| **Constructor Injection** | Tiêm phụ thuộc qua constructor (phổ biến nhất)           |
| **Setter Injection**      | Tiêm qua phương thức setter                              |
| **Interface Injection**   | Lớp implement interface để nhận dependency qua method     |

---

## 5. Ví dụ Dependency Injection trong Laravel (PHP)

Laravel sử dụng DI thông qua **Service Container**:

```php
class Mailer {
    public function send() {
        echo "Sending mail";
    }
}

class UserController {
    protected $mailer;

    public function __construct(Mailer $mailer) {
        $this->mailer = $mailer;
    }

    public function notifyUser() {
        $this->mailer->send();
    }
}
```

Laravel sẽ **tự động inject** `Mailer` vào `UserController`.

---

## 6. Ví dụ Dependency Injection trong Java

### a. ❌ Không dùng DI

```java
public class Service {
    public void doSomething() {
        System.out.println("Doing something...");
    }
}

public class Controller {
    private Service service;

    public Controller() {
        this.service = new Service(); // Coupling chặt
    }
}
```

### b. ✅ Dùng Constructor Injection (thủ công)

```java
public class Controller {
    private Service service;

    public Controller(Service service) {
        this.service = service;
    }

    public void execute() {
        service.doSomething();
    }
}

public class Main {
    public static void main(String[] args) {
        Service service = new Service();
        Controller controller = new Controller(service);
        controller.execute();
    }
}
```

### c. ✅ Dùng Spring Framework

```java
@Component
public class Service {
    public void doSomething() {
        System.out.println("Doing something...");
    }
}

@Component
public class Controller {
    private final Service service;

    @Autowired
    public Controller(Service service) {
        this.service = service;
    }

    public void execute() {
        service.doSomething();
    }
}

@SpringBootApplication
public class MyApp {
    public static void main(String[] args) {
        ApplicationContext context = SpringApplication.run(MyApp.class, args);
        Controller controller = context.getBean(Controller.class);
        controller.execute();
    }
}
```

---

## 7. Ưu và nhược điểm

| Ưu điểm                                 | Nhược điểm                                |
|-----------------------------------------|-------------------------------------------|
| ✅ Dễ test                                | ❌ Cần setup nhiều nếu không có DI container |
| ✅ Tăng khả năng mở rộng                  | ❌ Code có vẻ phức tạp hơn ban đầu         |
| ✅ Tuân thủ tốt các nguyên lý OOP (SOLID) | ❌ Cần hiểu rõ cách hoạt động của DI       |

---

## 8. Các framework hỗ trợ DI

| Ngôn ngữ  | Framework/Thư viện              |
|-----------|---------------------------------|
| Java      | Spring, Guice                   |
| PHP       | Laravel (Service Container)     |
| C#        | .NET Core DI                    |
| Python    | `dependency-injector`, `injector` |



