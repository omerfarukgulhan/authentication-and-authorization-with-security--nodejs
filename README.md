# authentication-and-authorization-with-security--nodejs

## Table of Contents

1. [Introduction](#introduction)
2. [Tech Stack](#tech-stack)
3. [Installation and Usage](#installation-and-usage)
4. [API Endpoints](#api-endpoints)

## Introduction

Welcome to my authentication and authorization backend application repository! This project is built using Node.js and Express, with a focus on adhering to solid and dry design principles to ensure robustness and maintainability.

Users can perform actions such as signing up, logging in, resetting forgotten passwords, updating their information, and even deleting their accounts. Additionally, administrators have special privileges, including the ability to delete users and view a list of all users.

To enhance security, passwords are encrypted using bcrypt, a widely recognized cryptographic hashing function. Authentication is managed through JSON Web Tokens (JWT), providing a secure and efficient mechanism for user authorization.

The application includes a robust email system for handling password reset requests, ensuring that users can securely regain access to their accounts if needed.

It also have functions such as filtering, sorting, field limiting, and pagination for listing users and can be implemented elsewhere.

With global error handling in place, the application ensures a smooth and reliable experience for all users, effectively managing and communicating errors to facilitate troubleshooting and resolution.

In summary, the authentication and authorization backend application combines the latest technologies and best practices to deliver a secure, efficient, and user-friendly experience for both administrators and end-users alike.

## Tech Stack

### Security

- bcryptjs: ^2.4.3
- express-mongo-sanitize: ^2.2.0
- helmet: ^7.1.0
- hpp: ^0.2.3
- jsonwebtoken: ^9.0.2
- xss-clean: ^0.1.4

### Dependencies

- dotenv: ^16.4.5
- express: ^4.18.2
- express-rate-limit: ^7.2.0
- mongodb: ^6.3.0
- mongoose: ^5.5.2
- morgan: ^1.10.0
- nodemailer: ^6.9.12
- slugify: ^1.6.6
- validator: ^10.11.0

## Installation and Usage

### Prerequisites

- Node.js version 18.17.1 or later
- MongoDB Atlas account or local MongoDB server running

### Installation

1. Clone the repository to your local machine:

```bash
git clone https://github.com/omerfarukgulhan/authentication-and-authorization-with-security--nodejs.git
```

2. Start the server:

```bash
cd server
npm install
npm run dev
```

After installation and starting the server app should start on http://localhost:3000/

## API Endpoints

### Authentication

- **Sign Up**

  - Method: POST
  - URL: `http://localhost:3000/api/v1/users/signup`
  - Body:
    ```json
    {
      "name": "test",
      "email": "test@test.com",
      "password": "pass1234",
      "passwordConfirm": "pass1234"
    }
    ```
  - Description: Registers a new user.

- **Login**

  - Method: POST
  - URL: `http://localhost:3000/api/v1/users/login`
  - Body:
    ```json
    {
      "email": "test@test.com",
      "password": "{{password}}"
    }
    ```
  - Description: Logs in an existing user.

- **Forgot Password**

  - Method: POST
  - URL: `http://localhost:3000/api/v1/users/forgotPassword`
  - Body:
    ```json
    {
      "email": "test@test.com"
    }
    ```
  - Description: Sends an email to reset the password for a user.

- **Reset Password**

  - Method: PATCH
  - URL: `http://localhost:3000/api/v1/users/resetPassword/:token`
  - Body:
    ```json
    {
      "password": "newpassword",
      "passwordConfirm": "newpassword"
    }
    ```
  - Description: Resets the password using the provided token.

- **Update Current User Password**
  - Method: PATCH
  - URL: `http://localhost:3000/api/v1/users/updateMyPassword`
  - Auth: Bearer Token
  - Body:
    ```json
    {
      "passwordCurrent": "pass1234",
      "password": "newpassword",
      "passwordConfirm": "newpassword"
    }
    ```
  - Description: Updates the password of the currently authenticated user.

### Users

- **Get All Users**

  - Method: GET
  - URL: `http://localhost:3000/api/v1/users?role=user`
  - Auth: Bearer Token
  - Description: Retrieves a list of all users with the role 'user'.

- **Get User**

  - Method: GET
  - URL: `http://localhost:3000/api/v1/users/:id`
  - Auth: Bearer Token
  - Description: Retrieves details of a specific user by ID.

- **Update User**

  - Method: PATCH
  - URL: `http://localhost:3000/api/v1/users/:id`
  - Auth: Bearer Token
  - Body:
    ```json
    {
      "name": "Administrator"
    }
    ```
  - Description: Updates user details.

- **Delete User**

  - Method: DELETE
  - URL: `http://localhost:3000/api/v1/users/:id`
  - Auth: Bearer Token
  - Description: Deletes a user by ID.

- **Get Current User**

  - Method: GET
  - URL: `http://localhost:3000/api/v1/users/me`
  - Auth: Bearer Token
  - Description: Retrieves details of the currently authenticated user.

- **Update Current User**

  - Method: PATCH
  - URL: `http://localhost:3000/api/v1/users/updateMe`
  - Auth: Bearer Token
  - Body:
    ```json
    {
      "name": "tester"
    }
    ```
  - Description: Updates details of the currently authenticated user.

- **Delete Current User**
  - Method: DELETE
  - URL: `http://localhost:3000/api/v1/users/deleteMe`
  - Auth: Bearer Token
  - Description: Deletes the currently authenticated user.
