# slashmark-task-1
import json
import os

todo_file = "todo_list.json"

def load_tasks():
    if os.path.exists(todo_file):
        with open(todo_file, "r") as file:
            return json.load(file)
    return []

def save_tasks(tasks):
    with open(todo_file, "w") as file:
        json.dump(tasks, file, indent=4)

def add_task(task):
    tasks = load_tasks()
    tasks.append({"task": task, "done": False})
    save_tasks(tasks)
    print("Task added successfully!")

def view_tasks():
    tasks = load_tasks()
    if not tasks:
        print("No tasks found.")
    else:
        for i, task in enumerate(tasks, 1):
            status = "[X]" if task["done"] else "[ ]"
            print(f"{i}. {status} {task['task']}")

def mark_done(index):
    tasks = load_tasks()
    if 0 <= index < len(tasks):
        tasks[index]["done"] = True
        save_tasks(tasks)
        print("Task marked as done!")
    else:
        print("Invalid task number.")

def remove_task(index):
    tasks = load_tasks()
    if 0 <= index < len(tasks):
        tasks.pop(index)
        save_tasks(tasks)
        print("Task removed successfully!")
    else:
        print("Invalid task number.")

def main():
    while True:
        print("\nTo-Do List")
        print("1. Add Task")
        print("2. View Tasks")
        print("3. Mark Task as Done")
        print("4. Remove Task")
        print("5. Exit")
        choice = input("Choose an option: ")
        
        if choice == "1":
            task = input("Enter the task: ")
            add_task(task)
        elif choice == "2":
            view_tasks()
        elif choice == "3":
            view_tasks()
            index = int(input("Enter task number to mark as done: ")) - 1
            mark_done(index)
        elif choice == "4":
            view_tasks()
            index = int(input("Enter task number to remove: ")) - 1
            remove_task(index)
        elif choice == "5":
            print("Goodbye!")
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()
