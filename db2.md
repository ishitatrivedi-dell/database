# ASSIGNMENT - 10 
1) ADD MULTIPLE STUDENTS 
db.students.insertMany

([
 
  { 
    "name": "Jenil",
    "rollNumber": 101,
    "department": "Computer Science",
    "year": 2,
    "subjectsEnrolled": ["React", "NodeJS", "MongoDB"]
  },

  { 
    "name": "Mahir",
    "rollNumber": 102,
    "department": "Computer Science",
    "year": 2,
    "subjectsEnrolled": ["React", "NodeJS"]
  },

  { 
    "name": "Arjun",
    "rollNumber": 103,
    "department": "Electrical Engineering",
    "year": 3,
    "subjectsEnrolled": ["Circuit Theory", "Electrical Machines"]
  },

   { name: "David", 
   rollNumber: 104,
    department: "Computer Science", 
    year: 2, 
    coursesEnrolled: ["CS101", "CS201"] 
    },

  { name: "Eve", 
  rollNumber: 105, 
  department: "Mechanical",
   year: 3, 
   coursesEnrolled: ["ME301"]
    }

]);


2) CREATING SUBJECT COLLECTION BY USING COMMAND : db.createCollection("subjects");

* db.subjects.insertMany([
  
  
  { 
    "subjectName": "React",
    "topics": [
      "JSX", 
      "Components", 
      "State", 
      "Props", 
      "Hooks"
    ]
  },


  { 
    "subjectName": "NodeJS", 
    "topics": [
      "Modules", 
      "Express", 
      "File System", 
      "Asynchronous Programming"
    ]
  },


  { 
    "subjectName": "MongoDB", 
    "topics": [
      "Database Design", 
      "CRUD Operations", 
      "Aggregation", 
      "Indexes"
    ]
  }


]);

* here there is nested document which has a parent document 

3) Query students based on subject enrollment
 

 * db.students.find({ "subjectEnrolled": "nodejs" });

 4) Add a new topic to a subject

 * db.subject.updateOne({"subjectName": "Mongodb"},
 { $push : {"topics" : "chemistry"}});


5) Query subjects with multiple topics

 * to find wether the subject has at least 4 topics or not 

 * db.subjects.find({ "topics.3": { $exists: true } });

 * this is the operation you can use to find the at least

 6)  Update student enrollment

* db.student.updateOne({"name" : "Jenil"},
{ $push: { "topics": "Advanced Hooks" }}
);

7) Query all students
Query all students in the database and print out their names and enrolled subjects.

* db.students.find({ name: 1, coursesEnrolled: 1, _id: 0 });

8) Update multiple students' year

* db.students.updateMany({"department" : "computer science"},
{$set: {"year" : 4}}

    );

9) Add new topics to multiple subjects

* as we cannot use upadatemany we have to manually add the topics to each subject 

* db.subjects.upadateOne(
    {"subjectName": "React" },
    {$push : {"topics" : "react hooks"}}
);
* db.subjects.upadateOne(
    {"subjectName": "Nodejs" },
    {$push : {"topics" : " express framework"}}
);
* db.subjects.upadateOne(
    {"subjectName": "mongodb" },
    {$push : {"topics" : "aggregation"}}
);

here we cannot write upadtemany and give all the upadtes in ine go 

10) remove a topic from a subject
 
 *db.subjects.deleteOne({ "subjectName": "nodejs" });


 * here we will not use detleteone as it deletes the entire data of that particular file 

 * correct way to delete is to use the upadate one and pull it 

 * db.subjects.updateOne(
  { name: "Nodejs" }, 
  { $pull: { topics: "Express" } }
);

11) Query all students in a specific year

 * db.students.find({
  $or: [{ year: 2 }, { year : 3 }]
});

12) Delete a student by roll number

* db.students.deleteOne({ "rollNumber": 102 });

13) Delete all students from a department 

 * db.students.deleteMany({ "department" : "Electrical Engineering"});

 14) Query the MongoDB subject and retrieve all topics listed for it.

 * db.subjects.find({ "subjectName" : "mongodb"} , 
 { _id : 0 });

 15) Count the number of subjects in which a student is enrolled

 * 

