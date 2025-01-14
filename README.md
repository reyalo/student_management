#include <iostream>
#include <vector>
using namespace std;

// Class to manage student information
class Student {
private:
    string name;
    int age;
    string studentID;
    vector<string> hobbies;
    string course;

public:
    // Constructor
    Student(string name, int age, string studentID, vector<string> hobbies, string course) {
        this->name = name;
        this->age = age;
        this->studentID = studentID;
        this->hobbies = hobbies;
        this->course = course;
    }

    // Get student name
    string getName() const {
        return name;
    }

    // Get student ID
    string getStudentID() const {
        return studentID;
    }

    // Get student age
    int getAge() const {
        return age;
    }

    // Get student course
    string getCourse() const {
        return course;
    }

    // Get student hobbies
    void getHobbies() const {
        cout << "Hobbies: ";
        for (const auto &hobby : hobbies) {
            cout << hobby << " ";
        }
        cout << endl;
    }

    // Display all student information
    void displayInfo() const {
        cout << "Name: " << name << endl;
        cout << "Age: " << age << endl;
        cout << "Student ID: " << studentID << endl;
        cout << "Course: " << course << endl;
        getHobbies();
    }

    // --- Functions for Updating Student Information ---

    // Update student name
    void updateName(const string& newName) {
        name = newName;
    }

    // Update student age
    void updateAge(int newAge) {
        age = newAge;
    }

    // Update student ID
    void updateStudentID(const string& newID) {
        studentID = newID;
    }

    // Update student course
    void updateCourse(const string& newCourse) {
        course = newCourse;
    }

    // Update student hobbies
    void updateHobbies(const vector<string>& newHobbies) {
        hobbies = newHobbies;
    }
};

// Function to display a list and get the user's selection
int getSelection(const vector<string>& options) {
    int choice;
    cout << "Select an option by entering the number:" << endl;
    for (size_t i = 0; i < options.size(); ++i) {
        cout << i + 1 << ". " << options[i] << endl;
    }
    cin >> choice;
    while (choice < 1 || choice > options.size()) {
        cout << "Invalid choice. Please try again: ";
        cin >> choice;
    }
    return choice - 1; // Adjust for 0-based indexing
}

// Function to update student information
void updateStudentInfo(Student& student) {
    int option;
    cout << "\nWhat would you like to update?\n";
    cout << "1. Name\n2. Age\n3. Student ID\n4. Course\n5. Hobbies\n";
    cin >> option;

    switch(option) {
        case 1: {
            string newName;
            cout << "Enter new name: ";
            cin.ignore(); // To clear the buffer
            getline(cin, newName);
            student.updateName(newName);
            break;
        }
        case 2: {
            int newAge;
            cout << "Enter new age: ";
            cin >> newAge;
            student.updateAge(newAge);
            break;
        }
        case 3: {
            string newID;
            cout << "Enter new student ID: ";
            cin >> newID;
            student.updateStudentID(newID);
            break;
        }
        case 4: {
            vector<string> availableCourses = {"Computer Science", "Mechanical Engineering", "Electrical Engineering", "Business Administration", "Biology"};
            cout << "\nSelect a new course:\n";
            int courseIndex = getSelection(availableCourses);
            student.updateCourse(availableCourses[courseIndex]);
            break;
        }
        case 5: {
            vector<string> availableHobbies = {"Reading", "Swimming", "Painting", "Hiking", "Gaming", "Cooking"};
            int numOfHobbies;
            cout << "\nHow many hobbies do you want to select (max 3)? ";
            cin >> numOfHobbies;
            numOfHobbies = min(numOfHobbies, 3);  // Limit to 3 hobbies

            vector<string> selectedHobbies;
            for (int i = 0; i < numOfHobbies; ++i) {
                cout << "\nSelect hobby " << i + 1 << ":" << endl;
                int hobbyIndex = getSelection(availableHobbies);
                selectedHobbies.push_back(availableHobbies[hobbyIndex]);
            }
            student.updateHobbies(selectedHobbies);
            break;
        }
        default:
            cout << "Invalid option." << endl;
    }
}

int main() {
    vector<string> hobbies1 = {"Reading", "Swimming"};
    Student student("John Doe", 20, "S001", hobbies1, "Computer Science");

    // Display initial student information
    cout << "Initial Student Information:" << endl;
    student.displayInfo();

    // Update student information
    updateStudentInfo(student);

    // Display updated student information
    cout << "\nUpdated Student Information:" << endl;
    student.displayInfo();

    return 0;
}
