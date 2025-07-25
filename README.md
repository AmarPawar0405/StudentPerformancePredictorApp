# StudentPerformancePredictorApp
Student Performance Predictor 
 
•	Title 
•	Student Performance Prediction Web Application  
  (Rule-Based Classification , Linear Rgression Based)  
Scope
This project is a web-based application designed to help educators predict student performance using academic data such as attendance, study hours, mock interviews, MCQ test scores, and internal assessments. The system uses machine learning models like Rule-Based Classification, Linear Regression to analyze the data and provide performance predictions. The goal is to identify students who may need academic support early, enabling timely intervention and guidance.

Purpose: 
The purpose of this document is to clearly define the structure and functionality of the Student Performance Prediction Web Application. It describes the overall design, including the system architecture, data flow, user interface, and machine learning components. This document serves as a blueprint for developing the application and helps ensure that all key elements are well understood by both the developer and any reviewers involved in the evaluation process. The goal is to support a smooth implementation and demonstrate a clear understanding of how the system works.
The system evaluates a student's placement preparation level using the following factors:
•	Aptitude and reasoning test score
•	Technical knowledge (coding skills, subject understanding)
•	Communication skills (spoken and written)
•	Participation in group discussions and mock HR rounds
•	Class attendance 
•	Daily study hours and routine discipline
•	Performance in internal tests, MCQs, and mock interviews
Prediction Output Categories
Based on the evaluation, students will be classified into the following categories:
•	Highly Ready – The student is well-prepared for placements and has done well in most of the key areas.

•	Ready – The student is mostly prepared but may still need to improve in a few small areas.

•	Needs Improvement – The student shows average performance and should work more on important skills before placements.

•	Not Ready –The student is currently not prepared for placements and needs to improve in multiple areas
•	.Objectives 
The main objective of this project is to design a web-based application that can help educators predict and understand a student’s academic and placement performance using real data. This will allow institutions to take early action to support students better.
Specifically, the project aims to:
•	Collect student performance data such as attendance, study hours, internal test marks, MCQ scores, and mock interview results.
•	Predict the student’s final academic result using a trained Linear Regression model.
•	Evaluate placement preparation using models like Rule-Based Classification and K-Nearest Neighbors (KNN).
•	Classify students into categories such as Highly Ready, Ready, Needs Improvement, and Not Ready.
•	Help educators easily identify the top-performing students who are ready for placements.
•	Help plan extra training or support for average or struggling students.
•	Store all student and prediction data securely in a MySQL database.
•	Design the system to be scalable and maintainable, so it can grow with future needs. 
Architectural Overview 
A multi-tiered architecture with: 
•	Presentation Layer (HTML/CSS/JS) 
•	Application Layer (Node.js + Express.js) 
•	Data Layer (MySQL Database) 
 
  
•	Description of Architecture 
•	Client-side: HTML/CSS/JavaScript-based UI for form input and result display. 
•	Server-side: Node.js/Express.js handles API requests, logic routing, and connects to ML engine. 
•	Database: Stores student data, prediction inputs, and results (MySQL). 

 
 
Tech Stack 
Layer 	Technology 
Frontend 	EJS Templates,HTML,CSS 
Backend 	Node.js + Express , JAVA
Database 	MySQL / MySQL2
Auth 	JWT + Bcrypt 
Terminal	Nodemon,
  
Folder Structure project-root/ 
├── backend/ 
│   ├── controllers/ 
│   ├── routes/ 
│   ├── models/ 
│   ├── utils/ 
│   │   └── predictor.js 
│   ├── middleware/ 
│   └── app.js 
├── views/               # EJS Templates 
│   ├── dashboard.ejs 
│   ├── profile.ejs 
│   └── shortlist.ejs 
├── public/              # CSS, JS 
├── package.json 
 
Database: 
students 
Column Name 	Data Type 	Constraints 
id 	INT 	PRIMARY KEY, AUTO_INCREMENT 
 
name 	VARCHAR(100) 	
email 	VARCHAR(100) 	NOT NULL UNIQUE 
course_id 	INT 	FOREIGN KEY → courses(id) 
  
 performance_data: 
Column Name 	Data Type 	Constraints 
id 	INT 	PRIMARY KEY, 
AUTO_INCREMENT 
student_id 	INT 	FOREIGN KEY → students(id) 
 
attendance_percentage 	DECIMAL(5,2) 	 
Machine Test 	DECIMAL(5,2) 	
MCQ Test 	DECIMAL(5,2) 	 
 
mock_interview_score 	DECIMAL(5,2) 	 
final_score 	DECIMAL(5,2) 	
  
Predictions: 
Column Name 	Data Type 	Constraints 
id 	INT 	PRIMARY KEY, AUTO_INCREMENT 
student_id 	INT 	FOREIGN KEY → students(id) 
 
readiness_level 	VARCHAR(50) 	 
shortlisted 	BOOLEAN 	
created_at 	TIMESTAMP 	DEFAULT CURRENT_TIMESTAMP 
  
  
courses 
Column Name 	Data Type 	Constraints 
id 	INT 	PRIMARY KEY, AUTO_INCREMENT 
name 	VARCHAR(100) 	UNIQUE 
 
 
 
Tables and Their Relationships 
1.	students 
•	Purpose: Stores basic student details 
•	Primary Key: id 
•	Foreign Key: course_id → courses.id 
•	Fields: name, email, course_id 
  
2.	performance_data 
•	Purpose: Stores performance metrics of each student 
•	Primary Key: id 
•	Foreign Key: student_id → students.id 
•	Fields: attendance_percentage, Machine Test, MCQ Test,mock_interview_score, final_score 
  
3.	predictions 
•	Purpose: Stores predicted readiness of students based on performance 
•	Primary Key: id 
•	Foreign Key: student_id → students.id 
•	Fields: readiness_level, shortlisted, created_at 
  
4.	courses 
•	Purpose: Stores course information 
•	Primary Key: id 
•	Fields: name 
  Entity-Relationship Overview 
•	Each student has multiple academic records. 
•	Each academic record has one prediction result. 
•	Admin can manage all data; optionally users can only view their own entries. 
  
 
API Endpoints (Express): 
Auth 
•	POST /auth/register — Register new user 
•	POST /auth/login — Login & receive JWT 
Students 
•	GET /students — View all students (EJS page) 
•	POST /students — Add new student 
Performance 
•	POST /performance/:id — Submit/update student performance 
•	GET /performance/:id — View performance form 
Prediction 
•	GET /predict/:id — Trigger prediction 
•	GET /shortlist — View all shortlisted students 
  
 
 
  EJS Frontend Pages 
Page 	Description 
dashboard.ejs : Student list with readiness, confidence profile.ejs : 	Input/edit performance scores shortlist.ejs 	View shortlisted students 
  
  Auth Flow (JWT + Bcrypt) 
1.	User registers or logs in via form 
2.	JWT is issued and stored in cookies 
3.	Auth middleware protects student/score routes 
  
Dependencies & Libraries 
Core Server Libraries 
 
Package 	Purpose 
express 	Web framework for Node.js 
ejs 	Template engine for rendering HTML pages 
body-parser 	Parses incoming request bodies 
dotenv 	Load environment variables from .env file 
mysql2 / pg 	MySQL or PostgreSQL database connection 
 
  
Security Consideration 
•	Authentication and Authorization 
•	JWT for secure access (if multi-user) 
•	Passwords hashed using bcrypt 
•	Role-wise access (Admin/Viewer) 

Authentication & Security :
Package 	Purpose 
bcrypt 	Password hashing 
jsonwebtoken 	JWT-based authentication 
cookie-parser 	Parse cookies for session handling 
  
Development Utilities :
Package 	Purpose 
nodemon 	Auto-restarts server on change 
morgan 	HTTP request logger 

 
Project Modules (with User Roles):  

 	Module 
Name 	Purpose 	Features 	User 
Access 	Tables Used 
1 	User 
Management 
Module 	Manage 
student records and 
authentication 	-	Add, edit, delete student 
profiles 
-	View student list with 
filtering 
-	Assign students to courses 	Admin 	students, courses 
2 	Course 
Management 
Module 	Manage academic courses offered 	- Create/edit/delete course records - Assign students to courses 	Admin 	courses 
3 	Performance 
Tracking 
Module 	Track student academic & 
soft skills 
performance 	-	Enter/update performance metrics - View performance dashboards 
-	Upload bulk data 
(CSV/Excel) 	 Admin 
 Student (View only) 	performance
_data, students 
4 	Prediction 
Engine 
Module 	Predict job readiness based on student data 	- Generate predictions - Store suggestions & confidence levels - Trigger ML/rule-based model 	Admin 	predictions, performance
_data, students 
5 	Feedback & Recommend
ation Module 	Provide insights, appreciation, and guidance 	-	View personalized suggestions 
-	Display appreciation 
messages 
-	Show improvement areas 	 Admin 
Student 	predictions 
6 	Shortlisting 
Module 	Identify and filter jobready students 	-	Filter students by 
readiness 
-	Generate reports 	Admin 	predictions, students 
			- View by 
course/readiness level 		
7 	Reporting & 
Dashboard 
Module 	Visualize system-wide data & trends 	- Readiness level stats - Performance summaries - Export reports 
(PDF/Excel) 	Admin 
Student 
(personal dashboard only) 	All 
8 	Admin Panel 
Module 	Central control 
panel for admin operations 	-	Manage users, courses, data 
-	View prediction history 
-	Monitor system logs 	 Admin only 	All 
  
User Roles Summary: 
Role 	Description 
Admin 	Has full control over system data, predictions, and dashboards 
Student 	Can view personal profile, performance, feedback, and readiness status 
  
 Role-Based Access Example: 
Feature 	Admin 	Student 
Edit student data 	 ✅	  ❌
View course-wise performance stats 	 ✅	  ❌
Trigger prediction engine 	 ✅ 	  ❌
View feedback/appreciation 	 ✅ 	  ✅
 
  Exception and Error Handling 
•	Try-Catch Blocks:
All major operations (like saving data or making predictions) are written inside try...catch blocks. If something goes wrong, the error is caught and passed to the next step.

•	Centralized Error Handler:
We have used a single error-handling middleware in Express.js. This helps us manage all kinds of errors (like missing input, database errors, or server errors) from one place.

•	User-Friendly Messages:
Instead of showing technical errors to users, we send simple messages like “Something went wrong” or “Please fill all required fields.”


•	Logging Errors:
Errors are logged in the console so that developers can easily debug and fix issues during development.
ER Diagram

 
 
  
