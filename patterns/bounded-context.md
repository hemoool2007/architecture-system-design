# Bounded Context (DDD) trong .NET

## 🎯 Mục tiêu
Bounded Context là khái niệm cốt lõi của Domain-Driven Design (DDD), giúp chia hệ thống lớn thành các **vùng domain rõ ràng**, tránh việc business logic bị trộn lẫn và khó maintain.  
Tài liệu này tập trung vào:
- Hiểu đúng Bounded Context
- Cách áp dụng trong Modular Monolith & Microservices
- Trade-offs và kinh nghiệm thực tế trong .NET

---

## 🧠 Bounded Context là gì

Bounded Context là **ranh giới logic** trong đó:
- Ngôn ngữ (Ubiquitous Language) thống nhất
- Model domain có ý nghĩa nhất quán
- Business rule không bị mâu thuẫn

> Cùng một thuật ngữ có thể mang ý nghĩa khác nhau ở các Bounded Context khác nhau.

---

## ❌ Vấn đề khi không có Bounded Context

- Domain model phình to, khó hiểu
- Business rule chồng chéo
- Thay đổi một chỗ ảnh hưởng nhiều chỗ
- Dễ tạo “Big Ball of Mud”

Ví dụ:
- `Order` vừa dùng cho bán hàng, vừa dùng cho kế toán, vừa dùng cho vận chuyển
- Mỗi nơi hiểu `Order` khác nhau → bug và coupling

---

## 🧩 Ví dụ Bounded Context

| Context | Ý nghĩa |
|-------|--------|
| Sales | Tạo đơn hàng, pricing, discount |
| Billing | Thanh toán, hóa đơn |
| Shipping | Vận chuyển, trạng thái giao hàng |

Mỗi context có:
- Entity riêng
- Rule riêng
- Database schema riêng (hoặc logical separation)

---

## 🏗️ Áp dụng trong Modular Monolith

- Mỗi Bounded Context = **1 Module**
- Module có:
  - Domain
  - Application
  - Infrastructure
  - API riêng
- Module giao tiếp qua interface hoặc event

Ví dụ structure:
Modules/
├── Sales/
├── Billing/
└── Shipping/


---

## 🔁 Áp dụng trong Microservices

- Mỗi Bounded Context thường map 1–1 với 1 Microservice
- Database **riêng cho mỗi service**
- Giao tiếp qua:
  - REST
  - Event (preferred)

---

## 🔄 Giao tiếp giữa các Bounded Context

### Cách 1: Synchronous (API)
- Đơn giản
- Coupling cao
- Phù hợp query đơn giản

### Cách 2: Asynchronous (Event)
- Loose coupling
- Scalable
- Phù hợp business workflow

👉 Trong hệ thống lớn, **event-driven** thường là lựa chọn tốt hơn.

---

## ⚖️ Trade-offs & Kinh nghiệm

### Ưu điểm
- Domain rõ ràng
- Dễ scale team
- Giảm coupling
- Dễ migrate sang microservices

### Hạn chế
- Cần hiểu domain sâu
- Phải làm việc chặt với business
- Overhead ban đầu

### Kinh nghiệm thực tế
- Không cố chia quá sớm
- Bắt đầu từ Modular Monolith
- Refine context dần theo thời gian
- Ưu tiên clarity hơn technical perfection

---

## 📌 Kết luận

Bounded Context là nền tảng:
- Giúp hệ thống lớn **không bị rối**
- Là cầu nối giữa business và kỹ thuật
- Rất quan trọng với Solution Architect

Kết hợp tốt nhất:
- Bounded Context + Modular Monolith
- Bounded Context + Clean Architecture
