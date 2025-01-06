# ASSIGNMENT 9

1) creating a database called Codinggita

2) adding two collections {students , courses}

3) inserting student data with Name, roll number, department, year, courses enrolled
* db.students.insertMany

([
  { 
    "name": "Jenil",
    "rollNumber": 101,
    "department": "Computer Science",
    "year": 2,
    "coursesEnrolled": ["CS101", "CS102"]
  },

  { 
    "name": "Mahir",
    "rollNumber": 102,
    "department": "Computer Science",
    "year": 2,
    "coursesEnrolled": ["CS101", "CS103"]
  },
  
  { 
    "name": "Arjun",
    "rollNumber": 103,
    "department": "Electrical Engineering",
    "year": 3,
    "coursesEnrolled": ["EE101", "EE102"]
  }
]);

4) courses detail : 
* db.courses.insertMany

([
  { 
    "courseCode": "CS101", 
    "courseName": "Introduction to Programming", 
    "credits": 3, 
    "instructor": "Prof. Sharma" 
  },

  { 
    "courseCode": "CS102", 
    "courseName": "Data Structures", 
    "credits": 3, 
    "instructor": "Prof. Gupta" 
  },

  { 
    "courseCode": "CS103", 
    "courseName": "Algorithms", 
    "credits": 3, 
    "instructor": "Prof. Kapoor" 
  },

  { 
    "courseCode": "EE101", 
    "courseName": "Basic Electrical Engineering", 
    "credits": 4, 
    "instructor": "Prof. Verma" 
  },

  { 
    "courseCode": "EE102", 
    "courseName": "Circuit Theory", 
    "credits": 4, 
    "instructor": "Prof. Yadav" 
  }
]);



# TASK-2 
## CRUD OPERATION 

5) Adding more students data follows the same thing 
db.students.insertMany

([
  { name: "David", rollNumber: 104, department: "Computer Science", year: 2, coursesEnrolled: ["CS101", "CS201"] },


  { name: "Eve", rollNumber: 105, department: "Mechanical", year: 3, coursesEnrolled: ["ME301"] }
]);

6) query data based in students department : 

 * db.students.find({ department : "Computer Science"});

* db.student.find({ year : 4});

* db.students.find({ coursesEnrolled: "CS101" });

7) update data 
 
 * db.courses.updateOne({ name : "Arjun" } , {$set : {"instructor" : "prof.mehta}}
 
    );

8) delete one 

* db.students.deleteOne({ "name": "Arjun" });