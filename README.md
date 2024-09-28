# CODSOFT_TASK01
class TodoList:
    def __init__(self):
        self.tasks = []

    def add_task(self, task):
        self.tasks.append({"task": task, "completed": False})

    def view_tasks(self):
        for i, task in enumerate(self.tasks, start=1):
            status = "Completed" if task["completed"] else "Not completed"
            print(f"{i}. {task['task']} - {status}")

    def update_task(self, task_number, new_task):
        try:
            self.tasks[task_number - 1]["task"] = new_task
        except IndexError:
            print("Invalid task number.")

    def delete_task(self, task_number):
        try:
            del self.tasks[task_number - 1]
        except IndexError:
            print("Invalid task number.")

    def mark_task_as_completed(self, task_number):
        try:
            self.tasks[task_number - 1]["completed"] = True
        except IndexError:
            print("Invalid task number.")

    def save_tasks(self, file_path):
        with open(file_path, 'w') as f:
            json.dump(self.tasks, f)

    def load_tasks(self, file_path):
        if os.path.exists(file_path):
            with open(file_path, 'r') as f:
                self.tasks = json.load(f)
        else:
            print("File not found.")

def main():
    todo = TodoList()

    while True:
        print("\n1. Add task")
        print("\n2. View tasks")
        print("\n3. Update task")
        print("\n4. Delete task")
        print("\n5. Mark task as completed")
        print("\n6. Save tasks to file")
        print("\n7. Load tasks from file")
        print("\n8. Quit")

        choice = input("Choose an option: ")

        if choice == "1":
            task = input("Enter a task: ")
            todo.add_task(task)
        elif choice == "2":
            todo.view_tasks()
        elif choice == "3":
            task_number = int(input("Enter the task number to update: "))
            new_task = input("Enter the new task: ")
            todo.update_task(task_number, new_task)
        elif choice == "4":
            task_number = int(input("Enter the task number to delete: "))
            todo.delete_task(task_number)
        elif choice == "5":
            task_number = int(input("Enter the task number to mark as completed: "))
            todo.mark_task_as_completed(task_number)
        elif choice == "6":
            file_path = input("Enter the file path to save: ")
            todo.save_tasks(file_path)
        elif choice == "7":
            file_path = input("Enter the file path to load: ")
            todo.load_tasks(file_path)
        elif choice == "8":
            break
        else:
            print("Invalid choice. Please choose a valid option.")

if __name__ == "__main__":
    main()
