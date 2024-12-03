
# Duolingo Test Plan Document (Based on IEEE Standard 829-1983)

## Test Plan Identifier:
**TP-DL-2024**

---

## Introduction

This document outlines the test plan for Duolingo, a language-learning platform, based on the ANSI/IEEE Standard 829-1983. It includes the scope, approach, resources, and schedule for the intended testing activities, as well as the features and test items to be assessed.

- **Summary of Items to Be Tested**: The test items include all language courses, user interface elements, and core features such as lessons, speech recognition, user profiles, and gamification elements.
- **History of the Items**: This test plan applies to the latest release version of Duolingo as of November 2024.
- **References to Related Documents**:
  - Relevant Standards: ANSI/IEEE Standard 829-1983

---

## Test Items

### Test Items and Their Versions
- **Language Courses**: Spanish, French, German, Italian, Japanese (Version 1.2)
- **Mobile App (iOS and Android)**: Version 4.5
- **Web App**: Version 1.1.0
- **Speech Recognition Engine**: Version 2.3
- **User Profile Management System**: Version 3.0
- **Gamification Features (XP, Streaks)**: Version 1.1

### Characteristics of Their Transmittal Media
- **Mobile App**: Available via App Store and Google Play
- **Web App**: Accessible via modern web browsers
- **Speech Recognition**: Server-based API
- **User Profile**: Cloud database

### References to Related Documents
- Requirements Specification: [Duolingo Requirements Doc](https://github.com/IIITLucknowSWEngg/CSITTeam005/blob/fce44310fa3cde3fbd8bcc16d3232f267a969344/Assignment1/SRS.md#software-requirements-specification-srs-for-duolingo)
- Design Specification: [Duolingo Design Doc](https://github.com/IIITLucknowSWEngg/CSITTeam005/blob/fce44310fa3cde3fbd8bcc16d3232f267a969344/Assignment%202/Design.md)

### Items Not Going to Be Tested
- **Payment Gateway**: Not relevant to the current release.
- **External API Integrations**: Will be tested in a separate phase.

---

## Features to Be Tested

### Core Learning Features
- **Lesson Content**: Ensure accuracy and functionality of lessons.
- **Speech Recognition**: Test accuracy and responsiveness.
- **Adaptive Learning Paths**: Verify difficulty adjustment based on user performance.

### User Account Management
- **Login System**: Test login functionality with valid/invalid credentials.
- **Profile Management**: Ensure users can create/edit profiles.
- **Progress Tracking**: Verify user progress is tracked accurately.

### Gamification
- **XP System**: Ensure proper XP awards.
- **Leaderboards**: Verify correct updates.
- **Streaks**: Test streak tracking and notifications.

### Mobile App Performance
- **Load Times**: Measure and optimize app startup/screen transitions.
- **Offline Mode**: Test app functionalities without internet.
- **Responsiveness**: Ensure smooth user interactions.

### Web App Performance
- **Cross-Browser Compatibility**: Verify functionality across Chrome, Firefox, Safari, and Edge.
- **Responsive Design**: Test UI responsiveness on various screen sizes.
- **Accessibility**: Ensure compliance with WCAG 2.1 standards.
- **Performance**: Test page load times and responsiveness during peak usage.

### Cross-Platform Consistency
- **UI/UX Consistency**: Verify consistency across web, Android, and iOS platforms.
- **Device Compatibility**: Test various screen sizes and OS versions.

---

## Features Not to Be Tested

- **Payment Integration**: Outside the scope of this release.
- **Backend Infrastructure**: Server-side components excluded.

---

## Approach

### Overall Approach
Testing will be conducted in multiple phases:
1. **Unit Testing**: Test individual components like lessons.
2. **Integration Testing**: Verify app-backend interactions.
3. **System Testing**: End-to-end feature validation.
4. **Performance Testing**: Stress test app under various conditions.

### Techniques and Tools
- **Manual Testing**: User interface testing.
- **Automated Testing**: Selenium (web) and Appium (mobile).
- **Load Testing**: JMeter for traffic simulation.

### Constraints
- Limited availability of test devices.
- Testing period bound by project deadlines.

---

## Item Pass/Fail Criteria
Each item will pass if:
- It meets functional requirements.
- No critical defects (e.g., crashes or data loss) are found.
- Performance and usability requirements are met.

---

## Suspension Criteria and Resumption Requirements
Testing will be suspended if:
- Critical blockers (e.g., app crashes) are encountered.
- Resources (e.g., devices) are unavailable.
Testing resumes once blockers are resolved or resources become available.

---

## Test Deliverables

### Deliverables
- **Test Plan**: This document.
- **Test Cases**: Detailed cases for each feature.
- **Test Summary Reports**: Results of test execution.
- **Defect Logs**: List of identified issues.

### Test Input/Output
- **Input**: Test cases and scripts.
- **Output**: Logs and test results.

---

## Testing Tasks
- Prepare testing environments.
- Develop and execute test cases.
- Log defects and track resolutions.
- Summarize results in final reports.

---

## Environmental Needs
- **Hardware**: Android/iOS devices, testing machines.
- **Software**: Duolingo app, Selenium, Appium, JMeter.
- **Web Browsers**: Chrome, Firefox, Safari, Edge.

---

## Staffing and Training Needs
- Skilled QA engineers with mobile and web testing experience.
- Onboarding for testing tools and automation frameworks.

---

## Schedule

### Estimated Durations
- Test case development: **10 days**.
- Test execution: **5 days**.
- Defect resolution: **Ongoing**.

### Key Dates
- Resource allocation begins: **December 1, 2024**.

---

## Risks and Contingencies
- **Risk**: Limited device availability.
- **Mitigation**: Use emulators or procure additional devices.

---

# BDD Test Cases for Duolingo

## Scenario 1: User Completes a Lesson and Earns XP

### Gherkin
```gherkin
Given the user has completed a lesson  
When the user finishes the last exercise  
Then the user should complete the lesson successfully  
And the progress bar should be at 100%  
And the user should earn XP points  
```

### Chai Test
```javascript
it('should complete the lesson successfully and earn XP points', () => {
  expect(this.lessonCompleted).to.be.true; // Verify lesson completion.
  expect(this.progressBarValue).to.equal(100); // Progress bar at 100%.
  expect(this.XP).to.be.above(0); // User earns XP.
});
```

---

## Scenario 2: User Earns a Streak After Consecutive Days

### Gherkin
```gherkin
Given the user has logged into Duolingo  
And the user has completed lessons for 5 consecutive days  
When the user logs in on the 6th day  
Then the user should see a streak badge  
And the streak should show 6 days  
```

### Chai Test
```javascript
it('should earn a streak after consecutive days of learning', () => {
  expect(this.streakDays).to.equal(6); // Streak shows 6 days.
  expect(this.hasStreakBadge).to.be.true; // Streak badge is displayed.
});
```
