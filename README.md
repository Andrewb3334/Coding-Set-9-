# Coding-Set-9-

import pickle

def load_data(filename):
    try:
        with open(filename, 'rb') as f:
            return pickle.load(f)
    except FileNotFoundError:
        return {}

def save_data(data, filename):
    with open(filename, 'wb') as f:
        pickle.dump(data, f)

def main():
    # Define your filename
    filename = 'contacts.pickle'
    
    # Load existing data or initialize an empty dictionary
    contacts = load_data(filename)
    
    # Example usage: Adding a contact
    name = 'John Doe'
    email = 'john.doe@example.com'
    contacts[name] = email
    
    # Save data after making changes
    save_data(contacts, filename)
    
    # Other operations can be performed here...

if __name__ == "__main__":
    main()

filename = '/path/to/your/directory/contacts.pickle'

import pickle
import os

# Function loading the dictionary from a certain file 
def load_data(filename):
    data = {}
    if os.path.exists(filename):
        with open(filename, 'rb') as file:
            data = pickle.load(file)
    return data

# Function that will save the dictionary to a file
def save_data(data, filename):
    with open(filename, 'wb') as file:
        pickle.dump(data, file)

#Function to show the menu and choose user choices
def main():
    filename = 'contacts.pickle' # File to store the dictionary
    contacts = load_data(filename) # Find existing contacts and create an empty dictionary 

    while True:
        print("\n***** Menu *****")
        print("1. Look up an email address")
        print("2. Add a new name and email address")
        print("3. Change an email address")
        print("4. Delete a name and email address")
        print("5. Display all names and email addresses")
        print("6. Exit")

        choice = input("Enter your choice (1-6): ")

        if choice == '1':
            name = input("Enter a name to look up: ").strip().lower()
            if name in contacts: 
                print(f"Email address for {name}: {contacts[name]}")
            else:
                print(f"{name} not found in contacts.")
        
        elif choice == '2':
            name = input("Enter new name: ").strip().lower()
            email = input("Enter new email address: ").strip()
            contacts[name] = email
            save_data(contacts, filename)
            print(f"{name} added to contacts.")
        
        elif choice == '3':
            name = input("Enter name to change email address: ").strip().lower()
            if name in contacts: 
                new_email = input("Enter new email address: ").strip()
                contacts[name] = new_email
                save_data(contacts, filename)
                print(f"Email address updated for {name}.")
            else:
                print(f"{name} not found in contacts.")

        elif choice == '4': 
            name = input("Enter name to delete: ").strip().lower
            if name in contacts: 
                del contacts[name]
                save_data(contacts, filename)
                print(f"{name} deleted from contacts.")
            else:
                print(f"{name} not found in contacts.")

        elif choice == '6':
            save_data(contacts, filename)
            print("Exiting program.")
            break

        else:
            print("Invalid choice. Please enter a number from 1 to 6.")

if __name__ == "__main__":
    main()
