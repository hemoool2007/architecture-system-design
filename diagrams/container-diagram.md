# Container Diagram (C4 Model) cho hệ thống .NET

## 🎯 Mục tiêu
Container Diagram trong C4 Model mô tả **các container chính** của hệ thống (ứng dụng, database, message broker, external system) và **cách chúng giao tiếp với nhau**.  
Mục tiêu của file này:
- Cho cái nhìn tổng quan kiến trúc hệ thống
- Giải thích ranh giới trách nhiệm giữa các container
- Chuẩn bị cho trao đổi kỹ thuật và phỏng vấn Solution Architect

---

## 🧠 Container là gì trong C4 Model

Trong C4 Model:
- **Container** ≠ Docker container
- Container là một **application hoặc data store có thể deploy độc lập**

Ví dụ container:
- ASP.NET Core Web API
- Database
- Message Broker
- External Service

---

## 🏗️ Container Diagram – Modular Monolith (.NET)

### Mô tả
- Người dùng truy cập qua Web / Mobile Client
- ASP.NET Core Web API là **1 deployable monolith**
- Database dùng chung
- Message Broker hỗ trợ async communication
- External Services được gọi qua adapter

### Mermaid Diagram

```mermaid
flowchart LR
    User[User / Client]
    Api[ASP.NET Core Web API<br/>(Modular Monolith)]
    Db[(Relational Database)]
    Broker[(Message Broker)]
    External[External Services]

    User --> Api
    Api --> Db
    Api --> Broker
    Api --> External

🔍 Giải thích chi tiết
ASP.NET Core Web API

Deploy như 1 ứng dụng duy nhất

Chứa nhiều module (Bounded Context)

Áp dụng Clean Architecture + Hexagonal Architecture

Là trung tâm xử lý business logic

Database

Shared database hoặc logical separation theo schema

Không truy cập trực tiếp từ client

Chỉ Application Core thông qua repository

Message Broker

Xử lý async communication

Publish domain event

Giảm coupling giữa các module / context

External Services

Payment gateway

Email / Notification service

Auth provider

Tích hợp qua adapter

🔄 Container Diagram – Hướng Microservices (tương lai)
flowchart LR
    User[User / Client]
    ApiGW[API Gateway]
    ServiceA[Service A<br/>(Sales)]
    ServiceB[Service B<br/>(Billing)]
    ServiceC[Service C<br/>(Shipping)]
    DbA[(DB A)]
    DbB[(DB B)]
    DbC[(DB C)]
    Broker[(Message Broker)]

    User --> ApiGW
    ApiGW --> ServiceA
    ApiGW --> ServiceB
    ApiGW --> ServiceC

    ServiceA --> DbA
    ServiceB --> DbB
    ServiceC --> DbC

    ServiceA --> Broker
    ServiceB --> Broker
    ServiceC --> Broker

⚖️ Trade-offs & Kinh nghiệm
Modular Monolith

Dễ deploy

Ít overhead

Phù hợp team nhỏ–vừa

Microservices

Scale tốt

Phức tạp hơn

Cần mature DevOps & observability

Kinh nghiệm thực tế

Bắt đầu Modular Monolith

Thiết kế container rõ ràng

Chuẩn bị khả năng tách service sau này

📌 Kết luận

Container Diagram giúp:

Hiểu nhanh hệ thống ở mức cao

Giao tiếp kiến trúc hiệu quả

Là artifact rất mạnh khi phỏng vấn Solution Architect

👉 Diagram này là cầu nối giữa System Context Diagram và Component Diagram trong C4 Model.
