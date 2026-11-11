# ShopEase – Microservices-Based E-Commerce Management System

## Project Overview

ShopEase is an enterprise-style backend e-commerce management system developed using **Python, FastAPI, MySQL, and Docker**, following a microservices architecture.

The project is designed to simulate a real-world e-commerce platform by dividing application functionality into independent microservices. Each service is responsible for a specific business domain and maintains its own application structure, business logic, configuration, and database where applicable.

The architecture promotes service independence, separation of concerns, database isolation, scalability, maintainability, and independent deployment.

The project covers the complete backend development lifecycle, including REST API development, database integration, authentication, authorization, service-level responsibilities, containerization, API testing, and version control.

## Microservices Architecture

The ShopEase project currently consists of three independent microservices.

### 1. Product Management Service

**Location:** `product-service/`

The Product Management Service handles product catalog and inventory-related operations.

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
- Support pagination using skip and limit.
- Validate incoming product information.
- Handle invalid requests and missing products.
- Return appropriate HTTP status codes.
- Interactive API documentation through Swagger UI.

**REST API Endpoints:**

| Method | Endpoint | Description |
|---|---|---|
| POST | `/api/products/` | Create a product |
| GET | `/api/products/` | Retrieve all products |
| GET | `/api/products/{product_id}` | Retrieve a product |
| PUT | `/api/products/{product_id}` | Update a product |
| DELETE | `/api/products/{product_id}` | Delete a product |

**Storage:** In-memory Python data structure.

The Product Service operates independently and does not use MySQL for this assessment.

### 2. Authentication Service

**Location:** `auth-service/`

The Authentication Service manages user registration, login, password security, and JWT-based authentication.

**Technology Stack:**
- Python
- FastAPI
- MySQL 8.0
- SQLAlchemy ORM
- Alembic
- PyJWT
- Argon2 Password Hashing
- Pydantic
- Docker
- Docker Compose

**Core Features:**
- User registration.
- Email format validation.
- Password strength validation.
- Secure password hashing using Argon2.
- Duplicate email prevention.
- User login and credential verification.
- JWT access token generation.
- JWT signature and expiration validation.
- Authenticated user profile retrieval.
- Protected API endpoints.
- Access token verification.
- Password change functionality.
- Inactive account login prevention.
- MySQL database integration.
- Database schema migrations using Alembic.
- Dedicated MySQL container with persistent storage.

**REST API Endpoints:**

| Method | Endpoint | Description |
|---|---|---|
| POST | `/api/auth/register` | Register a new user |
| POST | `/api/auth/login` | Authenticate a user |
| GET | `/api/auth/me` | Retrieve authenticated user details |
| POST | `/api/auth/verify-token` | Verify an access token |
| POST | `/api/auth/change-password` | Change the authenticated user's password |

**Database:** `shopease_auth_db`

The Authentication Service maintains ownership of user credentials, password hashes, account authentication, and JWT generation.

### 3. User Management Service

**Location:** `user-service/`

The User Management Service handles customer profile management, contact information, delivery addresses, and account-related operations.

It integrates with the Authentication Service through JWT-based authentication to identify users and enforce user-level access restrictions.

**Technology Stack:**
- Python
- FastAPI
- MySQL 8.0
- SQLAlchemy ORM
- Alembic
- Pydantic
- JWT Authentication
- Docker
- Docker Compose

**Core Features:**

**User Profile Management**
- Create customer profiles.
- Retrieve the authenticated user's profile.
- Update existing profile information.
- Partially update profile information.
- Delete user profiles.
- Prevent duplicate profiles.
- Validate contact information.
- Identify users through authenticated JWT claims.

**Address Management**
- Add delivery addresses.
- Retrieve all saved addresses.
- Retrieve individual addresses.
- Update existing addresses.
- Delete saved addresses.
- Set a default delivery address.
- Automatically remove the previous default address when another address is selected.
- Maintain only one default address per user.
- Enforce address ownership.

**Account Management and Security**
- Integrate with the Authentication Service.
- Validate JWT access tokens.
- Extract authenticated user information.
- Prevent unauthorized profile access.
- Prevent users from accessing another user's addresses.
- Handle missing and invalid authentication tokens.
- Support account deactivation functionality.
- Maintain separation between authentication credentials and user profile information.

**User Profile REST API Endpoints:**

| Method | Endpoint | Description |
|---|---|---|
| POST | `/api/users/profile` | Create user profile |
| GET | `/api/users/profile` | Retrieve current user's profile |
| PUT | `/api/users/profile` | Update user profile |
| PATCH | `/api/users/profile` | Partially update user profile |
| DELETE | `/api/users/profile` | Delete user profile |

**Address Management REST API Endpoints:**

| Method | Endpoint | Description |
|---|---|---|
| POST | `/api/users/addresses` | Add a new address |
| GET | `/api/users/addresses` | Retrieve all saved addresses |
| GET | `/api/users/addresses/{address_id}` | Retrieve a specific address |
| PUT | `/api/users/addresses/{address_id}` | Update an address |
| DELETE | `/api/users/addresses/{address_id}` | Delete an address |
| PATCH | `/api/users/addresses/{address_id}/default` | Set default delivery address |

**Database:** `shopease_user_db`

The User Management Service maintains its own database for customer profiles and delivery addresses. Authentication credentials remain exclusively managed by the Authentication Service.

## Overall Project Structure

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
├── user-service/
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

Each microservice maintains its own application components, dependencies, environment configuration, database configuration where applicable, and Docker deployment files.

## Architecture and Design Principles

The project follows the following architectural principles:

### 1. Microservices Architecture
Each microservice handles an independent business responsibility and can be developed, maintained, and deployed separately.

### 2. Separation of Concerns
API routing, request validation, business logic, database operations, security functions, and configuration are maintained in separate components.

### 3. Independent Database Ownership
Each database-backed microservice owns its data.

- Authentication Service owns authentication credentials and account information.
- User Management Service owns customer profiles and delivery addresses.
- Product Service uses in-memory storage for product information in its assigned implementation.

Services should access another service's information through its APIs rather than directly accessing another service's database.

### 4. JWT-Based Authentication
The Authentication Service generates JWT access tokens after successful login. Protected services validate the token and use its authenticated identity to authorize requests.

### 5. RESTful API Design
The microservices use HTTP methods such as GET, POST, PUT, PATCH, and DELETE to perform operations through structured JSON requests and responses.

### 6. Independent Containerization
Each microservice has its own Docker configuration and can be executed independently.

### 7. Database Migrations
SQLAlchemy ORM and Alembic are used for database models, schema management, and database migrations in the MySQL-backed services.

### 8. API Documentation
FastAPI automatically generates interactive Swagger UI documentation for testing and exploring API endpoints.

## Service Configuration

| Microservice | Application Port | Storage |
|---|---:|---|
| Product Service | 8003 | In-memory |
| Authentication Service | 8002 | MySQL 8.0 |
| User Management Service | Configured through service settings | MySQL 8.0 |

Each service maintains its own deployment configuration.

## Application Workflow

The ShopEase backend is designed around the following e-commerce workflow:

1. A customer registers through the Authentication Service.
2. The customer logs in using registered credentials.
3. The Authentication Service validates the credentials and generates a JWT access token.
4. The customer uses the JWT token to access protected services.
5. The customer creates and manages their profile through the User Management Service.
6. The customer adds and manages delivery addresses.
7. The customer browses available products through the Product Service.
8. Product information is retrieved through REST APIs.
9. The authenticated user's identity is used to enforce access control in protected operations.

**Conceptual Architecture:**

```text
                    CLIENT APPLICATION
                            |
                            |
                   AUTHENTICATION SERVICE
                            |
                       JWT ACCESS TOKEN
                            |
             +--------------+--------------+
             |                             |
             v                             v
       USER SERVICE                  PRODUCT SERVICE
             |                             |
             v                             v
      USER DATABASE                 IN-MEMORY STORAGE
             |
             |
      USER PROFILES
      USER ADDRESSES
```

The architecture can be extended with additional services such as Order Management, Payment Management, and an API Gateway.

## Running the Microservices

Each microservice can be started independently from its respective directory.

### Product Service

Navigate to the Product Service directory:

```bash
cd product-service
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Run locally:

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

Start the Authentication Service and MySQL database:

```bash
docker compose up -d --build
```

Check running containers:

```bash
docker compose ps
```

View application logs:

```bash
docker compose logs auth-service
```

Swagger documentation:

`http://localhost:8002/docs`

### User Management Service

Navigate to the User Management Service directory:

```bash
cd user-service
```

Configure the required environment variables in the `.env` file, including database connectivity and Authentication Service integration settings.

Install dependencies:

```bash
pip install -r requirements.txt
```

Start the User Management Service and its MySQL database:

```bash
docker compose up -d --build
```

Check running containers:

```bash
docker compose ps
```

View application logs:

```bash
docker compose logs
```

Open the Swagger documentation using the application port configured for the User Management Service.

## Database Management

The project uses independent database ownership for its MySQL-backed microservices.

| Database | Owner | Purpose |
|---|---|---|
| `shopease_auth_db` | Authentication Service | User credentials and authentication |
| `shopease_user_db` | User Management Service | Customer profiles and addresses |

**Database Technologies:**
- MySQL 8.0
- SQLAlchemy ORM
- Alembic migrations
- Independent database connections
- Reusable database session management
- Persistent Docker volumes

Database credentials and connection URLs are configured using environment variables.

## Security and Configuration

Security is an important part of the ShopEase backend architecture.

The project implements:

- Secure password hashing using Argon2.
- JWT-based access authentication.
- Token signature and expiration validation.
- Protected API endpoints.
- User-level authorization.
- Email and request validation.
- Environment-based configuration.
- Separation of authentication credentials and profile information.
- Docker configuration that excludes local environment files.
- Independent database ownership.

**Important:** Environment files containing database credentials and JWT secrets must never be committed to GitHub or included in Docker images.

## API Documentation and Testing

FastAPI provides interactive Swagger UI documentation for each microservice.

| Microservice | Swagger UI |
|---|---|
| Product Service | `http://localhost:8003/docs` |
| Authentication Service | `http://localhost:8002/docs` |
| User Management Service | Available through its configured application port at `/docs` |

The APIs can be tested using:

- FastAPI Swagger UI.
- Postman.
- REST API requests.
- Docker container logs.
- MySQL database verification.

Testing covers successful operations, invalid requests, missing resources, authentication failures, authorization restrictions, and appropriate HTTP status codes.

## Docker and Containerization

Each microservice includes its own Docker configuration.

Docker is used to:

- Package application code and dependencies.
- Build independent Docker images.
- Execute services in isolated containers.
- Map application ports.
- Configure environment variables.
- Inspect application logs.
- Manage service containers.

Docker Compose is used for the MySQL-backed services to coordinate application containers and their respective database containers.

Persistent named volumes are configured for database storage.

## Technology Stack

| Category | Technologies |
|---|---|
| Programming Language | Python |
| Backend Framework | FastAPI |
| ASGI Server | Uvicorn |
| Data Validation | Pydantic |
| Database | MySQL 8.0 |
| ORM | SQLAlchemy |
| Database Migrations | Alembic |
| Authentication | JWT |
| Password Security | Argon2 |
| API Communication | REST APIs |
| API Documentation | Swagger UI |
| API Testing | Postman |
| Containerization | Docker |
| Container Orchestration | Docker Compose |
| Version Control | Git |
| Repository Hosting | GitHub |

## Development and Version Control

The project is maintained using Git and GitHub.

Development practices include:

- Independent microservice development.
- Organized project structures.
- Service-specific dependency management.
- Meaningful Git commit messages.
- Environment secret protection.
- Updated README documentation.
- Independent API testing.
- Docker-based application execution.

## Project Completion

The current ShopEase implementation covers three core microservices:

1. Product Management Service.
2. Authentication Service.
3. User Management Service.

Together, these services establish the foundation of a microservices-based e-commerce backend with product management, secure user authentication, customer profile management, delivery address management, REST API communication, independent database ownership, and Docker-based deployment.
