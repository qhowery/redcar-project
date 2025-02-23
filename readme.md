
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

---

## Overview

This application provides a seamless experience where:
- Users can **register** and **login** using JWT-based authentication.
- Authenticated users can submit questions to the `/ask` endpoint.
- The backend processes the question via the OpenAI API and streams answer updates in real time.
- The frontend displays the question, streaming updates, and the final answer.

### Deployment:
- **Backend:** Hosted on [Railway](https://railway.app/)  
- **Database:** Managed using [Neon PostgreSQL](https://neon.tech/)  
- **Frontend:** Deployed via [Vercel](https://vercel.com/)  

---

## Features

- **JWT Authentication:** Secure authentication system using Railway-hosted backend and Neon PostgreSQL.
- **Protected Endpoints:** Only authenticated users can access the question endpoint.
- **Real-Time Streaming:** Uses Socket.IO to stream interim updates and final responses.
- **Vercel Deployment:** Frontend is hosted on Vercel with static build optimizations.
- **Enhanced Session Management:** Session expiration handling with automatic logout.
- **Automated Testing:** Unit and e2e tests for authentication and protected routes.

---

## Technologies

- **Backend:** NestJS, TypeScript, Axios, Socket.IO, JWT, Passport, PostgreSQL
- **Frontend:** React, TypeScript, Socket.IO-client
- **Deployment:** Railway (backend), Neon (PostgreSQL), Vercel (frontend)
- **Testing:** Jest, Supertest

---

## Setup Instructions

### Backend Setup

1. **Clone the repository:**
   ```bash
   git clone https://github.com/qhowery/redcar-project.git
   cd redcar-project/backend
   ```
2. **Install dependencies:**
   ```bash
   npm install
   ```
3. **Configure environment variables:**
   Create a `.env` file in the `backend` folder with:
   ```
   DATABASE_URL=your_neon_postgresql_database_url
   JWT_SECRET=your_jwt_secret
   OPENAI_API_KEY=your_openai_api_key
   ```
4. **Run database migrations:**
   ```bash
   npm run migration:run
   ```
5. **Start the backend server in development mode:**
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
   The app should open in your browser (typically at [http://localhost:3000](http://localhost:3000)).

### Environment Variables

- **DATABASE_URL:** Connection string for the PostgreSQL database (hosted on Neon).
- **JWT_SECRET:** A secret key used to sign JWT tokens.
- **OPENAI_API_KEY:** Your API key for accessing the OpenAI API.

---

## API Endpoints

### User Registration

- **Endpoint:** `POST /auth/register`
- **Description:** Registers a new user.
- **Request Body:**
  ```json
  {
    "email": "newuser@example.com",
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

- **Endpoint:** `POST /auth/login`
- **Description:** Logs in a user and returns a JWT token.
- **Request Body:**
  ```json
  {
    "email": "test@example.com",
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

- **Endpoint:** `POST /ask`
- **Description:** Submits a question to generate an answer. Requires a valid JWT in the `Authorization` header.
- **Request Body:**
  ```json
  {
    "question": "Is redcar.io a B2B company?"
  }
  ```
- **Response:** The generated answer (streamed in real time via Socket.IO).

---

## Real-Time Streaming

The backend uses Socket.IO to send real-time updates. When a question is submitted:
- The backend initially emits a "Processing" message.
- It then streams answer chunks as they are generated.
- The frontend listens for `serverMessage` events and displays these updates.

Additionally, the frontend fetches the latest server message every **5 seconds** to ensure smooth user experience.

---

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

- **Authentication Flow:** Verify login, logout, and session management.
- **Database Transactions:** Ensure PostgreSQL queries function correctly.
- **Streaming Messages:** Validate real-time updates via Socket.IO.
- **Error Handling:** Test invalid credentials, expired sessions, and API errors.

---

## Future Enhancements

- **Role-Based Access Control:** Implement admin and user roles with different permissions.
- **Improved Real-Time Features:** Enhance the streaming mechanism for smoother updates.
- **Analytics Dashboard:** Track question trends and usage statistics.
- **CI/CD Pipeline:** Set up automated testing and deployment workflows.
- **Improved UI/UX:** Optimize the frontend layout and design.

---

## Deployment

### Backend Deployment (Railway)

The backend is hosted on **Railway**. Deploy by running:
```bash
git push railway main
```
Ensure **DATABASE_URL** and **JWT_SECRET** are set in Railway environment variables.

### Database Setup (Neon PostgreSQL)

The database is hosted on **Neon**. You can manage migrations with:
```bash
npm run migration:run
```
Ensure the **DATABASE_URL** is configured properly.

### Frontend Deployment (Vercel)

The frontend is deployed on **Vercel** using the following build configuration:
```json
{
  "builds": [
    {
      "src": "frontend/package.json",
      "use": "@vercel/static-build",
      "config": {
        "distDir": "build"
      }
    }
  ]
}
```
Deploy with:
```bash
git push vercel main
```

---

## Contact

For questions or support, please contact [Quonlee Howery] at [qhowery@princeton.edu].
