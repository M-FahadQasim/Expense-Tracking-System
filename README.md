#include <iostream>
#include <map>
#include <string>

using namespace std;

// Structure to represent an expense
struct Expense {
    string date;
    string description;
    double amount;
};

// Map to store expenses
map<string, Expense> expenses;

// Function to add an expense
void addExpense() {
    Expense expense;
    cout << "Enter date (YYYY-MM-DD): ";
    cin >> expense.date;
    cout << "Enter description: ";
    cin.ignore();
    getline(cin, expense.description);
    cout << "Enter amount: ";
    cin >> expense.amount;
    expenses[expense.date + " - " + expense.description] = expense;
    cout << "Expense added successfully!" << endl;
}

// Function to modify an expense
void modifyExpense() {
    string key;
    cout << "Enter date and description of expense to modify (YYYY-MM-DD - Description): ";
    cin.ignore();
    getline(cin, key);
    if (expenses.find(key) != expenses.end()) {
        Expense expense;
        cout << "Enter new date (YYYY-MM-DD): ";
        cin >> expense.date;
        cout << "Enter new description: ";
        cin.ignore();
        getline(cin, expense.description);
        cout << "Enter new amount: ";
        cin >> expense.amount;
        expenses.erase(key);
        expenses[expense.date + " - " + expense.description] = expense;
        cout << "Expense modified successfully!" << endl;
    } else {
        cout << "No Expense  found!" << endl;
    }
}

// Function to remove an expense
void removeExpense() {
    string key;
    cout << "Enter date and description of expense to remove (YYYY-MM-DD - Description): ";
    cin.ignore();
    getline(cin, key);
    if (expenses.find(key) != expenses.end()) {
        expenses.erase(key);
        cout << "Expense removed successfully!" << endl;
    } else {
        cout << "Expense not found!" << endl;
    }
}

// Function to display weekly report
void weeklyReport() {
    double total = 0;
    cout << "Weekly Report:" << endl;
    for (auto& expense : expenses) {
        total += expense.second.amount;
    }
    cout << "Total expenses for the week: " << total << endl;
}

// Function to display monthly report
void monthlyReport() {
    double total = 0;
    string month;
    cout << "Enter month (MM): ";
    cin >> month;
    cout << "Monthly Report for month " << month << ":" << endl;
    for (auto& expense : expenses) {
        if (expense.first.substr(5, 2) == month) {
            total += expense.second.amount;
        }
    }
    cout << "Total expenses for the month: " << total << endl;
}

// Function to display yearly report
void yearlyReport() {
    double total = 0;
    string year;
    cout << "Enter year (YYYY): ";
    cin >> year;
    cout << "Yearly Report for year " << year << ":" << endl;
    for (auto& expense : expenses) {
        if (expense.first.substr(0, 4) == year) {
            total += expense.second.amount;
        }
    }
    cout << "Total expenses for the year: " << total << endl;
}

int main() {
    int choice;
    while (true) {
        cout << "Expense Tracking System" << endl;
        cout << "1. Add Expense" << endl;
        cout << "2. Modify Expense" << endl;
        cout << "3. Remove Expense" << endl;
        cout << "4. Weekly Report" << endl;
        cout << "5. Monthly Report" << endl;
        cout << "6. Yearly Report" << endl;
        cout << "7. Exit" << endl;
        cout << "Enter your choice: ";
        cin >> choice;
        switch (choice) {
            case 1:
                addExpense();
                break;
            case 2:
                modifyExpense();
                break;
            case 3:
                removeExpense();
                break;
            case 4:
                weeklyReport();
                break;
            case 5:
                monthlyReport();
                break;
            case 6:
                yearlyReport();
                break;
            case 7:
                return 0;
            default:
                cout << "Invalid choice. Please try again." << endl;
        }
    }
    return 0;
}
