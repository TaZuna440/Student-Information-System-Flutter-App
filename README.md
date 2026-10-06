Step-by-Step Coding Tutorial: Student Information System in Flutter
This mini-project is designed for complete beginners. We will build a simple Student Information System (SIS) progressively rather than giving you the entire application at once.
What we will build
The application will eventually allow users to:
●	View a list of students
●	Add a student
●	View student details
●	Edit student information
●	Delete a student
●	Search students
●	Validate basic input
For this first version, we will use in-memory data—meaning the data exists only while the application is running. We will introduce a database later.
________________________________________
1. Project Architecture
Our first version will use a simple structure:
Student Information System
│
├── Student Model
│
├── Student List
│
├── Add Student
│
├── Student Details
│
├── Edit Student
│
└── Delete Student
The development progression will be:
Step 1 → Create Project
Step 2 → Build Basic UI
Step 3 → Create Student Model
Step 4 → Display Students
Step 5 → Add Student
Step 6 → View Student Details
Step 7 → Edit Student
Step 8 → Delete Student
Step 9 → Search Students
Step 10 → Improve UI and Validation
________________________________________
2. Step 1 — Create the Flutter Project
Open VS Code.
Open the terminal:
Terminal → New Terminal
Run:
flutter create student_information_system
Move into the project:
cd student_information_system
Run the project:
flutter run
Make sure your Android Emulator is running.
You should initially see Flutter's default counter application.
________________________________________
3. Step 2 — Understand the Project
Open:
student_information_system
The most important file for now is:
lib/main.dart
Our initial project will be kept simple:
student_information_system/
│
├── android/
├── ios/
├── lib/
│   └── main.dart
│
├── test/
├── web/
├── windows/
└── pubspec.yaml
For this beginner project, most of our work initially happens inside:
lib/main.dart
Later, when the project becomes larger, we will divide the code into multiple files.
________________________________________
4. Step 3 — Remove the Default Flutter Code
Open:
lib/main.dart
Delete the existing code.
Start with:
import 'package:flutter/material.dart';

void main() {
  runApp(const StudentInformationSystem());
}
At this point, we have imported Flutter's Material Design widgets and created the application's entry point.
________________________________________
5. Step 4 — Create the Main Application
Under main(), add:
class StudentInformationSystem extends StatelessWidget {
  const StudentInformationSystem({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      title: 'Student Information System',
      home: const HomePage(),
    );
  }
}
Our structure is now:
main()
   │
   ▼
StudentInformationSystem
   │
   ▼
MaterialApp
   │
   ▼
HomePage
However, we haven't created HomePage yet.
________________________________________
6. Step 5 — Create the Home Page
Add this below the previous class:
class HomePage extends StatelessWidget {
  const HomePage({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Student Information System'),
      ),
      body: const Center(
        child: Text(
          'Welcome to the Student Information System',
        ),
      ),
    );
  }
}
Your complete code should now be:
import 'package:flutter/material.dart';

void main() {
  runApp(const StudentInformationSystem());
}

class StudentInformationSystem extends StatelessWidget {
  const StudentInformationSystem({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      title: 'Student Information System',
      home: const HomePage(),
    );
  }
}

class HomePage extends StatelessWidget {
  const HomePage({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Student Information System'),
      ),
      body: const Center(
        child: Text(
          'Welcome to the Student Information System',
        ),
      ),
    );
  }
}
Run the application.
You should see:
┌─────────────────────────────────┐
│ Student Information System      │
├─────────────────────────────────┤
│                                 │
│ Welcome to the Student          │
│ Information System              │
│                                 │
└─────────────────────────────────┘
________________________________________
7. Step 6 — Create the Student Model
Our application needs to represent students.
For example, a student might have:
Student ID
Name
Course
Year Level
Email
Instead of storing these as unrelated variables, we create a class.
Create a new folder:
lib/models
Inside it create:
student.dart
Your structure becomes:
lib/
├── main.dart
└── models/
    └── student.dart
________________________________________
8. Step 7 — Write the Student Class
Inside student.dart:
class Student {
  int id;
  String name;
  String course;
  int yearLevel;
  String email;

  Student({
    required this.id,
    required this.name,
    required this.course,
    required this.yearLevel,
    required this.email,
  });
}
We have created a model class.
A model represents a type of data used by the application.
Conceptually:
Student
│
├── id
├── name
├── course
├── yearLevel
└── email
________________________________________
9. Step 8 — Understand the Constructor
This part:
Student({
  required this.id,
  required this.name,
  required this.course,
  required this.yearLevel,
  required this.email,
});
is the constructor.
It allows us to create a student like this:
Student(
  id: 1,
  name: 'Juan Dela Cruz',
  course: 'BSIT',
  yearLevel: 2,
  email: 'juan@example.com',
)
We can now represent a complete student using one object.
________________________________________
10. Step 9 — Create Sample Students
Go back to:
main.dart
Import the model:
import 'models/student.dart';
Now create sample data.
Change HomePage from:
class HomePage extends StatelessWidget {
to:
class HomePage extends StatefulWidget {
  const HomePage({super.key});

  @override
  State<HomePage> createState() => _HomePageState();
}
Then create the state:
class _HomePageState extends State<HomePage> {
Inside _HomePageState, add:
List<Student> students = [
  Student(
    id: 1,
    name: 'Juan Dela Cruz',
    course: 'BS Information Technology',
    yearLevel: 2,
    email: 'juan@example.com',
  ),
  Student(
    id: 2,
    name: 'Maria Santos',
    course: 'BS Information Technology',
    yearLevel: 1,
    email: 'maria@example.com',
  ),
];
________________________________________
11. Step 10 — Display the Students
Replace the existing body with:
body: ListView.builder(
  itemCount: students.length,
  itemBuilder: (context, index) {
    final student = students[index];

    return ListTile(
      leading: const Icon(Icons.person),
      title: Text(student.name),
      subtitle: Text(student.course),
    );
  },
),
The page now displays:
Student Information System

👤 Juan Dela Cruz
   BS Information Technology

👤 Maria Santos
   BS Information Technology
________________________________________
12. Understanding ListView.builder
This is important:
ListView.builder(
creates a scrollable list.
The:
itemCount: students.length
tells Flutter how many students exist.
The:
itemBuilder:
describes how each student should appear.
This:
final student = students[index];
gets the current student.
For example:
index = 0 → Juan
index = 1 → Maria
________________________________________
13. Step 11 — Add an "Add Student" Button
We want the user to be able to add students.
Inside Scaffold, add:
floatingActionButton: FloatingActionButton(
  onPressed: () {
    // We will implement this later.
  },
  child: const Icon(Icons.add),
),
Your Scaffold now looks like:
return Scaffold(
  appBar: AppBar(
    title: const Text('Student Information System'),
  ),
  body: ListView.builder(
    itemCount: students.length,
    itemBuilder: (context, index) {
      final student = students[index];

      return ListTile(
        leading: const Icon(Icons.person),
        title: Text(student.name),
        subtitle: Text(student.course),
      );
    },
  ),
  floatingActionButton: FloatingActionButton(
    onPressed: () {},
    child: const Icon(Icons.add),
  ),
);
Run the application.
You should see a + button.
It doesn't do anything yet.
That's intentional.
________________________________________
14. Step 12 — Create the Add Student Screen
Create:
lib/screens
Inside it create:
add_student_page.dart
Start with:
import 'package:flutter/material.dart';

class AddStudentPage extends StatelessWidget {
  const AddStudentPage({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Add Student'),
      ),
      body: const Center(
        child: Text('Add Student Form'),
      ),
    );
  }
}
________________________________________
15. Step 13 — Navigate to Add Student
Go back to main.dart.
Import:
import 'screens/add_student_page.dart';
Change the FloatingActionButton:
floatingActionButton: FloatingActionButton(
  onPressed: () {
    Navigator.push(
      context,
      MaterialPageRoute(
        builder: (context) => const AddStudentPage(),
      ),
    );
  },
  child: const Icon(Icons.add),
),
Now pressing + should open:
Add Student
This introduces navigation.
________________________________________
16. Step 14 — Create the Student Form
Change AddStudentPage into a StatefulWidget.
class AddStudentPage extends StatefulWidget {
  const AddStudentPage({super.key});

  @override
  State<AddStudentPage> createState() => _AddStudentPageState();
}
Then:
class _AddStudentPageState extends State<AddStudentPage> {
Create controllers:
final nameController = TextEditingController();
final courseController = TextEditingController();
final yearController = TextEditingController();
final emailController = TextEditingController();
These controllers allow us to retrieve information entered into text fields.
________________________________________
17. Step 15 — Build the Form
Replace the body with:
body: Padding(
  padding: const EdgeInsets.all(16),
  child: Column(
    children: [
      TextField(
        controller: nameController,
        decoration: const InputDecoration(
          labelText: 'Student Name',
          border: OutlineInputBorder(),
        ),
      ),

      const SizedBox(height: 16),

      TextField(
        controller: courseController,
        decoration: const InputDecoration(
          labelText: 'Course',
          border: OutlineInputBorder(),
        ),
      ),

      const SizedBox(height: 16),

      TextField(
        controller: yearController,
        keyboardType: TextInputType.number,
        decoration: const InputDecoration(
          labelText: 'Year Level',
          border: OutlineInputBorder(),
        ),
      ),

      const SizedBox(height: 16),

      TextField(
        controller: emailController,
        decoration: const InputDecoration(
          labelText: 'Email',
          border: OutlineInputBorder(),
        ),
      ),

      const SizedBox(height: 24),

      ElevatedButton(
        onPressed: () {},
        child: const Text('Save Student'),
      ),
    ],
  ),
),
You now have a basic form.
________________________________________
18. Step 16 — Understand TextEditingController
Consider:
final nameController = TextEditingController();
The controller gives our program access to what the user types.
If the user enters:
Juan Dela Cruz
we can retrieve it using:
nameController.text
Similarly:
courseController.text
yearController.text
emailController.text
________________________________________
19. Step 17 — Return Student Data to the Home Page
When the user presses Save Student, we want to return the new student to the previous screen.
First import the model:
import '../models/student.dart';
Then modify the Save button:
ElevatedButton(
  onPressed: () {
    final student = Student(
      id: DateTime.now().millisecondsSinceEpoch,
      name: nameController.text,
      course: courseController.text,
      yearLevel: int.parse(yearController.text),
      email: emailController.text,
    );

    Navigator.pop(context, student);
  },
  child: const Text('Save Student'),
),
We now create a Student object from the form.
________________________________________
20. Step 18 — Receive the New Student
Go back to the Home Page.
Change the navigation code.
Instead of:
Navigator.push(
  context,
  MaterialPageRoute(
    builder: (context) => const AddStudentPage(),
  ),
);
use:
final newStudent = await Navigator.push<Student>(
  context,
  MaterialPageRoute(
    builder: (context) => const AddStudentPage(),
  ),
);
Because await is used, the onPressed function must become asynchronous:
onPressed: () async {
Then:
if (newStudent != null) {
  setState(() {
    students.add(newStudent);
  });
}
The complete button becomes:
floatingActionButton: FloatingActionButton(
  onPressed: () async {
    final newStudent = await Navigator.push<Student>(
      context,
      MaterialPageRoute(
        builder: (context) => const AddStudentPage(),
      ),
    );

    if (newStudent != null) {
      setState(() {
        students.add(newStudent);
      });
    }
  },
  child: const Icon(Icons.add),
),
Now the workflow is:
Home Page
    │
    │ press +
    ▼
Add Student
    │
    │ enter information
    ▼
Save Student
    │
    ▼
Student object created
    │
    ▼
Return to Home Page
    │
    ▼
students.add()
    │
    ▼
setState()
    │
    ▼
List updates
This is a very important Flutter pattern.
________________________________________
21. Step 19 — View Student Details
We now want this:
Student List
     │
     │ tap student
     ▼
Student Details
Create:
lib/screens/student_details_page.dart
Add:
import 'package:flutter/material.dart';
import '../models/student.dart';

class StudentDetailsPage extends StatelessWidget {
  final Student student;

  const StudentDetailsPage({
    super.key,
    required this.student,
  });

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Student Details'),
      ),
      body: Padding(
        padding: const EdgeInsets.all(16),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Text(
              student.name,
              style: const TextStyle(
                fontSize: 24,
                fontWeight: FontWeight.bold,
              ),
            ),

            const SizedBox(height: 20),

            Text('Student ID: ${student.id}'),
            Text('Course: ${student.course}'),
            Text('Year Level: ${student.yearLevel}'),
            Text('Email: ${student.email}'),
          ],
        ),
      ),
    );
  }
}
________________________________________
22. Step 20 — Make Students Clickable
Import:
import 'screens/student_details_page.dart';
Change your ListTile:
return ListTile(
  leading: const Icon(Icons.person),
  title: Text(student.name),
  subtitle: Text(student.course),
  onTap: () {
    Navigator.push(
      context,
      MaterialPageRoute(
        builder: (context) => StudentDetailsPage(
          student: student,
        ),
      ),
    );
  },
);
Now the user can tap a student.
________________________________________
23. Step 21 — Add Delete Functionality
A simple first implementation is to add a delete button to each list item.
Change ListTile to:
return ListTile(
  leading: const Icon(Icons.person),
  title: Text(student.name),
  subtitle: Text(student.course),
  trailing: IconButton(
    icon: const Icon(Icons.delete),
    onPressed: () {
      setState(() {
        students.removeAt(index);
      });
    },
  ),
  onTap: () {
    Navigator.push(
      context,
      MaterialPageRoute(
        builder: (context) => StudentDetailsPage(
          student: student,
        ),
      ),
    );
  },
);
Now:
Student
              🗑
pressing the delete button removes that student from the list.
________________________________________
24. Important: Why setState()?
Consider:
students.removeAt(index);
This changes the list.
But Flutter needs to know that the UI should be updated.
Therefore:
setState(() {
  students.removeAt(index);
});
tells Flutter:
"The state has changed. Rebuild this widget so the user interface reflects the new state."
This is one of the fundamental concepts of Flutter.
________________________________________
25. Step 22 — Add a Search Bar
Now let's make the application more useful.
At the top of the student list, we want:
Search students...
Add a search controller:
final searchController = TextEditingController();
We'll also maintain a filtered list.
Add:
List<Student> filteredStudents = [];
However, we need to initialize it.
A simple approach is to initialize it in initState():
@override
void initState() {
  super.initState();
  filteredStudents = students;
}
________________________________________
26. Step 23 — Implement Search
Create:
void searchStudents(String query) {
  setState(() {
    filteredStudents = students.where((student) {
      return student.name
          .toLowerCase()
          .contains(query.toLowerCase());
    }).toList();
  });
}
This searches student names.
________________________________________
27. Step 24 — Add Search Field
Change your body to:
body: Column(
  children: [
    Padding(
      padding: const EdgeInsets.all(16),
      child: TextField(
        controller: searchController,
        onChanged: searchStudents,
        decoration: const InputDecoration(
          labelText: 'Search Student',
          prefixIcon: Icon(Icons.search),
          border: OutlineInputBorder(),
        ),
      ),
    ),

    Expanded(
      child: ListView.builder(
        itemCount: filteredStudents.length,
        itemBuilder: (context, index) {
          final student = filteredStudents[index];

          return ListTile(
            leading: const Icon(Icons.person),
            title: Text(student.name),
            subtitle: Text(student.course),
          );
        },
      ),
    ),
  ],
),
Now the student list responds to search input.
________________________________________
28. Step 25 — Important Bug to Fix
There is a subtle problem.
When adding a new student:
students.add(newStudent);
we also need to update:
filteredStudents
Otherwise, the new student might not appear correctly when searching.
Change:
students.add(newStudent);
to:
students.add(newStudent);
filteredStudents = students;
inside setState():
setState(() {
  students.add(newStudent);
  filteredStudents = students;
});
This is a good example of why managing application state becomes increasingly important as applications grow.
________________________________________
29. Current Project Structure
At this point, our project looks like:
lib/
│
├── main.dart
│
├── models/
│   └── student.dart
│
└── screens/
    ├── add_student_page.dart
    └── student_details_page.dart
This is already better than putting everything into main.dart.
________________________________________
30. Final Application Workflow
The application now follows this basic workflow:
                   ┌─────────────────┐
                    │    Home Page    │
                    │ Student List    │
                    └────────┬────────┘
                             │
             ┌───────────────┼────────────────┐
             │               │                │
             ▼               ▼                ▼
        Add Student     View Student       Delete
             │             Details           │
             ▼               │                ▼
        Student Form        │          Remove from List
             │               │
             ▼               │
        Save Student         │
             │               │
             └───────┬───────┘
                     ▼
                Student List
________________________________________
31. What Students Have Learned
This mini-project introduces several important Flutter concepts.
Concept	Where We Used It
MaterialApp	Application root
Scaffold	Screen structure
AppBar	Application header
Text	Display information
Column	Vertical layout
ListView	Student list
ListTile	Student item
TextField	Input/search
ElevatedButton	Form submission
FloatingActionButton	Add student
StatefulWidget	Changing student list
setState()	Updating UI
Navigator	Screen navigation
TextEditingController	Reading user input
Model class	Representing student data
List<Student>	Storing multiple students
________________________________________
32. The Most Important Architecture Lesson
Notice what we have created:
UI
│
├── HomePage
├── AddStudentPage
└── StudentDetailsPage
        │
        ▼
Student Model
        │
        ▼
List<Student>
The model represents our data.
The screens display and interact with the data.
This separation is the beginning of proper application architecture.
________________________________________
33. Current Limitation: Data Is Not Persistent
There is an important limitation.
Our students are currently stored in:
List<Student> students
This means the data exists only in memory.
If the application is closed:
Application running
       │
       ▼
Student added
       │
       ▼
Student exists
       │
       ▼
Application closed
       │
       ▼
Data disappears
This is not yet a production Student Information System.
The next stage is persistence.
________________________________________
34. Recommended Next Version
After students understand this basic version, upgrade the project through these stages:
Version 1 — In-Memory SIS
Student Model
     ↓
List<Student>
     ↓
CRUD
Version 2 — Local Storage
Introduce:
●	SQLite
●	sqflite
●	local persistence
Flutter
   ↓
Repository
   ↓
SQLite
Version 3 — REST API
Introduce a backend:
Flutter
   ↓
HTTP/REST API
   ↓
Spring Boot / Laravel / Django
   ↓
MySQL
Version 4 — Authentication
Add:
Login
  ↓
Authentication
  ↓
Role
  ├── Admin
  ├── Faculty
  └── Student
Version 5 — Production Architecture
Eventually introduce:
Presentation Layer
        ↓
State Management
        ↓
Service / Repository Layer
        ↓
REST API
        ↓
Backend
        ↓
Database
This progression allows beginners to first understand Flutter itself before introducing databases, APIs, authentication, and architectural complexity.
________________________________________
35. Beginner Challenge Tasks
Once the basic SIS works, students should implement these independently.
Challenge 1 — Edit Student
Add an Edit button.
The user should be able to modify:
●	name;
●	course;
●	year level;
●	email.
________________________________________
Challenge 2 — Delete Confirmation
Instead of immediately deleting a student, display:
Are you sure you want to delete
Juan Dela Cruz?

[Cancel] [Delete]
Use AlertDialog.
________________________________________
Challenge 3 — Search by Course
Modify the search functionality so students can search by:
●	name;
●	course.
________________________________________
Challenge 4 — Student Count
Display:
Total Students: 25
using:
students.length
________________________________________
Challenge 5 — Empty State
If there are no students, display:
No students found.
instead of an empty screen.
________________________________________
Challenge 6 — Form Validation
Prevent the user from saving a student if:
●	name is empty;
●	course is empty;
●	year level is invalid;
●	email is empty.
________________________________________
36. Final Beginner Checkpoint
Before moving to databases, students should be able to explain this entire sequence:
User taps "+"
       ↓
Navigator.push()
       ↓
AddStudentPage
       ↓
User enters information
       ↓
TextEditingController
       ↓
Student object created
       ↓
Navigator.pop(student)
       ↓
HomePage receives Student
       ↓
students.add(student)
       ↓
setState()
       ↓
ListView rebuilds
       ↓
New student appears
If you understand this flow, you have moved beyond simply copying Flutter widgets—you are beginning to understand how a Flutter application works.
Official references
●	Flutter Documentation
●	Dart Documentation
●	Flutter Navigation and Routing
●	Flutter Forms Documentation
●	Flutter Layout Documentation

