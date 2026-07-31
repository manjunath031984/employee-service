# Employee Service - Spring Boot REST API on Google Cloud Platform

A simple Spring Boot REST API deployed on **Google Cloud Compute Engine** and connected to **Google Cloud SQL (PostgreSQL)**.

---

# Architecture

```
                    Internet
                        │
                        │
                +----------------+
                | Browser/Postman|
                +--------+-------+
                         |
                         |
                http://VM-IP:8080
                         |
                         |
        +--------------------------------+
        | Compute Engine VM              |
        | Ubuntu 26.04                   |
        | Java 17                        |
        | Maven                          |
        | Spring Boot REST API           |
        +---------------+----------------+
                        |
                        |
                JDBC (SSL)
                        |
                        |
        +--------------------------------+
        | Cloud SQL PostgreSQL           |
        | PostgreSQL 18                  |
        | Public IP                      |
        +--------------------------------+
```

---

# Technology Stack

| Technology | Version |
|------------|---------|
| Java | 17 |
| Spring Boot | 3.x |
| Maven | Latest |
| PostgreSQL | 18 |
| Google Cloud Compute Engine | Ubuntu 26.04 |
| Google Cloud SQL | PostgreSQL |
| Git | Latest |

---

# GCP Resources

## Project

```
Project ID:
gcp-dev-july-2026
```

---

## Compute Engine VM

```
VM Name:
employee-service-vm

Region:
us-central1

Zone:
us-central1-a

Operating System:
Ubuntu 26.04 LTS

Machine Type:
e2-micro
```

---

## Cloud SQL

```
Database Engine:
PostgreSQL

Version:
18

Instance Name:
employee-postgres-db
```

---

# Prerequisites

Install

- Java 17
- Maven
- Git

---

# Verify Java

```bash
java -version
```

Expected

```
openjdk version "17"
```

---

# Verify Maven

```bash
mvn -version
```

---

# Clone Repository

```bash
git clone https://github.com/<github-username>/employee-service.git
```

Go to project

```bash
cd employee-service
```

---

# Build Project

```bash
mvn clean package
```

Verify

```bash
ls target
```

Expected

```
employee-service-0.0.1-SNAPSHOT.jar
```

---

# Cloud SQL

Connect from VM

```bash
psql -h CLOUD_SQL_PUBLIC_IP \
     -U postgres \
     -d postgres
```

Example

```bash
psql -h 34.59.108.155 \
     -U postgres \
     -d postgres
```

---

# Create Database

```sql
CREATE DATABASE employee_db;
```

Connect

```sql
\c employee_db
```

Verify

```sql
\dt
```

Expected

```
Did not find any relations.
```

---

# Spring Boot Configuration

Edit

```
src/main/resources/application.properties
```

Example

```properties
spring.application.name=employee-service

server.port=8080

spring.datasource.url=jdbc:postgresql://34.59.108.155:5432/employee_db
spring.datasource.username=postgres
spring.datasource.password=YOUR_PASSWORD

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true

spring.jpa.database-platform=org.hibernate.dialect.PostgreSQLDialect
```

---

# Run Application

```bash
java -jar target/employee-service-0.0.1-SNAPSHOT.jar
```

Expected

```
Started EmployeeServiceApplication
Tomcat started on port(s): 8080
```

---

# Run in Background

```bash
nohup java -jar target/employee-service-0.0.1-SNAPSHOT.jar > app.log 2>&1 &
```

Check process

```bash
ps -ef | grep java
```

View logs

```bash
tail -f app.log
```

Stop application

```bash
pkill -f employee-service
```

---

# Verify Database

Connect

```bash
psql -h 34.59.108.155 \
-U postgres \
-d employee_db
```

List tables

```sql
\dt
```

Spring Boot should automatically create tables when

```
spring.jpa.hibernate.ddl-auto=update
```

is configured.

---

# Firewall Rules

Allow

| Port | Purpose |
|------|----------|
| 22 | SSH |
| 8080 | Spring Boot REST API |

Example

```
Name:
allow-http-8080

Direction:
Ingress

Protocols:
tcp:8080
```

---

# Test REST API

Health Check

```
http://VM_EXTERNAL_IP:8080
```

Example

```
http://34.xxx.xxx.xxx:8080
```

---

## Create Employee

POST

```
http://VM_EXTERNAL_IP:8080/api/employees
```

Body

```json
{
  "name":"John",
  "department":"Cloud",
  "salary":90000
}
```

---

## Get Employees

GET

```
http://VM_EXTERNAL_IP:8080/api/employees
```

---

## Get Employee

GET

```
http://VM_EXTERNAL_IP:8080/api/employees/1
```

---

## Update Employee

PUT

```
http://VM_EXTERNAL_IP:8080/api/employees/1
```

---

## Delete Employee

DELETE

```
http://VM_EXTERNAL_IP:8080/api/employees/1
```

---

# Useful Commands

Current Directory

```bash
pwd
```

List Files

```bash
ls -la
```

Build

```bash
mvn clean package
```

Run

```bash
java -jar target/employee-service-0.0.1-SNAPSHOT.jar
```

Run Background

```bash
nohup java -jar target/employee-service-0.0.1-SNAPSHOT.jar > app.log 2>&1 &
```

View Logs

```bash
tail -f app.log
```

Check Java

```bash
java -version
```

Check Maven

```bash
mvn -version
```

Check PostgreSQL

```bash
psql --version
```

Connect Database

```bash
psql -h 34.59.108.155 \
-U postgres \
-d employee_db
```

---

# Troubleshooting

## Database does not exist

```
FATAL:
database "employee_db" does not exist
```

Solution

```sql
CREATE DATABASE employee_db;
```

---

## Connection Timeout

Check

- Public IP enabled
- Authorized Network configured
- VM connectivity
- Cloud SQL instance is RUNNING

---

## Maven Error

```
No POM found
```

Go to project directory

```bash
cd employee-service
```

Verify

```bash
ls
```

Should contain

```
pom.xml
```

---

## Java Not Installed

```bash
sudo apt update

sudo apt install openjdk-17-jdk -y
```

---

# Future Improvements

- Docker
- Docker Compose
- Nginx Reverse Proxy
- HTTPS
- Cloud SQL Private IP
- Cloud SQL Auth Proxy
- CI/CD using GitHub Actions
- Jenkins Deployment
- Google Cloud Load Balancer
- Managed Instance Group
- Monitoring with Cloud Monitoring
- Logging with Cloud Logging

---

# License

This project is intended for learning and educational purposes.
