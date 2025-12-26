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