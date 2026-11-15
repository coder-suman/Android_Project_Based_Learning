<div align="center">

<img src="App_logo/eduquiz.png" alt="EduQuiz Logo" width="140"/>

# EduQuiz

### Learn • Attempt • Improve

An Android quiz application with a **Student Panel** and an **Admin Panel**, powered by Firebase.

![Platform](https://img.shields.io/badge/Platform-Android-3DDC84?logo=android&logoColor=white)
![Language](https://img.shields.io/badge/Language-Java-ED8B00?logo=openjdk&logoColor=white)
![Backend](https://img.shields.io/badge/Backend-Firebase-FFCA28?logo=firebase&logoColor=black)
![Min SDK](https://img.shields.io/badge/minSdk-24-blue)
![Target SDK](https://img.shields.io/badge/targetSdk-34-blue)

</div>

---

## Table of Contents

- [About the Project](#about-the-project)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [App Screens and Flow](#app-screens-and-flow)
- [Database Structure](#database-structure)
- [System Diagrams](#system-diagrams)
- [Getting Started](#getting-started)
- [Firebase Security Rules](#firebase-security-rules)
- [Future Enhancements](#future-enhancements)
- [Team](#team)
- [Documentation](#documentation)

---

## About the Project

**EduQuiz** is an Android application that makes learning through quizzes simple, organised and measurable. Traditional practice tests are slow to prepare, slow to check and hard to track. EduQuiz brings the whole cycle into one cloud-backed app.

It provides two separate experiences:

- **Student Panel**: learners attempt subject-wise or random quizzes and track their progress.
- **Admin Panel**: authorised administrators create subjects, build and publish quizzes, and review student feedback.

A published quiz becomes available to students immediately.

This project was developed as part of the **Master of Computer Application (MCA)** programme, Department of Computational Sciences, **Brainware University**.

---

## Features

### Student Panel

- Secure registration and login (Firebase Authentication)
- Browse and search subjects
- Read quiz instructions before starting
- Multiple-choice questions with an optional **countdown timer**
- Selected answers are retained while moving between questions
- Automatic submission when time expires
- Instant result: score, correct and wrong answers, and percentage
- **Random Quiz**: a mixed quiz picked randomly from published questions across all subjects
- **Performance dashboard**: overall accuracy, subject-wise accuracy, total attempts and quiz history
- **Study streak** of consecutive active days
- Profile screen and feedback submission

### Admin Panel

- Protected admin login
- Dashboard showing the total number of registered students
- Add subjects
- Create quizzes and add questions (four options and one correct answer)
- Preview a quiz and **publish** it only when it is complete
- Edit or delete subjects and quizzes (Manage Content)
- Read student feedback

---

## Tech Stack

| Category | Technology |
|---|---|
| Language | Java 8 |
| UI | XML layouts, Material Components, ConstraintLayout, RecyclerView, CardView |
| IDE | Android Studio |
| Build System | Gradle (Kotlin DSL), Version Catalog (`libs.versions.toml`) |
| Authentication | Firebase Authentication |
| Database | Firebase Realtime Database |
| Monitoring | Firebase Crashlytics plugin |
| Testing | JUnit 4, AndroidX Test, Espresso |

**Build configuration**

| Setting | Value |
|---|---|
| Application ID | `com.example.eduquiz` |
| Min SDK | 24 (Android 7.0) |
| Target / Compile SDK | 34 |
| Version | 1.0 (code 1) |
| Android Gradle Plugin | 8.5.2 |
| Firebase BoM | 34.2.0 |
| View Binding | Enabled |

---

## Project Structure

```
Android_Project_Based_Learning/
├── App_logo/                     # App logo
├── All_Diagram/                  # DFD, ER, Class, Use Case and System Flow diagrams (PDF)
├── documentation/
│   └── EduQuiz-documentation.pdf # Full project report
├── Output/
│   └── Database_ouput_json.json  # Sample exported Firebase database output
└── EduQuiz/                      # Android Studio project
    ├── database-seed.json        # Sample data to import into Firebase
    ├── database.rules.json       # Firebase Realtime Database security rules
    └── app/
        ├── google-services.json  # Firebase config
        └── src/main/
            ├── AndroidManifest.xml
            ├── java/com/example/eduquiz/
            │   ├── splashscreenActivity.java   # Launcher screen
            │   ├── MainActivity.java           # Student home
            │   ├── userDetails/    # Login, Register, Profile, Feedback, Admin login
            │   ├── quiz/           # QuizList, Instructions, Quiz, Result, Random, Performance
            │   ├── admin/          # Dashboard, AddSubject, AddQuiz, AddQuestions, Publish,
            │   │                   # ManageContent, AdminFeedback
            │   ├── models/         # User, Admin, Subject, Quiz, Section, Question,
            │   │                   # QuizAttempt, FeedbackModel
            │   ├── adapters/       # Subject, Quiz, Section, Performance adapters
            │   └── utils/          # FirebaseHelper, TestActivity
            └── res/                # Layouts, drawables, fonts, strings, themes
```

---

## App Screens and Flow

**Student flow**

```
Splash → Login / Register → Home (Subjects) → Quiz List → Instructions
       → Quiz (timer) → Result → Performance
                      ↳ Random Quiz, Feedback, Profile
```

**Admin flow**

```
Splash → Admin Login → Admin Dashboard
       → Add Subject → Add Quiz → Add Questions → Publish Quiz
       → Manage Content (edit / delete)
       → Student Feedback
```

---

## Database Structure

EduQuiz uses Firebase Realtime Database with the following top-level nodes:

| Node | Description |
|---|---|
| `users` | Student profiles and stats (`totalAttempts`, `totalCorrect`, `totalWrong`, `streak`, `lastActiveDate`) |
| `admins` | Admin accounts with `role: admin` |
| `subjects` | Subject details (`name`, `description`, `icon`, `quizCount`, `questionCount`) |
| `quizzes` | Quiz details (`subjectId`, `title`, `totalQuestions`, `timeLimitMinutes`, `published`, `createdAt`) |
| `questions` | Questions with `optionA`–`optionD` and `correctAnswer` (1 = A, 2 = B, 3 = C, 4 = D) |
| `attempts` | Per-user quiz attempts (`score`, `scorePercentage`, `correctAnswers`, `quizId`, `dateString`) |
| `feedback` | Feedback submitted by students |

**Sample seed data** (`EduQuiz/database-seed.json`) includes four subjects: Mathematics, Science, Computer Science and History.

---

## System Diagrams

All planning diagrams are in the [`All_Diagram`](All_Diagram) folder:

| Diagram | File |
|---|---|
| Level 0 DFD | [Level_0_Diagram.pdf](All_Diagram/Level_0_Diagram.pdf) |
| Class Diagram | [Class_Diagram.pdf](All_Diagram/Class_Diagram.pdf) |
| Student Use Case | [Student_usecase_Diagram.pdf](All_Diagram/Student_usecase_Diagram.pdf) |
| Admin Use Case | [Admin_usecase_Diagram.pdf](All_Diagram/Admin_usecase_Diagram.pdf) |
| Student ER Diagram | [Student_ER_Diagram.pdf](All_Diagram/Student_ER_Diagram.pdf) |
| Admin ER Diagram | [Admin_ER_Diagram.pdf](All_Diagram/Admin_ER_Diagram.pdf) |
| Student System Flow | [Student_System_flow_Diagram.pdf](All_Diagram/Student_System_flow_Diagram.pdf) |
| Admin System Flow | [Admin_System_flow_diagram.pdf](All_Diagram/Admin_System_flow_diagram.pdf) |

---

## Getting Started

### Prerequisites

- [Android Studio](https://developer.android.com/studio) (recent version supporting AGP 8.5.2)
- JDK 8 or higher
- An Android device or emulator running Android 7.0 (API 24) or above
- A Google account for Firebase

### Installation

1. **Clone the repository**

   ```bash
   git clone https://github.com/coder-suman/Android_Project_Based_Learning.git
   ```

2. **Open the project**

   Open the `EduQuiz` folder in Android Studio and let Gradle sync.

3. **Set up your own Firebase project** (recommended)

   - Go to the [Firebase Console](https://console.firebase.google.com/) and create a project.
   - Add an Android app with package name `com.example.eduquiz`.
   - Download `google-services.json` and replace the file at `EduQuiz/app/google-services.json`.
   - Enable **Authentication → Email/Password**.
   - Create a **Realtime Database**.

4. **Import sample data (optional)**

   In Realtime Database, use **Import JSON** and select `EduQuiz/database-seed.json`.

5. **Apply security rules**

   Copy the contents of `EduQuiz/database.rules.json` into the **Rules** tab of your Realtime Database.

6. **Create an admin account**

   Register a user in Firebase Authentication, then add an entry under the `admins` node using that user's UID:

   ```json
   "admins": {
     "<USER_UID>": {
       "name": "Admin Name",
       "email": "admin@example.com",
       "role": "admin"
     }
   }
   ```

7. **Run the app** on an emulator or device.

---

## Firebase Security Rules

The rules in `EduQuiz/database.rules.json` follow these principles:

- All reads require authentication.
- A user can write only to their own `users/<uid>` record.
- A user can read and write only their own `attempts/<uid>` records.
- Content nodes (`subjects`, `quizzes`, `questions`) and `feedback` require authentication to write.

> **Note:** Admin-only write protection is currently enforced in the app flow. For production use, tighten the rules so that only UIDs listed under `admins` can write content.

---

## Future Enhancements

- Server-side protection of answers
- Leaderboards
- Richer question types
- Advanced analytics

---

## Team

Brainware University, Department of Computational Sciences, MCA (2026)

| Name | Roll Number | Registration No. |
|---|---|---|
| Kuntal Bera | 25102410031 | BWU/MCA/25/037 |
| Suman Bajani | 25102410033 | BWU/MCA/25/039 |
| Jinat Yeasmin | 25102410036 | BWU/MCA/25/042 |

**Project Guide:** Professor Samrat Kundu

---

## Documentation

The complete project report (introduction, objectives, analysis, design, implementation and testing) is available here:

📄 [EduQuiz-documentation.pdf](documentation/EduQuiz-documentation.pdf)

---

<div align="center">

Made with ❤️ using Java and Firebase

</div>
