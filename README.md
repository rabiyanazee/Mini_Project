# Mini_Project
# Student Database Management System in C++


#include <iostream>
#include <iomanip>
#include <vector>
#include <algorithm>
using namespace std;
struct Student {
    string name;
    int rollNumber;
    float marks;
};
class StudentDatabase {
private:
    vector<Student> students;
public:
    void addStudent() {
        Student newStudent;
        cout << "Enter name: ";
        getline(cin, newStudent.name);
        cout << "Enter roll number: ";
        cin >> newStudent.rollNumber;
        cout << "Enter marks: ";
        cin >> newStudent.marks;
        students.push_back(newStudent);
        cout << "Student added successfully!\n";
    }
    void displayAllStudents() {
        if (students.empty()) {
            cout << "No students in the database.\n";
        } else {
            cout << "List of all students:\n";
            cout << setw(20) << "Name" << setw(15) << "Roll Number" << setw(10) << "Marks\n";
            for (const auto &student : students) {
                cout << setw(20) << student.name << setw(15) << student.rollNumber << setw(10) << student.marks << "\n";
            }
        }
    }
    void deleteStudent(int rollNumber) {
        auto it = find_if(students.begin(), students.end(),
                          [rollNumber](const Student &s) { return s.rollNumber == rollNumber; });
        if (it != students.end()) {
            students.erase(it);
            cout << "Student with roll number " << rollNumber << " deleted successfully!\n";
        } else {
            cout << "Student with roll number " << rollNumber << " not found.\n";
        }
    }
    void updateStudent(int rollNumber) {
        auto it = find_if(students.begin(), students.end(),
                          [rollNumber](const Student &s) { return s.rollNumber == rollNumber; });
        if (it != students.end()) {
            cout << "Enter new name: ";
            getline(cin, it->name);
            cout << "Enter new marks: ";
            cin >> it->marks;
            cout << "Student with roll number " << rollNumber << " updated successfully!\n";
        } else {
            cout << "Student with roll number " << rollNumber << " not found.\n";
        }
    }
};
int main() {
    StudentDatabase database;
    int choice, rollNumber;
    do {
        cout << "\nStudent Database Management System\n";
        cout << "1. Add Student\n";
        cout << "2. Display All Students\n";
        cout << "3. Delete Student\n";
        cout << "4. Update Student\n";
        cout << "5. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;
        switch (choice) {
            case 1:
                cin.ignore(); // Clear newline character from the buffer
                database.addStudent();
                break;
            case 2:
                database.displayAllStudents();
                break;
            case 3:
                cout << "Enter roll number to delete: ";
                cin >> rollNumber;
                database.deleteStudent(rollNumber);
                break;
            case 4:
                cout << "Enter roll number to update: ";
                cin >> rollNumber;
                cin.ignore(); // Clear newline character from the buffer
                database.updateStudent(rollNumber);
                break;
            case 5:
                cout << "Exiting program.\n";
                break;
            default:
                cout << "Invalid choice. Please try again.\n";
        }
    } while (choice != 5);
    return 0;
    }
