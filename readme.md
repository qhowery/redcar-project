Below is an example README in Markdown that documents everything we have so far:

# Company Question Answering Project

This project is a full-stack application that allows users to ask questions about companies and receive real-time answers generated via the OpenAI API. It features JWT-based authentication (login and registration), a protected question endpoint, and real-time streaming of answer updates using Socket.IO.

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Technologies](#technologies)
- [Setup Instructions](#setup-instructions)
  - [Backend Setup](#backend-setup)
  - [Frontend Setup](#frontend-setup)
  - [Environment Variables](#environment-variables)
- [API Endpoints](#api-endpoints)
  - [User Registration](#user-registration)
  - [User Login](#user-login)
  - [Ask Question (Protected)](#ask-question-protected)
- [Real-Time Streaming](#real-time-streaming)
- [Testing](#testing)
- [Future Enhancements](#future-enhancements)
- [Deployment](#deployment)
- [License](#license)
- [Contact](#contact)

## Overview

This application provides a seamless experience where:
- Users can **register** and **login** to obtain a JWT.
- Authenticated users can submit questions to the `/ask` endpoint.
- The backend processes the question via the OpenAI API and streams answer updates in real time.
- The frontend displays the question, streaming updates, and the final answer.

## Features

- **JWT Authentication:** Secure login and registration with token-based access.
- **Protected Endpoints:** Only authenticated users can access the question endpoint.
- **Real-Time Streaming:** Uses Socket.IO to stream interim updates and final responses.
- **User-Friendly UI:** Built with React to provide login, registration, and interactive question submission.
- **Automated Testing:** Unit and e2e tests for authentication and protected routes.

## Technologies

- **Backend:** NestJS, TypeScript, Axios, Socket.IO, JWT, Passport
- **Frontend:** React, TypeScript, Socket.IO-client
- **Testing:** Jest, Supertest

## Setup Instructions

### Backend Setup

1. **Navigate to the backend folder:**
   ```bash
   cd backend
   ```
2. **Install dependencies:**
   ```bash
   npm install
   ```
3. **Configure environment variables:**
   Create a `.env` file in the `backend` folder with:
   ```
   JWT_SECRET=your_jwt_secret
   OPENAI_API_KEY=your_openai_api_key
   ```
4. **Start the backend server in development mode:**
   ```bash
   npm run start:dev
   ```

### Frontend Setup

1. **Navigate to the frontend folder:**
   ```bash
   cd ../frontend
   ```
2. **Install dependencies:**
   ```bash
   npm install
   ```
3. **Start the React development server:**
   ```bash
   npm start
   ```
   The app should open in your browser (typically at [http://localhost:3000](http://localhost:3000), or another port if there is a conflict).

### Environment Variables

- **JWT_SECRET:** A secret key used to sign JWT tokens.
- **OPENAI_API_KEY:** Your API key for accessing the OpenAI API.

Make sure these are securely set, especially in production.

## API Endpoints

### User Registration

- **Endpoint:** `POST /auth/register` (or `/api/auth/register` if a global prefix is used)
- **Description:** Registers a new user.
- **Request Body:**
  ```json
  {
    "username": "newuser",
    "password": "newpassword"
  }
  ```
- **Response:**
  ```json
  {
    "message": "Registration successful"
  }
  ```

### User Login

- **Endpoint:** `POST /auth/login` (or `/api/auth/login`)
- **Description:** Logs in a user and returns a JWT token.
- **Request Body:**
  ```json
  {
    "username": "test",
    "password": "password"
  }
  ```
- **Response:**
  ```json
  {
    "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
  }
  ```

### Ask Question (Protected)

- **Endpoint:** `POST /ask` (or `/api/ask`)
- **Description:** Submits a question to generate an answer. Requires a valid JWT in the `Authorization` header.
- **Request Body:**
  ```json
  {
    "question": "Is redcar.io a B2B company?"
  }
  ```
- **Response:** The generated answer (streamed in real time via Socket.IO).

## Real-Time Streaming

The backend uses Socket.IO to send real-time updates. When a question is submitted:
- The backend initially emits a "Processing" message.
- It then streams answer chunks (using true streaming or a simulated approach) as they are generated.
- The frontend listens for `serverMessage` events and displays these updates.

## Testing

### Running Tests

From the backend folder, you can run:
- **Unit and Integration Tests:**
  ```bash
  npm run test
  ```
- **Generate Coverage Report:**
  ```bash
  npm run test:cov
  ```
- **End-to-End (E2E) Tests:**
  ```bash
  npm run test:e2e
  ```

### What to Test

- **AuthService:** Validate that user credentials are checked properly and that tokens are generated.
- **Authentication Flow:** E2E tests to simulate a login flow and then accessing protected endpoints.
- **Error Scenarios:** Test invalid credentials, duplicate registration, expired tokens, etc.

## Future Enhancements

- **Persistent Database Integration:** Replace the in-memory user store with a real database and hash passwords securely.
- **Role-Based Access Control:** Implement roles and guards to manage different access levels.
- **Improved Streaming:** Enhance real-time streaming by processing API response streams directly.
- **UI/UX Improvements:** Refine the frontend with advanced styling and user feedback.
- **CI/CD Pipeline:** Set up automated testing and deployment workflows.

## Deployment

- **Environment Variables:** Ensure that production secrets (JWT secret, API keys, database credentials) are managed securely.
- **Platforms:** Consider deploying the backend to Heroku, AWS, or similar and the frontend to Vercel, Netlify, etc.
- **Update URLs:** Adjust API URLs in the frontend for production.

## Contact

For questions or support, please contact [Quonlee Howery] at [qhowery@princeton.edu].
