# Messaging-Service

A RESTful messaging service built with **Spring Boot** and **MongoDB**.  
This service provides features such as user registration, authentication (HTTP Basic), messaging, blocking, and activity logging.

---

## 🚀 How to Run

### 1. Clone the Repository

```bash
git clone <your-repo-url>
cd Messaging-Service
```

### 2. Run with Docker (Recommended)

Make sure you have Docker and Docker Compose installed.  
This will spin up both the Spring Boot application and a MongoDB container.

```bash
docker-compose up --build
```

Once containers are up, the API will be available at:

```
http://localhost:8080/
```

> MongoDB will be running in a separate container and accessible to the Spring Boot app automatically.

---

### ⚙️ Alternative: Run Locally Without Docker

#### 1. Start MongoDB Manually

Ensure MongoDB is running locally (default port `27017`), or update the connection string in `src/main/resources/application.properties`.

#### 2. Run the Application

##### Using Maven Wrapper

```bash
./mvnw spring-boot:run
```

##### Or build and run the JAR

```bash
./mvnw clean package
java -jar target/Messaging-Service-0.0.1-SNAPSHOT.jar
```

---

## 📌 API Endpoints

### 🧑‍💼 User

| Method | Endpoint                        | Description                |
|--------|----------------------------------|----------------------------|
| POST   | `/api/users/register`           | Register a new user       |
| POST   | `/api/users/login`              | Login and retrieve user   |
| GET    | `/api/users`                    | Get all users (auth)      |
| DELETE | `/api/users/{username}`         | Delete a user (auth)      |

### ✉️ Messaging

| Method | Endpoint                                  | Description                        |
|--------|--------------------------------------------|------------------------------------|
| POST   | `/api/messages`                            | Send a message (auth)             |
| GET    | `/api/messages/sender/{senderUsername}`    | Get sent messages by user (auth)  |
| GET    | `/api/messages/receiver/{receiverUsername}`| Get received messages (auth)      |
| DELETE | `/api/messages/{messageId}`                | Delete a message (auth)           |

### 🚫 Blocking

| Method | Endpoint                                  | Description                             |
|--------|--------------------------------------------|-----------------------------------------|
| POST   | `/api/blocks/block`                        | Block a user (auth)                     |
| GET    | `/api/blocks/blocker/{username}`           | Get users blocked by the user (auth)   |

### 📜 Activity Log

| Method | Endpoint                                  | Description                           |
|--------|--------------------------------------------|---------------------------------------|
| GET    | `/api/activity-logs/{username}`            | Get activity logs for a user (auth)  |

---

## 🔐 Notes

- Passwords are encrypted using **BCrypt**.
- All endpoints except `register` and `login` require **HTTP Basic Authentication**.
- MongoDB URI can be customized in:  
  `src/main/resources/application.properties`.

---

## 📁 Project Structure

- `entity/` - MongoDB documents (User, Message, Block, Log)
- `dto/` - Data Transfer Objects
- `api/` - REST controllers
- `business/` - Service logic (abstract & concrete)
- `dao/` - MongoDB repositories
- `core/` - Config, exceptions, utilities

---

## 🛠️ Technologies Used

- Java 21+
- Spring Boot 3.x
- Spring Security
- Spring Data MongoDB
- Lombok
- Maven
- **Docker & Docker Compose**