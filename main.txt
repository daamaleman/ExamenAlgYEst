from municipality import Municipality

def main():
    municipality = Municipality()
    
    while True:
        print("\nMunicipality Procedure Management System")
        print("1. Add citizen to queue")
        print("2. Process next citizen")
        print("3. Display waiting queue")
        print("4. View citizen's procedure history")
        print("5. Exit")
        
        choice = input("Select an option (1-5): ")
        
        if choice == "1":
            name = input("Enter citizen's name: ")
            procedure = input("Enter procedure (e.g., Birth Certificate, Building Permit): ")
            municipality.add_citizen(name, procedure)
            print(f"{name} added to queue with procedure: {procedure}")
        
        elif choice == "2":
            result = municipality.process_next()
            print(result)
        
        elif choice == "3":
            queue = municipality.display_queue()
            print("Waiting Queue:")
            if isinstance(queue, str):
                print(queue)
            else:
                for item in queue:
                    print(item)
        
        elif choice == "4":
            name = input("Enter citizen's name to view history: ")
            history = municipality.get_citizen_history(name)
            print(f"History for {name}:")
            if isinstance(history, str):
                print(history)
            else:
                for item in history:
                    print(item)
        
        elif choice == "5":
            print("Exiting system.")
            break
        
        else:
            print("Invalid option. Please try again.")

if __name__ == "__main__":
    main()