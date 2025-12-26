<p align="right">
  <a href="README.md">Tiếng Việt</a> | <a href="README.en.md">English</a>
</p>

# System Design & Architecture (.NET)

Repository này tập trung vào **System Design & Software Architecture**
theo góc nhìn của **Solution Architect .NET**.

Đây không phải repo tutorial hay framework-specific,
mà là nơi **hệ thống hóa tư duy kiến trúc**, cách phân rã hệ thống
và lý do đằng sau các quyết định thiết kế.

---

## 🎯 Mục tiêu

- Củng cố **architectural thinking** (không chỉ code)
- Hiểu rõ:
  - System boundary
  - Service / module responsibility
  - Trade-off giữa các lựa chọn kiến trúc
- Áp dụng trực tiếp vào **ASP.NET Core / .NET ecosystem**
- Dùng làm:
  - Tài liệu ôn tập
  - Tài liệu phỏng vấn
  - Nền tảng cho các repo chuyên sâu khác

---

## 🧠 Phạm vi nội dung chính

### 1. Architectural Fundamentals

Tập trung vào **tư duy nền tảng**, độc lập công nghệ:

- C4 Model (System → Container → Component)
- System decomposition
- Bounded Context (DDD-level thinking)
- Sync vs Async communication
- Coupling / Cohesion

📄 Tài liệu liên quan:
- `docs/architecture/context-diagram.md`
- `docs/architecture/container-diagram.md`
- `docs/architecture/component-diagram.md`

---

### 2. Architecture Styles

Phân tích các style phổ biến và **khi nào nên / không nên dùng**:

- Monolith
- Modular Monolith
- Microservices

Trọng tâm:
- Trade-off
- Chi phí vận hành
- Độ phức tạp tổ chức & team

---

### 3. .NET Architecture Patterns

Các pattern thường gặp trong hệ sinh thái .NET:

- Clean Architecture
- Onion Architecture
- Hexagonal Architecture
- Dependency Injection & Dependency Rule

Không chỉ mô tả pattern, mà tập trung:
- Vì sao tồn tại
- Giải quyết vấn đề gì
- Khi nào trở thành over-engineering

---

### 4. API Design & Boundaries

- API contracts & boundary definition
- API versioning strategies
- Backward compatibility
- Consumer-driven considerations

---

## 🧪 Demo & Lab

Repo này có thể chứa **demo nhỏ / lab minh họa** cho các khái niệm:

- Modular Monolith trong ASP.NET Core
- Phân tách module & dependency đúng cách
- API versioning thực tế

> Các demo lớn hoặc theo domain riêng sẽ được tách sang repository khác.

---

## 📐 Documentation-first Approach

Repo này theo hướng:

**Documentation → Design → Implementation**

- Mỗi phần kiến trúc đều có tài liệu đi kèm
- Các quyết định quan trọng được ghi lại rõ ràng
- Code chỉ là kết quả cuối cùng của tư duy thiết kế

---

## 📌 Định hướng sử dụng

- Ôn tập System Design & Architecture
- Chuẩn bị phỏng vấn Solution Architect / Senior Engineer
- Là **nền tảng kiến trúc** cho các repo tiếp theo:
  - Database & Data Modeling
  - Scalability & Performance
  - Messaging & Event-driven
  - Security & Identity

---

## 🔗 Liên kết

- Portfolio HUB: **solution-architect-portfolio**
