# Async Communication & Event-Driven Architecture trong .NET

## 🎯 Mục tiêu
Async Communication là nền tảng cho các hệ thống **scalable, loosely coupled**.  
Tài liệu này tập trung vào:
- Khi nào nên dùng async communication
- Event-driven architecture
- Messaging patterns phổ biến
- Trade-offs & best practices trong .NET

---

## ❓ Vì sao cần Async Communication

Giao tiếp synchronous (HTTP/REST) có hạn chế:
- Coupling chặt giữa các module/service
- Dễ bị cascade failure
- Khó scale theo tải không đồng đều

Async Communication giúp:
- Loose coupling
- Tăng khả năng chịu lỗi
- Scale tốt hơn
- Phù hợp workflow business phức tạp

---

## 🧠 Các khái niệm cốt lõi

### Message
- Dữ liệu gửi giữa các thành phần
- Không chia sẻ state

### Event
- Thể hiện **điều đã xảy ra**
- Không yêu cầu phản hồi

### Command
- Yêu cầu **làm một việc**
- Thường có intent rõ ràng

---

## 🏗️ Event-Driven Architecture (EDA)

- Hệ thống phản ứng dựa trên event
- Producer không biết consumer
- Consumer subscribe event mình quan tâm

Ví dụ:
- `OrderCreated`
- `PaymentCompleted`
- `ShipmentDispatched`

---

## 🧩 Messaging Patterns phổ biến

### 1️⃣ Point-to-Point (Queue)
- 1 message → 1 consumer
- Dùng cho command / task

Ví dụ:
- Background processing
- Email sending

### 2️⃣ Publish / Subscribe
- 1 event → nhiều consumer
- Dùng cho business event

Ví dụ:
- OrderCreated → Billing, Shipping, Notification

---

## 🔁 Giao tiếp giữa Bounded Context

### Synchronous
- REST API
- GraphQL

### Asynchronous (khuyến nghị)
- Event-based
- Message broker

> Trong hệ thống lớn, async communication giúp tránh tight coupling giữa context.

---

## 💻 Áp dụng trong .NET

### Message Broker phổ biến
- RabbitMQ
- Azure Service Bus
- Kafka

### Thư viện thường dùng
- MassTransit
- NServiceBus
- Azure.Messaging.ServiceBus

---

## 🧪 Ví dụ Event trong .NET

```csharp
public record OrderCreatedEvent(Guid OrderId, decimal TotalAmount);
Publish Event
await _bus.Publish(new OrderCreatedEvent(order.Id, order.Total));

Consume Event
public class OrderCreatedConsumer : IConsumer<OrderCreatedEvent>
{
    public async Task Consume(ConsumeContext<OrderCreatedEvent> context)
    {
        var message = context.Message;
        // handle event
    }
}

🔄 Saga Pattern

Saga dùng để xử lý business transaction phân tán.

2 kiểu Saga

Orchestration: 1 coordinator điều phối

Choreography: các service phản ứng event

Khi dùng Saga

Nhiều bước business

Có rollback logic

Không dùng distributed transaction

⚖️ Trade-offs & Kinh nghiệm
Ưu điểm

Loose coupling

Scale tốt

Tăng resiliency

Phù hợp domain phức tạp

Hạn chế

Debug khó hơn

Eventual consistency

Cần monitoring tốt

Kinh nghiệm thực tế

Không async hóa mọi thứ

Bắt đầu sync, scale thì async

Event name phải rõ nghĩa

Log & trace event đầy đủ

📌 Kết luận

Async Communication là chìa khóa cho hệ thống hiện đại:

Giảm coupling

Tăng scalability

Chuẩn bị tốt cho microservices

Với Solution Architect .NET, hiểu rõ khi nào nên dùng async và khi nào không là điểm cộng rất lớn khi phỏng vấn.
