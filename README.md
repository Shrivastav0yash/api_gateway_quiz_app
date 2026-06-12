# API Gateway Service

## Overview

The API Gateway is the single entry point for all client requests in the Quiz Application Microservices Architecture.

It routes incoming requests to the appropriate microservice using Spring Cloud Gateway and Eureka Service Discovery, eliminating the need for clients to communicate directly with individual services.

---

## Features

* Centralized request routing
* Eureka Service Discovery integration
* Load-balanced service communication
* Dynamic service resolution using service names
* Simplified client access to microservices
* Scalable microservice architecture support

---

## Tech Stack

* Java 22
* Spring Boot 4.1.0
* Spring Cloud Gateway MVC
* Spring Cloud Netflix Eureka Client
* Maven

---

## Architecture

```text
Client
   |
   v
+----------------+
|   API Gateway  |
|    Port 8765   |
+----------------+
       |
       +-------------------+
       |                   |
       v                   v

+---------------+   +---------------+
| Quiz Service  |   |Question Service|
|   Port 8090   |   |   Port 8080    |
+---------------+   +---------------+
```

---

## Service Registration

The API Gateway registers itself with Eureka Server and discovers all available services dynamically.

### Registered Services

* QUIZ-SERVICE
* QUESTION-SERVICE

---

## Routing Configuration

### Quiz Service

```yaml
- id: quiz-service
  uri: lb://QUIZ-SERVICE
  predicates:
    - Path=/quiz/**
```

### Question Service

```yaml
- id: question-service
  uri: lb://QUESTION-SERVICE
  predicates:
    - Path=/question/**
```

---

## API Examples

### Quiz Service APIs

#### Create Quiz

```http
POST /quiz/create
```

#### Get Quiz Questions

```http
GET /quiz/get/{id}
```

#### Submit Quiz

```http
POST /quiz/submit/{id}
```

---

### Question Service APIs

#### Get All Questions

```http
GET /question/allQuestions
```

#### Get Questions By Category

```http
GET /question/category/{category}
```

#### Add Question

```http
POST /question/add
```

---

## Eureka Configuration

```yaml
eureka:
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka
```

---

## Running the Project

### 1. Start Eureka Server

```bash
mvn spring-boot:run
```

Eureka Dashboard:

```text
http://localhost:8761
```

### 2. Start Question Service

```bash
mvn spring-boot:run
```

### 3. Start Quiz Service

```bash
mvn spring-boot:run
```

### 4. Start API Gateway

```bash
mvn spring-boot:run
```

---

## Gateway Endpoint

```text
http://localhost:8765
```

Example:

```text
http://localhost:8765/quiz/get/1
```

Instead of:

```text
http://localhost:8090/quiz/get/1
```

---

## Benefits of API Gateway

* Single entry point for all requests
* Reduced client complexity
* Dynamic service discovery
* Load balancing support
* Better scalability
* Improved maintainability
* Easier monitoring and security integration

---

## Future Enhancements

* JWT Authentication
* Role-Based Authorization
* Rate Limiting
* Circuit Breaker
* Distributed Tracing
* Centralized Logging
* API Documentation with OpenAPI/Swagger

---

## Author

Yash Shrivastav

GitHub:
https://github.com/Shrivastav0yash
