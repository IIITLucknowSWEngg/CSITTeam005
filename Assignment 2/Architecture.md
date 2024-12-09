# Duolingo Documentation Architecture
## 1. System Context Diagram
The System Context Diagram provides a high-level view of the Duolingo documentation system, showcasing how external actors (users and services) interact with the primary subsystems within the application. 

 ![image](https://github.com/user-attachments/assets/1b701eac-f29c-4388-95df-023e3a10f006)



```
@startuml
' External Actors
actor "Learner" as Player
actor "Educator" as Admin
actor "Notification Service" as NotificationService

' System Boundary: Duolingo App
package "Duolingo App" {

    ' Subsystems
    rectangle "User Authentication \nand Profile Management" as AuthSystem
    rectangle "Course Selection \nand Lesson Management" as LessonSystem
    rectangle "Progress Tracker \nand Analytics" as ProgressTracker
    rectangle "Leaderboard \nand Statistics" as Leaderboard
    rectangle "In-Game Chat \nand Social Interaction" as ChatSystem
    rectangle "Educator Panel" as AdminPanel
}

' Relationships between actors and system components
Player --> AuthSystem : Sign Up/Login
Player --> LessonSystem : Learn Language
Player --> ProgressTracker : Track Progress
Player --> Leaderboard : View Rankings
Player --> ChatSystem : Chat with Other Learners

Admin --> AdminPanel : Manage Users and Content
LessonSystem --> NotificationService : Send Lesson Reminders
@enduml


```
---
## 2. Container Diagram 
The Container Diagram outlines the high-level architecture of the Duolingo documentation system, breaking it into containers that represent major building blocks of the system. It provides a detailed view of the system's structure, showing how these containers interact with each other and with external services.

![image](https://github.com/user-attachments/assets/c86f2248-cd49-4f85-8b28-052db572d79c)


```
@startuml
title Container Diagram - Duolingo Documentation

' Add primary containers
rectangle "Web/Mobile App" as App <<User Interface>> #lightblue
rectangle "API Gateway" as APIGateway <<API Gateway>> #lightgreen
rectangle "Lesson Service" as LessonService <<Service>> #lightyellow
rectangle "Progress Tracker Service" as ProgressService <<Service>> #lightyellow
rectangle "Leaderboard Service" as LeaderboardService <<Service>> #lightyellow
rectangle "Chat Service" as ChatService <<Service>> #lightyellow

' Database containers
database "User Database" as UserDB <<Database>> #lightpink
database "Lesson Database" as LessonDB <<Database>> #lightpink
database "Leaderboard Database" as LeaderboardDB <<Database>> #lightpink

' External services
rectangle "Notification Service" as NotificationService <<External Service>> #lightgray

' Relationships between containers
App --> APIGateway : API Requests
APIGateway --> LessonService : Manage Lessons
APIGateway --> ProgressService : Track Progress
APIGateway --> LeaderboardService : Rankings
APIGateway --> ChatService : Messaging
APIGateway --> NotificationService : Player Notifications

LessonService --> LessonDB : Manage Lessons
ProgressService --> UserDB : User Progress
LeaderboardService --> LeaderboardDB : Update Rankings
@enduml


```
---
## 3. Component Diagrams
The Component Diagram breaks down the key subsystems of the Duolingo documentation system and explains how individual components interact to fulfill system functionality. This diagram is presented from two perspectives: Learners (Players) and Admins (Educators), focusing on their unique interactions with the system.

### 3.1 Component Diagram for Learners (Players)
This diagram shows the system components and interactions from the learner's perspective.

![image](https://github.com/user-attachments/assets/43eda53c-004a-460e-9f7d-119f347081bf)




```
@startuml
' External Actor
actor "Learner" as Player

' System Boundary: Duolingo App
package "Duolingo App" {

    ' Subsystems for Player
    rectangle "Authentication \nand Profile Management" as AuthSystem
    rectangle "Course Selection \nand Lesson Management" as LessonSystem
    rectangle "Progress Tracker \nand Analytics" as ProgressTracker
    rectangle "Leaderboard \nand Statistics" as Leaderboard
    rectangle "In-Game Chat \nand Social Interaction" as ChatSystem
}

' Relationships between Player and system components
Player --> AuthSystem : Sign Up/Login
Player --> LessonSystem : Learn Language
Player --> ProgressTracker : Track Progress
Player --> Leaderboard : View Rankings
Player --> ChatSystem : Chat with Other Learners
@enduml

```
### 3.2 Component Diagram for Admins
This diagram shows the system components and interactions from the admin's perspective.

![image](https://github.com/user-attachments/assets/eadba074-9b95-40dd-9627-6fe29b7a39d0)



```
@startuml
' External Actor
actor "Admin" as Admin

' System Boundary: Duolingo Admin Panel
package "Admin Panel" {

    ' Subsystems for Admin
    rectangle "User Management" as UserManagement
    rectangle "Course and Content Management" as ContentManagement
    rectangle "Leaderboard Management" as LeaderboardManagement
    rectangle "Notification Management" as NotificationManagement
    rectangle "Reports and Analytics" as ReportsAnalytics
}

' Relationships between Admin and system components
Admin --> UserManagement : Manage Users
Admin --> ContentManagement : Manage Courses
Admin --> LeaderboardManagement : Manage Rankings
Admin --> NotificationManagement : Send Notifications
Admin --> ReportsAnalytics : Generate Reports
@enduml

```
---
## 4. Code Diagrams
### 1. Authentication and Profile Management
This component manages user authentication and profile data.
```
@startuml
title C4 Code Diagram - Authentication and Profile Management

package "Authentication and Profile Management" {
    class AuthService {
        + register(user: User): User
        + login(email: String, password: String): Token
        + logout(token: Token): void
    }

    class User {
        - id: String
        - name: String
        - email: String
        - passwordHash: String
        + validateCredentials(): Boolean
    }

    class Profile {
        - userId: String
        - bio: String
        - avatar: String
        + updateProfile(bio: String, avatar: String): void
    }

    class AuthRepository {
        + findUserByEmail(email: String): User
        + saveUser(user: User): void
        + getUserProfile(userId: String): Profile
    }
}

AuthService --> User : "Validates Credentials"
AuthService --> AuthRepository : "Fetch/Store User Data"
AuthRepository --> "Database (Users Table)" : "CRUD Operations"
Profile --> "Database (Users Table)" : "Stores User Info"
@enduml

```
![image](https://github.com/user-attachments/assets/63a411a6-e203-482a-bfb6-22b718c8d052)

### 2. Course and Content Management
This component is responsible for course material, lessons, and exercises.
```
@startuml
title C4 Code Diagram - Course and Content Management

package "Course and Content Management" {
    class CourseService {
        + fetchCourses(): List<Course>
        + createCourse(course: Course): Course
        + updateCourse(course: Course): Course
    }

    class Course {
        - id: String
        - title: String
        - description: String
        - lessons: List<Lesson>
        + getTitle(): String
        + getDescription(): String
    }

    class Lesson {
        - id: String
        - title: String
        - content: String
        + getContent(): String
    }

    class CourseRepository {
        + findCourseById(courseId: String): Course
        + saveCourse(course: Course): void
        + fetchAllCourses(): List<Course>
    }
}

CourseService --> Course : "Manages Course Data"
CourseService --> CourseRepository : "Fetch/Store Course Data"
CourseRepository --> "Database (Lessons Table)" : "CRUD Operations"
@enduml

```
![image](https://github.com/user-attachments/assets/f142a389-1f5a-4e76-a1be-c2753086a9a1)

### 3. Progress Tracker and Analytics
This component tracks user progress in lessons.
```
@startuml
title C4 Code Diagram - Progress Tracker and Analytics

package "Progress Tracker and Analytics" {
    class ProgressTracker {
        + recordProgress(userId: String, lessonId: String, status: String): void
        + getProgress(userId: String): List<Progress>
        + calculateScore(userId: String): int
    }

    class Progress {
        - userId: String
        - lessonId: String
        - status: String
        - timestamp: Date
        + getStatus(): String
        + setStatus(status: String): void
    }

    class ProgressRepository {
        + saveProgress(progress: Progress): void
        + fetchProgress(userId: String): List<Progress>
    }
}

ProgressTracker --> Progress : "Tracks Progress"
ProgressTracker --> ProgressRepository : "CRUD Operations"
ProgressRepository --> "Database (Progress Table)" : "Stores Progress"
@enduml
```
![image](https://github.com/user-attachments/assets/1ad5810e-eced-4815-b444-515227a90ec8)


### 4. Leaderboard and Statistics
This component displays and manages the leaderboard.
```
@startuml
title C4 Code Diagram - Leaderboard and Statistics

package "Leaderboard and Statistics" {
    class LeaderboardService {
        + getLeaderboard(): List<UserScore>
        + updateScore(userId: String, score: int): void
    }

    class UserScore {
        - userId: String
        - score: int
        + getScore(): int
        + setScore(score: int): void
    }

    class LeaderboardRepository {
        + fetchScores(): List<UserScore>
        + saveScore(userScore: UserScore): void
    }
}

LeaderboardService --> UserScore : "Manages Scores"
LeaderboardService --> LeaderboardRepository : "CRUD Operations"
LeaderboardRepository --> "Database (Progress Table)" : "Stores Score Data"
@enduml

```
![image](https://github.com/user-attachments/assets/dd2051f4-352c-4ea0-968f-b3c9994da8d7)

### 5. In-Game Chat and Social Interaction
This component handles in-game communication between players.
```
@startuml
title C4 Code Diagram - In-Game Chat and Social Interaction

package "In-Game Chat and Social Interaction" {
    class ChatService {
        + sendMessage(senderId: String, receiverId: String, message: String): void
        + getMessages(userId: String): List<Message>
    }

    class Message {
        - senderId: String
        - receiverId: String
        - content: String
        - timestamp: Date
        + getContent(): String
        + getTimestamp(): Date
    }

    class ChatRepository {
        + saveMessage(message: Message): void
        + fetchMessages(userId: String): List<Message>
    }
}

ChatService --> Message : "Manages Messages"
ChatService --> ChatRepository : "CRUD Operations"
ChatRepository --> "Database (Messages Table)" : "Stores Messages"
@enduml

```
![image](https://github.com/user-attachments/assets/d77fb0b8-85a2-40f5-8f98-7c912a4d467b)

### 6. Admin Panel Components
#### 6.1 User Management
```
@startuml
title C4 Code Diagram - User Management

package "User Management" {
    class UserService {
        + createUser(user: User): User
        + updateUser(userId: String, user: User): User
        + deleteUser(userId: String): void
    }

    class User {
        - id: String
        - name: String
        - email: String
        + getName(): String
        + setEmail(email: String): void
    }

    class UserRepository {
        + findUserById(userId: String): User
        + saveUser(user: User): void
        + deleteUser(userId: String): void
    }
}

UserService --> User : "Manages User Data"
UserService --> UserRepository : "CRUD Operations"
UserRepository --> "Database (Users Table)" : "CRUD Operations"
@enduml

```
![image](https://github.com/user-attachments/assets/c0b97527-3250-4c7d-9bcb-e470f830215e)

#### 6.2Content Management
```
v@startuml
title C4 Code Diagram - Content Management

package "Content Management" {
    class ContentService {
        + createCourse(course: Course): Course
        + updateCourse(courseId: String, course: Course): Course
        + deleteCourse(courseId: String): void
    }

    class Course {
        - id: String
        - title: String
        - description: String
        + getTitle(): String
        + setDescription(description: String): void
    }

    class ContentRepository {
        + findCourseById(courseId: String): Course
        + saveCourse(course: Course): void
        + deleteCourse(courseId: String): void
    }
}

ContentService --> Course : "Manages Course Data"
ContentService --> ContentRepository : "CRUD Operations"
ContentRepository --> "Database (Courses Table)" : "CRUD Operations"
@enduml

```
![image](https://github.com/user-attachments/assets/9ff57e46-fee9-4d4e-8f9d-3c5dca87ba22)

---
# 5. Deployment Diagram
The Deployment Diagram illustrates the physical deployment of the Duolingo documentation system, including the hardware, software, and external services involved. It showcases how the system’s components are distributed across various nodes and interact to deliver functionality.

![image](https://github.com/user-attachments/assets/2b95a395-2a60-41e0-a9ef-1f9603930c45)


```
@startuml
title Deployment Diagram - Duolingo Documentation

node "Player's Device" {
    [Web/Mobile App] <<User Interface>>
}

node "Server" {
    [API Gateway] <<API Gateway>>
    [Lesson Service] <<Service>>
    [Progress Tracker Service] <<Service>>
    [Leaderboard Service] <<Service>>
    [Chat Service] <<Service>>
}

node "Database Server" {
    database "User Database" as UserDB
    database "Lesson Database" as LessonDB
    database "Leaderboard Database" as LeaderboardDB
}

cloud "External Services" {
    [Notification Service] <<External Service>>
}

' Connections
[Web/Mobile App] --> [API Gateway] : API Calls
[API Gateway] --> [Lesson Service] : Manage Lessons
[API Gateway] --> [Progress Tracker Service] : Track Progress
[API Gateway] --> [Leaderboard Service] : Rankings
[API Gateway] --> [Chat Service] : Chat Messages
[Lesson Service] --> LessonDB : Store Lesson Data
[Progress Tracker Service] --> UserDB : User Data
[Leaderboard Service] --> LeaderboardDB : Rankings
@enduml

```
---
