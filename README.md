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

from datetime import date, timedelta


class Book:
    def __init__(self, book_id, title):
        self.book_id = book_id
        self.title = title
        self.available = True


class User:
    def __init__(self, user_id, name):
        self.user_id = user_id
        self.name = name
        self.borrowed_books = {}


class Library:
    def __init__(self):
        self.books = {}
        self.users = {}

    def add_book(self, book):
        self.books[book.book_id] = book

    def add_user(self, user):
        self.users[user.user_id] = user

    def borrow_book(self, user_id, book_id):
        user = self.users[user_id]
        book = self.books[book_id]

        if book.available:
            book.available = False
            due_date = date.today() + timedelta(days=7)
            user.borrowed_books[book_id] = due_date

            print(f"{user.name} borrowed '{book.title}'")
            print(f"Due Date: {due_date}")
        else:
            print("Book is not available.")

    def return_book(self, user_id, book_id):
        user = self.users[user_id]
        book = self.books[book_id]

        due_date = user.borrowed_books[book_id]
        return_date = date.today()

        late_days = max(0, (return_date - due_date).days)
        penalty = late_days * 10

        book.available = True
        del user.borrowed_books[book_id]

        print(f"{user.name} returned '{book.title}'")
        print(f"Late Days: {late_days}")
        print(f"Penalty: ₹{penalty}")

    def show_available_books(self):
        print("\nAvailable Books:")
        for book in self.books.values():
            if book.available:
                print(f"{book.book_id} - {book.title}")


# Creating library
library = Library()

# Adding books
library.add_book(Book("B101", "Python Programming"))
library.add_book(Book("B102", "Data Structures"))
library.add_book(Book("B103", "Machine Learning"))

# Adding users
library.add_user(User("U101", "Rahul"))
library.add_user(User("U102", "Priya"))

# Display available books
library.show_available_books()

# Borrow a book
library.borrow_book("U101", "B101")

# Display available books
library.show_available_books()

# Return the book
library.return_book("U101", "B101")

# Display final available books
library.show_available_books()
