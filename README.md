class Task:
    def __init__(self, name, priority):
        self.name = name
        self.priority = priority
        self.completed = False

    def mark_done(self):
        self.completed = True

    def show(self):
        status = "Done" if self.completed else "Pending"
        print(f"{self.name} | Priority: {self.priority} | Status: {status}")


class ImportantTask(Task):
    def __init__(self, name):
        super().__init__(name, priority=1)

    def show(self):
        print("Important Task -", end=" ")
        super().show()


class TaskManager:
    def __init__(self):
        self.tasks = []

    def add(self, task):
        self.tasks.append(task)

    def view_all(self):
        if not self.tasks:
            print("No tasks available.")
        for task in self.tasks:
            task.show()

    def view_by_priority(self):
        if not self.tasks:
            print("No tasks available.")
        sorted_tasks = sorted(self.tasks, key=lambda x: x.priority)
        for task in sorted_tasks:
            task.show()

    def mark_done(self, name):
        for task in self.tasks:
            if task.name == name:
                task.mark_done()
                print("Task marked as done.")
                return
        print("Task not found.")

    def delete(self, name):
        for task in self.tasks:
            if task.name == name:
                self.tasks.remove(task)
                print("Task deleted.")
                return
        print("Task not found.")


def main():
    manager = TaskManager()

    while True:
        print("\nTask Scheduler Menu")
        print("1. Add Task")
        print("2. Add Important Task")
        print("3. View All Tasks")
        print("4. View Tasks by Priority")
        print("5. Mark Task as Done")
        print("6. Delete Task")
        print("7. Exit")

        choice = input("Choose an option (1-7): ")

        if choice == '1':
            name = input("Task name: ")
            priority = int(input("Priority (1 = High, 5 = Low): "))
            manager.add(Task(name, priority))

        elif choice == '2':
            name = input("Important task name: ")
            manager.add(ImportantTask(name))

        elif choice == '3':
            manager.view_all()

        elif choice == '4':
            manager.view_by_priority()

        elif choice == '5':
            name = input("Enter the task name to mark as done: ")
            manager.mark_done(name)

        elif choice == '6':
            name = input("Enter the task name to delete: ")
            manager.delete(name)

        elif choice == '7':
            print("Exiting the program. Goodbye!")
            break

        else:
            print("Invalid choice. Please enter a number from 1 to 7.")


main()
