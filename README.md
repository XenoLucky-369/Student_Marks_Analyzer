# Student_Marks_Analyzer
This is my first project using NumPy, where I generated random data and visualized it using a histogram with Matplotlib. The goal was to start exploring NumPy arrays and understand how data behaves when plotted.

import json
import os
import numpy as np
from datetime import datetime

Filename = "Student.json"


class Student_details():
    def __init__(self, roll, student_name, age, standard, dob, maths, science, rocket_science, astrophysics, computer_science):
        self.__roll = roll
        self.__student_name = student_name
        self.__age = age
        self.__standard = standard
        self.__dob = dob
        self.__maths = maths
        self.__science = science
        self.__rocket_science = rocket_science
        self.__astrophysics = astrophysics
        self.__computer_science = computer_science


    def for_store(self):
        return {
            "roll": self.__roll,
            "name": self.__student_name,
            "age": self.__age,
            "standard": self.__standard,
            "dob": self.__dob,
            "maths": self.__maths,
            "science": self.__science,
            "rocket_science": self.__rocket_science,
            "astrophysics": self.__astrophysics,
            "computer_science": self.__computer_science
        }
    
    def load_data(self):
        if os.path.exists(Filename):
            try:
                with open(Filename, "r") as file:
                    data = json.load(file)
                    return data
            except (FileNotFoundError, json.JSONDecodeError):
                print("File Not Found!")
        return []
    
    def save_data(self, roll, student_name, age, standard, dob, maths, science, rocket_science, astrophysics, computer_science):
        student = Student_details(roll, student_name, age, standard, dob, maths, science, rocket_science, astrophysics, computer_science)
        data = self.load_data()
        store = student.for_store()
        data.append(store)
        with open(Filename, "w") as file:
            json.dump(data, file, indent=3)

    


def mymenu():# I am not adding a session its only for one year.

    print("\n____________________| SCHOOL'S MARKS ANALYZER FOR STUDENTS |____________________")
    print("\n1. For Adding your Account in the school.")
    print("2. For Viewing your Account details.")
    print("3. For Viewing the student's Detailed Analysis.")
    print("4. For Exit")


while True:
    mymenu()

    try:

        enter = int(input("\nEnter: "))

        if enter == 1:
            while True:
                try:
                    roll = int(input("Enter your roll number: "))
                    if roll < 1000 or roll > 10000:
                        print("Your Number is Invalid.")
                        continue
                    break
                except ValueError:
                    print("Please Enter a Valid Roll Number.")
        
            while True:
                try:
                    name = input("Enter your Name: ")
                    if name.isdigit():
                        print("You are Enter a Invalid.")
                        continue
                    break
                except ValueError:
                    print("Please Enter a Valid Input.")
            
            while True:
                try:
                    age = int(input("Enter your age: "))
                    if age < 3 or age > 25:
                        print("Your age is invalid.")
                        continue
                    break
                except ValueError:
                    print("Please Enter a valid age.")
            
            while True:
                try:
                    standard = int(input("Enter Your Class: "))
                    if standard < 1 or standard > 12:
                        print("You are Enter a invalid input.")
                        continue
                    break
                except ValueError:
                    print("Enter a valid input.")
            
            
            current_year = datetime.now().year

            while True:
                dob = input("Enter your Birthday (eg. 03-08-2010): ")
                try:
                    dob_date = datetime.strptime(dob, "%d-%m-%Y")
                    year = dob_date.year
                    if year > current_year or year < 1900:
                        print(f"Year must be between 1900 and {current_year}. Please try again.")
                        continue
                    break
                except ValueError:
                    print("Invalid format. Please enter as dd-mm-yyyy (e.g., 03-08-2010).")


            while True:
                try:
                    maths = int(input("Enter the marks of Maths: "))
                    if maths < 0 or maths > 100:
                        print("You are enter a invalid marks.")
                        continue
                    break
                except ValueError:
                    print("Enter a valid marks.")

            while True:
                try:
                    science = int(input("Enter the marks of Science: "))
                    if science < 0 or science > 100:
                        print("You are enter a invalid marks.")
                        continue
                    break
                except ValueError:
                    print("Enter a valid marks.")

            while True:
                try:
                    rocket_science = int(input("Enter the marks of Rocket Science: "))
                    if rocket_science < 0 or rocket_science > 100:
                        print("You are enter a invalid marks.")
                        continue
                    break
                except ValueError:
                    print("Enter a valid marks.")

            while True:
                try:
                    astrophysics = int(input("Enter the marks of Astrophysics: "))
                    if astrophysics < 0 or astrophysics > 100:
                        print("You are enter a invalid marks.")
                        continue
                    break
                except ValueError:
                    print("Enter a valid marks.")

            
            while True:
                try:
                    computer_science = int(input("Enter the marks of Computer Science: "))
                    if computer_science < 0 or computer_science > 100:
                        print("You are enter a invalid marks.")
                        continue
                    break
                except ValueError:
                    print("Enter a valid marks.")

            
            details = Student_details(roll,
                              name,
                              age,
                              standard,
                              dob_date.strftime("%d-%m-%Y"),
                              maths,
                              science,
                              rocket_science,
                              astrophysics,
                              computer_science
                    )
            details.save_data(roll,
                              name,
                              age,
                              standard,
                              dob_date.strftime("%d-%m-%Y"),
                              maths,
                              science,
                              rocket_science,
                              astrophysics,
                              computer_science
                    )
            
            print("You Are Successfully Added!")

        elif enter == 2:
            roll = int(input("Enter Your Roll Number: "))
            found = False
            data = details.load_data()
            
            for i, detail in enumerate(data):
                if detail['roll'] == roll:
                    found = True
                    print("Your All Details:-")
                    print(f"\n1. Roll Number of Student: {detail['roll']}")
                    print(f"2. Names of Student: {detail['name']}")
                    print(f"3. Age of Student: {detail['age']}")
                    print(f"4. Standard: {detail['standard']}")
                    print(f"5. Birth of Student: {detail['dob']}")
                    print("\nMarks of All Subjects:-")
                    print(f"\n1. Marks of Maths: {detail['maths']}")
                    print(f"2. Marks of Science: {detail['science']}")
                    print(f"3. Marks of Rocket Science: {detail['rocket_science']}")
                    print(f"4. Marks of Astrophysics: {detail['astrophysics']}")
                    print(f"5. Marks of Computer: {detail['computer_science']}")

            if not found:
                print("Roll number not found.")

        elif enter == 3:
            roll = int(input("Enter Your Roll Number: "))
            found = False
            data = details.load_data()
            for i, detail in enumerate(data):
                if detail['roll'] == roll:
                    found = True


                    math = detail['maths']
                    sciences = detail['science']
                    rocket = detail['rocket_science']
                    astro = detail['astrophysics']
                    computer = detail['computer_science']

                    subject = ["Maths","Science","Rocket Science", "Astrophysics", "Computer Science"]
                    arr = np.array(maths,sciences,rocket,astro,computer)
                    sort_mark = np.sort(arr)[::-1]
                    max_mark = np.argmax(arr)
                    min_mark = np.argmin(arr)
                    mean_mark = np.mean(arr)
                    total = np.sum(arr)
                    std_mark = np.std(arr)
                    percent = total * 100/500

                    print("\nAll Subjects Marks:-")
                    for num in range(len(sort_mark)):
                        print(f"\nMarks of {subject[num]}: {sort_mark[num]}")

                    print(f"\nHighest Marks: {subject[max_mark]} | {arr[max_mark]}")
                    print(f"\nLowest Marks: {subject[min_mark]} | {arr[min_mark]}")
                    print(f"\nAverage Marks: {mean_mark}")
                    print(f"\nTotal Marks: {total}")
                    print(f"\nPercentage You have scored: {percent}")

                    print(f"\nStandard Diveation: {std_mark}")
            if not found:
                print("Roll number not found.")

        elif enter == 4:
            print("Goodbye!")
            break     
        

        else:
            print("Invalid Input")

    except Exception as e:
        print(f"Error: {e}")
        print("Please Enter a Valid Input")



    





