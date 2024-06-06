# motioncut2
# Expense tracker
import csv
import os
from datetime import datetime

FILE_NAME = 'expenses.csv'

def initialize_file():
    """Initialize the CSV file if it doesn't exist."""
    if not os.path.exists(FILE_NAME):
        with open(FILE_NAME, mode='w', newline='') as file:
            writer = csv.writer(file)
            writer.writerow(['Date', 'Category', 'Description', 'Amount'])

def add_expense():
    """Prompt the user to add a new expense."""
    date = datetime.now().strftime("%Y-%m-%d")
    category = input("Enter category: ")
    description = input("Enter description: ")
    try:
        amount = float(input("Enter amount: "))
    except ValueError:
        print("Invalid amount. Please enter a numeric value.")
        return
    
    with open(FILE_NAME, mode='a', newline='') as file:
        writer = csv.writer(file)
        writer.writerow([date, category, description, amount])
    print(f"Added expense: {date}, {category}, {description}, {amount}")

def view_expenses():
    """Display all recorded expenses."""
    if os.path.exists(FILE_NAME):
        with open(FILE_NAME, mode='r') as file:
            reader = csv.reader(file)
            next(reader)  # Skip header row
            expenses = list(reader)
            if expenses:
                print(f"\n{'Date':<15} {'Category':<20} {'Description':<30} {'Amount':<10}")
                print("-" * 75)
                for row in expenses:
                    print(f"{row[0]:<15} {row[1]:<20} {row[2]:<30} {row[3]:<10}")
            else:
                print("No expenses recorded.")
    else:
        print("No expenses found. Please add an expense first.")

def main():
    """Main function to run the expense tracker application."""
    initialize_file()
    
    while True:
        print("\nExpense Tracker")
        print("1. Add Expense")
        print("2. View Expenses")
        print("3. Exit")
        choice = input("Choose an option (1-3): ")

        if choice == '1':
            add_expense()
        elif choice == '2':
            view_expenses()
        elif choice == '3':
            print("Exiting...")
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()
