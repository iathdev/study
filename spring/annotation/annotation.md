1. Annotation Cơ Bản – Spring Core (DI, IoC)

| Annotation       | Mục đích                                              |
| ---------------- | ----------------------------------------------------- |
| `@Component`     | Đánh dấu class là bean để Spring quản lý              |
| `@Service`       | Tương tự `@Component`, dùng cho tầng service          |
| `@Repository`    | Tương tự `@Component`, dùng cho DAO/repository        |
| `@Controller`    | Đánh dấu class là controller (Spring MVC)             |
| `@Autowired`     | Tự động inject bean vào một field hoặc constructor    |
| `@Qualifier`     | Dùng kết hợp với `@Autowired` để chỉ định bean cụ thể |
| `@Value`         | Inject giá trị từ `application.properties`            |
| `@Configuration` | Đánh dấu class cấu hình Spring                        |
| `@Bean`          | Tạo một bean trong `@Configuration`                   |

2. Spring MVC – Xây dựng Web App

| Annotation                                                     | Mục đích                                |
| -------------------------------------------------------------- | --------------------------------------- |
| `@RestController`                                              | Kết hợp `@Controller` + `@ResponseBody` |
| `@RequestMapping`                                              | Định nghĩa URL cho controller/method    |
| `@GetMapping`, `@PostMapping`, `@PutMapping`, `@DeleteMapping` | Rút gọn của `@RequestMapping`           |
| `@PathVariable`                                                | Lấy giá trị từ URL path                 |
| `@RequestParam`                                                | Lấy query param từ URL                  |
| `@RequestBody`                                                 | Convert JSON -> Object (input)          |
| `@ResponseBody`                                                | Convert Object -> JSON (output)         |
| `@ModelAttribute`                                              | Bind dữ liệu form vào object            |
| `@ExceptionHandler`                                            | Xử lý ngoại lệ tại controller           |


3. Spring Boot – Tự động cấu hình

| Annotation                 | Mục đích                                                                             |
| -------------------------- | ------------------------------------------------------------------------------------ |
| `@SpringBootApplication`   | Kết hợp 3 annotation: `@Configuration`, `@EnableAutoConfiguration`, `@ComponentScan` |
| `@EnableAutoConfiguration` | Cho phép Spring Boot tự động cấu hình                                                |
| `@ComponentScan`           | Quét các package để tìm bean                                                         |
| `@ConfigurationProperties` | Mapping toàn bộ cấu hình từ file properties vào object                               |
| `@Profile`                 | Cấu hình cho từng môi trường (`dev`, `prod`, ...)                                    |

4. Spring Data JPA – Làm việc với Database

| Annotation        | Mục đích                                         |
| ----------------- | ------------------------------------------------ |
| `@Entity`         | Đánh dấu class là entity trong JPA               |
| `@Table`          | Gán tên table trong DB                           |
| `@Id`             | Primary key                                      |
| `@GeneratedValue` | Auto-increment key                               |
| `@Column`         | Gán tên column, nullable, length...              |
| `@Repository`     | Giao tiếp với DB (có thể extend `JpaRepository`) |
| `@Query`          | Viết query tùy chỉnh                             |

5. Spring Security – Bảo mật

| Annotation                 | Mục đích                             |
| -------------------------- | ------------------------------------ |
| `@EnableWebSecurity`       | Bật cấu hình bảo mật Spring          |
| `@PreAuthorize`            | Phân quyền dựa trên biểu thức        |
| `@Secured`                 | Phân quyền theo role                 |
| `@WithMockUser`            | Dùng trong test                      |
| `@AuthenticationPrincipal` | Inject thông tin người dùng hiện tại |


6. AOP – Aspect-Oriented Programming

| Annotation                     | Mục đích                                                 |
| ------------------------------ | -------------------------------------------------------- |
| `@Aspect`                      | Đánh dấu một aspect                                      |
| `@Before`, `@After`, `@Around` | Hook vào trước/sau method                                |
| `@Pointcut`                    | Định nghĩa điểm cắt (ví dụ: tất cả method trong service) |

7. Annotation cho Unit Test

| Annotation           | Mục đích                   |
| -------------------- | -------------------------- |
| `@SpringBootTest`    | Tạo context Spring để test |
| `@WebMvcTest`        | Test controller riêng biệt |
| `@DataJpaTest`       | Test repository và JPA     |
| `@MockBean`          | Inject mock vào context    |
| `@TestConfiguration` | Cấu hình riêng cho test    |
| `@WithMockUser`      | Mô phỏng user login        |



