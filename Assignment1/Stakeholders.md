# Stakeholders

This document outlines the key stakeholders involved in the Duolingo project. Stakeholders include individuals, groups, and organizations that are affected by or have an interest in the success of this project.

---

## Stakeholder Groups

### 1. Project Team

| Key Stakeholders             | Role                                                          | Responsibilities                                                                    | Impact                                                              | Qualifications                                                     |
|-------------------------------|--------------------------------------------------------------|------------------------------------------------------------------------------------|--------------------------------------------------------------------|--------------------------------------------------------------------|
| The Development Team          | Responsible for coding, testing, and implementing the platform. | - Developing and maintaining the Duolingo application.<br>- Implementing new features and updates.<br>- Conducting thorough testing to ensure a high-quality user experience. | Drive innovation and ensure technical quality of the platform.      | Experts in computer science and software development with experience in building scalable systems. |
| Project Manager               | Oversees project timeline and execution.                     | - Managing project tasks and assignments.<br>- Ensuring adherence to schedule and scope.<br>- Main contact for project-related communication and coordination. | Ensure successful delivery of the project within time and scope.    | Experienced in project management, skilled in agile methodologies and tools. |
| Content Moderators            | Monitor and moderate user-generated content on the platform. | - Reviewing flagged content for inappropriate behavior.<br>- Enforcing platform policies.<br>- Reporting on abuse incidents.<br>- Collaborating with developers on detecting abuse patterns. | Ensure a safe and respectful community environment on the platform. | Experience in online community moderation, familiarity with content guidelines and abuse prevention. |
| Customer Support Team         | Assist users with troubleshooting and queries.               | - Responding to user queries and resolving platform-related issues.<br>- Handling account problems.<br>- Providing technical and customer support. | Enhance user satisfaction and retention through efficient support.  | Skilled in customer service and technical troubleshooting.         |
| Data Analysts                 | Analyze platform data to derive insights.                   | - Generating reports.<br>- Interpreting user behavior.<br>- Recommending platform improvements. | Improve the learning experience and optimize platform performance.  | Experts in data analysis and statistics, with proficiency in analytics tools. |
| Administrators                | Manage platform settings and user access.                   | - Performing administrative tasks.<br>- Managing user roles.<br>- Ensuring platform stability and security. | Maintain platform integrity and operational efficiency.             | Experienced in administrative management and IT operations.        |

---

### 2. Product Stakeholders

| Key Stakeholders             | Role                                                          | Responsibilities                                                                    | Impact                                                              | Qualifications                                                     |
|-------------------------------|--------------------------------------------------------------|------------------------------------------------------------------------------------|--------------------------------------------------------------------|--------------------------------------------------------------------|
| Learners                     | Use the platform to learn languages.                        | - Engaging with lessons and games.<br>- Tracking progress and milestones.<br>- Providing feedback to improve user experience. | Core users driving platform engagement and content relevance.       | Diverse backgrounds and proficiency levels in language learning.   |
| Language Experts             | Plan and review course structures and content.               | - Designing course plans and identifying improvement areas.<br>- Reporting necessary changes to Educational Content Developers.<br>- Ensuring cultural and linguistic accuracy in courses. | Enhance the structure and authenticity of language-learning courses. | Professionals with academic or native proficiency in multiple languages. |
| Educational Content Developers | Develop and modify course materials.                        | - Creating and updating educational content.<br>- Incorporating feedback from Language Experts.<br>- Ensuring consistency and engagement in course delivery. | Improve the quality and effectiveness of language-learning materials. | Educators, linguists, or instructional designers with expertise in content development. |

---

### 3. External Stakeholders

| Key Stakeholders             | Role                                                          | Responsibilities                                                                    | Impact                                                              | Qualifications                                                     |
|-------------------------------|--------------------------------------------------------------|------------------------------------------------------------------------------------|--------------------------------------------------------------------|--------------------------------------------------------------------|
| Educational Institutions      | Schools and universities utilizing the platform.             | - Integrating Duolingo into their curriculum.<br>- Providing feedback on educational effectiveness.<br>- Collaborating on research and development. | Contribute to the platform's educational credibility and adoption. | Established institutions with expertise in pedagogy and curriculum design. |
| Investors or Sponsors         | Provide financial support.                                   | - Offering funding or resources in exchange for revenue share or partnership benefits.<br>- Supporting marketing and expansion efforts. | Enable scalability and provide resources for expansion.            | Individuals or organizations with expertise in ed-tech investments and partnerships. |
| Developers Community          | Contribute to open-source enhancements.                     | - Providing code enhancements, bug fixes, and feedback.<br>- Engaging with the community for collaborative development. | Support platform innovation and improve code quality.              | Skilled developers passionate about contributing to ed-tech solutions. |

---

### 4. Regulatory Stakeholders

| Key Stakeholders             | Role                                                          | Responsibilities                                                                    | Impact                                                              | Qualifications                                                     |
|-------------------------------|--------------------------------------------------------------|------------------------------------------------------------------------------------|--------------------------------------------------------------------|--------------------------------------------------------------------|
| Data Privacy and Security Authorities | Ensure compliance with data privacy laws.                  | - Overseeing adherence to global/regional data privacy regulations (e.g., GDPR).<br>- Ensuring the security and privacy of user data. | Ensure legal compliance and build user trust by protecting data.   | Accredited agencies specializing in data protection and privacy laws. |
| Language Regulatory Bodies   | Standardize language learning content.                        | - Monitoring adherence to language guidelines and norms.<br>- Ensuring that courses align with recognized language standards.<br>- Validating the accuracy of language content. | Enhance credibility and maintain high linguistic standards.         | Renowned institutions or boards specializing in language regulation and education. |

---

## User Personas

To better understand the diverse learner base, refer to the following user personas:  
1. [Beginner Learners: Shreya Singh](../Assignment1/Personas.md#beginner-learner-persona)  
2. [Intermediate Learners: Vishal Mane](../Assignment1/Personas.md#intermediate-learner-persona)   
3. [Advanced Learners: Geetanjali Gada](../Assignment1/Personas.md#advanced-learner-persona)  
4. [Casual Learners: Vijay Chandrashekhar](../Assignment1/Personas.md#casual-learner-persona)  

---

### Production Login Users

The following stakeholders require login access to the platform to perform their respective roles effectively:  

| **Stakeholder**      | **Degree of Privilege**                      | **Rights and Access**                                                                                  |
|-----------------------|---------------------------------------------|--------------------------------------------------------------------------------------------------------|
| **Development Team**  | High                                        | - Access to production environments.<br>- Manage server settings and infrastructure.<br>- Resolve technical issues and deploy updates. |
| **Content Moderators**| Limited to content moderation tools         | - Review and act on flagged content.<br>- Enforce community guidelines.<br>- Report abuse incidents.<br>- No access to sensitive user data or server configurations. |
| **Learners**          | User-level                                  | - Access lessons, progress tracking, and achievements.<br>- Save and retrieve personal learning data.<br>- Customize learning preferences. |
| **Language Experts**           | Limited to planning and review tools          | - Design course structures and recommend improvements.<br>- Identify and report issues to Educational Content Developers.<br>- Ensure cultural and linguistic accuracy in courses.<br>- No access to content modification or administrative tools. |
| **Educational Content Developers** | Full access to content creation tools         | - Develop, modify, and localize course content.<br>- Implement feedback from Language Experts.<br>- Ensure consistency and engagement in course delivery.<br>- No access to administrative or user data. |
| **Customer Support Team** | Moderate                                 | - Access to user accounts for troubleshooting.<br>- View platform logs for issue resolution.<br>- Restricted from accessing financial data or sensitive personal information. |
| **Marketing Team**    | Moderate                                    | - Access analytics dashboards for campaign performance.<br>- Manage user engagement and acquisition strategies.<br>- No access to user-specific personal data. |
| **Data Analysts**     | Moderate                                    | - Generate and view aggregate reports.<br>- Analyze platform usage trends and user behavior.<br>- No ability to modify platform content or settings. |
| **Administrators**    | Highest                                     | - Manage platform settings and configurations.<br>- Assign or revoke user roles.<br>- Oversee security, data protection, and overall operations.<br>- Access all application areas, including sensitive user and system data. |


---

# Stakeholder Map

## Visual Representation

![image](https://github.com/user-attachments/assets/1bdc9299-5388-4cea-a9d9-ca8e57e1a59f)

## PlantUML Source

```plantuml
@startuml StakeholderMap

actor "Learners" as Learners
actor "Language Experts" as LanguageExperts
actor "Educational Content Developers" as ContentDevelopers
actor "Educational Institutions" as EduInstitutions
actor "Investors or Sponsors" as Investors
actor "Developers Community" as DevCommunity
actor "Data Privacy Authorities" as PrivacyAuthorities
actor "Language Regulatory Bodies" as RegulatoryBodies

package "Project Team" {
  actor "Development Team" as DevTeam
  actor "Project Manager" as ProjectManager
  actor "Content Moderators" as Moderators
  actor "Customer Support Team" as SupportTeam
  actor "Data Analysts" as DataAnalysts
  actor "Administrators" as Admins
}

Learners --> Moderators : Report Content
Learners --> SupportTeam : Request Support
Learners --> DataAnalysts : Provide Usage Data
LanguageExperts --> ContentDevelopers : Provide Course Plans & Feedback
ContentDevelopers --> DevTeam : Collaborate on Feature Implementation
ContentDevelopers --> Admins : Implement Course Updates
EduInstitutions --> ProjectManager : Provide Feedback
EduInstitutions --> DataAnalysts : Request Performance Reports
Investors --> ProjectManager : Fund the Project
DevCommunity --> DevTeam : Contribute Code and Ideas
PrivacyAuthorities --> Admins : Ensure Data Compliance
RegulatoryBodies --> LanguageExperts : Validate Language Standards
RegulatoryBodies --> DevTeam : Validate Compliance

@enduml

