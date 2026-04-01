# Fitness Tracker API

A production-ready RESTful Fitness Tracker application built with **Spring Boot**. Features JWT authentication, role-based access control, activity tracking, personalized recommendations, and full Swagger documentation — containerized with Docker and ready for cloud deployment.

## Table of Contents

- [Features](#features)
- [Tech Stack](#tech-stack)
- [Architecture](#architecture)
- [Getting Started](#getting-started)
- [Environment Variables](#environment-variables)
- [API Overview](#api-overview)
- [Running with Docker](#running-with-docker)
- [Cloud Deployment](#cloud-deployment)
- [Project Structure](#project-structure)
- [Course Curriculum](#course-curriculum)
- [Contributing](#contributing)

---

## Features

- User registration and login with JWT-based authentication
- Role-Based Access Control (RBAC) — USER and ADMIN roles
- Activity logging (running, cycling, swimming, strength training, etc.)
- Personalized fitness recommendations
- Secure REST APIs with Spring Security
- Password encryption with BCrypt
- Input validation with detailed error responses
- Interactive API documentation via Swagger / OpenAPI 3
- Dockerized for consistent local and cloud environments
- MySQL database with JPA & Hibernate ORM

---

## Tech Stack

| Layer | Technology |
|---|---|
| Language | Java 17 |
| Framework | Spring Boot 3.x |
| Security | Spring Security + JWT |
| ORM | Spring Data JPA + Hibernate |
| Database | MySQL 8 |
| Docs | Springdoc OpenAPI (Swagger UI) |
| Build | Maven |
| Container | Docker + Docker Compose |
| Utilities | Lombok, ModelMapper |

---

## Architecture

```
Client
  └── HTTP Request
        └── Spring Security Filter Chain (JWT validation)
              └── Controller Layer (REST endpoints)
                    └── Service Layer (business logic)
                          └── Repository Layer (JPA)
                                └── MySQL Database
```

Design patterns used: DTO Pattern, Builder Pattern, Repository Pattern.

---

## Getting Started

### Prerequisites

- Java 17+
- Maven 3.8+
- MySQL 8+
- Docker (optional)

### Clone the repo

```bash
git clone https://github.com/your-username/springboot-fitness-tracker.git
cd springboot-fitness-tracker
```

### Configure the database

Create a MySQL database:

```sql
CREATE DATABASE fitness_tracker;
```

Update `src/main/resources/application.properties`:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/fitness_tracker
spring.datasource.username=your_mysql_user
spring.datasource.password=your_mysql_password
spring.jpa.hibernate.ddl-auto=update
```

### Run the application

```bash
mvn spring-boot:run
```

The API will be available at `http://localhost:8080`.
Swagger UI: `http://localhost:8080/swagger-ui/index.html`

---

## Environment Variables

| Variable | Description | Default |
|---|---|---|
| `DB_URL` | JDBC connection URL | `jdbc:mysql://localhost:3306/fitness_tracker` |
| `DB_USERNAME` | MySQL username | — |
| `DB_PASSWORD` | MySQL password | — |
| `JWT_SECRET` | Secret key for signing tokens | — |
| `JWT_EXPIRATION` | Token expiry in ms | `86400000` (24h) |

---

## API Overview

### Auth endpoints

| Method | Endpoint | Description |
|---|---|---|
| POST | `/api/auth/register` | Register a new user |
| POST | `/api/auth/login` | Login and receive JWT |

### Activity endpoints (requires auth)

| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/activities` | Get all activities for current user |
| POST | `/api/activities` | Log a new activity |
| GET | `/api/activities/{id}` | Get activity by ID |
| PUT | `/api/activities/{id}` | Update an activity |
| DELETE | `/api/activities/{id}` | Delete an activity |

### Recommendations (requires auth)

| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/recommendations` | Get personalized recommendations |

### Admin endpoints (ADMIN role only)

| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/admin/users` | List all users |
| DELETE | `/api/admin/users/{id}` | Delete a user |

Full interactive docs available at `/swagger-ui/index.html` when running.

---

## Running with Docker

```bash
docker-compose up --build
```

This spins up both the Spring Boot app and a MySQL container. Services:
- App: `http://localhost:8080`
- MySQL: `localhost:3306`

`docker-compose.yml` is included in the repo root.

---

## Cloud Deployment

This project is configured for free-tier deployment on **Railway** or **Render**:

1. Push your repo to GitHub
2. Connect to Railway / Render
3. Add environment variables (see table above)
4. Deploy — the platform will use the included `Dockerfile`

Step-by-step deployment walkthrough is covered in the course.

---

## Project Structure

```
src/
└── main/
    ├── java/com/fitnesstracker/
    │   ├── config/          # Security config, JWT config, Swagger config
    │   ├── controller/      # REST controllers
    │   ├── dto/             # Data Transfer Objects
    │   ├── entity/          # JPA entities
    │   ├── exception/       # Global exception handling
    │   ├── repository/      # Spring Data JPA repositories
    │   ├── security/        # JWT filter, UserDetailsService
    │   └── service/         # Business logic
    └── resources/
        └── application.properties
```



> Built with Spring Boot · Secured with JWT · Documented with Swagger · Deployed with Docker