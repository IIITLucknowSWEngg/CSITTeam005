# Duolingo Clone Architecture
## 1. System Context Diagram

 ![duol1](https://github.com/user-attachments/assets/2fad14d1-d971-4eb9-94e6-95379a30ed56)


```
@startuml
' External Actors
actor "Learner" as Player
actor "Educator" as Admin
actor "Notification Service" as NotificationService

' System Boundary: Duolingo Clone App
package "Duolingo Clone App" {

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
The container diagram breaks down the system into high-level containers and their interactions.

![containerd](https://github.com/user-attachments/assets/e2ebdcb0-3063-45d9-bbab-ce5f399a0616)

```
@startuml
title Container Diagram - Duolingo Clone

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
### 3.1 Component Diagram for Learners (Players)
This diagram shows the system components and interactions from the learner's perspective.

![component](https://github.com/user-attachments/assets/f853e061-2c7e-4443-a7ca-3a083b068480)


```
@startuml
' External Actor
actor "Player" as Player

' System Boundary: Duolingo Clone App
package "Duolingo Clone App" {

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

![educatorcomponent](https://github.com/user-attachments/assets/09bd840e-a1a6-4df3-94b3-80e52f33c87f)


```
@startuml
' External Actor
actor "Admin" as Admin

' System Boundary: Duolingo Clone Admin Panel
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
# 4. Deployment Diagram
This diagram outlines the physical deployment of the system across servers, databases, and external services.

![deployment diagram](https://github.com/user-attachments/assets/d1e87501-f46a-427c-b12c-1667e5e94a9e)

```
@startuml
title Deployment Diagram - Duolingo Clone

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
