# API Versioning trong ASP.NET Core

## 🎯 Mục tiêu
API Versioning là chủ đề **rất hay bị hỏi khi phỏng vấn Solution Architect**, đặc biệt với hệ thống public API hoặc hệ thống có nhiều client (web, mobile, partner).  
Tài liệu này tập trung vào:
- Vì sao cần versioning
- Các chiến lược versioning phổ biến
- Trade-offs từng cách
- Best practices trong ASP.NET Core

---

## ❓ Vì sao cần API Versioning

API gần như **không thể thay đổi tùy ý** khi đã có client sử dụng.  
Những thay đổi sau **gây breaking change**:
- Đổi format request/response
- Đổi tên field
- Thay đổi validation
- Thay đổi business rule

Versioning giúp:
- Giữ backward compatibility
- Cho phép migrate client dần dần
- Tránh deploy “big bang”

---

## 🧠 Các chiến lược API Versioning

### 1️⃣ URI Versioning
/api/v1/users
/api/v2/users

**Ưu điểm**
- Rõ ràng, dễ hiểu
- Dễ debug
- Phổ biến nhất

**Nhược điểm**
- URL thay đổi
- Không REST-pure tuyệt đối

👉 **Khuyến nghị cho đa số hệ thống .NET**

---

### 2️⃣ Query String Versioning
/api/users?version=1

**Ưu điểm**
- URL gọn
- Dễ test

**Nhược điểm**
- Dễ bị bỏ qua
- Không rõ ràng với người dùng API

---

### 3️⃣ Header Versioning
X-API-Version: 1

**Ưu điểm**
- REST-pure
- URL không đổi

**Nhược điểm**
- Khó debug
- Client phải set header

---

### 4️⃣ Media Type Versioning
Accept: application/vnd.myapp.v1+json

**Ưu điểm**
- Chuẩn REST nhất
- Rất linh hoạt

**Nhược điểm**
- Phức tạp
- Ít được dùng thực tế

---

## 📊 So sánh nhanh

| Strategy | Dễ dùng | Rõ ràng | Phổ biến |
|--------|--------|--------|---------|
| URI | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ |
| Query | ⭐⭐⭐ | ⭐⭐ | ⭐⭐ |
| Header | ⭐⭐ | ⭐⭐ | ⭐⭐ |
| Media Type | ⭐ | ⭐ | ⭐ |

---

## 💻 API Versioning trong ASP.NET Core

### Cài package
```bash
dotnet add package Microsoft.AspNetCore.Mvc.Versioning

Cấu hình Versioning
builder.Services.AddApiVersioning(options =>
{
    options.DefaultApiVersion = new ApiVersion(1, 0);
    options.AssumeDefaultVersionWhenUnspecified = true;
    options.ReportApiVersions = true;
});

Controller với version
[ApiController]
[ApiVersion("1.0")]
[Route("api/v{version:apiVersion}/users")]
public class UsersV1Controller : ControllerBase
{
    [HttpGet]
    public IActionResult Get() => Ok("Users V1");
}

[ApiController]
[ApiVersion("2.0")]
[Route("api/v{version:apiVersion}/users")]
public class UsersV2Controller : ControllerBase
{
    [HttpGet]
    public IActionResult Get() => Ok("Users V2 with new contract");
}


🔄 Versioning & Modular Monolith

Trong Modular Monolith:

Versioning thường nằm ở Presentation Layer

Application & Domain không cần biết version

Có thể reuse Application Service cho nhiều version

Ví dụ:

UsersV1Controller → UserService

UsersV2Controller → UserService

⚖️ Trade-offs & Kinh nghiệm thực tế
Nên làm

Bắt đầu versioning ngay từ đầu

Version theo URI cho public API

Giữ version cũ càng đơn giản càng tốt

Log usage theo version

Không nên

Version mọi thay đổi nhỏ

Xóa version cũ quá sớm

Để business logic khác nhau quá nhiều giữa các version

📌 Kết luận

API Versioning là bắt buộc với hệ thống nghiêm túc.
Trong ASP.NET Core:

URI Versioning là lựa chọn thực tế nhất

Presentation chịu trách nhiệm version

Core business không bị ảnh hưởng

Hiểu rõ trade-off versioning là điểm rất mạnh khi phỏng vấn Solution Architect.