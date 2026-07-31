# Employee Service - Spring Boot REST API

A simple RESTful API built with **Spring Boot**, **Java 17**, **Spring Data JPA**, and **PostgreSQL**.

This project demonstrates how to build a CRUD (Create, Read, Update, Delete) REST API using Spring Boot and PostgreSQL.

---

# Technology Stack

| Technology | Version |
|------------|---------|
| Java | 17 |
| Spring Boot | 3.5.x (Recommended) |
| Maven | Latest |
| PostgreSQL | 17 or later |
| Spring Data JPA | Latest |
| Hibernate | Latest |
| IntelliJ IDEA | Community/Ultimate |
| Postman | Latest |

---

# Features

- Create Employee
- Get All Employees
- Get Employee By ID
- Update Employee
- Delete Employee
- PostgreSQL Database
- Spring Data JPA
- REST APIs
- Maven Build
- Layered Architecture

---

# Project Structure

```
employee-service
│
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/
│   │   │       └── company/
│   │   │           └── employee_service/
│   │   │
│   │   │               ├── controller/
│   │   │               │     └── EmployeeController.java
│   │   │               │
│   │   │               ├── entity/
│   │   │               │     └── Employee.java
│   │   │               │
│   │   │               ├── exception/
│   │   │               │     └── ResourceNotFoundException.java
│   │   │               │
│   │   │               ├── repository/
│   │   │               │     └── EmployeeRepository.java
│   │   │               │
│   │   │               ├── service/
│   │   │               │     └── EmployeeService.java
│   │   │               │
│   │   │               └── EmployeeServiceApplication.java
│   │   │
│   │   └── resources/
│   │         └── application.properties
│   │
│   └── test/
│       └── java/
│
├── target/
│
├── .gitattributes
├── .gitignore
├── HELP.md
├── mvnw
├── mvnw.cmd
├── pom.xml
└── README.md
```

---

# Prerequisites

Install the following software before starting.

- Java 17
- Maven
- IntelliJ IDEA
- PostgreSQL
- Git
- Postman

Verify installation.

## Java

```bash
java -version
```

Expected Output

```
openjdk version "17"
```

---

## Maven

```bash
mvn -version
```

---

## PostgreSQL

```bash
psql --version
```

---

# Clone Project

```bash
git clone https://github.com/manjunath031984/enterprise-employee-service.git
```

Open the project.

```bash
cd enterprise-employee-service
```

---

# PostgreSQL Installation

Install PostgreSQL.

During installation remember

```
Username : postgres
Password : your_password
Port : 5432
```

---

# Create Database

Login into PostgreSQL.

```sql
CREATE DATABASE employee_db;
```

Verify

```sql
\l
```

Connect

```sql
\c employee_db
```

---

# Configure Spring Boot

Open

```
src/main/resources/application.properties
```

Add

```properties
spring.application.name=employee-service

server.port=8080

spring.datasource.url=jdbc:postgresql://localhost:5432/employee_db
spring.datasource.username=postgres
spring.datasource.password=your_password

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true

spring.jpa.properties.hibernate.format_sql=true
spring.jpa.database-platform=org.hibernate.dialect.PostgreSQLDialect
```

---

# Build Project

Using Maven

```bash
mvn clean install
```

---

# Run Application

```bash
mvn spring-boot:run
```

OR

Run

```
EmployeeServiceApplication.java
```

from IntelliJ.

---

# Verify Application

Open browser

```
http://localhost:8080
```

If no root endpoint is configured, this may return a 404 response, which is expected.

---

# REST APIs

## Create Employee

POST

```
http://localhost:8080/api/employees
```

Request Body

```json
{
    "name":"John",
    "department":"Cloud",
    "salary":90000
}
```

---

## Get All Employees

GET

```
http://localhost:8080/api/employees
```

---

## Get Employee By Id

GET

```
http://localhost:8080/api/employees/1
```

---

## Update Employee

PUT

```
http://localhost:8080/api/employees/1
```

Body

```json
{
    "name":"John Smith",
    "department":"DevOps",
    "salary":120000
}
```

---

## Delete Employee

DELETE

```
http://localhost:8080/api/employees/1
```

---

# Expected Response

```json
{
    "id":1,
    "name":"John",
    "department":"Cloud",
    "salary":90000
}
```

---

# Build Project

```bash
mvn clean package
```

Jar location

```
target/
```

Run jar

```bash
java -jar target/employee-service-0.0.1-SNAPSHOT.jar
```

---

# Common Maven Commands

Clean

```bash
mvn clean
```

Compile

```bash
mvn compile
```

Test

```bash
mvn test
```

Package

```bash
mvn package
```

Install

```bash
mvn install
```

---

# Database Table

If using

```
spring.jpa.hibernate.ddl-auto=update
```

Hibernate automatically creates

```
employees
```

table.

Verify

```sql
SELECT * FROM employees;
```

---

# Common Errors

## PostgreSQL Connection Refused

Check

- PostgreSQL service is running
- Port is 5432

---

## Authentication Failed

Verify

```
spring.datasource.username

spring.datasource.password
```

---

## Port Already In Use

Change

```properties
server.port=8081
```

---

## Maven Dependency Error

Refresh Maven

```
Reload Maven Project
```

---

## Java Version Error

Verify

```bash
java -version
```

Must be Java 17.

---

# Future Improvements

- DTO Layer
- Global Exception Handling
- Validation
- Swagger/OpenAPI
- Logging
- Docker
- Docker Compose
- Unit Testing
- Integration Testing
- Spring Security
- JWT Authentication
- Pagination
- Sorting
- Search API
- Flyway Database Migration
- Microservices
- API Gateway
- Eureka Server
- Config Server
- OpenFeign

---

# Learning Objectives

After completing this project you will understand

- Spring Boot Basics
- REST API Development
- Controller Layer
- Service Layer
- Repository Layer
- Entity Mapping
- PostgreSQL Integration
- Spring Data JPA
- Hibernate
- Maven Build Lifecycle
- CRUD Operations

---

# License

This project is for educational purposes.