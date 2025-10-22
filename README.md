**Employee Management System (EMS) REST API**
A robust RESTful API built with Java and Spring Boot to perform complete CRUD (Create, Read, Update, Delete) operations for an Employee Management System. This project serves as a complete backend solution, leveraging Spring Data JPA and Hibernate for efficient database interaction with a PostgreSQL database.

**Features**
Create a new employee record.

Retrieve a list of all employees.

Retrieve a single employee by their unique ID.

Update an existing employee's information.

Delete an employee from the database.

DTO (Data Transfer Object) Pattern: Uses EmployeeDto to expose data to the client, separating the API layer from the database entity.

Mapper Class: Includes a dedicated EmployeeMapper for clean conversion between Employee entities and EmployeeDto objects.

Centralized Exception Handling: Uses a custom ResourceNotFoundException to return clear 404 NOT_FOUND responses.

**Technology Stack**
Java 17+

Spring Boot 3.x

Spring Data JPA: For repository-based data access.

Hibernate: The default JPA implementation for object-relational mapping.

PostgreSQL: A powerful, open-source object-relational database.

Maven: For project and dependency management.

**Prerequisites**
Before you begin, ensure you have the following installed on your system:

JDK (Java Development Kit) 17 or later

**Installation & Setup**
1. Clone the repository:
git clone https://github.com/your-username/ems-backend.git
cd ems-backend

2. Create PostgreSQL Database: Open your PostgreSQL client (like psql or pgAdmin) and create a new database.
CREATE DATABASE ems_db;

3. Configure Database Connection: Open the src/main/resources/application.properties file. You will need to add your PostgreSQL database configuration.
# PostgreSQL Database Configuration
spring.datasource.url=jdbc:postgresql://localhost:5432/ems_db
spring.datasource.username=your_postgres_username
spring.datasource.password=your_postgres_password

# JPA/Hibernate Configuration
spring.jpa.hibernate.ddl-auto=update
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect
spring.jpa.show-sql=true

Replace your_postgres_username and your_postgres_password with your credentials.

spring.jpa.hibernate.ddl-auto=update will automatically update the database schema based on your Employee entity.

4. Run the application: Use Maven to build and run the Spring Boot application.
mvn spring-boot:run

The application will start on the default port 8080. You should see the console output indicating that the Tomcat server has started.

**API Endpoints**
The API provides the following endpoints, all prefixed with /api/employees.

<img width="385" height="293" alt="image" src="https://github.com/user-attachments/assets/5d972692-e40b-4ea5-95ea-a843cc5690ee" />



** Example Usage (cURL)**
You can test the endpoints using a tool like Postman, Insomnia, or cURL.

1. Create Employee
curl -X POST http://localhost:8080/api/employees \
-H "Content-Type: application/json" \
-d '{"firstName": "Tony", "lastName": "Stark", "email": "tony@stark.com"}'
2. Get All Employees
curl -X GET http://localhost:8080/api/employees
3. Get Employee by ID (e.g., ID 1)
curl -X GET http://localhost:8080/api/employees/1
4. Update Employee (e.g., ID 1)
curl -X PUT http://localhost:8080/api/employees/1 \
-H "Content-Type: application/json" \
-d '{"firstName": "Anthony", "lastName": "Stark", "email": "tony.stark@avengers.com"}'
5. Delete Employee (e.g., ID 1)
curl -X DELETE http://localhost:8080/api/employees/1

**Project Structure**

<img width="365" height="290" alt="image" src="https://github.com/user-attachments/assets/f19b0173-dcc7-459c-9b57-3c46e353e41c" />


Apache Maven

PostgreSQL Database
