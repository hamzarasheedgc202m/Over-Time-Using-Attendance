# Over-Time-Using-Attendance.py
import sqlite3
import datetime

# Connect to the database
conn = sqlite3.connect('employee_data.db')
c = conn.cursor()

# Create the employee table
c.execute('''CREATE TABLE employees
             (id INTEGER PRIMARY KEY, name TEXT, password TEXT, standard_hours INTEGER, overtime_rate INTEGER)''')

# Log in system
def login():
    id_num = input("Enter your ID number: ")
    password = input("Enter your password: ")
    c.execute("SELECT * FROM employees WHERE id=? AND password=?", (id_num, password))
    result = c.fetchone()
    if result:
        check_in(result[0])
    else:
        print("Invalid login credentials.")
