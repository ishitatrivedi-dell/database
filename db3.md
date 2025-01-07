# ASSIGNMENT 12

1) TO ADD MORE STUDENTS 
db.students.insertMany([
  {
    name: "Aarav Sharma",
    rollNumber: "B123001",
    courses: ["Data Structures", "Algorithms", "Web Development"]
  },
  {
    name: "Isha Verma",
    rollNumber: "B123002",
    courses: ["Database Systems", "Operating Systems", "ReactJS"]
  },
  {
    name: "Rohan Mehta",
    rollNumber: "B123003",
    courses: ["Machine Learning", "Artificial Intelligence", "Python Programming"]
  },
  {
    name: "Ananya Kapoor",
    rollNumber: "B123004",
    courses: ["Cloud Computing", "Cybersecurity", "Big Data"]
  },
  {
    name: "Karthik Iyer",
    rollNumber: "B123005",
    courses: ["Blockchain", "Internet of Things", "C++ Programming"]
  }
]);
 

 2) db.createCollection("courses");

     db.courses.insertOne({})

3) Fetch a specific student's record by roll number


db.students.find({ rollNumber: "CS1002" });



Task 4: Query all students who are enrolled in a particular course

db.students.find({ coursesEnrolled: "MATH101" });


Task 5: Update a student's courses

db.students.updateOne(
  { rollNumber: "CS1001" },
  { $push: { coursesEnrolled: "CS202" } }
);


Task 6: Remove a course from a student's courses list

db.students.updateOne(
  { name: "Mahir" },
  { $pull: { coursesEnrolled: "MATH101" } }
);


Task 7: Find all courses with 3 credits

db.courses.find({ credits: 3 });
This will return all courses where the credits field equals 3.

Task 8: Find students who have enrolled in more than 2 courses

db.students.find({ "coursesEnrolled.2": { $exists: true } });

The $exists: true query checks if the third element (index 2) exists in the coursesEnrolled array, implying the student has more than 2 courses.

Task 9: Use the $in operator to find students enrolled in multiple courses

db.students.find({ coursesEnrolled: { $in: ["CS101", "MATH202"] } });


Task 10: Fetch all students from a specific department (e.g., CSE)

db.students.find({ department: "CSE" });

Task 11: Query students who are in their 3rd year

db.students.find({ year: 3 });

Task 12: Query students using a range for their year

db.students.find({ year: { $gte: 2, $lte: 3 } });

Task 13: Count the total number of students in each department

db.students.aggregate([
  {
    $group: {
      _id: "$department",     // Group by the 'department' field
      count: { $sum: 1 }      // Count how many students are in each department
    }
  }
]);


Task 14: Group courses by credits

db.courses.aggregate([
  {
    $group: {
      _id: "$credits",     // Group by the 'credits' field
      count: { $sum: 1 }    // Count how many courses there are for each credit value
    }
  }
]);

Task 15: finding the highest credit course 

db.courses.find().sort({ credits: 1 });

Task 16: Use the $and operator for filtering students

db.students.find({
  
  $and:
   [
    { department: "CSE" },  
    // Condition 1: Department is CSE
    
    { $expr: { $gt: [{ $size: "$coursesEnrolled" }, 2] } }  // Condition 2: More than 2 courses
  ]

});

Task 17 : 