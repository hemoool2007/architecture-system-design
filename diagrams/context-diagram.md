# System Context Diagram

## 1. Mục tiêu của tài liệu

Tài liệu này mô tả **bối cảnh tổng thể (System Context)** của hệ thống ở mức cao nhất, giúp người đọc nhanh chóng hiểu:

- Hệ thống này **làm gì**
- **Ai** là người sử dụng
- Hệ thống **tương tác với các hệ thống bên ngoài nào**
- Phạm vi trách nhiệm (system boundary)

Đây là **Level 1** trong mô hình **C4 Model**, đóng vai trò nền tảng cho các tài liệu kiến trúc chi tiết hơn.

---

## 2. Tổng quan hệ thống

**Tên hệ thống:** Solution Architect Portfolio System  
**Mục đích chính:**  
Một hệ thống demo/portfolio nhằm thể hiện năng lực của một Solution Architect .NET thông qua:
- Tài liệu kiến trúc
- Demo kỹ thuật
- Các quyết định thiết kế thực tế

Hệ thống được thiết kế theo hướng **modular**, mỗi domain/skill có thể phát triển thành một repository riêng.

---

## 3. Actors (Người dùng / Vai trò)

### 3.1 Primary User – Recruiter / Interviewer
- Xem tổng quan năng lực kỹ thuật
- Đọc tài liệu kiến trúc
- Đánh giá tư duy hệ thống và design decision

### 3.2 Secondary User – Developer / Architect (Owner)
- Viết tài liệu
- Xây dựng demo
- Refactor và mở rộng kiến trúc theo thời gian

---

## 4. System Boundary

Hệ thống **Solution Architect Portfolio System** bao gồm:

- Tài liệu kiến trúc (Markdown)
- Source code demo (ở các repo liên kết)
- Diagram (C4, sequence, deployment…)

Không bao gồm:
- Hệ thống CI/CD thực tế
- Hạ tầng production thật

---

## 5. External Systems

| External System | Mục đích |
|-----------------|----------|
| GitHub | Lưu trữ source code & tài liệu |
| GitHub Pages | Render tài liệu dưới dạng website |
| External Demo Repositories | Chứa các project demo cho từng domain |
| Cloud Providers (AWS/Azure – demo) | Mô phỏng kiến trúc cloud |

---

## 6. High-level Interactions

- Người dùng truy cập **GitHub repository**
- Xem README → truy cập tài liệu kiến trúc
- Từ tài liệu, điều hướng sang các **repo demo**
- Các demo thể hiện:
  - Backend (.NET)
  - Database
  - Messaging
  - Cloud architecture

---

## 7. Context Diagram (Conceptual)

```text
+--------------------+
|     Recruiter      |
+---------+----------+
          |
          | View Docs / Code
          v
+----------------------------+
| Solution Architect         |
| Portfolio System           |
+------+---------------------+
       |
       | Reference
       v
+----------------------------+
| Demo Repositories          |
| (.NET, DB, Cloud, etc.)    |
+----------------------------+

8. Architectural Principles

Documentation-first

Realistic but simplified

Modular & extensible

Focus on reasoning, not chỉ code

9. Liên kết tài liệu tiếp theo

Container Diagram

Component Diagram

Architecture Decision Records

10. Ghi chú

Tài liệu này được viết với mục tiêu:

Phục vụ phỏng vấn Solution Architect

Là nền tảng cho các level kiến trúc chi tiết hơn
