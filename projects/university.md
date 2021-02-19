# SQL University Database

This is a SQL Capstone project for my Aalto course **CS-A1153 Databases**, during which I designed a database for a university.The database contains information about courses, rooms, room reservations and enrollments.

[Github](https://github.com/tiendatscorpy/sql-university-database)

## Task
- Draw an UML diagram based on the information in the following sections.
- Convert the UML diagram to the relational data model. Present the schemas of the relations and underline the attributes which form the key for each relation.
- Provides functional dependencies, form of redundancy.
- Provides SQL statements for multiple tasks.

## UML and relational schema

<img src="../images/UML_university.PNG?raw=true"/>

The relational schema is as followed:
- Student (StudentID, Name, DateOfBirth, DegreeProgram, StartYear, 
                     ExpirationDate).
- Event (Type, ForeignID, StartTime, EndTime, Date, ReservationID).
- Course (CourseCode, Name, Credits).
- Course Instance (CourseInstanceID, CourseCode, StartDate, EndDate).
- Exam (ExamID,CourseCode).
- Exam Enrollment (ExamID, StudentID ).
- Lecture (LectureID, CourseInstanceID).
- Exercise group (ExerciseGroupID, CourseInstanceID, Limitation).
- Exercise group Enrollment (ExerciseGroupID, StudentID ).
- Exercise session (ExerciseSessionID, ExerciseGroupID).
- Building (BuildingID, Name, Address).
- Room (RoomID, BuildingID, NumberOfSeats, NumberOfExamSeats).
- Reservation (ReservationID, RoomID, StartTime, EndTime, Date).
- Equipment (EquipmentID, Name, Type, AssessibleBy).

