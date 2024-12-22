**[← Back](./README.md)**
# Documentation for the БАРС Electronic Journal System

## Description
The БАРС electronic journal system is designed to automate the process of maintaining educational documentation in schools. It allows teachers, students, parents, and administrators to track academic performance, attendance, homework, and other important aspects of the learning process.

## Data Structure

### 1. Users
The system supports multiple types of users:
- **Teacher** — has access to journals, homework, grades, and schedules.
- **Students** — can view their grades, attendance, and assignments.
- **Parents** — can monitor their children's performance.
- **Administrators** — manage the system and users.

### 2. Database Tables

#### 2.1. `user` Table (Users)
Stores information about the system users:
- `id`: User identifier.
- `first_name`: First name.
- `last_name`: Last name.
- `gender`: Gender.
- `birth_date`: Date of birth.
- `email`: Email address.
- `password`: Password.
- `role_id`: User role (link to the `role` table).

#### 2.2. `role` Table (Roles)
Contains user roles:
- `id`: Role identifier.
- `name`: Role name (e.g., "Teacher", "Student", "Parent", "Administrator").

#### 2.3. `subject` Table (Subjects)
Contains information about subjects:
- `id`: Subject identifier.
- `title`: Subject name.
- `description`: Subject description.
- `teacher_id`: Teacher identifier (link to the `user` table).
- `credit_hours`: Number of academic hours.

#### 2.4. `lesson` Table (Lessons)
Contains information about lessons:
- `id`: Lesson identifier.
- `subject_id`: Subject (link to the `subject` table).
- `class_id`: Class (link to the `schoolClass` table).
- `quarter_id`: Quarter (link to the `quarter` table).
- `date`: Lesson date.

#### 2.5. `attendance` Table (Attendance)
Tracks student attendance for lessons:
- `id`: Record identifier.
- `lesson_id`: Lesson (link to the `lesson` table).
- `student_id`: Student (link to the `user` table).
- `status`: Attendance status (e.g., "Present", "Absent").

#### 2.6. `grade` Table (Grades)
Contains student grades:
- `id`: Record identifier.
- `lesson_id`: Lesson (link to the `lesson` table).
- `student_id`: Student (link to the `user` table).
- `grade`: Grade.

#### 2.7. `homework` Table (Homework)
Contains information about homework assignments:
- `id`: Assignment identifier.
- `subject_id`: Subject (link to the `subject` table).
- `teacher_id`: Teacher (link to the `user` table).
- `description`: Assignment description.
- `due_date`: Due date.

### 3. REST API

#### 3.1. Authentication and Authorization
JWT tokens are used for system access.

##### 3.1.1. User Registration
**POST** `/api/auth/register`
- **Request Parameters**:
  - `first_name`: User's first name.
  - `last_name`: User's last name.
  - `email`: User's email address.
  - `password`: User's password.
- **Response**:
  - Status 200: Successful registration.

##### 3.1.2. User Login
**POST** `/api/auth/login`
- **Request Parameters**:
  - `email`: User's email address.
  - `password`: User's password.
- **Response**:
  - Status 200: Returns JWT token.

#### 3.2. Journal Management

##### 3.2.1. Get All Lessons for a Class
**GET** `/api/classes/{classId}/lessons`
- **Response**:
  - Status 200: List of lessons for the specified class.

##### 3.2.2. Add Grade
**POST** `/api/grades`
- **Request Parameters**:
  - `lesson_id`: Lesson identifier.
  - `student_id`: Student identifier.
  - `grade`: Grade.

#### 3.3. Attendance Management

##### 3.3.1. Get Attendance for a Lesson
**GET** `/api/attendance/{lessonId}`
- **Response**:
  - Status 200: List of attendance for the specified lesson.

##### 3.3.2. Add Attendance
**POST** `/api/attendance`
- **Request Parameters**:
  - `lesson_id`: Lesson identifier.
  - `student_id`: Student identifier.
  - `status`: Attendance status ("Present", "Absent").

## Dependencies and Technologies
- **Spring Boot** — the core technology for building the REST API.
- **JWT** — for authentication and authorization.
- **Liquibase** — for database migrations.
- **PostgreSQL** — database.

## Deployment
1. Clone the repository.
2. Configure database connection settings in `application.properties`.
3. Run the application using the following commands:
   - `./gradlew bootRun` (for Linux/macOS)
   - `gradlew bootRun` (for Windows)

## Roles and Authorization
The system supports user roles, each with specific privileges:
- **Administrator** — manages all aspects of the system.
- **Teacher** — manages subjects, lessons, grades, and homework assignments.
- **Student** — can view their grades, attendance, and assignments.
- **Parent** — can track their children's performance.

## Conclusion
The БАРС electronic journal provides an efficient interface for managing educational documentation in schools, offering various levels of access for system users.
