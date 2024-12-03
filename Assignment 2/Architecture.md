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

![image](https://github.com/user-attachments/assets/51efad0b-7926-43ce-a12a-b82152ce3f4f)



```
@startuml
' External Actor
actor "Player" as Player

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
# 4. Deployment Diagram
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
