# Monolith vs Modular Monolith vs Microservices (.NET)

## 🎯 Mục tiêu

File này phân tích các kiến trúc backend phổ biến trong .NET:

- Monolith truyền thống
- Modular Monolith
- Microservices

Mục tiêu:
- Hiểu trade-off
- Xác định khi nào nên chọn kiến trúc nào
- Chuẩn bị demo Modular Monolith trong ASP.NET Core

---

## 1️⃣ Monolith (truyền thống)

### Định nghĩa
- Tất cả code nằm trong **1 ứng dụng duy nhất**
- Shared database, shared codebase
- Deployment duy nhất

### Ưu điểm
- Triển khai đơn giản
- Dễ debug, test
- Không cần messaging / service discovery

### Hạn chế
- Khó scale từng module riêng
- Rủi ro thay đổi làm ảnh hưởng toàn hệ thống
- Deployment chậm khi app lớn

### Khi nên dùng
- Startup / MVP
- Hệ thống nhỏ, ít team

---

## 2️⃣ Microservices

### Định nghĩa
- Hệ thống tách thành **nhiều service độc lập**
- Mỗi service có database riêng
- Giao tiếp async / sync (API, messaging)

### Ưu điểm
- Scale từng service riêng
- Deployment độc lập
- Cho phép team phát triển độc lập

### Hạn chế
- Phức tạp: network, monitoring, transactions
- Cần service discovery, messaging, retry, circuit breaker
- Overhead cao với team nhỏ / dự án nhỏ

### Khi nên dùng
- Hệ thống lớn, nhiều team
- Yêu cầu scale từng phần riêng biệt

---

## 3️⃣ Modular Monolith (nền tảng cho .NET)

### Định nghĩa
- Ứng dụng **vẫn là 1 deployable monolith**
- Codebase chia thành **module / bounded context**
- Module **tách biệt rõ ràng**, có interface riêng
- Database có thể shared hoặc schema riêng

### Ưu điểm
- Deployment đơn giản (1 app)
- Module tách biệt, dễ maintain
- Đơn giản hơn microservices, ít overhead
- Dễ refactor sang microservices nếu cần

### Hạn chế
- Scale theo module không được độc lập
- Chưa hoàn toàn giải quyết vấn đề coupling runtime

### Khi nên dùng
- Hệ thống medium → large, team < 10 người
- Cần rõ ràng boundary nhưng muốn deploy đơn giản
- Sẵn sàng future-proof chuyển sang microservices

---

## 4️⃣ So sánh trực quan

| Tiêu chí            | Monolith | Modular Monolith | Microservices |
|--------------------|----------|-----------------|---------------|
| Deployment         | 1 lần    | 1 lần           | Nhiều lần     |
| Team development   | Đơn giản | Vừa             | Phân tách     |
| Scale              | Toàn bộ | Module          | Service       |
| Complexity         | Thấp     | Trung bình      | Cao           |
| Monitoring         | Dễ       | Trung bình      | Khó           |

---

## 5️⃣ Modular Monolith trong .NET

- ASP.NET Core Web API + Modules
- Dependency Injection phân tách theo module
- Layered structure (Presentation → Application → Domain → Infrastructure)
- Module có thể có **Database Schema riêng hoặc Shared DB**
- Chuẩn bị **demo code** trong folder `demos/modular-monolith-sample`

---

## 6️⃣ Kinh nghiệm cá nhân

- Luôn bắt đầu **Modular Monolith** cho medium-large .NET system
- Microservices khi hệ thống lớn, nhiều team
- Monolith chỉ dành cho MVP hoặc hệ thống nhỏ
- Document rõ ràng boundary & API contract ngay từ đầu

---

## 📌 Kết luận

- Monolith: dễ, nhanh, cho hệ thống nhỏ
- Microservices: mạnh, nhưng overhead cao
- Modular Monolith: cân bằng, phù hợp với đa số hệ thống .NET hiện nay
