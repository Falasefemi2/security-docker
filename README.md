# Security Docker - Spring Boot JWT Authentication Example

This project is a Spring Boot application demonstrating a secure REST API with JWT (JSON Web Token) based authentication and authorization. It provides endpoints for user registration, authentication, and a protected demo resource.

## Table of Contents
- [Features](#features)
- [Technologies Used](#technologies-used)
- [Prerequisites](#prerequisites)
- [Getting Started](#getting-started)
  - [Clone the Repository](#clone-the-repository)
  - [Build the Project](#build-the-project)
  - [Run the Application](#run-the-application)
- [API Endpoints](#api-endpoints)
  - [Authentication](#authentication)
  - [Protected Resource](#protected-resource)
- [Project Structure](#project-structure)
- [Contributing](#contributing)
- [License](#license)

## Features
- User Registration: Allows new users to sign up.
- User Authentication: Authenticates existing users and issues JWTs.
- JWT-based Authorization: Secures API endpoints using JWTs.
- Role-based Access Control: Demonstrates basic role management (e.g., `USER` role).
- H2 Database: In-memory database for development and testing.
- RESTful API: Clean and well-structured API endpoints.

## Technologies Used
- **Java 24+**: The core programming language.
- **Spring Boot 3.x**: Framework for building the application.
- **Spring Security**: For authentication and authorization.
- **JJWT (Java JWT)**: Library for handling JSON Web Tokens.
- **Maven**: Dependency management and build automation.
- **H2 Database**: In-memory relational database.

## Prerequisites
Before you begin, ensure you have the following installed:
- [Java Development Kit (JDK) 17 or higher](https://www.oracle.com/java/technologies/downloads/)
- [Apache Maven 3.x](https://maven.apache.org/download.cgi)

## Getting Started

### Clone the Repository
```bash
git clone https://github.com/Falasefemi2/security-docker.git
cd security-docker
```

### Build the Project
Use Maven to build the project:
```bash
mvn clean install
```

### Run the Application
You can run the Spring Boot application using Maven:
```bash
mvn spring-boot:run
```
The application will start on `http://localhost:8080` by default.

## API Endpoints

The application exposes the following REST endpoints:

### Authentication

#### 1. Register a New User
- **URL:** `/api/v1/auth/register`
- **Method:** `POST`
- **Content-Type:** `application/json`
- **Request Body Example:**
  ```json
  {
    "firstname": "John",
    "lastname": "Doe",
    "email": "john.doe@example.com",
    "password": "password123",
    "role": "USER"
  }
  ```
- **Success Response:**
  ```json
  {
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
  }
  ```

#### 2. Authenticate User
- **URL:** `/api/v1/auth/authenticate`
- **Method:** `POST`
- **Content-Type:** `application/json`
- **Request Body Example:**
  ```json
  {
    "email": "john.doe@example.com",
    "password": "password123"
  }
  ```
- **Success Response:**
  ```json
  {
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
  }
  ```

### Protected Resource

#### 1. Access Demo Endpoint
- **URL:** `/api/v1/demo`
- **Method:** `GET`
- **Headers:**
  - `Authorization: Bearer <YOUR_JWT_TOKEN>`
- **Success Response:**
  ```json
  "Hello from secured endpoint"
  ```
- **Error Response (if token is missing or invalid):**
  ```json
  {
    "timestamp": "...",
    "status": 403,
    "error": "Forbidden",
    "message": "Access Denied",
    "path": "/api/v1/demo"
  }
  ```

You can use the `.http` files in the `httprequests/` directory (e.g., `authenticate.http`, `register.http`, `demo.http`) with an IDE extension like "REST Client" (for VS Code) to easily test these endpoints.

## Project Structure

```
security-docker/
├───.mvn/                     # Maven wrapper files
├───httprequests/             # Example HTTP request files for testing
├───src/
│   ├───main/
│   │   ├───java/
│   │   │   └───com/
│   │   │       └───femi/
│   │   │           └───securitydocker/
│   │   │               ├───SecurityDockerApplication.java # Main application class
│   │   │               ├───config/                  # Spring Security and JWT configuration
│   │   │               ├───controller/              # REST API controllers
│   │   │               ├───dto/                     # Data Transfer Objects for requests/responses
│   │   │               ├───enumfolder/              # Enum definitions (e.g., Role)
│   │   │               ├───model/                   # JPA Entities (e.g., User)
│   │   │               ├───Repository/              # Spring Data JPA repositories
│   │   │               └───service/                 # Business logic and JWT service
│   │   └───resources/
│   │       ├───application.yml      # Application configuration (e.g., server port, H2 console)
│   │       ├───static/              # Static web resources
│   │       └───templates/           # Thymeleaf templates (if any)
│   └───test/                     # Unit and integration tests
├───pom.xml                   # Maven Project Object Model
└───README.md                 # This file
```

## Contributing
Contributions are welcome! Please feel free to fork the repository, create a new branch, and submit a pull request.

## License
This project is open-source and available under the [MIT License](https://opensource.org/licenses/MIT).
