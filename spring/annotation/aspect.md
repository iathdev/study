## Khái niệm

- `@Aspect` trong Java (Spring AOP)
- `@Aspect` là một annotation thuộc Spring AOP (Aspect-Oriented Programming) dùng để đánh dấu một class là một Aspect — tức là một lớp chứa các cross-cutting concerns (các logic dùng chung như logging, security, transaction, ...).

- Các loại Advice (thành phần logic trong Aspect)
| Annotation        | Mô tả                                                         |
| ----------------- | ------------------------------------------------------------- |
| `@Before`         | Chạy **trước** khi method được gọi                            |
| `@After`          | Chạy **sau** khi method kết thúc (dù thành công hay lỗi)      |
| `@AfterReturning` | Chạy **sau khi method return thành công**                     |
| `@AfterThrowing`  | Chạy nếu method **ném exception**                             |
| `@Around`         | Bao quanh method (cho phép kiểm soát toàn bộ vòng đời method) |

## Khi nào nên dùng @Aspect?
- Logging request/response
- Kiểm tra quyền trước khi truy cập method
- Tự động retry khi lỗi
- Tính thời gian thực thi method
- Bắt exception và xử lý chung

## Ví dụ

```java
@Aspect
@Component
public class LoggingAspect {

    // 1. @Before - Trước khi method thực thi
    @Before("execution(* com.example.demo.DemoService.*(..))")
    public void beforeAdvice(JoinPoint joinPoint) {
        System.out.println("Before: Đang gọi method: " + joinPoint.getSignature().getName());
    }

    // 2. @After - Sau khi method kết thúc (dù lỗi hay thành công)
    @After("execution(* com.example.demo.DemoService.*(..))")
    public void afterAdvice(JoinPoint joinPoint) {
        System.out.println("After: Method đã chạy: " + joinPoint.getSignature().getName());
    }

    // 3. @AfterReturning - Sau khi method return thành công
    @AfterReturning(pointcut = "execution(* com.example.demo.DemoService.sayHello(..))", returning = "result")
    public void afterReturningAdvice(JoinPoint joinPoint, Object result) {
        System.out.println("AfterReturning: Method trả về -> " + result);
    }

    // 4. @AfterThrowing - Sau khi method ném lỗi
    @AfterThrowing(pointcut = "execution(* com.example.demo.DemoService.throwException(..))", throwing = "ex")
    public void afterThrowingAdvice(JoinPoint joinPoint, Exception ex) {
        System.out.println("AfterThrowing: Method ném lỗi -> " + ex.getMessage());
    }

    // 5. @Around - Bao quanh method, kiểm soát toàn bộ luồng
    @Around("execution(* com.example.demo.DemoService.sayHello(..))")
    public Object aroundAdvice(ProceedingJoinPoint joinPoint) throws Throwable {
        System.out.println("Around: Trước khi thực thi");
        Object result = joinPoint.proceed(); // gọi method gốc
        System.out.println("Around: Sau khi thực thi");
        return result;
    }
}
```