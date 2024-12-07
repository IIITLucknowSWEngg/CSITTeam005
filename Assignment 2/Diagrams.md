# Diagram.md - Duolingo Project

This document provides an overview and description of the various UML diagrams that represent the architecture, use cases, and interactions within the Duolingo clone system. These diagrams serve as blueprints for understanding how different components and entities interact within the system.

---

## 1. **System Architecture Diagram**

### Description:
The **System Architecture Diagram** represents the overall structure of the Duolingo clone system. It details the interaction between the client-side (User's Device), server-side services, external services, and databases. This diagram provides a high-level overview of how different components are interconnected, ensuring smooth data flow and interactions.

### Components:
- **External Services**:
    - **Notification Service**: External service that handles notifications to users (e.g., reminders, alerts).
- **User Interface (Mobile/Web)**:
    - Represents the **Web/Mobile App** that the user interacts with to learn languages, access lessons, and track progress.
- **Server-Side Services**:
    - **API Gateway**: Manages API calls from the frontend and routes them to the appropriate service.
    - **Lesson Service**: Handles lesson data, fetching, and user interactions related to lessons.
    - **Progress Tracker Service**: Manages user progress tracking across lessons and exercises.
    - **Leaderboard Service**: Tracks and displays user rankings based on their achievements and points.
    - **Chat Service**: Facilitates user communication within the app (e.g., peer discussions).
- **Database Servers**:
    - **User Database (UserDB)**: Stores user-related information such as credentials, profile data, and learning progress.
    - **Lesson Database (LessonDB)**: Stores lesson content, including text, exercises, and media.
    - **Leaderboard Database (LeaderboardDB)**: Stores ranking and leaderboard data for users.

###UML Code
```UML 
@startuml
title System Architecture Diagram - Duolingo Documentation

' External Services
cloud "External Services" {
    [Notification Service] <<External Service>> 
}

' User Interface (Mobile/Web)
node "User's Device" {
    [Web/Mobile App] <<User Interface>> 
}

' Server-side services
node "Server" {
    [API Gateway] <<API Gateway>>
    [Lesson Service] <<Service>> 
    [Progress Tracker Service] <<Service>> 
    [Leaderboard Service] <<Service>> 
    [Chat Service] <<Service>> 
}

' Database Servers
node "Database Server" {
    database "User Database" as UserDB <<Database>> 
    database "Lesson Database" as LessonDB <<Database>> 
    database "Leaderboard Database" as LeaderboardDB <<Database>> 
}

' Relationships
[Web/Mobile App] --> [API Gateway] : API Calls
[API Gateway] --> [Lesson Service] : Manage Lessons
[API Gateway] --> [Progress Tracker Service] : Track Progress
[API Gateway] --> [Leaderboard Service] : Rankings
[API Gateway] --> [Chat Service] : Chat Messages
[Lesson Service] --> LessonDB : Store Lesson Data
[Progress Tracker Service] --> UserDB : User Data
[Leaderboard Service] --> LeaderboardDB : Rankings
[API Gateway] --> [Notification Service] : Send Notifications

@enduml

```
![System Architecture Diagram](https://github.com/user-attachments/assets/aeff24f5-d9c1-4012-8f62-d0f693d50612)


---

## 2. **Use Case Diagram**

### Description:
The **Use Case Diagram** outlines the different interactions between the users (Learners and Admins) and the Duolingo clone system. It highlights the main actions that users and administrators can perform within the system, including actions related to language learning, progress tracking, and system management.

### Actors:
- **Learner (User)**: The primary user who interacts with the system to learn languages, track progress, and engage with exercises.
- **Admin (Educator)**: Manages user data, content, and other system resources. Admins can also modify lesson content, manage progress, and handle user queries.
- **Notification Service**: Sends reminders or notifications to users, such as course reminders, achievement updates, etc.
- **Leaderboard System**: Updates rankings based on user performance in terms of lesson completion, points, and achievements.

###UML Code
```


@startuml
title Use Case Diagram - Duolingo Documentation

actor "Learner (User)" as User
actor "Admin (Educator)" as Admin
actor "Notification Service" as Notification
actor "Leaderboard System" as Leaderboard

rectangle "Duolingo System" {
    package "Learner Use Cases" {
        usecase "Sign Up/Login" as UC1
        usecase "Explore Languages" as UC2
        usecase "Start Learning" as UC3
        usecase "Progress Tracking" as UC4
        usecase "Engage in Leaderboards" as UC5
        usecase "Practice with Community" as UC6
    }

    package "Admin Use Cases" {
        usecase "User Management" as UC7
        usecase "Content Management" as UC8
        usecase "Analytics Dashboard" as UC9
        usecase "Notification Management" as UC10
    }
}

' Relationships for Learners
User --> UC1
User --> UC2
User --> UC3
User --> UC4
User --> UC5
User --> UC6

' Relationships for Admins
Admin --> UC7
Admin --> UC8
Admin --> UC9
Admin --> UC10

' External system interactions
Notification --> UC3 : "Sends Reminders"
Leaderboard --> UC5 : "Updates Rankings"

@enduml

```

![image](https://github.com/user-attachments/assets/d7ee9519-6a98-4505-92f5-e20de2cdaed5)


---

## 3. **Class Diagram**

### Description:
The **Class Diagram** provides a detailed view of the classes in the Duolingo clone system, their attributes, methods, and relationships. It models the core entities such as `User`, `Course`, `Lesson`, `Exercise`, and more.

### Key Classes:
- **User**: Represents the users of the system (Learners, Educators, Admins).
- **Course**: Represents a language course.
- **Lesson**: Represents individual lessons within a course.
- **Exercise**: Represents exercises within lessons.
- **Progress Tracker**: Tracks a user’s progress in a course.
- **Leaderboard**: Manages rankings of users based on points.
- **Notification**: Sends notifications to users.
- **Chat**: Manages user communication within the system.

###UML Code
```
@startuml

title Class Diagram - Duolingo Documentation

skinparam classBackgroundColor #FAFAFA
skinparam classBorderColor #005A9C
skinparam classFontColor #333333
skinparam classArrowColor #666666

' Main User Class
class User {
  - userID: int
  - name: String
  - email: String
  - password: String
  - role: String  <<enum {Learner, Educator, Admin}>>
  - nativeLanguage: String
  - targetLanguage: String
  + register()
  + login()
  + updateProfile()
}

' Course Class
class Course {
  - courseID: int
  - courseName: String
  - languagePair: String
  - difficultyLevel: String
  - description: String
  - educatorID: int
  + enroll(userID: int)
  + addLesson(lesson: Lesson)
  + getLesson(lessonID: int)
}

' Lesson Class
class Lesson {
  - lessonID: int
  - lessonName: String
  - content: String
  - exerciseList: List<Exercise>
  - duration: int
  + startLesson()
  + evaluateAnswers(userID: int, answers: List<String>)
}

' Exercise Class
class Exercise {
  - exerciseID: int
  - question: String
  - answerOptions: List<String>
  - correctAnswer: String
  - exerciseType: String <<enum {MCQ, FillInTheBlanks, Matching}>>
  + submitAnswer(userID: int, answer: String)
  + getFeedback()
}

' Progress Tracker Class
class ProgressTracker {
  - progressID: int
  - userID: int
  - courseID: int
  - completedLessons: List<int>
  - streak: int
  - totalPoints: int
  + updateProgress(lessonID: int, points: int)
  + getProgressReport()
}

' Leaderboard Class
class Leaderboard {
  - leaderboardID: int
  - courseID: int
  - rankings: Map<int, int> <<userID -> points>>
  + updateRankings(userID: int, points: int)
  + getTopLearners(count: int)
}

' Notification Class
class Notification {
  - notificationID: int
  - userID: int
  - message: String
  - notificationType: String <<enum {Reminder, Achievement, Announcement}>>
  - timestamp: Date
  + sendNotification(userID: int, message: String)
  + getNotifications(userID: int)
}

' Chat Class
class Chat {
  - chatID: int
  - participants: List<int>
  - messages: List<Message>
  + sendMessage(userID: int, message: String)
  + getChatHistory(chatID: int)
}

' Message Class
class Message {
  - messageID: int
  - senderID: int
  - content: String
  - timestamp: Date
  + editMessage(newContent: String)
  + deleteMessage()
}

' Relationships
User "1" -- "0..*" Course : "Enrolled In"
User "1" -- "0..*" ProgressTracker : "Tracks Progress"
User "1" -- "0..*" Notification : "Receives"
User "1" -- "0..*" Chat : "Participates In"
Course "1" -- "1..*" Lesson : "Contains"
Lesson "1" -- "0..*" Exercise : "Includes"
ProgressTracker "1" -- "1" User : "Belongs To"
Leaderboard "1" -- "0..*" User : "Ranks"
Chat "1" -- "0..*" Message : "Contains"
@enduml

```
![image](https://github.com/user-attachments/assets/b7327643-cafb-4687-b3f6-20969a32f22f)



---

## 4. **Activity Diagram**

### Description:
The **Activity Diagram** outlines the flow of activities that a learner follows during a session, starting from signing up or logging in to completing a lesson. It includes decision points such as language selection and completing exercises.

### Flow:
1. **Sign Up/Login**: The user starts by logging into the system.
2. **Language Selection**: The user selects a language to learn.
3. **Learning and Exercises**: The user completes lessons and exercises.
4. **Progress Update**: The user’s progress is updated based on performance.

###UML Code
```
@startuml
title Activity Diagram - Duolingo Project
start
:Sign Up/Login;
:Explore Languages;
:Select Language;

if (Is Language Selected?) then (yes)
  :Start Learning;
  :Begin Lesson;
  :Complete Lesson Steps;
  
  fork
    :Complete Exercise;
    :Submit Answer;
    :Get Feedback;
    
    if (Is Answer Correct?) then (yes)
      :Earn Points;
      :Update Progress;
    else (no)
      :Retry Exercise;
    endif
  end fork
  
  :Check If Lesson Completed;
  
  if (Is Lesson Completed?) then (yes)
    :Send Completion Message;
    :Update Progress Tracker;
    :Track Points;
    :Display Progress;
  else (no)
    :Continue Learning;
  endif
else (no)
  :Exit Application;
endif

stop
@enduml

```

![image](https://github.com/user-attachments/assets/e0443741-ddcc-4c0b-8a3e-164cca3ee770)


---

## 5. **Swimlane Diagram**

### Description:
The **Swimlane Diagram** shows the sequence of interactions between different system components (User, UI Layer, Backend Service, Database, etc.) during the login and lesson interaction flow. It divides the process into lanes, each representing different actors and components.

### Key Lanes:
- **User**: Represents the actions taken by the user.
- **UI Layer**: Represents the user interface, handling display and interaction.
- **Backend Service**: Represents the backend logic and services handling user data and content.
- **Database**: Represents data storage, such as user information and lessons.

##UML Code
```

@startuml
title Swimlane Diagram - Duolingo Project
|User|
start
:Sign Up/Login;
:Provide Credentials;

|UI Layer|
:Display Login Screen;
:Submit Credentials;

|Backend Service|
:Validate Credentials;
if (Credentials Valid?) then (yes)
  |Backend Service|
  :Retrieve User Data from Database;
  
  |Database|
  :Return User Data;
  
  |UI Layer|
  :Display Main Dashboard;
  :Show Available Languages;

  |User|
  :Select Language;
  
  |UI Layer|
  :Send Selected Language to Backend;

  |Backend Service|
  :Retrieve Language Content;
  
  |Database|
  :Fetch Language Lessons;
  
  |UI Layer|
  :Display Lesson Content;

  |User|
  :Start Learning;
  :Select Lesson;
  
  |Lesson Manager|
  :Retrieve Lesson Content;
  :Send Lesson to User;
  
  |UI Layer|
  :Display Exercise;
  :Collect User Responses;

  |User|
  :Complete Exercise;
  :Submit Answer;
  
  |Backend Service|
  :Check Answer from User;
  
  |Gamification Engine|
  :Evaluate Answer and Assign Points;
  
  |Progress Tracker|
  :Update User's Progress;
  
  |UI Layer|
  :Display Feedback (Correct/Incorrect);

  if (Answer Correct?) then (yes)
    |Gamification Engine|
    :Reward Points;
    :Unlock Achievements;
  else (no)
    |UI Layer|
    :Provide Feedback (Try Again);
  endif
  
  |User|
  :Continue Learning;
  :Review Progress and Scores;

  |Lesson Manager|
  :Check if Exercise is Complete;
  
  |UI Layer|
  :Display Lesson Completion Status;
  
  |User|
  :Complete Lesson;
  
  |Backend Service|
  :Update Progress in Database;
  
  |Database|
  :Store Updated Progress;
  
  |UI Layer|
  :Show Progress Summary;
  :Unlock Next Lesson;

  |Gamification Engine|
  :Track Overall Achievements;
else (no)
  |UI Layer|
  :Display Login Error;
  :Prompt Retry Login;
endif
stop
@enduml

```
![image](https://github.com/user-attachments/assets/bdf195d6-1b89-4440-813d-fc05a0d11297)


---

## 6. **Sequence Diagram**

### Description:
The **Sequence Diagram** depicts the sequence of interactions between the user and the system components, including the course system, lesson manager, exercise manager, and progress tracker.

### Flow:
1. **Enrollment**: The user enrolls in a course.
2. **Lesson Start**: The user starts a lesson and interacts with exercises.
3. **Progress Tracking**: The user's progress is tracked after completing exercises.

###UML Code
```
@startuml
title Sequence Diagram - Duolingo Project
actor User #LightBlue
participant "Course System" as Course #LightGreen
participant "Lesson Manager" as Lesson #LightYellow
participant "Exercise Manager" as Exercise #LightCoral
participant "Progress Tracker" as Tracker #LightSkyBlue

User -> Course: requestEnroll(courseID) #black
Course -> User: confirmEnrollment() #black

User -> Lesson: startLesson(lessonID) #black
Lesson -> User: sendLessonContent() #black

loop Each Exercise
    User -> Exercise: submitAnswer(exerciseID, answer) #black
    Exercise -> User: provideFeedback(isCorrect) #black
end

User -> Tracker: updateProgress(lessonID, points) #black
Tracker -> User: confirmProgressUpdate() #black

User -> Lesson: completeLesson() #black
Lesson -> User: sendCompletionMessage() #black

@enduml

```

![image](https://github.com/user-attachments/assets/2c560fe7-cb4e-4b1b-bb85-e609059fe619)


---

## Conclusion

The UML diagrams outlined in this document provide a comprehensive understanding of the Duolingo clone system’s architecture, use cases, class structure, activities, and interactions. These diagrams are essential for both the development and maintenance of the system.
