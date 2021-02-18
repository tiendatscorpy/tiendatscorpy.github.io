# SQL University Database

This is a SQL Capstone project for my Aalto course **CS-A1153 Databases**, during which I designed a database for a university.The database contains information about courses, rooms, room reservations and enrollments.

## Task
- Draw an UML diagram based on the information in the following sections.
- Convert the UML diagram to the relational data model. Present the schemas of the relations and underline the attributes which form the key for each relation.
- Provides functional dependencies, form of redundancy.
- Provides SQL statements for multiple tasks.

## UML and relational schema

<img src="../images/UML_university.png?raw=true"/>

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

## Justification of Database Design

### Course + Course Instance
The Course has the CourseCode as the primary key, and other foreign keys are Name and Credits. A course could have multiple instances. Each instance is different from each other through the time when the course is organized, that a course can be organized either in the same semester or in different semesters. A course may have lectures, exercise groups, and exams. Through the CourseInstanceID, it allows the student to query in the database and get information about the time of the Lecture and Exercise Groups. It is possible to query about exams of a certain course through the primary key CourseCode of the Course class.

### Student
The student has the student ID as the primary key and other foreign keys, including Name, DateOfBirth, DegreeProgram, StartYear, ExpirationDate. Through the Student ID, it allows for the teacher/teaching assistant to perform the querying operations for various purposes. For example: checking how many and who attends a specific exercise session, who registers for the lecture. 

### Building
The Building has 3 attributes (BuildingID, Name, StreetAddress), with BuildingID being the primary key. The university has several buildings, each of them contains rooms for teaching purposes (like lecture halls and classrooms). For each building, the database contains information about its name and street address through the corresponding attribute, and also it is possible to know which rooms are located in a certain building through querying using the BuildingID attribute. 

### Room 
The Room has its ID as the primary key and other foreign keys are the BuildingID, Number ofSeats, NumberOfExamSeats(it could be lesser because the students cannot sit too near each other in the exam). RoomID allows users to make queries about which rooms are currently being reserved, the Start Time and End Time of the reservation. A room can be used for either a lecture, an exercise session, or an exam. Room table has a one-to-one relationship with Reservation, where one Reservation record can only belong to one Room, and one Room can have only one Reservation at one time.

### Reservation
In the Reservation, it has its ReservationID as its primary key, and other attributes, including the RoomID, StartTime, EndTime, Date. The StartTime and EndTime attribute allow the user to know the length of the reservation, so he/she could make the reservation at another vacant time. Reservation table has a one-to-many relationship with the Event table, where an Event record can only belong to one Reservation, but one Reservation can have multiple events happening at the same time. This enables the possibility of having multiple exams in the same room.

### Equipment
The Room has the One-To-Many aggregation relationship with the Equipment, that one room could have many pieces of equipment inside the room (like a video projector, a computer for the teacher, a document camera, computers for students, etc.). Each Equipment has the EquipmentID as its primary key,and other attributes such as RoomID, Name, Type, AccessibleBy.


### Event
Event class has subclasses for different types of events: Lecture, Exam, ExerciseSession. The Event class has a composite key, consisting of Type and ForeignID. Type field is either of “Exam”, “Lecture”, or “ExerciseSession”, and ForeignID is the foreign key of the aforementioned field. This means, if Type is “Exam” and ForeignID is 2, this record has a subclass record in the Exam table and its ID is 2.
The inheritance design allows for the reservations to be booked by multiple event classes. In the first iteration, we had 3 fields in the Reservation table, one for ExamID, one for LectureID and one for ExerciseSessionID. But this poses 2 problems:
This doesn’t allow multiple exams happening in the same room, since the ExamID field can only hold one value.
If you want to add another table that can make a Reservation, we would need to add a field containing its foreign key to the Reservation table. This becomes more complicated when more event types are added to the database.
The Event table has a one-to-many relationship to the Reservation table, where an event can only belong to one Reservation, and a Reservation can have multiple events at the same time. As mentioned earlier, this allows for multiple exams in the same room.


### Exam
The Exam has examID as the primary key and CourseCode as a foreign key to the one table Courses. The exam date and time are inherited from the superclass Event.
Exam class has a one-to-many relationship with the Course table. An exam can only belong to one Course, while a Course can have multiple Exam records.

### Lecture
The Lecture has 2 attributes, LectureID and CourseInstanceID, with LectureID being the primary key.  A lecture belongs to a certain Course instance and it is possible to find the course in question by the foreign key, CourseInstanceID, in the table. Similar to the Exam table, Lecture inherits its date and time from the Event super class.

### Exercise Group
The Exercise Group has its ID as the primary key and a foreign key: CourseInstanceID. The Limitation attribute allows the teaching assistant / student to see how many students have enrolled in an exercise group so far, and also the database could take into account its value to prevent more students from enrolling if it has reached its limit. 

### Exercise Session
Exercise Session has a primary key in ExerciseSessionID and a foreign key in ExerciseGroupID. Exercise Session also inherits its date and time from Event. Exercise Session class has a one-to-many relationship with the Exercise Group table. A session can only belong to one exercise group, while a group can have multiple sessions.

