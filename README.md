# Spring Boot Tutorial – Software Engineers API

A small REST API built with Spring Boot 4, Spring Data JPA, and PostgreSQL. It stores software engineers (name and tech stack) and exposes endpoints to list, fetch, and create them.

## Tech stack

- Java 21+
- Spring Boot 4.1 (Web MVC, Data JPA)
- PostgreSQL (run via Docker Compose)
- Maven (wrapper included)

## Project structure

```
src/main/java/com/example/demo/
├── DemoApplication.java              # Entry point
├── SoftwareEngineer.java             # JPA entity
├── SoftwareEngineerRepository.java   # Spring Data repository
├── SoftwareEngineerService.java      # Business logic
└── SoftwareEngineerController.java   # REST endpoints
```

## Getting started

### 1. Start PostgreSQL

Make sure Docker Desktop is running, then from the project root:

```bash
docker compose up -d
```

This starts a `postgres-spring-boot` container exposed on `localhost:5332` (user `user`, password `1`).

### 2. Run the application

```bash
./mvnw spring-boot:run
```

On Windows:

```powershell
.\mvnw.cmd spring-boot:run
```

Or run `DemoApplication` from your IDE. The API starts on `http://localhost:8080`.

## Configuration

Database settings live in `src/main/resources/application.properties`:

```properties
spring.datasource.url=jdbc:postgresql://localhost:5332/user
spring.datasource.username=user
spring.datasource.password=1
spring.jpa.hibernate.ddl-auto=update
```

`ddl-auto=update` lets Hibernate create and update the tables from the entity classes automatically.

## API endpoints

Base path: `/api/v1/software-engineers`

| Method | Path    | Description                   |
|--------|---------|-------------------------------|
| GET    | `/`     | List all software engineers   |
| GET    | `/{id}` | Get a software engineer by id |
| POST   | `/`     | Create a new software engineer |

### Example: create an engineer

```bash
curl -X POST http://localhost:8080/api/v1/software-engineers \
  -H "Content-Type: application/json" \
  -d '{"name": "Youssef", "techStack": "Java, Spring Boot, PostgreSQL"}'
```

### Example: list engineers

```bash
curl http://localhost:8080/api/v1/software-engineers
```
