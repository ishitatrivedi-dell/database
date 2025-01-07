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
db.students.updateMany
(
  { },                 
  { $set: { activeStatus: true } } 
);

**filter()** : an empty filter matches all the documents in the collection 

**$set operater** : Adds the **activeStatus** field to each document and sets its value to true.

task 18 :  renaming 

db.students.updateMany

(
  { coursesEnrolled: { $exists: true } }, // Filter: Match documents where coursesEnrolled exists
  { $rename: { coursesEnrolled: "enrolledCourses" } } // Rename coursesEnrolled to enrolledCourses
);

task 19: setting default value of graduation year 

 db.students.updateMany({}, {$set: {graduationYear: 2025}});

 task 20: Use the $push operator to add a new course to a student’s course list

 db.students.updateOne({name: "Mahir"},
                      {$push :{coursesEnrolled: "CS303"}}
  

)
 task 21:  Use $pull to remove a course from a student's courses list
Remove the course CS101 from Jenil’s list.


db.students.updateOne({name: "Jenil"}, {$pull : {coursesEnrolled: "CS101"}})

task 22: Remove a student from the students collection

db.students.deleteOne({rollNumber: "CS1004"});

task 23 :  Find students who are enrolled in both CS101 and MATH202

db.students.find({
  enrolledCourses: { $all: ["CS101", "MATH202"] }
});

Task 24: Use $regex to search for students whose name starts with "A"
Use regular expressions to search for students whose names begin with the letter "A".


db.students.find({ name : {$regex: "A"}})

task 25: Use $exists to find students with enrolled courses
Query students who have an entry in the coursesEnrolled array.

db.students.find({ coursesEnrolled : {$exists: true}});


Task 26: Add a field to store students' grades for each course
Add a new field grades to the students collection and store an array of grades for each course.

db.students.updateMany({}, {$set : {grades: []}})

{}:

Matches all documents in the students collection.
$set:

Adds a new field grades with an initial value (in this case, an empty array []) to all matched documents.
If the field already exists, it will be overwritten.


task 27 :  Use $elemMatch to query students enrolled in specific courses
Find students enrolled in CS101 and have the grade A.


db.students.find({
  grades: { 
    $elemMatch: { 
      course: "CS101", 
      grade: "A" 
    } 
  }
});

Task 28: Use $size operator to query students with exactly 2 courses enrolled
Query students who have enrolled in exactly two courses.


db.students.find({
  enrolledCourses: { $size: 2 }
});


Task 29: Perform a text search for a course title
Use text indexing to search for the course Digital Electronics in the courses collection.

 -> **first we have to create a new index on the field where the course title is stored** 

 Once the text index is created, you can query the courses collection using the $text operator.

db.courses.find({
  $text: {
    $search: "Digital Electronics"
  }
}); 


Task 30: Create a compound index on department and year

db.students.createIndex({
  department: 1, 
  year: 1       
});


**A compound index on department and year allows efficient queries that involve these two fields.**


db.students.find({
  department: "Computer Science",
  year: 2
});

task 31: Use $sort to order students by their roll number
Sort the students in ascending order of their roll number.

db.students.find({}, { _id: 0 }).sort({ rollNumber: 1 });


Task 32: Create a unique index on the roll number
Create a unique index to ensure that the roll numbers in the students collection are unique.


db.students.createIndex(
  { rollNumber: 1 }, // Field and sort order (ascending)
  { unique: true }   // Ensures uniqueness
);


task 33 : Update the course name in the courses collection
Update the name of the course CS101 to Intro to Programming.


db.courses.updateOne(
  { courseCode: "CS101" }, // Filter: Find the document with courseCode "CS101"
  { $set: { name: "Intro to Programming" } } // Update: Change the course name
);


task 34: Create a backup of the CodingGitaStudents database
Use mongodump to back up the entire CodingGitaStudents database.

``` mongodump --db CodingGitaStudents --out /path/to/backup/directory ```

task 35: Restore the CodingGitaStudents database from the backup
Use mongorestore to restore the database after a backup.

``` mongorestore --db CodingGitaStudents /path/to/backup/directory/CodingGitaStudents ```

task 36 : Use $project to reshape data in aggregation
Project only the name and department of students using an aggregation query.

``` db.students.aggregate([{$project: {name: 1,department:1}}]);```

task 37 : Use $unwind to deconstruct the courses array
Use $unwind to split the coursesEnrolled array into individual documents.

``` db.students.aggregate([{$unwind: "$coursesEnrolled"}]);```

task 38 : Use $limit to retrieve only the first 3 students
Use $limit to limit the result to the first 3 students in the students collection.

```db.students.aggregate([{ $limit: 3 }]);```

task 39 : Use $skip to skip the first 2 students and get the rest
Use $skip to fetch all students except the first two.

```db.students.aggregate([{ $skip: 2 }]);```

task 40 : Use $lookup to join student data with courses
Use $lookup to fetch the course information for students.

db.students.aggregate([
  {
    $lookup: {
      from: "courses",                
      localField: "coursesEnrolled",  
      foreignField: "name",          
      as: "courseDetails"             
    }
  }
]);


task 41 : Create a new collection for storing studentFeedback
Create a collection studentFeedback with fields: studentRollNumber, feedbackText, date.

db.studentFeedback.insertMany([
  {
    studentRollNumber: 101,
    feedbackText: "Great course! Learned a lot about React.",
    date: new Date("2025-01-07")
  },
  {
    studentRollNumber: 102,
    feedbackText: "NodeJS is challenging but interesting.",
    date: new Date("2025-01-06")
  },
  {
    studentRollNumber: 103,
    feedbackText: "The course on MongoDB was very informative.",
    date: new Date("2025-01-05")
  }
]);

task 42: Query the studentFeedback collection to find feedback from a specific student
Use find() to retrieve feedback from Jenil.

```db.studentFeedback.find({ studentRollNumber: 101 });```

task 43: Use $set to update multiple fields at once
Use the $set operator to update the department and coursesEnrolled fields for Arjun.

db.students.updateOne(
  { rollNumber: 103 },  
  { 
    $set: {
      department: "Computer Science",     
      coursesEnrolled: ["React", "NodeJS"]  
    }
  }
);

task 44: Perform a query on nested documents in students collection
Query for students who have grades A in their courses.

``` db.students.createIndex({ coursesEnrolled: 1 });```

```db.students.find({ coursesEnrolled: "React" });```

```db.students.getIndexes();``

task 45 :  Perform a query on nested documents in students collection
Query for students who have grades A in their courses.

db.students.find({
  grades: { 
    $elemMatch: { 
      grade: "A" 
    } 
  }
});










