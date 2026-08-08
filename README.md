# Python-OOP-Project-Student-Report-Card-Generator
class Student:

    def __init__(self, roll_no, name):
        self.roll_no = roll_no
        self.name = name
        self.__marks = {}

    def add_marks(self, subject, marks):
        self.__marks[subject] = marks

    def calculate_average(self):
        total = 0

        for mark in self.__marks.values():
            total += mark

        average = total / len(self.__marks)

        print(f"{self.name}'s average: {average}")

        return average

    def calculate_grade(self):
        average = self.calculate_average()

        if average >= 90:
            return "A+"
        elif average >= 80:
            return "A"
        elif average >= 70:
            return "B"
        elif average >= 60:
            return "C"
        elif average >= 50:
            return "D"
        else:
            return "F"

    def check_result(self):
        for mark in self.__marks.values():
            if mark < 35:
                return "FAIL"

        return "PASS"

    def generate_report(self):
        print("\n----- STUDENT REPORT -----")
        print("Roll No:", self.roll_no)
        print("Name:", self.name)

        print("\nMarks:")
        for subject, mark in self.__marks.items():
            print(subject, ":", mark)

        average = self.calculate_average()
        grade = self.calculate_grade()
        result = self.check_result()

        print("Grade:", grade)
        print("Result:", result)



student = Student(101, "Varun")


student.add_marks("Python", 85)
student.add_marks("Maths", 78)
student.add_marks("English", 92)
student.add_marks("Science", 67)

student.generate_report()

class Discount:
    def get_discount(self):
        return 0

class RegularCustomer(Discount):
    def get_discount(self):
        return 10

class PremiumCustomer(Discount):
    def get_discount(self):
        return 20
