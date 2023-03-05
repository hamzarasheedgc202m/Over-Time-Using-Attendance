# Over-Time-Using-Attendance.py
import datetime

attendance = {}

def check_in():
    employee_id = int(input("Enter employee ID: "))
    now = datetime.datetime.now()
    attendance[employee_id] = {'check_in': now}
    print(f"Employee {employee_id} checked in at {now}")

def check_out():
    employee_id = int(input("Enter employee ID: "))
    if employee_id not in attendance:
        print("Employee has not checked in.")
        return
    now = datetime.datetime.now()
    attendance[employee_id]['check_out'] = now
    print(f"Employee {employee_id} checked out at {now}")
    hours_worked = calculate_hours(employee_id)
    overtime = calculate_overtime(employee_id)
    print(f"Hours worked: {hours_worked:.2f}")
    print(f"Overtime: {overtime:.2f}")
    print(attendance)

def calculate_hours(employee_id):
    check_in_time = attendance[employee_id]['check_in']
    check_out_time = attendance[employee_id]['check_out']
    hours_worked = check_out_time - check_in_time
    return hours_worked.total_seconds() / 3600

def calculate_overtime(employee_id):
    hours_worked = calculate_hours(employee_id)
    if hours_worked > 8:
        overtime = hours_worked - 8
    else:
        overtime = 0
    return overtime

while True:
    print("Select an option:")
    print("1. Check in")
    print("2. Check out")
    print("3. Exit")
    choice = int(input())
    if choice == 1:
        check_in()
    elif choice == 2:
        check_out()
    elif choice == 3:
        break
    else:
        print("Invalid choice. Please try again.")
