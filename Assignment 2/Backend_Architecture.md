
# Backend Architecture

## Overview
This document outlines the backend architecture for the Duolingo clone project. It describes the components, their interactions, and the technologies used to build the backend.

---

## Technologies Used
1. **Framework:** Node.js with Express.js.
2. **Database:** MongoDB (Collections for each data type).  
3. **Authentication:** JWT for token-based authentication and Google OAuth/Social Logins for third-party authentication.  
4. **Real-Time Communication:** WebSocket (via Socket.IO) for live updates such as progress tracking and leaderboard rankings.  

---

## Components

### 1. Authentication Service
- **Purpose:**  
  Handles user authentication, including:  
  - Login and signup (using JWT).  
  - Integration with Google OAuth and other social media login APIs.  
- **Interactions:**  
  - Communicates with MongoDB `User Collection` to validate and store user information.  
  - Sends/validates JWT tokens for session management.  
  - Interacts with third-party APIs (e.g., Google OAuth).

### 2. Lesson Management Service
- **Purpose:**  
  Manages all lesson-related CRUD operations, including:  
  - Fetching lessons.  
  - Adding/editing/deleting lesson content.  
- **Interactions:**  
  - Queries the MongoDB `Lesson Collection` for all operations.  

### 3. Quiz Management Service
- **Purpose:**  
  Handles quiz-related data, including:  
  - Fetching questions.  
  - Managing answers and results.  
- **Interactions:**  
  - Connects to the MongoDB `Quiz Collection`.  

### 4. Progress Tracking Service
- **Purpose:**  
  Tracks and updates user progress, including:  
  - Lesson completion status.  
  - Quiz scores and achievements.  
- **Interactions:**  
  - Updates MongoDB `Progress Collection` with progress data.  
  - Fetches user-related data from the `User Collection`.  

### 5. Gamification Service
- **Purpose:**  
  Manages gamification elements like leaderboards, achievements, and badges.  
- **Interactions:**  
  - Connects to MongoDB `Gamification Collection` for storing leaderboard and badge data.  

### 6. WebSocket Service (Socket.IO)
- **Purpose:**  
  Provides real-time communication for live updates, such as:  
  - Broadcasting progress updates during lessons.  
  - Live leaderboard rankings.  
- **Interactions:**  
  - Fetches real-time data from the `Progress Tracking Service` and `Gamification Service`.

---

## Database (MongoDB)
The backend uses **MongoDB** with the following collections:  
- **User Collection:** Stores user credentials, profiles, and preferences.  
- **Lesson Collection:** Contains lesson data like titles, content, and media.  
- **Quiz Collection:** Stores quiz questions, answers, and metadata.  
- **Progress Collection:** Tracks user progress in lessons and quizzes.  
- **Gamification Collection:** Stores leaderboard data, badges, and achievements.  

---

## Interactions
### API Communication
- **REST API:**  
  All services interact via REST endpoints exposed through Express.js.

### Real-Time Communication
- **WebSocket (Socket.IO):**  
  Enables bi-directional communication for live updates. Examples include:  
  - Sending live progress updates to users during lessons.  
  - Broadcasting updated leaderboard rankings.

---

## Example Folder Structure
```
src
├── services
│   ├── authService.js
│   ├── lessonService.js
│   ├── quizService.js
│   ├── progressService.js
│   ├── gamificationService.js
├── database
│   ├── userModel.js
│   ├── lessonModel.js
│   ├── quizModel.js
│   ├── progressModel.js
│   ├── gamificationModel.js
├── routes
│   ├── authRoutes.js
│   ├── lessonRoutes.js
│   ├── quizRoutes.js
│   ├── progressRoutes.js
│   ├── gamificationRoutes.js
├── app.js
└── socket.js
```

---

## Future Considerations
1. **Microservices Architecture:**  
   Transition to a microservices-based architecture as the application grows.  
2. **Caching:**  
   Use Redis to cache frequent database queries for faster response times.  
3. **Deployment:**  
   Deploy on scalable platforms like AWS.

---
![image](https://github.com/user-attachments/assets/dfa7a7ed-9a72-4231-8db4-e22b99bcca0e)

---
