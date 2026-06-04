# User Backend - Spring Boot REST API

A complete Spring Boot application for User Management System with REST APIs, database integration, and comprehensive error handling.

## Features ✨

- ✅ **User Management System** - Create, Read, Update, Delete users
- ✅ **MySQL Database Integration** - Persistent data storage
- ✅ **REST API** - Complete CRUD operations
- ✅ **Data Validation** - Request validation with meaningful error messages
- ✅ **Exception Handling** - Global exception handler for consistent error responses
- ✅ **API Documentation** - Swagger UI for API exploration
- ✅ **Lombok** - Reduce boilerplate code
- ✅ **Spring Data JPA** - Easy database operations

## Tech Stack 🛠️

- **Spring Boot 3.1.5**
- **Java 17**
- **Spring Data JPA**
- **MySQL 8.0**
- **Lombok**
- **Springdoc OpenAPI (Swagger)**
- **Maven**

## Project Structure 📁

```
user-backend/
├── src/
│   ├── main/
│   │   ├── java/com/example/userbackend/
│   │   │   ├── controller/
│   │   │   │   └── UserController.java
│   │   │   ├── service/
│   │   │   │   ├── UserService.java
│   │   │   │   └── UserServiceImpl.java
│   │   │   ├── repository/
│   │   │   │   └── UserRepository.java
│   │   │   ├── entity/
│   │   │   │   └── User.java
│   │   │   ├── dto/
│   │   │   │   ├── UserDTO.java
│   │   │   │   └── UserResponseDTO.java
│   │   │   ├── exception/
│   │   │   │   ├── GlobalExceptionHandler.java
│   │   │   │   ├── UserNotFoundException.java
│   │   │   │   ├── EmailAlreadyExistsException.java
│   │   │   │   └── ErrorResponse.java
│   │   │   └── UserBackendApplication.java
│   │   └── resources/
│   │       └── application.properties
│   └── test/
└── pom.xml
```

## Prerequisites 📋

- **Java 17** or higher
- **Maven 3.6+**
- **MySQL 8.0+**
- **Git**

## Setup Instructions 🚀

### 1. Clone the Repository
```bash
git clone https://github.com/shivamverma8/user-backend.git
cd user-backend
```

### 2. Create MySQL Database
```sql
CREATE DATABASE user_backend_db;
```

### 3. Update Database Configuration
Edit `src/main/resources/application.properties`:
```properties
spring.datasource.url=jdbc:mysql://localhost:3306/user_backend_db
spring.datasource.username=your_mysql_username
spring.datasource.password=your_mysql_password
```

### 4. Build the Project
```bash
mvn clean install
```

### 5. Run the Application
```bash
mvn spring-boot:run
```

The application will start on `http://localhost:8080`

## API Endpoints 🔌

### Base URL
```
http://localhost:8080/api/users
```

### Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/users` | Create a new user |
| GET | `/users` | Get all users |
| GET | `/users/{id}` | Get user by ID |
| GET | `/users/active/list` | Get all active users |
| GET | `/users/email/{email}` | Get user by email |
| GET | `/users/search/firstname?firstName=name` | Search users by first name |
| PUT | `/users/{id}` | Update user |
| DELETE | `/users/{id}` | Delete user |

## Example Requests 💻

### Create User
```bash
curl -X POST http://localhost:8080/api/users \
  -H "Content-Type: application/json" \
  -d '{
    "firstName": "John",
    "lastName": "Doe",
    "email": "john@example.com",
    "phoneNumber": "9876543210",
    "address": "123 Main St"
  }'
```

### Get All Users
```bash
curl http://localhost:8080/api/users
```

### Get User by ID
```bash
curl http://localhost:8080/api/users/1
```

### Update User
```bash
curl -X PUT http://localhost:8080/api/users/1 \
  -H "Content-Type: application/json" \
  -d '{
    "firstName": "Jane",
    "lastName": "Doe",
    "email": "jane@example.com",
    "phoneNumber": "9876543210",
    "address": "456 Oak St",
    "active": true
  }'
```

### Delete User
```bash
curl -X DELETE http://localhost:8080/api/users/1
```

## Swagger API Documentation 📚

Access the interactive Swagger UI:
```
http://localhost:8080/api/swagger-ui.html
```

## Database Schema 🗄️

### Users Table
```sql
CREATE TABLE users (
  id BIGINT PRIMARY KEY AUTO_INCREMENT,
  first_name VARCHAR(100) NOT NULL,
  last_name VARCHAR(100) NOT NULL,
  email VARCHAR(100) NOT NULL UNIQUE,
  phone_number VARCHAR(20) NOT NULL,
  address TEXT,
  active BOOLEAN DEFAULT true,
  created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

## Error Handling 🚨

### Sample Error Responses

**404 - User Not Found:**
```json
{
  "timestamp": "2024-01-15T10:30:00",
  "status": 404,
  "error": "Not Found",
  "message": "User not found with id: 999",
  "path": "/api/users/999"
}
```

**409 - Email Already Exists:**
```json
{
  "timestamp": "2024-01-15T10:30:00",
  "status": 409,
  "error": "Conflict",
  "message": "Email already exists: john@example.com",
  "path": "/api/users"
}
```

**400 - Validation Error:**
```json
{
  "timestamp": "2024-01-15T10:30:00",
  "status": 400,
  "error": "Validation Error",
  "message": "Invalid input",
  "path": "/api/users",
  "fieldErrors": {
    "email": "Email should be valid",
    "firstName": "First name is required"
  }
}
```

## Running Tests 🧪

```bash
mvn test
```

## Build & Deploy 📦

### Build JAR
```bash
mvn clean package
```

### Run JAR
```bash
java -jar target/user-backend-1.0.0.jar
```

## Key Features Implementation 🎯

### Service Layer
- Business logic separation from controllers
- Data validation and error handling
- Database operations through repositories

### Exception Handling
- Global exception handler for consistent error responses
- Custom exceptions for specific error cases
- Proper HTTP status codes

### Data Transfer Objects (DTOs)
- Separate DTOs for request and response
- Input validation using annotations
- Secure data handling

### Database Integration
- JPA Entity mapping
- Spring Data Repository for CRUD operations
- Auto-timestamp management with @PrePersist and @PreUpdate

## Future Enhancements 🚀

- [ ] JWT Authentication
- [ ] Role-based Access Control (RBAC)
- [ ] Pagination and Sorting
- [ ] Advanced Search Filters
- [ ] Unit and Integration Tests
- [ ] Caching with Redis
- [ ] Email Notifications
- [ ] Audit Logging

## Contributing 🤝

Contributions are welcome! Please feel free to submit a Pull Request.

## Support 💬

For questions or issues, please create an issue on GitHub.

---

**Happy Coding!** 🚀