# C4 Model trong System Design (.NET)

## 🎯 Mục tiêu

C4 Model là phương pháp mô tả kiến trúc hệ thống theo nhiều mức độ chi tiết,
giúp:
- Truyền đạt kiến trúc rõ ràng
- Tránh sa đà vào chi tiết sớm
- Phù hợp trao đổi với nhiều đối tượng (PM, Dev, Architect)

Trong vai trò **Solution Architect .NET**, tôi sử dụng C4 Model như
**ngôn ngữ chung** để thiết kế và review hệ thống.

---

## 🧱 Tổng quan C4 Model

C4 gồm 4 cấp độ:

1. **Context**
2. **Container**
3. **Component**
4. **Code** (thường không cần vẽ chi tiết)

Nguyên tắc quan trọng:
> Đi từ **WHY → WHAT → HOW**, không đi ngược lại.

---

## 1️⃣ Context Diagram

### Mục đích
- Trả lời câu hỏi:  
  **Hệ thống này là gì và tương tác với ai?**
- Phù hợp cho stakeholder, PM, khách hàng

### Nội dung thể hiện
- Người dùng (User / Actor)
- Hệ thống chính
- Hệ thống bên ngoài (External Systems)

### Ví dụ (SaaS .NET)

- Người dùng truy cập qua Web / API
- Hệ thống SaaS Core
- Các hệ thống tích hợp:
  - Payment Gateway
  - Email Service
  - Identity Provider

> Context diagram **không nói công nghệ**, chỉ nói **vai trò & quan hệ**.

---

## 2️⃣ Container Diagram

### Mục đích
- Trả lời câu hỏi:  
  **Hệ thống được chia thành những khối lớn nào?**
- Phù hợp cho Architect & Tech Lead

### Nội dung thể hiện
- Web API
- Background worker
- Database
- Cache
- Message broker

### Áp dụng trong .NET

Ví dụ:
- ASP.NET Core Web API
- BackgroundService
- PostgreSQL / SQL Server
- Redis
- RabbitMQ / Kafka

### Lưu ý quan trọng
- Container **≠ Docker container**
- Container là **runtime boundary**

---

## 3️⃣ Component Diagram

### Mục đích
- Trả lời câu hỏi:  
  **Bên trong một container có những thành phần chính nào?**
- Phù hợp cho team dev

### Nội dung thể hiện
- Controllers / Endpoints
- Application services
- Domain services
- Repositories
- Integration adapters

### Góc nhìn .NET

Trong ASP.NET Core:
- Presentation layer
- Application layer
- Domain layer
- Infrastructure layer

Component diagram giúp:
- Tránh dependency ngược
- Kiểm soát coupling
- Review Clean Architecture

---

## 4️⃣ Code Level (khi nào cần?)

### Quan điểm thực tế

- **Không vẽ code-level diagram cho toàn hệ thống**
- Chỉ dùng khi:
  - Review critical flow
  - Phân tích performance
  - Onboarding dev mới

Trong đa số trường hợp:
> Code + Component diagram là đủ.

---

## 🧠 C4 Model & Modular Monolith

C4 Model **rất phù hợp** khi thiết kế Modular Monolith:

- Context: 1 hệ thống
- Container: 1 Web API + workers
- Component: chia theo module / bounded context

Ví dụ:
- Order Module
- Payment Module
- User Module

👉 Mỗi module có:
- Application layer riêng
- Domain riêng
- Infrastructure riêng (nếu cần)

---

## ⚖️ Trade-offs & Kinh nghiệm thực tế

### Ưu điểm
- Dễ truyền đạt
- Không phụ thuộc công nghệ
- Scale tốt theo độ phức tạp

### Hạn chế
- Không thể hiện chi tiết runtime behavior
- Cần kết hợp sequence diagram khi cần

### Kinh nghiệm cá nhân
- Luôn bắt đầu từ Context
- Không vẽ Component quá sớm
- Dùng C4 để **review**, không chỉ để thiết kế

---

## 📌 Kết luận

C4 Model là công cụ nền tảng trong tư duy System Design.
Đối với Solution Architect .NET, C4 giúp:
- Thiết kế hệ thống có cấu trúc
- Giao tiếp hiệu quả với nhiều vai trò
- Làm rõ boundary & responsibility

C4 không thay thế code,
nhưng giúp code **đi đúng hướng ngay từ đầu**.
