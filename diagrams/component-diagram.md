# Component Diagram (C4 Model) cho ASP.NET Core Modular Monolith

## 🎯 Mục tiêu
Component Diagram trong C4 Model đi sâu vào **bên trong một container**, mô tả:
- Các component chính
- Trách nhiệm của từng component
- Cách các component tương tác với nhau

File này tập trung vào **ASP.NET Core Web API (Modular Monolith)** áp dụng:
- Clean Architecture
- Hexagonal Architecture
- Bounded Context

---

## 🧠 Component là gì trong C4 Model

Component là:
- Một phần có trách nhiệm rõ ràng trong container
- Có thể là controller, service, module, repository
- Không nhất thiết là class đơn lẻ

Component Diagram giúp:
- Dev hiểu nhanh cấu trúc hệ thống
- Architect kiểm soát coupling
- Phỏng vấn viên thấy được tư duy kiến trúc

---

## 🏗️ Component Diagram – Tổng quan

### Mô tả
- Mỗi Module đại diện cho một Bounded Context
- Mỗi Module tuân theo Clean Architecture
- Giao tiếp giữa Module qua Application Layer hoặc Event

---

## 🧩 Component Diagram (Mermaid)

```mermaid
flowchart TB
    subgraph Presentation["Presentation Layer"]
        ControllerA[UserController]
        ControllerB[OrderController]
    end

    subgraph Application["Application Layer"]
        UserService[UserService]
        OrderService[OrderService]
        EventPublisher[Domain Event Publisher]
    end

    subgraph Domain["Domain Layer"]
        UserEntity[User Entity]
        OrderEntity[Order Entity]
        DomainRules[Business Rules]
    end

    subgraph Infrastructure["Infrastructure Layer"]
        UserRepo[UserRepository]
        OrderRepo[OrderRepository]
        Db[(Database)]
        MessageBus[(Message Broker)]
    end

    ControllerA --> UserService
    ControllerB --> OrderService

    UserService --> UserEntity
    OrderService --> OrderEntity

    UserService --> UserRepo
    OrderService --> OrderRepo

    UserRepo --> Db
    OrderRepo --> Db

    UserService --> EventPublisher
    OrderService --> EventPublisher
    EventPublisher --> MessageBus
🔍 Giải thích chi tiết
Presentation Layer

Nhận HTTP request

Validate input

Map DTO → Application command

Không chứa business logic

Application Layer

Điều phối use case

Gọi Domain logic

Giao tiếp Infrastructure thông qua interface

Publish domain event khi cần

Domain Layer

Chứa entity, value object

Business rule thuần

Không phụ thuộc framework

Infrastructure Layer

Implement repository

Kết nối database

Gửi message, gọi external service

Là adapter cho core

🔄 Giao tiếp giữa các Module
Cách 1: Application-to-Application

Gọi service nội bộ

Dễ nhưng coupling cao

Cách 2: Event-driven (Khuyến nghị)

Publish domain event

Module khác subscribe

Loose coupling

⚖️ Trade-offs & Kinh nghiệm
Ưu điểm

Rõ ràng trách nhiệm từng component

Dễ test từng layer

Kiểm soát dependency tốt

Hạn chế

Số lượng component tăng

Overhead với hệ thống nhỏ

Cần discipline khi code

Kinh nghiệm thực tế

Controller mỏng

Application service điều phối, không nhồi logic

Domain giữ business rule thật sự

Infrastructure không leak vào core

📌 Kết luận

Component Diagram là mảnh ghép cuối trong C4 Model:

Giúp hiểu hệ thống từ macro → micro

Là artifact rất mạnh khi trình bày kiến trúc

Thể hiện rõ tư duy của Solution Architect .NET

👉 Kết hợp:

System Context Diagram

Container Diagram

Component Diagram