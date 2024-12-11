# Duolingo Documentation Architecture
## 1. System Context Diagram
The System Context Diagram provides a high-level view of the Duolingo documentation system, showcasing how external actors (users and services) interact with the primary subsystems within the application. 

![image](https://github.com/user-attachments/assets/e8ac034e-cdc6-43b8-93ce-8055a0b18edb)


```
@startuml
!define RECTANGLE class
actor "Project Team" as projectTeam
actor "Users" as users
actor "Language Experts" as languageExperts
actor "Educational Content Developers" as contentDevs
actor "Educational Institutions" as eduInstitutions
actor "Investors/Sponsors" as investors
actor "Developers Community" as devCommunity
actor "Regulatory Authorities" as regulatoryAuthorities

rectangle DuolingoSystem {
    usecase "Provide Language Lessons" as UC1
    usecase "Track Learning Progress" as UC2
    usecase "Provide Feedback to Learners" as UC3
    usecase "Moderate Content" as UC4
    usecase "Manage User Accounts" as UC5
    usecase "Monitor App Performance" as UC6
    usecase "Manage Data Privacy & Security" as UC7
}

' User actors interacting with the system
users --> UC1 : "Engage with Language Lessons"
users --> UC2 : "Track Learning Progress"
users --> UC3 : "Provide Feedback on Lessons"

' Project Team actors interacting with the system
projectTeam --> UC6 : "Monitor App Performance"
projectTeam --> UC5 : "Manage User Accounts"

' Language Experts interacting with the system
languageExperts --> UC1 : "Create & Review Language Content"
languageExperts --> UC3 : "Provide Content Feedback"

' Educational Content Developers interacting with the system
contentDevs --> UC1 : "Create Educational Content"
contentDevs --> UC3 : "Provide Content Feedback"

' Educational Institutions interacting with the system
eduInstitutions --> UC1 : "Integrate with Curriculum"
eduInstitutions --> UC7 : "Ensure Data Privacy Compliance"

' Investors/Sponsors interacting with the system
investors --> UC6 : "Monitor Financial & Performance Metrics"

' Developers Community interacting with the system
devCommunity --> UC1 : "Contribute Features and Enhancements"
devCommunity --> UC7 : "Assist in Data Security Features"

' Regulatory Authorities interacting with the system
regulatoryAuthorities --> UC7 : "Audit & Enforce Data Privacy & Security Standards"
@enduml

```
---
## 2. Container Diagram 
The Container Diagram outlines the high-level architecture of the Duolingo documentation system, breaking it into containers that represent major building blocks of the system. It provides a detailed view of the system's structure, showing how these containers interact with each other and with external services.

![image](https://github.com/user-attachments/assets/8dda4d4a-ce76-45ea-afcb-1bfe4ce4bc93)



```
@startuml
!define RECTANGLE class
!define INTERFACE interface

' Define Containers
RECTANGLE "Duolingo Mobile App" as mobileApp {
  RECTANGLE "User Interface" as ui
  RECTANGLE "Local Storage" as storage
  INTERFACE "Mobile API Client" as mobileAPI
}

RECTANGLE "Duolingo Web App" as webApp {
  RECTANGLE "User Interface" as uiWeb
  RECTANGLE "Web Server" as webServer
  INTERFACE "Web API Client" as webAPI
}

RECTANGLE "API Server" as apiServer {
  RECTANGLE "API Endpoints" as apiEndpoints
  RECTANGLE "Authentication Service" as authService
  RECTANGLE "Data Processing Service" as dataService
}

RECTANGLE "Database" as database {
  RECTANGLE "User Data" as userData
  RECTANGLE "Lesson Data" as lessonData
  RECTANGLE "Progress Tracking" as progressData
}

' Define Relationships
mobileApp -down-> mobileAPI : Uses
mobileApp -down-> storage : Stores Local Data
mobileAPI -down-> apiServer : Communicates via REST API
apiServer -down-> apiEndpoints : Exposes API Endpoints
apiServer -down-> authService : Manages User Authentication
apiServer -down-> dataService : Provides Data Processing
apiServer -down-> database : Queries Data

webApp -down-> webAPI : Uses
webApp -down-> webServer : Hosts Web Application
webAPI -down-> apiServer : Communicates via REST API
webServer -down-> apiEndpoints : Requests Data from API
webServer -down-> authService : Manages User Authentication

database -down-> userData : Stores User Data
database -down-> lessonData : Stores Lesson Content
database -down-> progressData : Stores Learning Progress

' External Systems and Stakeholders
INTERFACE "Content Moderators" as contentModerators
INTERFACE "Customer Support" as customerSupport
INTERFACE "Data Analysts" as dataAnalysts
INTERFACE "Language Experts" as languageExperts

contentModerators -down-> apiServer : Reviews and Flags Content
customerSupport -down-> apiServer : Handles User Queries
dataAnalysts -down-> apiServer : Analyzes User Data
languageExperts -down-> apiServer : Reviews and Curates Content

@enduml

```
---
## 3. Component Diagrams
The Component Diagram breaks down the key subsystems of the Duolingo documentation system and explains how individual components interact to fulfill system functionality. This diagram is presented from two perspectives: Learners (Players) and Admins (Educators), focusing on their unique interactions with the system.

### 3.1 Component Diagram for Learners (Players)
This diagram shows the system components and interactions from the learner's perspective.


![image](https://github.com/user-attachments/assets/ca714b82-679b-4a24-a0c5-9e914b399ef8)


```
@startuml

!define RECTANGLE class

' Components for user interaction
package "Player Interaction" {
    RECTANGLE Player {
        +signUp()
        +login()
        +completeLesson()
        +trackProgress()
        +giveFeedback()
        +viewLeaderboard()
    }

    RECTANGLE LessonModule {
        +startLesson()
        +takeQuiz()
        +getInstantFeedback()
        +viewLessonHistory()
    }

    RECTANGLE SocialFeatures {
        +sendChallenge()
        +viewFriendProgress()
        +viewFriendLeaderboard()
    }

    RECTANGLE FeedbackSystem {
        +submitBugReport()
        +submitContentFeedback()
        +rateLesson()
    }

    RECTANGLE ProgressTracker {
        +viewProgress()
        +trackSkillLevels()
        +setGoals()
    }

    Player --> LessonModule : interacts with
    Player --> SocialFeatures : engages with
    Player --> FeedbackSystem : provides feedback to
    Player --> ProgressTracker : tracks progress through
}

' Components for content and performance management
package "Content & Performance" {
    RECTANGLE ContentManager {
        +createLesson()
        +updateLesson()
        +localizeLesson()
    }

    RECTANGLE PerformanceTracker {
        +analyzeUserData()
        +generateReports()
        +suggestImprovements()
    }

    RECTANGLE Analytics {
        +collectUserData()
        +generateInsights()
        +improveLearningPaths()
    }

    ContentManager --> LessonModule : provides lessons to
    PerformanceTracker --> ProgressTracker : tracks user performance via
    Analytics --> PerformanceTracker : provides data to
}

' Components for system administration and security
package "Admin & Security" {
    RECTANGLE AdminPanel {
        +manageUserAccounts()
        +assignPermissions()
        +auditAppUsage()
    }

    RECTANGLE SecurityModule {
        +monitorForVulnerabilities()
        +ensureDataPrivacy()
        +performSecurityAudits()
    }

    AdminPanel --> Player : manages
    AdminPanel --> ContentManager : updates lessons
    SecurityModule --> Player : protects user data
    SecurityModule --> ContentManager : ensures content security
}

' External Stakeholders for integration and compliance
package "External Stakeholders" {
    RECTANGLE DataPrivacy {
        +ensureGDPRCompliance()
        +monitorDataHandling()
    }

    RECTANGLE EducationalInstitutions {
        +integrateWithCurriculum()
        +provideFeedback()
    }

    DataPrivacy --> SecurityModule : monitors compliance
    EducationalInstitutions --> ContentManager : provides curriculum insights
}

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

### 5. Admin Panel Components
#### 5.1 User Management
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

#### 5.2Content Management
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

![image](https://github.com/user-attachments/assets/135b649f-562a-4170-a31a-79b9817cc398)

```
@startuml
' Define cloud provider
node "Cloud Provider (AWS)" as CloudProvider {
    node "Global Infrastructure" as GlobalInfra {
        node "User Devices" as UserDevices {
            component "Mobile App" as MobileApp
            component "Web App" as WebApp
        }
        node "Frontend Servers" as FrontendServers {
            component "API Server" as APIServer
            component "Load Balancer" as LoadBalancer
        }
        node "Content Delivery Network" as CDNNode {
            component "Global CDN" as CDN
        }
        node "Application Servers" as AppServers {
            component "Language Learning Engine" as LearningEngine
            component "Content Management System" as CMS
            component "Authentication Service" as AuthService
        }
        node "Database Servers" as DBServers {
            component "User Database" as UserDB
            component "Course Database" as CourseDB
            component "Analytics Database" as AnalyticsDB
        }
    }
}

' Define relationships
UserDevices -down-> CDN : Retrieve Cached Content
CDN -down-> APIServer : Request Dynamic Content
UserDevices -down-> APIServer : Uses API
APIServer -down-> LoadBalancer : Distributes Requests
LoadBalancer -down-> LearningEngine : Forwards Requests for Learning Services
LoadBalancer -down-> CMS : Forwards Requests for Content Services
LoadBalancer -down-> AuthService : Forwards Authentication Requests
LearningEngine -down-> CourseDB : Retrieves Course Data
LearningEngine -down-> UserDB : Retrieves User Progress Data
LearningEngine -down-> AnalyticsDB : Sends Performance Data
CMS -down-> CourseDB : Updates Course Content
CMS -down-> CDN : Pushes Static Content
AuthService -down-> UserDB : Validates User Credentials
FrontendServers -down-> AppServers : Relays Requests
AppServers -down-> DBServers : Data Storage and Retrieval

' Define notes
note right of CloudProvider
  "Cloud-based infrastructure providing 
  global scalability and reliability"
end note
note right of CDNNode
  "Distributed network of cached content 
  to reduce latency and improve 
  application performance"
end note
note right of UserDevices
  "Mobile and Web Apps used by end users 
  to access language learning features"
end note
@enduml
```
---
