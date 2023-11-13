# Expense--Tracker
#a basic expense tracker that allows users to input their expenses, categorize them, and view a summary of their spending over time. Using java

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
import java.util.Scanner;

class Expense {
    String category;
    double amount;
    String date;

    Expense(String category, double amount, String date) {
        this.category = category;
        this.amount = amount;
        this.date = date;
    }
}

public class ExpenseTracker {
    private static List<Expense> expenses = new ArrayList<>();
    private static Map<String, Double> categoryTotal = new HashMap<>();

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.println("\nExpense Tracker Menu:");
            System.out.println("1. Add Expense");
            System.out.println("2. View Expenses");
            System.out.println("3. Exit");
            System.out.print("Enter your choice: ");

            int choice = scanner.nextInt();
            scanner.nextLine(); // Consume the newline character

            switch (choice) {
                case 1:
                    addExpense(scanner);
                    break;
                case 2:
                    viewExpenses();
                    break;
                case 3:
                    System.out.println("Exiting Expense Tracker. Goodbye!");
                    System.exit(0);
                default:
                    System.out.println("Invalid choice. Please enter a valid option.");
            }
        }
    }

    private static void addExpense(Scanner scanner) {
        System.out.print("Enter expense category: ");
        String category = scanner.nextLine();

        System.out.print("Enter expense amount: ");
        double amount = scanner.nextDouble();

        System.out.print("Enter expense date (MM/DD/YYYY): ");
        String date = scanner.next();
        scanner.nextLine(); // Consume the newline character

        Expense expense = new Expense(category, amount, date);
        expenses.add(expense);

        // Update category total
        categoryTotal.put(category, categoryTotal.getOrDefault(category, 0.0) + amount);

        System.out.println("Expense added successfully!");
    }

    private static void viewExpenses() {
        if (expenses.isEmpty()) {
            System.out.println("No expenses to display.");
            return;
        }

        System.out.println("\nExpense Summary:");
        for (Expense expense : expenses) {
            System.out.println("Category: " + expense.category + " | Amount: $" + expense.amount + " | Date: " + expense.date);
        }

        System.out.println("\nCategory Totals:");
        for (Map.Entry<String, Double> entry : categoryTotal.entrySet()) {
            System.out.println(entry.getKey() + ": $" + entry.getValue());
        }
    }
}
