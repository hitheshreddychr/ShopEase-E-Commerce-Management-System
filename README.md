# ShopEase – Microservices-Based E-Commerce Management System

## Project Overview

ShopEase is a backend e-commerce management system developed using **Python and FastAPI**, following a microservices architecture.

The project is designed to divide e-commerce functionality into independent services, where each microservice handles a specific business responsibility. Each service maintains its own application structure, dependencies, configuration, and deployment setup.

The system is being developed incrementally as part of the ShopEase backend development project.

## Microservices Architecture

The project currently contains the following independent microservices:

### 1. Product Management Service

**Location:** `product-service/`

Responsible for managing product information and inventory-related operations.

**Technology Stack:**
- Python 3.11+
- FastAPI
- Uvicorn
- Pydantic
- In-memory data storage
- Docker

**Core Features:**
- Create new products.
- Retrieve all available products.
- Retrieve individual products using product IDs.
- Update existing product information.
- Delete products.
- Filter products by category.
- Support pagination.
- Validate incoming product data.
- Handle API exceptions.

### 2. Authentication Service

**Location:** `auth-service/`

Responsible for user registration, authentication, password security, and JWT-based access control.

**Technology Stack:**
- Python
- FastAPI
- MySQL 8.0
- SQLAlchemy
- Alembic
- PyJWT
- Argon2 Password Hashing
- Pydantic
- Docker
- Docker Compose

**Core Features:**
- User registration.
- Email validation.
- Secure password hashing.
- User login.
- JWT access token generation.
- JWT token verification.
- Authenticated user profile retrieval.
- Protected API endpoints.
- Password change functionality.
- MySQL database integration.
- Database schema migrations using Alembic.

## Project Structure

```text
ShopEase/
│
├── product-service/
│   ├── app/
│   │   ├── config/
│   │   ├── models/
│   │   ├── routers/
│   │   ├── schemas/
│   │   ├── services/
│   │   └── main.py
│   │
│   ├── Dockerfile
│   ├── .dockerignore
│   ├── docker-compose.yml
│   ├── requirements.txt
│   └── README.md
│
├── auth-service/
│   ├── app/
│   │   ├── core/
│   │   ├── database/
│   │   ├── models/
│   │   ├── routers/
│   │   ├── schemas/
│   │   ├── services/
│   │   └── main.py
│   │
│   ├── alembic/
│   │   └── versions/
│   │
│   ├── alembic.ini
│   ├── Dockerfile
│   ├── .dockerignore
│   ├── docker-compose.yml
│   ├── requirements.txt
│   └── README.md
│
├── .gitignore
└── README.md
```

## Architecture and Design Principles

The project follows these development principles:

- **Microservices Architecture:** Each service operates independently and handles a specific business responsibility.
- **Separation of Concerns:** API routing, request validation, business logic, data models, and configuration are maintained separately.
- **Independent Deployment:** Each microservice has its own Docker configuration.
- **Secure Authentication:** Passwords are stored as secure hashes, and JWT tokens are used for authentication.
- **Database Isolation:** The Authentication Service uses its own MySQL database.
- **API Documentation:** FastAPI automatically generates interactive Swagger documentation.

## Service Configuration

| Microservice | Application Port | Storage |
|---|---:|---|
| Product Service | 8003 | In-memory |
| Authentication Service | 8002 | MySQL 8.0 |

Each microservice is configured and executed independently.

## Running the Microservices

### Product Service

Navigate to the Product Service directory:

```bash
cd product-service
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Start the application locally:

```bash
uvicorn app.main:app --reload --port 8003
```

Run using Docker Compose:

```bash
docker compose up -d --build
```

Swagger documentation:

`http://localhost:8003/docs`

### Authentication Service

Navigate to the Authentication Service directory:

```bash
cd auth-service
```

Configure the required environment variables in the `.env` file.

Install dependencies:

```bash
pip install -r requirements.txt
```

Start the application and MySQL database using Docker Compose:

```bash
docker compose up -d --build
```

Swagger documentation:

`http://localhost:8002/docs`

## API Documentation

Both microservices provide interactive API documentation through FastAPI Swagger UI.

| Service | Swagger Documentation |
|---|---|
| Product Service | `http://localhost:8003/docs` |
| Authentication Service | `http://localhost:8002/docs` |

## Security and Configuration

- Database credentials and JWT secrets are maintained in environment variables.
- Environment files are excluded from Git version control.
- Passwords are never stored as plain text.
- JWT tokens have configurable expiration times.
- Protected authentication endpoints require valid access tokens.
- Docker build contexts exclude local environment files and unnecessary development files.

**Important:** Never commit `.env` files, database passwords, or JWT secrets to the repository.

## Development and Testing

The microservices are developed and tested independently using:

- FastAPI Swagger UI.
- REST API requests.
- Docker container execution.
- Docker Compose.
- MySQL database verification.
- Git and GitHub for version control.

## Project Development

ShopEase is being developed incrementally, with each assessment introducing additional backend functionality and microservices.

The current development scope includes:

1. Product Management Service.
2. Authentication Service.

Future microservices can be added as independent services while maintaining the existing architecture.

## Repository Structure

The repository contains the source code, service-specific configurations, Docker files, dependency definitions, and documentation required for the individual microservices.
