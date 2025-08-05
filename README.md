# 🛒 Product & Order Microservices Assignment

This project demonstrates two microservices — **Product Service** and **Order Service**, built using Java Spring Boot, communicating via REST, and containerized with Docker.

---

## 📦 Microservices Overview

### ✅ Product Service (Port: 8081)
- Add, get, and list products
- Fields: `id`, `name`, `price`, `stockQuantity`
- Database: PostgreSQL

### ✅ Order Service (Port: 8082)
- Place and list orders
- Checks product stock by calling Product Service
- Updates stock upon successful order
- Uses Redis to cache product info
- Database: PostgreSQL

---

## 🔧 Technologies Used

| Layer         | Stack                         |
|---------------|-------------------------------|
| Backend       | Java 17, Spring Boot          |
| Database      | PostgreSQL                    |
| Caching       | Redis (for Order Service)     |
| Communication | REST (via WebClient)          |
| Containers    | Docker, Docker Compose        |
| Build Tool    | Maven                         |

---

## 📁 Project Structure

project-root/
├── product-service/
│ ├── Dockerfile
│ └── Spring Boot app
├── order-service/
│ ├── Dockerfile
│ └── Spring Boot app
├── init.sql # Creates productdb and orderdb
└── docker-compose.yml # Multi-container setup

---

## 🚀 How to Run

### Step 1: Build JARs
```bash
cd product-service
mvn clean package -DskipTests

cd ../order-service
mvn clean package -DskipTests

### Step 2: Run with Docker Compose

bash
Copy
Edit
docker-compose down -v   # Optional: Clean previous volumes
docker-compose up --build

This will start:
PostgreSQL (with productdb & orderdb)
Redis
Product Service (8081)
Order Service (8082)

📮 API Endpoints
🔹 Product Service
Method	Endpoint	Description
POST	/products	Add product
GET	/products	List all products
GET	/products/{id}	Get product by ID
PUT	/products/{id}/decrease-stock?quantity=5	Reduce stock (called by order-service)

🔹 Order Service
Method	Endpoint	Description
POST	/orders	Place new order
GET	/orders	List all orders

🧪 Test with Postman
1. Add Product
POST http://localhost:8081/products

json
Copy
Edit
{
  "name": "Keyboard",
  "price": 1200,
  "stockQuantity": 10
}
2. Place Order
POST http://localhost:8082/orders

json
Copy
Edit
{
  "productId": 1,
  "quantity": 2
}
✅ Features Covered
✅ Microservices Communication (REST)

✅ Redis Caching for Product Lookup

✅ Docker + Docker Compose

✅ PostgreSQL Integration

✅ Clean Architecture (Controller → Service → Repository)

Author
Ankit Arya
Java Backend Developer | Microservices | Spring Boot | Docker | REST APIs

