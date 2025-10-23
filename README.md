Employee Management System (ems-backend)
Simple Spring Boot RESTful backend for an Employee Management System (EMS). This project provides CRUD APIs to manage employees and is implemented with Spring Boot, Spring Data JPA, PostgreSQL, and Lombok.

Project Snapshot
Artifact: net. javaguides:ems-backend
Version: 0.0.1-SNAPSHOT
Java: 21
Spring Boot: 3.5.6
Database: PostgreSQL (runtime)
Features
Create, read, update, and delete employees via REST endpoints
Uses JPA entities and DTOs with a simple mapper
Example configuration included for PostgreSQL
Tech Stack
Java 21
Spring Boot (web, data-jpa)
PostgreSQL
Lombok (compile-time)
Maven build
Getting Started
Prerequisites:

Java 21 JDK
Maven 3.6+
PostgreSQL (or any JDBC-compatible DB)
Clone the repository to your machine.
Configure the database in application.properties (example values are included):
Create the ems database in PostgreSQL (or change the URL to point to your DB).

Build and run the application with Maven:

Or build the jar and run it:

The application starts on the default Spring Boot port 8080.

REST API
Base URL: http://localhost:8080/api/employees

Endpoints:

POST /api/employees
Create a new employee
Request JSON (example):
Response: 201 Created with created employee DTO including id.

GET /api/employees

Retrieve list of all employees
Response: 200 OK with JSON array of employee objects
GET /api/employees/{id}

Retrieve employee by id
Response: 200 OK with employee object or 404 if not found
PUT /api/employees/{id}

Update employee by id
Request JSON (same shape as create)
Response: 200 OK with updated employee object
DELETE /api/employees/{id}

Delete an employee
Response: 200 OK with success message
Employee DTO shape:

Notes:

The project uses EmployeeDto for request/response and Employee entity for persistence. Field names are mapped by a small EmployeeMapper.
The example application.properties points to a local PostgreSQL instance and uses spring.jpa.hibernate.ddl-auto=update for convenience in development.
Tests
There is a starter test class at EmsBackendApplicationTests.java. Run tests with:

Contributing
Feel free to open issues or PRs. For local development, ensure Lombok is enabled in your IDE so generated getters/setters are recognized.

License
This project contains no license information in the POM. Add a license file (for example, MIT) if you plan to publish the code.

Completion summary

Added README.md to repository root with build/run steps, API docs, and configuration notes.
Verified key project details from pom.xml and source files.
Next steps (optional)

Add curl examples or Postman collection to README.
Add LICENSE file and update POM metadata.
Create GitHub Action for CI.
Tell me which of those (if any) you want next, or if you want any wording changes to the README before you push it to GitHub.

GPT-5 mini • 0.9x
