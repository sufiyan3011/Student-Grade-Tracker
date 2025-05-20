# Student-Grade-Tracker
import json

class Student:
    def __init__(self, name):
        self.name = name
        self.grades = {}

    def add_grade(self, subject, grade):
        self.grades[subject] = grade

    def update_grade(self, subject, grade):
        if subject in self.grades:
            self.grades[subject] = grade
        else:
            print(f"{subject} not found for {self.name}.")

    def calculate_average(self):
        if not self.grades:
            return 0
        return sum(self.grades.values()) / len(self.grades)

    def display_grades(self):
        print(f"\nGrades for {self.name}:")
        for subject, grade in self.grades.items():
            print(f"{subject}: {grade}")
        print(f"Average: {self.calculate_average():.2f}")

class GradeTracker:
    def __init__(self):
        self.students = {}

    def add_student(self, name):
        if name not in self.students:
            self.students[name] = Student(name)
            print(f"Student '{name}' added.")
        else:
            print("Student already exists.")

    def add_grade(self, name, subject, grade):
        if name in self.students:
            self.students[name].add_grade(subject, grade)
        else:
            print("Student not found.")

    def update_grade(self, name, subject, grade):
        if name in self.students:
            self.students[name].update_grade(subject, grade)
        else:
            print("Student not found.")

    def show_student(self, name):
        if name in self.students:
            self.students[name].display_grades()
        else:
            print("Student not found.")

def main():
    tracker = GradeTracker()

    while True:
        print("\n--- Grade Tracker Menu ---")
        print("1. Add student")
        print("2. Add grade")
        print("3. Update grade")
        print("4. Show student grades")
        print("5. Exit")

        choice = input("Enter your choice: ")

        if choice == "1":
            name = input("Student name: ")
            tracker.add_student(name)

        elif choice == "2":
            name = input("Student name: ")
            subject = input("Subject: ")
            try:
                grade = float(input("Grade (0-100): "))
                tracker.add_grade(name, subject, grade)
            except ValueError:
                print("Invalid grade input.")

        elif choice == "3":
            name = input("Student name: ")
            subject = input("Subject: ")
            try:
                grade = float(input("New Grade (0-100): "))
                tracker.update_grade(name, subject, grade)
            except ValueError:
                print("Invalid grade input.")

        elif choice == "4":
            name = input("Student name: ")
            tracker.show_student(name)

        elif choice == "5":
            print("Exiting Grade Tracker.")
            break

        else:
            print("Invalid option. Please try again.")

if __name__ == "__main__":
    main()
