Employee Management System (EMS) REST API
A robust RESTful API built with Java and Spring Boot to perform full CRUD (Create, Read, Update, Delete) operations for managing employees. It uses Spring Data JPA with Hibernate for database access and PostgreSQL as the data store. The project follows clean architecture practices with DTOs, mappers, and centralized exception handling.
Features

* Create a new employee
* Retrieve all employees
* Retrieve a single employee by ID
* Update an existing employee
* Delete an employee
* DTO pattern: EmployeeDto separates API layer from persistence layer
* Mapper class: EmployeeMapper for converting between Entity and DTO
* Centralized exception handling with ResourceNotFoundException (returns 404 NOT_FOUND)

Tech Stack

* Java 17+
* Spring Boot 3.x
* Spring Data JPA
* Hibernate
* PostgreSQL
* Maven

Prerequisites

* JDK 17 or later
* Apache Maven
* PostgreSQL

Getting Started
1) Clone the repository
