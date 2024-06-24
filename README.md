package sectiona.todolist;

import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.ArrayList;
import java.util.Date;
import java.util.List;
import java.util.Scanner;

public class ToDoList {
    private List<Task> tasks;
    private List<Category> categories;

    public ToDoList() {
        tasks = new ArrayList<>();
        categories = new ArrayList<>();
    }

    public void addTask(Task task) {
        tasks.add(task);
    }

    public void removeTask(int index) {
        if (index >= 0 && index < tasks.size()) {
            tasks.remove(index);
        } else {
            System.out.println("Invalid task index.");
        }
    }

    public void displayTasks() {
        if (tasks.isEmpty()) {
            System.out.println("No tasks added yet.");
        } else {
            System.out.println("Tasks:");
            for (int i = 0; i < tasks.size(); i++) {
                System.out.println((i + 1) + ". " + tasks.get(i));
            }
        }
    }

    public void addCategory(Category category) {
        categories.add(category);
    }

    public void removeCategory(int index) {
        if (index >= 0 && index < categories.size()) {
            categories.remove(index);
        } else {
            System.out.println("Invalid category index.");
        }
    }

    public void displayCategories() {
        if (categories.isEmpty()) {
            System.out.println("No categories added yet.");
        } else {
            System.out.println("Categories:");
            for (int i = 0; i < categories.size(); i++) {
                System.out.println((i + 1) + ". " + categories.get(i).getName());
            }
        }
    }

    public static void main(String[] args) {
        ToDoList toDoList = new ToDoList();
        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.println("\nMenu:");
            System.out.println("1. Add Task");
            System.out.println("2. Remove Task");
            System.out.println("3. View Tasks");
            System.out.println("4. Add Category");
            System.out.println("5. Remove Category");
            System.out.println("6. View Categories");
            System.out.println("7. Exit");
            System.out.print("Enter your choice: ");

            int choice;
            try {
                choice = Integer.parseInt(scanner.nextLine());
            } catch (NumberFormatException e) {
                System.out.println("Invalid choice. Please enter a number.");
                continue;
            }

            switch (choice) {
                case 1:
                    System.out.println("Adding Task:");
                    System.out.print("Enter task description: ");
                    String description = scanner.nextLine();
                    System.out.print("Enter task priority (1-High, 2-Medium, 3-Low): ");
                    int priority;
                    try {
                        priority = Integer.parseInt(scanner.nextLine());
                    } catch (NumberFormatException e) {
                        System.out.println("Invalid priority. Using default priority (Medium).");
                        priority = 2;
                    }
                    System.out.print("Enter task due date (dd/MM/yyyy): ");
                    String dueDateStr = scanner.nextLine();
                    Date dueDate;
                    try {
                        dueDate = new SimpleDateFormat("dd/MM/yyyy").parse(dueDateStr);
                    } catch (ParseException e) {
                        System.out.println("Invalid date format. Using current date as due date.");
                        dueDate = new Date();
                    }
                    Task task = new Task(description, priority, dueDate);
                    toDoList.addTask(task);
                    System.out.println("Task added successfully.");
                    break;
                case 2:
                    System.out.println("Removing Task:");
                    System.out.print("Enter task number to remove: ");
                    int taskNumber;
                    try {
                        taskNumber = Integer.parseInt(scanner.nextLine());
                    } catch (NumberFormatException e) {
                        System.out.println("Invalid task number.");
                        continue;
                    }
                    toDoList.removeTask(taskNumber - 1);
                    break;
                case 3:
                    System.out.println("Viewing Tasks:");
                    toDoList.displayTasks();
                    break;
                case 4:
                    System.out.println("Adding Category:");
                    System.out.print("Enter category name: ");
                    String categoryName = scanner.nextLine();
                    Category category = new Category(categoryName);
                    toDoList.addCategory(category);
                    System.out.println("Category added successfully.");
                    break;
                case 5:
                    System.out.println("Removing Category:");
                    System.out.print("Enter category number to remove: ");
                    int categoryNumber;
                    try {
                        categoryNumber = Integer.parseInt(scanner.nextLine());
                    } catch (NumberFormatException e) {
                        System.out.println("Invalid category number.");
                        continue;
                    }
                    toDoList.removeCategory(categoryNumber - 1);
                    break;
                case 6:
                    System.out.println("Viewing Categories:");
                    toDoList.displayCategories();
                    break;
                case 7:
                    System.out.println("Exiting...");
                    scanner.close();
                    return;
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        }
    }
}

class Task {
    private String description;
    private int priority;
    private Date dueDate;
    private boolean completed;

    public Task(String description, int priority, Date dueDate) {
        this.description = description;
        this.priority = priority;
        this.dueDate = dueDate;
        this.completed = false;
    }

    public void markCompleted() {
        completed = true;
    }

    @Override
    public String toString() {
        return "Description: " + description + ", Priority: " + getPriorityString() +
                ", Due Date: " + new SimpleDateFormat("dd/MM/yyyy").format(dueDate) +
                ", Completed: " + completed;
    }

    private String getPriorityString() {
        switch (priority) {
            case 1:
                return "High";
            case 2:
                return "Medium";
            case 3:
                return "Low";
            default:
                return "Unknown";
        }
    }
}

class Category {
    private String name;

    public Category(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}

 class Reminder {
    private String description;
    private Date reminderDate;

    public Reminder(String description, Date reminderDate) {
        this.description = description;
        this.reminderDate = reminderDate;
    }

    public String getDescription() {
        return description;
    }

    public Date getReminderDate() {
        return reminderDate;
    }

    @Override
    public String toString() {
        return "Reminder: " + description + ", Reminder Date: " + reminderDate;
    }
}

 class Note {
    private String title;
    private String content;

    public Note(String title, String content) {
        this.title = title;
        this.content = content;
    }

    public String getTitle() {
        return title;
    }

    public String getContent() {
        return content;
    }

    @Override
    public String toString() {
        return "Title: " + title + ", Content: " + content;
    }
