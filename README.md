# NestJS Clean Architecture API with Prisma & JWT Auth

A production-ready, highly-scalable, and maintainable NestJS backend service conforming to clean architecture standards.

## Tech Stack
* **Framework**: NestJS (v10)
* **Language**: TypeScript
* **Database & ORM**: PostgreSQL & Prisma ORM
* **Security & Auth**: Passport JWT, bcrypt (for password hashing)
* **Validation**: `class-validator`, `class-transformer`
* **Configuration**: `dotenv` via `@nestjs/config`

---

## Directory Structure
```text
src/
│
├── common/
│   ├── decorators/           # Custom decorators (e.g. @GetUser)
│   ├── filters/              # Global HttpExceptionFilter
│   ├── guards/               # JwtAuthGuard
│   ├── strategies/           # Passport JWT Strategy
│   └── utils/
│
├── config/                   # Configuration bindings
│
├── prisma/                   # Prisma service and global module
│
├── auth/                     # Authentication Module
│   ├── dto/                  # LoginDto, RegisterDto
│   ├── guards/
│   ├── strategies/
│   ├── auth.controller.ts
│   ├── auth.service.ts
│   └── auth.module.ts
│
├── users/                    # Users Module
│   ├── dto/                  # CreateUserDto
│   ├── entities/             # UserEntity
│   ├── users.controller.ts
│   ├── users.service.ts
│   └── users.module.ts
│
├── app.module.ts             # Root AppModule
└── main.ts                   # Application Entry point
```

---

## Installation & Setup

### 1. Install Dependencies
```bash
npm install
```

### 2. Configure Environment Variables
Copy `.env.example` into a new `.env` file and update your PostgreSQL credentials:
```bash
cp .env.example .env
```

Ensure the `DATABASE_URL` matches your local database settings. E.g.:
```env
DATABASE_URL="postgresql://postgres:postgres@localhost:5432/review_api?schema=public"
```

### 3. Generate Prisma Client and Run Database Migrations
Create your database and generate migrations using Prisma CLI:
```bash
npx prisma migrate dev --name init
```

This will run the migrations and generate the Prisma Client automatically.

---

## Running the Application

### Development mode
```bash
npm run start:dev
```

### Production mode
Build and run the compiled outputs:
```bash
npm run build
npm run start:prod
```

---

## API Testing Reference

All APIs are prefixed with `/api`.

### 1. Register a new user
* **Endpoint**: `POST /api/auth/register`
* **Request Body**:
  ```json
  {
    "fullName": "John Doe",
    "email": "john@gmail.com",
    "password": "12345678"
  }
  ```
* **Response (201 Created)**:
  ```json
  {
    "id": "a1b2c3d4-e5f6-7a8b-9c0d-1e2f3a4b5c6d",
    "email": "john@gmail.com",
    "fullName": "John Doe",
    "createdAt": "2026-07-10T12:00:00.000Z"
  }
  ```

### 2. Login
* **Endpoint**: `POST /api/auth/login`
* **Request Body**:
  ```json
  {
    "email": "john@gmail.com",
    "password": "12345678"
  }
  ```
* **Response (200 OK)**:
  ```json
  {
    "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "user": {
      "id": "a1b2c3d4-e5f6-7a8b-9c0d-1e2f3a4b5c6d",
      "email": "john@gmail.com",
      "fullName": "John Doe"
    }
  }
  ```

### 3. Retrieve User Profile (Authenticated)
* **Endpoint**: `GET /api/auth/profile`
* **Headers**: `Authorization: Bearer <your-access-token>`
* **Response (200 OK)**:
  ```json
  {
    "id": "a1b2c3d4-e5f6-7a8b-9c0d-1e2f3a4b5c6d",
    "email": "john@gmail.com",
    "fullName": "John Doe"
  }
  ```
# Review
# teamvipe-api
