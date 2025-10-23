<!-- prettier-ignore -->
<!--
  A clean, attractive README optimized for GitHub display.
  Includes badges, a concise hero, file tree, quick start, API examples (PowerShell), Docker, and next steps.
-->

# EMS Backend

[![Maven Central](https://img.shields.io/badge/maven-3.8+-blue.svg?style=flat-square)](https://maven.apache.org/)
[![Java](https://img.shields.io/badge/java-21-brightgreen.svg?style=flat-square)](#)
[![Spring Boot](https://img.shields.io/badge/spring--boot-3.5.6-green.svg?style=flat-square)](https://spring.io/projects/spring-boot)
[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg?style=flat-square)](./LICENSE)

An elegant, minimal Employee Management System (EMS) backend built with Spring Boot, Spring Data JPA, PostgreSQL and Lombok.

> Small, well-structured demo app for CRUD operations on employees. Ideal for learning or quickly bootstrapping a microservice.

---

## Table of Contents

- [Demo & Screenshot](#demo--screenshot)
- [Quick Start](#quick-start)
- [Local Development (PowerShell)](#local-development-powershell)
- [API Reference](#api-reference)
- [Project Structure](#project-structure)
- [Configuration](#configuration)
- [Docker (optional)](#docker-optional)
- [Testing](#testing)
- [Next Steps](#next-steps)
- [Contributing](#contributing)
- [License](#license)

---

## Demo & Screenshot

This backend exposes a JSON REST API at `/api/employees` supporting create/read/update/delete operations. Use Postman, curl or the PowerShell examples below.

_(No UI included — it's a backend service.)_

---

## Quick Start

1. Clone the repository

```powershell
git clone https://github.com/RaghavSingal2002/ems-backend.git
cd ems-backend
```

2. Configure a PostgreSQL database (see Configuration below) or use Docker.

3. Build and run with the included Maven wrapper:

```powershell
.\mvnw.cmd clean package -DskipTests
.\mvnw.cmd spring-boot:run
```

Or run the built JAR:

```powershell
java -jar target\ems-backend-0.0.1-SNAPSHOT.jar
```

The app starts on port 8080 by default (`http://localhost:8080`).

---

## Local Development (PowerShell)

Set environment variables and run without changing `application.properties`:

```powershell
$env:SPRING_DATASOURCE_URL='jdbc:postgresql://localhost:5432/ems_db';
$env:SPRING_DATASOURCE_USERNAME='ems_user';
$env:SPRING_DATASOURCE_PASSWORD='password';
.\mvnw.cmd spring-boot:run
```

Enable Lombok in your IDE (annotation processing) to avoid red squiggles.

---

## API Reference

Base: `http://localhost:8080/api/employees`

All endpoints accept/return JSON. Example request bodies below assume fields: `firstName`, `lastName`, `email`.

- Create employee

  - Method: POST
  - URL: `/api/employees`
  - Example (PowerShell):

```powershell
curl -Method POST -Uri http://localhost:8080/api/employees -Headers @{"Content-Type"="application/json"} -Body (@{firstName='John'; lastName='Doe'; email='john.doe@example.com'} | ConvertTo-Json)
```

  - Success: 201 Created with created Employee JSON (including `id`).

- Get employee by id

  - Method: GET
  - URL: `/api/employees/{id}`

```powershell
curl http://localhost:8080/api/employees/1
```

- Get all employees

  - Method: GET
  - URL: `/api/employees`

```powershell
curl http://localhost:8080/api/employees
```

- Update employee

  - Method: PUT
  - URL: `/api/employees/{id}`

```powershell
curl -Method PUT -Uri http://localhost:8080/api/employees/1 -Headers @{"Content-Type"="application/json"} -Body (@{firstName='Jane'; lastName='Doe'; email='jane.doe@example.com'} | ConvertTo-Json)
```

- Delete employee

  - Method: DELETE
  - URL: `/api/employees/{id}`

```powershell
curl -Method DELETE http://localhost:8080/api/employees/1
```

Small note: the controller returns a short success message on delete.

---

## Project Structure (detailed)

```
ems-backend/
├─ mvnw, mvnw.cmd
├─ pom.xml
└─ src/
   ├─ main/
   │  ├─ java/net/javaguides/ems/
   │  │  ├─ EmsBackendApplication.java        # Spring Boot entrypoint
   │  │  ├─ controller/                       # REST controllers
   │  │  │  └─ EmployeeController.java
   │  │  ├─ dto/                              # Data Transfer Objects
   │  │  │  └─ EmployeeDto.java
   │  │  ├─ entity/                           # JPA entities
   │  │  │  └─ Employee.java
   │  │  ├─ exception/                        # Custom exceptions
   │  │  │  └─ ResourceNotFoundException.java
   │  │  ├─ mapper/                           # Map entity <-> dto
   │  │  │  └─ EmployeeMapper.java
   │  │  ├─ repository/                       # Spring Data JPA repos
   │  │  │  └─ EmployeeRepository.java
   │  │  └─ service/                          # Business logic
   │  │     ├─ EmployeeService.java
   │  │     └─ impl/EmployeeServiceImpl.java
   │  └─ resources/
   │     └─ application.properties
   └─ test/
      └─ java/net/javaguides/ems/
         └─ EmsBackendApplicationTests.java
```

If you'd like, I can collapse this into a GitHub tree-view snippet (for long READMEs) or include a class diagram.

---

## Configuration

Edit `src/main/resources/application.properties` (or set environment variables).

Recommended (development):

``properties
spring.datasource.url=jdbc:postgresql://localhost:5432/ems_db
spring.datasource.username=ems_user
spring.datasource.password=password
spring.jpa.hibernate.ddl-auto=update
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect
server.port=8080
```

Be cautious with `ddl-auto=update` in production.

---

## Docker (optional)

Quick local PostgreSQL + app using Docker Compose (create `docker-compose.yml`):

```yaml
version: '3.8'
services:
  db:
    image: postgres:15
    environment:
      POSTGRES_DB: ems_db
      POSTGRES_USER: ems_user
      POSTGRES_PASSWORD: password
    ports:
      - 5432:5432
  app:
    build: .
    depends_on:
      - db
    ports:
      - 8080:8080
    environment:
      - SPRING_DATASOURCE_URL=jdbc:postgresql://db:5432/ems_db
      - SPRING_DATASOURCE_USERNAME=ems_user
      - SPRING_DATASOURCE_PASSWORD=password
```

If you'd like, I can add a Dockerfile for the Spring Boot app and a ready-to-go `docker-compose.yml`.

---

## Testing

Run unit tests with the wrapper:

```powershell
.\mvnw.cmd test
```

Add integration tests using Testcontainers to run an isolated PostgreSQL instance during test runs.

---

## Next steps (recommended)

- Add OpenAPI/Swagger (springdoc-openapi) for interactive API docs.
- Add GitHub Actions CI to build and run tests on push/PR.
- Add Dockerfile and `docker-compose.yml` to run the app + Postgres locally.
- Provide a Postman collection or an OpenAPI JSON/YAML export.

I can implement any of these — tell me which one you want first.

---

## Contributing

Contributions are welcome. Please open an issue or a pull request. Keep changes small and add tests for new behavior.

Suggested checklist for PRs:

- [ ] Branch from `main` with a descriptive name
- [ ] Add unit/integration tests for new behavior
- [ ] Update README if you change public APIs or configuration

---

## License

This repo uses the MIT license. Add a `LICENSE` file at the project root if you want to include the full license text.

---

Thank you — tell me which enhancement you'd like next (Dockerfile, GitHub Actions, Swagger/OpenAPI, Postman collection, or a class diagram). 
# EMS Backend (Employee Management System)

A simple Spring Boot REST API for managing employees. This project demonstrates a typical layered architecture using Spring Boot, Spring Data JPA, PostgreSQL and Lombok.

---

## Table of Contents

- Project overview
- Tech stack & requirements
- File structure (full)
- Configuration (database, properties)
- API endpoints (examples)
- Build & run (Windows PowerShell)
- Tests
- Notes & tips
- Next steps / suggestions

---

## Project overview

This repository is a small Employee Management System backend. It exposes CRUD REST endpoints to create, read, update and delete employees and persists data to PostgreSQL using Spring Data JPA.

Primary goals:

- Demonstrate a layered Spring Boot application (controller, service, repository, mapper, DTOs, entities).
- Use PostgreSQL as the persistence store.
- Keep the code minimal and easy to follow for learning or quick prototyping.

---

## Tech stack & requirements

- Java 21
- Maven (wrapper included: `mvnw`, `mvnw.cmd`)
- Spring Boot 3.x (parent 3.5.6 in pom.xml)
- Spring Data JPA
- PostgreSQL (runtime dependency)
- Lombok (used for DTOs/entity boilerplate)

Before running, ensure you have:

- Java 21 installed and `JAVA_HOME` pointing to it.
- A running PostgreSQL database and credentials.

---

## Full file structure

Below is the repository layout with short descriptions for important files.

```
ems-backend/
  mvnw
  mvnw.cmd
  pom.xml                    # Maven project file (artifactId: ems-backend)
  src/
    main/
      java/
        net/javaguides/ems/
          EmsBackendApplication.java   # Spring Boot main class
          controller/
            EmployeeController.java    # REST controllers (API endpoints)
          dto/
            EmployeeDto.java           # Data Transfer Object for Employee
          entity/
            Employee.java              # JPA entity mapped to DB
          exception/
            ResourceNotFoundException.java
          mapper/
            EmployeeMapper.java        # Mapping between entity <-> dto
          repository/
            EmployeeRepository.java    # Spring Data JPA repository
          service/
            EmployeeService.java       # Service interface
            impl/
              EmployeeServiceImpl.java # Service implementation
      resources/
        application.properties        # Application configuration (DB url, user, pass)
    test/
      java/
        net/javaguides/ems/
          EmsBackendApplicationTests.java

```

Files omitted above are supportive or tests; the main application logic lives under `net.javaguides.ems`.

---

## Configuration

Application properties live in `src/main/resources/application.properties`.

You need to configure PostgreSQL connection settings. Typical properties:

```
spring.datasource.url=jdbc:postgresql://localhost:5432/ems_db
spring.datasource.username=ems_user
spring.datasource.password=your_password
spring.jpa.hibernate.ddl-auto=update
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect
server.port=8080
```

Replace the values with your database host, name, user and password.

Note: `spring.jpa.hibernate.ddl-auto=update` is convenient for development. For production, use migrations (Flyway/Liquibase) and a safer schema strategy.

---

## API Endpoints

Base path: `/api/employees`

All examples below use PowerShell-friendly curl (Windows). You can also use Postman or httpie.

- Create employee

  - Method: POST
  - URL: http://localhost:8080/api/employees
  - Body (JSON):

```
{
  "firstName": "John",
  "lastName": "Doe",
  "email": "john.doe@example.com"
}
```

PowerShell curl example:

```powershell
curl -Method POST -Uri http://localhost:8080/api/employees -Headers @{"Content-Type"="application/json"} -Body (@{firstName='John'; lastName='Doe'; email='john.doe@example.com'} | ConvertTo-Json)
```

- Get employee by id

  - Method: GET
  - URL: http://localhost:8080/api/employees/{id}

PowerShell example:

```powershell
curl http://localhost:8080/api/employees/1
```

- Get all employees

  - Method: GET
  - URL: http://localhost:8080/api/employees

```powershell
curl http://localhost:8080/api/employees
```

- Update employee

  - Method: PUT
  - URL: http://localhost:8080/api/employees/{id}
  - Body (JSON): same shape as create

```powershell
curl -Method PUT -Uri http://localhost:8080/api/employees/1 -Headers @{"Content-Type"="application/json"} -Body (@{firstName='Jane'; lastName='Doe'; email='jane.doe@example.com'} | ConvertTo-Json)
```

- Delete employee

  - Method: DELETE
  - URL: http://localhost:8080/api/employees/{id}

```powershell
curl -Method DELETE http://localhost:8080/api/employees/1
```

Responses are typical JSON payloads and standard HTTP status codes (201 Created on POST, 200 OK on successful GET/PUT/DELETE). The controller returns a message string on successful delete.

---

## DTO / Entity shape

The project contains `EmployeeDto` and `Employee` entity. Typical fields in this sample project are:

- id (Long)
- firstName (String)
- lastName (String)
- email (String)

Check `src/main/java/net/javaguides/ems/dto/EmployeeDto.java` and `entity/Employee.java` for exact fields and annotations.

---

## Build & Run (Windows PowerShell)

From the project root (`ems-backend`):

Build:

```powershell
.\mvnw.cmd clean package -DskipTests
```

Run (using the wrapper):

```powershell
.\mvnw.cmd spring-boot:run
```

Or run the built jar:

```powershell
java -jar target\ems-backend-0.0.1-SNAPSHOT.jar
```

If you prefer Maven directly and have it installed:

```powershell
mvn clean package
mvn spring-boot:run
```

Environment variables can also be used to override configuration at runtime. For example (PowerShell):

```powershell
$env:SPRING_DATASOURCE_URL='jdbc:postgresql://localhost:5432/ems_db'; .\mvnw.cmd spring-boot:run
```

---

## Tests

Run tests with:

```powershell
.\mvnw.cmd test
```

There is a minimal test class `EmsBackendApplicationTests` under `src/test/java`.

---

## Notes & tips

- Lombok: The project uses Lombok to reduce boilerplate. If your IDE doesn't recognize Lombok annotations, install the Lombok plugin and enable annotation processing.
- Database: Use a dedicated DB and user for development. If you don't want to run PostgreSQL locally, consider using Docker Compose for a quick PostgreSQL container.

Example Docker Compose snippet:

```yaml
version: '3.8'
services:
  db:
    image: postgres:15
    environment:
      POSTGRES_DB: ems_db
      POSTGRES_USER: ems_user
      POSTGRES_PASSWORD: password
    ports:
      - 5432:5432

```

---

## Next steps / suggestions

- Add integration tests that run against a testcontainer/Postgres instance.
- Add API documentation (Swagger/OpenAPI). Springdoc OpenAPI is a small dependency to add.
- Add a Dockerfile to containerize the app and a GitHub Actions workflow to build and run tests on each PR.
- Add a Postman collection or OpenAPI spec for easier client testing.

---

If you'd like, I can also:

- Generate a Dockerfile and Docker Compose to run the app + Postgres.
- Add a simple GitHub Actions CI workflow.
- Create a Postman collection or OpenAPI (Swagger) docs.

---

Thank you — tell me if you'd like formatting tweaks or additional sections (diagrams, sequence flows, sample responses, or live demo instructions).
