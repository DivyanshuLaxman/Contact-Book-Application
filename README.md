# Contact-Book-Application
Making simple contact book app using python 
import csv
import os

# Defining the CSV file name
csv_file = 'contacts.csv'

# Making function to add a new contact
def add_contact(name, phone, email, address):
    with open(csv_file, 'a', newline='') as file:  # Opening the csv_file in append mode
        writer = csv.writer(file)  # Creating a CSV writer object
        writer.writerow([name, phone, email, address])  # Writing the contact details as a row
    print(f"Contact {name} added successfully!")  # Confirmation msg after saving the contact

# Making function to view all contacts
def view_contacts():
    if not os.path.exists(csv_file):  # Checking if the file exists
        print("No contacts found.")
        return

    with open(csv_file, 'r') as file:  # Opening the file in read mode
        reader = csv.reader(file)  # Creating a CSV reader object
        for row in reader:  
            print(f"Name: {row[0]}, Phone: {row[1]}, Email: {row[2]}, Address: {row[3]}")  # Print contact details

# Making function to update a contact
def update_contact(name, phone=None, email=None, address=None):
    contacts = []

    with open(csv_file, 'r') as file:
        reader = csv.reader(file)  # Creating a CSV reader object
        found = False
        for row in reader:
            if row[0] == name:  # Checking if the contact name matches
                found = True
                if phone: row[1] = phone  # This update phone if provided
                if email: row[2] = email  # This update email if provided
                if address: row[3] = address  # This update address if provided
                print(f"Contact {name} updated successfully!")  # Printing confirmation message after update
            contacts.append(row)

        if not found:
            print(f"Contact {name} not found.")  # Inform the user if the contact is not found

    with open(csv_file, 'w', newline='') as file:  # Opening the file in write mode
        writer = csv.writer(file)  # Creating a CSV writer object
        writer.writerows(contacts)  # Writing all updated contacts back to the file

# Making function to delete a contact
def delete_contact(name):
    contacts = []

    with open(csv_file, 'r') as file:  # Opening the file in read mode
        reader = csv.reader(file)  # Creating a CSV reader object
        found = False
        for row in reader:
            if row[0] == name:  # Checking if the contact name matches
                found = True
                print(f"Contact {name} deleted successfully!")  # Confirmation message
                continue
            contacts.append(row)

        if not found:
            print(f"Contact {name} not found.")  # Inform the user if the contact is not found

    with open(csv_file, 'w', newline='') as file:  # Opening the file in write mode
        writer = csv.writer(file)  # Creating a CSV writer object
        writer.writerows(contacts)  # Writing all remaining contacts back to the file

# Making function to search for a contact
def search_contact(name):
    with open(csv_file, 'r') as file:  # Opening the file in read mode
        reader = csv.reader(file)  # Creating a CSV reader object
        found = False
        for row in reader:
            if row[0] == name:  # Checking if the contact name matches
                found = True
                print(f"Found contact - Name: {row[0]}, Phone: {row[1]}, Email: {row[2]}, Address: {row[3]}")  # Print contact details
                break

        if not found:
            print(f"Contact {name} not found.")  # Inform the user if the contact is not found

# Making Main menu with several function
def menu():
    while True:
        print("\nContact Book Menu:")
        print("1. Add Contact")
        print("2. View Contacts")
        print("3. Update Contact")
        print("4. Delete Contact")
        print("5. Search Contact")
        print("6. Exit")
        
        choice = input("Enter your choice: ")
        
        if choice == '1':
            name = input("Enter name: ")
            phone = input("Enter phone: ")
            email = input("Enter email: ")
            address = input("Enter address: ")
            add_contact(name, phone, email, address)
        
        elif choice == '2':
            view_contacts()
        
        elif choice == '3':
            name = input("Enter name of the contact to update: ")
            phone = input("Enter new phone (leave blank to keep current): ")
            email = input("Enter new email (leave blank to keep current): ")
            address = input("Enter new address (leave blank to keep current): ")
            update_contact(name, phone, email, address)
        
        elif choice == '4':
            name = input("Enter name of the contact to delete: ")
            delete_contact(name)
        
        elif choice == '5':
            name = input("Enter name to search: ")
            search_contact(name)
        
        elif choice == '6':
            print("Exiting the Contact Book. Goodbye!")
            break
        
        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    menu()
