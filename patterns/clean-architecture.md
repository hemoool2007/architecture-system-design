# Clean Architecture trong .NET

## 🎯 Mục tiêu
Clean Architecture là pattern nền tảng cho các hệ thống Modular Monolith và Microservices trong .NET, giúp tách biệt layer rõ ràng, giữ code dễ maintain, test và mở rộng. Quy tắc dependency đi từ ngoài vào trong, chuẩn bị tốt cho Modular Monolith demo.

## 🧱 Nguyên lý cơ bản
1. **Dependency Rule**: code chỉ phụ thuộc layer bên trong, Domain Layer không biết gì về Application hay Infrastructure.  
2. **Entities / Domain**: chứa core business rules, không phụ thuộc framework.  
3. **Use Cases / Application**: logic ứng dụng, gọi Domain Layer.  
4. **Interface Adapters / Presentation**: API Controller / UI, map DTO → Domain.  
5. **Infrastructure**: Database, Messaging, External APIs, cung cấp implementation cho interface inner layer.

## 🧠 Layered Structure (.NET)
Presentation (API, UI)
↓
Application (UseCases, Services)
↓
Domain (Entities, Business Rules)
↓
Infrastructure (EF Core, Repositories, External Service Clients)

Ví dụ Modular Monolith:  
- **User Module**: Domain (`User`, `Role`), Application (`UserService`), Infrastructure (`UserRepository`), Presentation (`UserController`).  
- **Order Module**: Domain (`Order`, `OrderItem`), Application (`OrderService`), Infrastructure (`OrderRepository`), Presentation (`OrderController`).  

Layered structure giúp tách module, tránh coupling, deploy 1 Monolith duy nhất.

## ⚖️ Trade-offs & Kinh nghiệm
**Ưu điểm**: dễ test, module độc lập, dependency rõ ràng, future-proof.  
**Hạn chế**: overhead với project nhỏ, cần discipline tuân thủ dependency rule, cần template/folder chuẩn.  
**Tips thực tế**: sử dụng DI container, module có interface riêng, DTO đi từ inner → outer layer, document module boundary & dependencies.

## 💻 Ví dụ code

**Domain Layer**
```csharp
public class User
{
    public Guid Id { get; private set; }
    public string Email { get; private set; }
    public void ChangeEmail(string newEmail) => Email = newEmail;
}

Application Layer
public class UserService
{
    private readonly IUserRepository _repo;
    public UserService(IUserRepository repo) => _repo = repo;
    public void UpdateEmail(Guid userId, string newEmail)
    {
        var user = _repo.GetById(userId);
        user.ChangeEmail(newEmail);
        _repo.Update(user);
    }
}

Infrastructure Layer
public class UserRepository : IUserRepository
{
    private readonly AppDbContext _db;
    public UserRepository(AppDbContext db) => _db = db;
    public User GetById(Guid id) => _db.Users.Find(id);
    public void Update(User user) => _db.SaveChanges();
}

Presentation Layer
[ApiController]
[Route("api/users")]
public class UserController : ControllerBase
{
    private readonly UserService _service;
    public UserController(UserService service) => _service = service;

    [HttpPut("{id}/email")]
    public IActionResult UpdateEmail(Guid id, [FromBody] string email)
    {
        _service.UpdateEmail(id, email);
        return Ok();
    }
}

📌 Kết luận

Clean Architecture là xương sống cho Modular Monolith và các hệ thống .NET phức tạp: tách layer rõ ràng, tuân thủ Dependency Rule, dễ maintain, test và scale.
Demo Modular Monolith sử dụng Clean Architecture: modular-monolith-sample