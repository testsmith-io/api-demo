# Demo API with JWT Authentication and Swagger Documentation

A RESTful API built with Laravel for Demo purpose, secured with JSON Web Tokens (JWT) and documented using Swagger. This API uses a SQLite database for quick and easy development.

## Features

- **User Registration and Login**: Supports creating new users and authenticating them via JWT.
- **JWT Authentication**: Secures protected endpoints with JSON Web Tokens.
- **Swagger Documentation**: Generates interactive API documentation using OpenAPI with `darkaonline/l5-swagger`.

## Prerequisites

- PHP >= 7.4
- Composer
- SQLite

## Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/testsmith-io/demo-api.git
   cd demo-api
   ```

2. **Install dependencies**:
   ```bash
   composer install
   ```

3. **Run migrations**:
   ```bash
   php artisan migrate:fresh
   ```

## Packages Used

- **[tymon/jwt-auth](https://github.com/tymondesigns/jwt-auth)**: Handles JWT-based authentication.
- **[darkaonline/l5-swagger](https://github.com/DarkaOnLine/L5-Swagger)**: Generates Swagger documentation based on OpenAPI specification.

## Running the API

To start the Laravel development server, run:
```bash
php artisan serve
```

The API will be accessible at `http://localhost:8000`.

## Endpoints

### User Registration

- **URL**: `POST /api/register`
- **Description**: Registers a new user.
- **Request Body**:
  ```json
  {
    "name": "John Doe",
    "email": "johndoe@example.com",
    "password": "password123"
  }
  ```
- **Response**:
    - `201 Created`:
      ```json
      {
        "message": "User successfully registered"
      }
      ```
    - `422 Unprocessable Entity` (Validation errors):
      ```json
      {
        "name": ["The name field is required."],
        "email": ["The email has already been taken."]
      }
      ```

### User Login

- **URL**: `POST /api/login`
- **Description**: Authenticates a user and returns a JWT token.
- **Request Body**:
  ```json
  {
    "email": "johndoe@example.com",
    "password": "password123"
  }
  ```
- **Response**:
    - `200 OK`:
      ```json
      {
        "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
      }
      ```
    - `401 Unauthorized`:
      ```json
      {
        "error": "Unauthorized"
      }
      ```

## JWT Authentication

To access protected routes, include the JWT token in the Authorization header:
```
Authorization: Bearer <token>
```

### Example Protected Route (User List)

- **URL**: `GET /api/users`
- **Description**: Retrieves a list of users. Only accessible with a valid JWT token.

## Swagger Documentation

Swagger documentation is automatically generated for this API. To view it, go to:
```
http://localhost:8000/api/documentation
```

### Generating or Updating Swagger Documentation

If you make changes to the API and need to regenerate the Swagger docs:
```bash
php artisan l5-swagger:generate
```

## Project Structure

- **`app/Http/Controllers/UserController.php`**: Contains logic for user registration and login.
- **`app/Http/Requests/RegisterUserRequest.php`**: Handles validation for user registration.
- **`routes/api.php`**: Defines API routes for registration, login, and protected routes.
- **`config/l5-swagger.php`**: Swagger configuration for documentation generation.

## List all routes

If you want to list all available routes, use the following command:

```bash
php artisan route:list
```
