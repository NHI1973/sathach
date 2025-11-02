# 🧩 EProject Phase 1 — Microservices with Node.js, MongoDB & RabbitMQ

Dự án mô phỏng kiến trúc **Microservices** gồm các service:  
- `api-gateway` — gateway định tuyến các request tới từng service
- `auth` — xác thực & quản lý người dùng  
- `product` — quản lý sản phẩm và đặt hàng  
- `order` — xử lý đơn hàng  
Service `order` và `product`giao tiếp thông qua **RabbitMQ** 
Dữ liệu được Lưu trữ dữ liệu trên **MongoDB** (chạy trong Docker).

---

## 🚀 Công nghệ sử dụng

| Thành phần | Công nghệ |
|-------------|------------|
| Ngôn ngữ | Node.js (Express.js) |
| Cơ sở dữ liệu | MongoDB |
| Message Queue | RabbitMQ |
| Containerization | Docker & Docker Compose |
| API Test | Postman |
| Authentication | JWT (JSON Web Token) |

---

## 🧱 Cấu trúc thư mục

EProject-Phase-1/
│
├── auth/ # Service quản lý người dùng và xác thực
│ ├── src/
│ │ ├── config/ # cấu hình mongo và jwt
│ │ ├── controllers/ # Xử lý logic các request từ client
│ │ ├── models/ # Định nghĩa các model dữ liệu
│ │ ├── repositories/ # Tầng truy xuất dữ liệu
│ │ ├── routes/ # Định nghĩa router cho gateway
│ │ ├── services/ # logic nghiệp vụ (API)
│ │ ├── middlewares/ # tầng bảo mật
│ │ └── test/ # Unit tests cho auth
│ ├── Dockerfile
│ ├── index.js
│ ├── .env
│ ├── package-lock.json
│ └── package.json
│
├── product/ # Service quản lý sản phẩm
│ ├── src/
│ │ ├── config/ # cấu hình mongo và jwt
│ │ ├── controllers/ # Xử lý logic các request từ client
│ │ ├── models/ # Định nghĩa các model dữ liệu
│ │ ├── repositories/ # Tầng truy xuất dữ liệu
│ │ ├── routes/ # Định nghĩa router cho gateway
│ │ ├── services/ # Giao tiếp với các service khác 
│ │ ├── test/ # Unit tests cho product
│ │ ├── app.js
│ │ └── config.js
│ ├── Dockerfile
│ ├── index.js
│ ├── .env
│ ├── package-lock.json
│ └── package.json
│
├── order/ # Service quản lý đơn hàng
│ ├── src/
│ │ ├── model/ # Định nghĩa các model dữ liệu 
│ │ ├── utils/ # Xác thực và giao tiếp với các service khác
│ │ ├── app.js
│ │ └── config.js
│ ├── Dockerfile
│ ├── index.js
│ ├── .env
│ ├── package-lock.json
│ └── package.json
│
├── api-gateway/ # Gateway định tuyến các request tới từng service
│ ├── Dockerfile
│ ├── index.js
│ ├── .env
│ ├── package-lock.json
│ └── package.json
│
├── utils/ 
│ ├── isAuthenticated.js # Xác thực token
│
├── docker-compose.yml # Cấu hình Docker Compose cho toàn hệ thống
├── package.json
├── package-lock.json
└── .gitignore


---

## ⚙️ Cài đặt & Chạy dự án

### 1️ Cấu hình môi trường

Mỗi service (`auth`, `product`, `order`, `api-gateway`) cần file `.env` riêng.  
mỗi Servece (`auth`, `product`, `order`, `api-gateway`) cần file `Dockerfile` riêng.

### 2️ Chạy dự án bằng Docker Compose

`docker-compose up --build`

Sau khi chạy, Docker sẽ tạo các container:

mongodb → MongoDB database

rabbitmq → RabbitMQ server (UI: http://localhost:15672)

auth → Service xác thực người dùng (port 3000)

product → Service sản phẩm (port 3001)

order → Service đặt đơn hàng (port 3002)

api-gateway → Gateway cho toàn hệ thống (port 3003)


---

### 3 RabbitMQ Dashboard

Truy cập:
👉 http://localhost:15672

Mặc định:

Username: guest

Password: guest

Tại đây có thể xem các exchange, queue, và message giữa các service.
- Queue trong RabbitMQ 
  ![RabbitMQ-Queue](./public/results/rabbitMQ.png)  
  `./public/results/rabbitMQ.png`

---

### 4 🧹 Dừng dự án

`docker-compose stop`

---

### 5 Xóa dự án

`docker-compose down`

---

### 5 👨‍💻 Tác giả

22713701 - Nguyễn Phú Bảo

📧 Email: phubao12as@gmail.com
💼 Fullstack Developer (Node.js, Docker, Microservices)