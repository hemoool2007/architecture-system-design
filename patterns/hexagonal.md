# Hexagonal Architecture (Ports & Adapters) trong .NET

## 🎯 Mục tiêu
Hexagonal Architecture (còn gọi là Ports & Adapters) là một kiến trúc giúp tách **core business logic** khỏi **hạ tầng và framework**, từ đó tăng khả năng test, maintain và thay đổi công nghệ. Pattern này rất phù hợp để kết hợp với Clean Architecture và Modular Monolith trong .NET.

---

## 🧠 Khái niệm cốt lõi

Hexagonal Architecture xoay quanh ý tưởng:
- **Application Core** (Domain + Application) nằm ở trung tâm
- Mọi tương tác với thế giới bên ngoài đi qua **Ports**
- Các công nghệ cụ thể được triển khai bằng **Adapters**

Application **không phụ thuộc** vào:
- Database
- Web framework
- Message broker
- External services

---

## 🧩 Ports & Adapters

### Port
- Là **interface** do Application/Core định nghĩa
- Đại diện cho một khả năng mà hệ thống cần từ bên ngoài
- Ví dụ: Repository, External API Client, Message Publisher

### Adapter
- Là **implementation** của Port
- Gắn với công nghệ cụ thể (EF Core, HTTP Client, Kafka, RabbitMQ…)

> Core chỉ biết **Port**, không biết **Adapter**.

---

## 🏗️ Cấu trúc tổng quát

            ┌────────────────────┐
            │   Presentation     │
            │ (API / UI Adapter) │
            └─────────▲──────────┘
                      │
    ┌─────────────────┼─────────────────┐
    │                 │                 │
    │          Application Core          │
    │      (Domain + Application)        │
    │   Ports (Interfaces) Defined Here │
    │                                   │
    └─────────────────┼─────────────────┘
                      │
            ┌─────────▼──────────┐
            │   Infrastructure   │
            │ (DB, External API) │
            │     Adapters       │
            └────────────────────┘

---

## 🔁 So sánh với Clean Architecture

| Clean Architecture | Hexagonal Architecture |
|-------------------|------------------------|
| Tập trung vào layer | Tập trung vào hướng phụ thuộc |
| Layered rõ ràng | In/Out adapters rõ ràng |
| Dependency Rule | Core không phụ thuộc infra |
| Phù hợp monolith | Phù hợp cả monolith & microservices |

👉 Thực tế trong .NET, **2 pattern này thường được dùng chung**.

---

## 💻 Ví dụ trong .NET

### Port (Application Layer)
```csharp
public interface IUserRepository
{
    User GetById(Guid id);
    void Save(User user);
}

Adapter – Infrastructure
public class EfUserRepository : IUserRepository
{
    private readonly AppDbContext _db;
    public EfUserRepository(AppDbContext db) => _db = db;

    public User GetById(Guid id) => _db.Users.Find(id);
    public void Save(User user) => _db.SaveChanges();
}


Application Core sử dụng Port
public class UserService
{
    private readonly IUserRepository _repo;
    public UserService(IUserRepository repo) => _repo = repo;

    public void ChangeEmail(Guid id, string email)
    {
        var user = _repo.GetById(id);
        user.ChangeEmail(email);
        _repo.Save(user);
    }
}

Presentation Adapter (API)
[ApiController]
[Route("api/users")]
public class UserController : ControllerBase
{
    private readonly UserService _service;
    public UserController(UserService service) => _service = service;

    [HttpPut("{id}/email")]
    public IActionResult UpdateEmail(Guid id, string email)
    {
        _service.ChangeEmail(id, email);
        return Ok();
    }
}

⚖️ Trade-offs & Kinh nghiệm
Ưu điểm

Core business độc lập framework

Test dễ (mock Port)

Thay đổi DB / External API không ảnh hưởng Core

Chuẩn bị tốt cho Microservices

Hạn chế

Số lượng interface tăng

Overhead với hệ thống nhỏ

Cần discipline kiến trúc

Kinh nghiệm thực tế

Áp dụng Hexagonal cho module quan trọng

Không cần cực đoan với module CRUD đơn giản

Rất hiệu quả khi tích hợp external system

Kết hợp tốt với Modular Monolith + Clean Architecture

📌 Kết luận

Hexagonal Architecture giúp:

Bảo vệ core business

Giảm coupling với công nghệ

Tăng khả năng test và thay đổi

Trong .NET, đây là pattern rất được đánh giá cao khi phỏng vấn Solution Architect, đặc biệt khi bạn giải thích được vì sao không phải lúc nào cũng cần áp dụng toàn diện.

👉 Demo áp dụng Hexagonal Architecture nằm trong:
demos/modular-monolith-sample
