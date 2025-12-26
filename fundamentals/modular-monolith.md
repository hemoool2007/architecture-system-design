# Modular Monolith trong .NET

## 🎯 Mục tiêu

File này tập trung vào **Modular Monolith**, giải thích chi tiết:

- Khái niệm & nguyên lý
- Lợi ích và hạn chế
- Khi nào nên chọn Modular Monolith
- Áp dụng trong ASP.NET Core
- Liên kết đến demo code thực tế

Modular Monolith là **nền tảng lý tưởng** trước khi đi microservices, đặc biệt với .NET.

---

## 🧱 Khái niệm

- Ứng dụng **vẫn deploy như 1 monolith** duy nhất
- **Codebase chia thành module / bounded context**
- Module tách biệt:  
  - Interface riêng  
  - Layer riêng (Presentation → Application → Domain → Infrastructure)
- Database:  
  - Shared DB hoặc schema riêng cho mỗi module

### Ví dụ Modules:
- User Module
- Order Module
- Payment Module

> Mỗi module có thể được phát triển, test và maintain gần như độc lập, nhưng vẫn deploy cùng một ứng dụng.

---

## ⚖️ Lợi ích

1. **Deployment đơn giản**  
   - Vẫn deploy 1 ứng dụng, không cần nhiều service
2. **Tách biệt code rõ ràng**  
   - Giảm coupling, dễ maintain
3. **Future-proof**  
   - Có thể refactor sang microservices sau này
4. **Dễ review & test**  
   - Module boundary rõ ràng
5. **Thích hợp cho team nhỏ đến vừa**  
   - < 10 dev, tránh overhead của microservices

---

## ⚠️ Hạn chế

1. **Scale module chưa độc lập**  
   - Không thể scale một module riêng mà không scale cả app
2. **Runtime coupling vẫn tồn tại**  
   - Network / process không tách biệt như microservices
3. **Cần discipline**  
   - Nếu module boundary không rõ → lại trở thành monolith truyền thống

---

## 🧠 Khi nào nên dùng

- Hệ thống medium → large, team < 10 người  
- Cần rõ ràng boundary nhưng muốn **deployment đơn giản**  
- Muốn dễ refactor sang microservices sau này nếu cần  
- ASP.NET Core là nền tảng chính  

> Lưu ý: nếu hệ thống quá lớn hoặc team > 10, microservices có thể cần thiết.

---

## 💻 Áp dụng trong .NET

1. **Structure Layered / Clean Architecture**
Presentation -> Application -> Domain -> Infrastructure
2. **Module tách biệt**
- Mỗi module có: Application Service + Domain + Repository
3. **Dependency Injection**
- Module chỉ inject interface, không phụ thuộc implementation bên ngoài
4. **Database**
- Shared DB hoặc schema riêng
5. **Bounded Context**
- Module đại diện cho 1 Bounded Context DDD
6. **Unit test / Integration test**
- Test module riêng trước khi tích hợp

---

## 🧪 Demo code

Demo thực tế: [modular-monolith-sample](../demos/modular-monolith-sample)  
- 2–3 module
- ASP.NET Core Web API
- DI chuẩn, module tách biệt
- Không cần business logic phức tạp, focus **structure & decision**

---

## ✅ Kinh nghiệm thực tế

- Luôn bắt đầu với **Modular Monolith** cho medium-large .NET system  
- Microservices chỉ khi **hệ thống quá lớn / nhiều team**  
- Document **module boundary & API contract** ngay từ đầu  
- Review kiến trúc định kỳ để tránh drift thành monolith truyền thống

---

## 📌 Kết luận

Modular Monolith là **giải pháp cân bằng** giữa monolith và microservices:

- Dễ deploy  
- Code tách biệt  
- Sẵn sàng cho tương lai  
- Phù hợp hầu hết hệ thống .NET vừa và lớn
