# Learning Management System Server

RESTful Node.js/Express backend for a Canvas-inspired learning management platform, using MongoDB and Mongoose to manage users, courses, modules, assignments, quizzes, enrollments, grades, files, announcements, and session-based authentication.

This repository contains the backend API for the Learning Management System client. It handles data persistence, authentication/session logic, course-related API routes, and communication between the React frontend and MongoDB database.

## Live System

The backend is deployed on Render and is consumed by the Netlify-hosted React frontend.

Frontend live demo:

[Open the Learning Management System](https://learning-management-system-rayan.netlify.app/)

The live app may take a few moments to load if the Render backend has been inactive and needs to wake up.

## Related Repository

This backend works with the frontend repository:

```text
learning-management-system-client
```

The frontend is built with React and communicates with this backend through REST API calls.

## Tech Stack

- Node.js
- Express.js
- MongoDB
- Mongoose
- Express Session
- CORS
- Multer / file upload handling
- dotenv
- Render deployment
- Netlify frontend integration

## System Role

This repository represents the backend layer of the full-stack learning management system.

```text
React Client
    ↓
Axios REST API Requests
    ↓
Node.js / Express Server
    ↓
Mongoose Models
    ↓
MongoDB Database
```

The backend is responsible for:

- Handling API requests from the React frontend
- Managing users and sessions
- Authenticating users
- Reading and writing course data
- Managing modules, lessons, assignments, quizzes, and results
- Handling enrollments
- Supporting file upload/download workflows
- Connecting the application to MongoDB

## Key Features

- RESTful Express API
- MongoDB database integration using Mongoose
- Session-based authentication
- CORS configuration for deployed Netlify frontend
- User signup, signin, profile, and signout routes
- Course management routes
- Module and lesson routes
- Assignment and assignment result routes
- Quiz, question, and quiz result routes
- Enrollment management
- Grade/result-related endpoints
- Announcement routes
- People/users routes
- File upload/download support
- Environment-based configuration for local and production deployment

## Environment Variables

Create a `.env` file in the root of the server project.

For local development:

```env
NODE_ENV=development
NETLIFY_URL=http://localhost:3000
SESSION_SECRET=your_session_secret_here
MONGO_CONNECTION_STRING=mongodb://localhost:27017/kanbas
PORT=4000
```

For production on Render:

```env
NODE_ENV=production
NETLIFY_URL=https://learning-management-system-rayan.netlify.app
SESSION_SECRET=your_production_session_secret
MONGO_CONNECTION_STRING=your_mongodb_atlas_connection_string
PORT=4000
```

Important: do not commit the real `.env` file to GitHub.

Use a `config.example.env` file to show the required variables without exposing secrets.

## Installation

Clone the repository:

```bash
git clone https://github.com/YOUR_USERNAME/learning-management-system-server.git
cd learning-management-system-server
```

Install dependencies:

```bash
npm install
```

Create a `.env` file:

```env
NODE_ENV=development
NETLIFY_URL=http://localhost:3000
SESSION_SECRET=your_session_secret_here
MONGO_CONNECTION_STRING=mongodb://localhost:27017/kanbas
PORT=4000
```

Start the server:

```bash
npm start
```

Or, if the project uses a development script:

```bash
npm run dev
```

The backend should run at:

```text
http://localhost:4000
```

## MongoDB Setup

The backend uses MongoDB through Mongoose.

For local development, you can use a local MongoDB connection:

```env
MONGO_CONNECTION_STRING=mongodb://localhost:27017/kanbas
```

For production deployment, use MongoDB Atlas:

```env
MONGO_CONNECTION_STRING=mongodb+srv://USERNAME:PASSWORD@cluster.mongodb.net/kanbas?retryWrites=true&w=majority
```

The database stores application data such as:

- Users
- Courses
- Enrollments
- Modules
- Lessons
- Assignments
- Assignment results
- Quizzes
- Quiz questions
- Quiz results
- Announcements
- Uploaded files

## CORS and Sessions

The backend is configured to allow requests from the frontend application.

For local development:

```env
NETLIFY_URL=http://localhost:3000
```

For production:

```env
NETLIFY_URL=https://learning-management-system-rayan.netlify.app
```

This is important because the frontend and backend are deployed separately. The React client runs on Netlify, while the Express API runs on Render.

Session-based authentication requires proper CORS and cookie configuration so the frontend can maintain authenticated user sessions across requests.

## Project Structure

```text
learning-management-system-server/
│
├── Kanbas/
│   ├── Account/
│   ├── Courses/
│   ├── Modules/
│   ├── Assignments/
│   ├── Quizzes/
│   ├── Grades/
│   ├── Enrollments/
│   ├── Announcements/
│   ├── People/
│   └── Files/
│
├── models/
│   └── Mongoose schema/model files
│
├── server.js
├── package.json
├── package-lock.json
├── config.example.env
├── .gitignore
└── README.md
```

Adjust the structure above if your actual folders are slightly different. The README should match the real repo exactly.

## Main Components

- `server.js` initializes the Express app, configures middleware, connects to MongoDB, enables CORS, configures sessions, and registers application routes.
- Account routes handle signup, signin, signout, profile, and session-based user authentication.
- Course routes handle course creation, retrieval, editing, and deletion.
- Module routes manage course modules and lessons.
- Assignment routes manage assignments, submissions, and assignment results.
- Quiz routes manage quizzes, questions, quiz-taking, and quiz results.
- Enrollment routes connect users to courses.
- People/users routes support course participant views.
- Announcement routes support course-level announcements.
- File routes support upload and download workflows.
- Mongoose models define the structure of application data stored in MongoDB.

## API Overview

The backend exposes REST API endpoints for the frontend.

Common route categories include:

```text
/api/users
/api/courses
/api/modules
/api/assignments
/api/quizzes
/api/enrollments
/api/announcements
/api/files
```

The exact endpoints depend on the route files in the project, but the API is organized around the main learning management system resources.

## Core Workflows

### Authentication

The backend supports user authentication using session-based login. Users can sign up, sign in, retrieve their profile, and sign out.

### Course Management

The server provides routes for retrieving, creating, updating, and deleting courses. These routes are consumed by the React dashboard and course pages.

### Enrollment Management

The backend tracks which users are enrolled in which courses, allowing the frontend to show personalized course dashboards.

### Modules and Lessons

Course modules and lessons are managed through backend routes, allowing instructors to organize course content.

### Assignments

The backend supports assignment creation, editing, submission tracking, file handling, and result storage.

### Quizzes

The quiz API supports quiz creation, question management, quiz-taking workflows, and result tracking.

### Grades and Results

The backend stores and returns results from assignments and quizzes so students and instructors can view performance data.

### Announcements

Course announcements are stored and served through API routes for display in the frontend.

### Files

The backend supports file-related workflows used by course content and student submissions.

## Deployment

The backend is designed to be deployed on Render.

Production environment variables should be configured directly in Render:

```env
NODE_ENV=production
NETLIFY_URL=https://learning-management-system-rayan.netlify.app
SESSION_SECRET=your_production_session_secret
MONGO_CONNECTION_STRING=your_mongodb_atlas_connection_string
```

After updating environment variables on Render, redeploy the backend service.

The frontend on Netlify should point to the Render backend using:

```env
REACT_APP_REMOTE_SERVER=https://your-render-backend-url.onrender.com
```

## Security Notes

- Do not commit `.env` files.
- Do not expose MongoDB credentials in GitHub.
- Use MongoDB Atlas credentials only through Render environment variables.
- Use a strong `SESSION_SECRET` in production.
- Restrict CORS to the deployed frontend URL instead of allowing all origins.
- Avoid hardcoding backend URLs directly in source files.

## Why This Project Matters

This backend supports a realistic full-stack learning management system with many of the same data relationships found in real educational platforms:

- Users belong to courses through enrollments.
- Courses contain modules, assignments, quizzes, announcements, and files.
- Students submit work and receive results.
- Instructors manage content and evaluate submissions.
- The frontend and backend communicate through structured REST APIs.
- Data is persisted in MongoDB using Mongoose models.

The project demonstrates backend engineering, API design, database modeling, authentication, deployment configuration, and full-stack integration.

## Future Improvements

- Add stronger role-based authorization for students, instructors, and admins
- Add request validation middleware
- Add centralized error handling
- Add API documentation with Swagger or Postman
- Add automated backend tests
- Add pagination for large user/course datasets
- Improve file storage strategy for production
- Add logging and monitoring for deployed API requests
- Add password hashing if not already implemented
- Add stricter production security settings for cookies and CORS

## Project Context

This backend was built as part of a full-stack learning management system inspired by Canvas. It powers the React frontend by providing REST API endpoints, session-based authentication, MongoDB data persistence, and server-side logic for courses, users, assignments, quizzes, modules, enrollments, and results.

The goal was to build a realistic educational platform with enough backend depth to support students, instructors, course content, submissions, grades, and administrative workflows.