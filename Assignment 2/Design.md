
# Table of Contents
## Introduction
### 1.1 Purpose
### 1.2 Scope
### 1.3 Overview
### 1.4 Reference Material
### 1.5 Definitions and Acronyms

## System Overview

## System Architecture
### 3.1 Architectural Design
### 3.2 Decomposition Description
### 3.3 Design Rationale

## Data Design
### 4.1 Data Description
### 4.2 Data Dictionary

## Component Design
### 5.1 Gamification Engine

## Human Interface Design
### 6.1 Overview of User Interface
### 6.2 Screen Images
### 6.3 Screen Objects and Actions

## Requirements Matrix

## Appendices

## 1. Introduction
### 1.1 Purpose
The purpose of this document is to outline the software design for Duolingo, a gamified language-learning app. This document serves as a blueprint for the development team, detailing the architectural structure, data organization, and component functionalities needed to bring the system to life. It is also intended to provide clarity for stakeholders and future maintainers to understand how the app is designed to meet its goals.

### 1.2 Scope
Duolingo is a user-friendly, interactive app that uses gamification and adaptive learning techniques to help people learn languages at their own pace. It aims to make language learning fun, engaging, and accessible to users around the world. Key objectives include:
- *Gamified Learning*: Features like points, streaks, and leaderboards motivate users to stay consistent.
- *Personalized Experience*: Lessons are adapted to the user's progress and performance, ensuring effective learning.
- *Diverse Practice Options*: Exercises cover vocabulary, grammar, listening, and speaking to develop all-round skills.
- *Community Engagement*: Users can connect with others, compete in challenges, and share achievements.
- *Progress Tracking*: Provides detailed analytics on completed lessons, strengths, and areas for improvement. <br>
While the app offers a robust foundation for language learning, it is not a replacement for formal education or immersive real-world experiences.

### 1.3 Overview
This document is structured to guide the development of the Duolingo app. It includes:
- *System Overview*: A high-level description of the app’s functionality.
- *System Architecture*: The overall design, broken into logical modules.
- *Data Design*: Details on how user and course data is stored and managed.
- *Component Design*: A closer look at each core system component and how they work.
- *Human Interface Design*: Screens, interactions, and the overall user experience.
- *Requirements Matrix*: Mapping features to system components to ensure alignment.

### 1.4 Reference Material
IEEE Std 1016 – Software Design Descriptions.
Studies on gamification and its impact on education.
Speech recognition technologies and APIs.
Feedback and research from existing Duolingo users.

### 1.5 Definitions and Acronyms
Term - Definition
- *UI{User Interface}* – The part of the app users interact with directly.
- *Gamification* - Using game elements like points, badges, and rewards in non-game contexts to boost engagement.
- *API	{Application Programming Interface}* – Allows the app to communicate with its backend server.
- *Adaptive Learning* -	Learning tailored to individual progress and performance.
- *Leaderboard*	- A feature that ranks users based on their performance or points.

 ## 2. System Overview
Duolingo is designed to provide an engaging language-learning experience for users of all ages and skill levels. It is a mobile-first application, but it also supports a web version.

At its core, the app delivers short, gamified lessons that are tailored to a user’s progress. Each lesson integrates a variety of exercises to target different aspects of language learning, such as grammar, vocabulary, listening, and speaking. Real-time feedback, rewards, and progress tracking are key elements that keep users motivated and engaged.

## 3. System Architecture
### 3.1 Architectural Design
The Duolingo system architecture is modular, designed to handle the app's complexity and scalability requirements. The major components include:

- *User Interface Layer*: Handles user interactions, displays lessons, and updates leaderboards.
- *Backend Services*: Manages user profiles, stores lesson data, and tracks gamification metrics.
- *Speech Recognition Engine*: Processes spoken input and provides feedback on pronunciation.
- *Gamification Engine*: Calculates points, updates streaks, and manages leaderboard rankings.
- *Database Layer*: Stores all user data, lesson content, and progress statistics.

### 3.2 Decomposition Description
Each module is further broken into submodules. For instance:

#### UI Module:
- Login and Registration
- Dashboard and Progress Viewer
- Lesson Viewer

#### Gamification Module:
- Points System
- Badges and Achievements
- Leaderboard Updates

#### Diagram: 
- A simple flowchart showing the interaction between these components would go here.

### 3.3 Design Rationale
The modular design ensures scalability, maintainability, and flexibility. For example, the speech recognition engine can be updated independently without affecting other components. This modularity is crucial for a large-scale system like Duolingo, which supports millions of users.

## 4. Data Design
### 4.1 Data Description
Duolingo organizes its data into three major categories:
- *User Data* - Includes personal details, progress, and achievements.
- *Course Data* - Contains lessons, vocabulary, and multimedia files.
- *Gamification Data* - Tracks points, streaks, and leaderboard positions.
  
### 4.2 Data Dictionary
![image](https://github.com/user-attachments/assets/30cfe2db-ac48-4a55-a1a9-92eba77eb513)

## 5. Component Design
Each component in Duolingo is documented with pseudocode, algorithms, and descriptions.
### 5.1 Gamification Engine
Algorithm to Calculate Streaks:
![image](https://github.com/user-attachments/assets/ce3db62f-d12e-42fb-a4cb-be6f42c772d0)

## 6. Human Interface Design
### 6.1 Overview of User Interface
The app’s interface is designed to be intuitive and engaging, ensuring users can:

- Navigate lessons quickly.
- View their progress effortlessly.
- Participate in challenges with minimal effort.
  
### 6.2 Screen Images
The following are key screens in the application:

- *Login Page* - Allows users to log in to their accounts.
- *Dashboard* - Displays user progress, streaks, and leaderboards.
- *Lesson Screen* - Presents vocabulary and exercises interactively.
- *Progress Tracker* - Provides a visual representation of the user's learning journey.

### 6.3 Screen Objects and Actions
![image](https://github.com/user-attachments/assets/9260d725-5735-4d3a-bc9f-81dacf8b4a31)

## Requirements Matrix
![image](https://github.com/user-attachments/assets/0c3dee43-da38-426d-b928-adc72b35066c)

## Appendices
This section includes additional materials such as:

- Detailed diagrams of system workflows.
- Technical notes on data storage and retrieval.
- Research references and resources used in designing the system.

