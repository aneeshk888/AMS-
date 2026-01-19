Attendance Marking System in C++

comments
An Attendance Marking System is a simple console-based application to manage and monitor attendance records efficiently. In this project, we will create a C++ program that allows administrators to mark attendance and students/employees to view their attendance status.

Features
Our attendance system will provide the following features:

Teacher Dashboard (Password-Protected):
Add New Student
Mark Attendance
Display All Records
Student Dashboard:
View Own Attendance Status
Project Requirements
The following C++ concepts are required:

C++ Fundamentals
Functions and Compound Data Types
Dynamic Memory Allocation
Additionally, you need a working C++ environment such as g++, clang++, or an IDE like Code::Blocks or Visual Studio Code.

Implementation
Let’s break the implementation into steps:

STEP 1: Basic Setup
We define a struct for student records and set up our global data:

```
#include <iostream>
#include <string>
using namespace std;

// max dates
const int MAX = 100;

// max students
const int MAX_DATES = 30;
const string ADMIN_PASS = "admin123";

struct Attendance {
    string date;
    bool isPresent;
};

struct Student {
    string name;
    Attendance records[MAX_DATES];
    int dateCount = 0;
};

Student students[MAX];
int studentCount = 0;
STEP 2: Add New Student
We create a function to add students to our system.


void addStudent() {
    if (studentCount >= MAX) {
        cout << "Maximum limit reached.\n";
        return;
    }
    cout << "Enter student name: ";
    getline(cin, students[studentCount].name);
    students[studentCount].dateCount = 0;
    studentCount++;
    cout << "Student added successfully.\n";
}
STEP 3: Mark Attendance
This function lets administrators mark a student as present or absent.


void markAttendance() {
    if (studentCount == 0) {
        cout << "No students to mark attendance.\n";
        return;
    }

    string date;
    cout << "Enter date (dd-mm-yyyy): ";
    getline(cin, date);

    for (int i = 0; i < studentCount; i++) {
        cout << "Mark attendance for " << students[i].name
             << " (P/A): ";
        char status;
        cin >> status;
        cin.ignore();

        if (students[i].dateCount >= MAX_DATES) {
            cout << "Max attendance records reached for "
                 << students[i].name << ".\n";
            continue;
        }

        students[i].records[students[i].dateCount].date = date;
        students[i].records[students[i].dateCount].isPresent =
            (status == 'P' || status == 'p');
        students[i].dateCount++;
    }

    cout << "Attendance marked for all students.\n";
}
STEP 4: Display All Records
Display the attendance status of all students.


void displayRecords() {
    if (studentCount == 0) {
        cout << "No records to display.\n";
        return;
    }

    for (int i = 0; i < studentCount; i++) {
        cout << "\nStudent: " << students[i].name << "\n";
        if (students[i].dateCount == 0) {
            cout << "  No attendance records.\n";
            continue;
        }

        for (int j = 0; j < students[i].dateCount; j++) {
            cout << "  Date: " << students[i].records[j].date
                 << ", Status: "
                 << (students[i].records[j].isPresent
                     ? "Present" : "Absent") << "\n";
        }
    }
}
STEP 5: Search Student Record
Search for a student by name using recursion.


int searchStudent(int index, const string& query) {
    if (index == studentCount) return -1;
    if (students[index].name == query) return index;
    return searchStudent(index + 1, query);
}
STEP 6: View Own Attendance
Students can view their attendance record.


void viewOwnAttendance() {
    string name;
    cout << "Enter your name: ";
    getline(cin, name);

    int idx = searchStudent(0, name);
    if (idx == -1) {
        cout << "Student not found.\n";
        return;
    }

    if (students[idx].dateCount == 0) {
        cout << "No attendance records.\n";
        return;
    }

    cout << "\nAttendance for " << students[idx].name << ":\n";
    for (int i = 0; i < students[idx].dateCount; i++) {
        cout << "  Date: " << students[idx].records[i].date
             << ", Status: "
             << (students[idx].records[i].isPresent
                 ? "Present" : "Absent") << "\n";
    }
}
STEP 7: Dashboard
We provide a menu-driven interface to access all features.


void teacherDashboard() {
    string pass;
    cout << "Enter admin password: ";
    getline(cin, pass);

    if (pass != ADMIN_PASS) {
        cout << "Incorrect password.\n";
        return;
    }

    int choice;
    while (true) {
        cout << "\n--- Teacher Dashboard ---\n";
        cout << "1. Add Student\n";
        cout << "2. Mark Attendance\n";
        cout << "3. Display All Records\n";
        cout << "4. Logout\n";
        cout << "Enter your choice: ";
        cin >> choice;
        cin.ignore();

        switch (choice) {
            case 1:
                addStudent();
                break;
            case 2:
                markAttendance();
                break;
            case 3:
                displayRecords();
                break;
            case 4:
                cout << "Logging out.\n";
                return;
            default:
                cout << "Invalid choice.\n";
        }
    }
}
Execution
```

```
// Spurce code
​
#include <iostream>
#include <string>
using namespace std;
​
// max students
const int MAX = 100;
​
// max dates
const int MAX_DATES = 30;
const string ADMIN_PASS = "admin123";
​
struct Attendance {
    string date;
    bool isPresent;
};
​
struct Student {
    string name;
    Attendance records[MAX_DATES];
    int dateCount = 0;
};
​
Student students[MAX];
int studentCount = 0;
void addStudent() {
    if (studentCount >= MAX) {
        cout << "Maximum limit reached.\n";
        return;
    }
    cout << "Enter student name: ";
    getline(cin, students[studentCount].name);
    students[studentCount].dateCount = 0;
    studentCount++;
    cout << "Student added successfully.\n";
}
void markAttendance() {
    if (studentCount == 0) {
        cout << "No students to mark attendance.\n";
        return;
    }
​
    string date;
    cout << "Enter date (dd-mm-yyyy): ";
    getline(cin, date);
​
    for (int i = 0; i < studentCount; i++) {
        cout << "Mark attendance for " << students[i].name
             << " (P/A): ";
        char status;
        cin >> status;
        cin.ignore();
​
        if (students[i].dateCount >= MAX_DATES) {
            cout << "Max attendance records reached for "
                 << students[i].name << ".\n";
            continue;
        }
​
        students[i].records[students[i].dateCount].date = date;
        students[i].records[students[i].dateCount].isPresent =
            (status == 'P' || status == 'p');
        students[i].dateCount++;
    }
​
    cout << "Attendance marked for all students.\n";
}
void displayRecords() {
    if (studentCount == 0) {
        cout << "No records to display.\n";
        return;
    }
​
    for (int i = 0; i < studentCount; i++) {
        cout << "\nStudent: " << students[i].name << "\n";
        if (students[i].dateCount == 0) {
            cout << "  No attendance records.\n";
            continue;
        }
​
        for (int j = 0; j < students[i].dateCount; j++) {
            cout << "  Date: " << students[i].records[j].date
                 << ", Status: "
                 << (students[i].records[j].isPresent
                     ? "Present" : "Absent") << "\n";
        }
    }
}
int searchStudent(int index, const string& query) {
    if (index == studentCount) return -1;
    if (students[index].name == query) return index;
    return searchStudent(index + 1, query);
}
void viewOwnAttendance() {
    string name;
    cout << "Enter your name: ";
    getline(cin, name);
​
    int idx = searchStudent(0, name);
    if (idx == -1) {
        cout << "Student not found.\n";
        return;
    }
​
    if (students[idx].dateCount == 0) {
        cout << "No attendance records.\n";
        return;
    }
​
    cout << "\nAttendance for " << students[idx].name << ":\n";
    for (int i = 0; i < students[idx].dateCount; i++) {
        cout << "  Date: " << students[idx].records[i].date
             << ", Status: "
             << (students[idx].records[i].isPresent
                 ? "Present" : "Absent") << "\n";
    }
}
void teacherDashboard() {
    string pass;
    cout << "Enter admin password: ";
    getline(cin, pass);
​
    if (pass != ADMIN_PASS) {
        cout << "Incorrect password.\n";
        return;
    }
​
    int choice;
    while (true) {
        cout << "\n--- Teacher Dashboard ---\n";
        cout << "1. Add Student\n";
        cout << "2. Mark Attendance\n";
        cout << "3. Display All Records\n";
        cout << "4. Logout\n";
        cout << "Enter your choice: ";
        cin >> choice;
        cin.ignore();
​
        switch (choice) {
            case 1:
                addStudent();
                break;
            case 2:
                markAttendance();
                break;
            case 3:
                displayRecords();
                break;
            case 4:
                cout << "Logging out.\n";
                return;
            default:
                cout << "Invalid choice.\n";
        }
    }
}
void studentDashboard() {
    viewOwnAttendance();
}
int main() {
    int choice;
    while (true) {
        cout << "\n--- Attendance System Main Menu ---\n";
        cout << "1. Teacher Dashboard\n";
        cout << "2. Student Dashboard\n";
        cout << "3. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;
        cin.ignore();
​
        switch (choice) {
            case 1:
                teacherDashboard();
                break;
            case 2:
                studentDashboard();
                break;
            case 3:
                cout << "Goodbye!\n";
                return 0;
            default:
                cout << "Invalid choice. Try again.\n";
        }
    }
}

```

On running this program, the user will see a menu where they can add students, mark attendance, display records, and view attendance status. The system uses simple arrays, functions, loops, and decision-making to achieve its functionality.

