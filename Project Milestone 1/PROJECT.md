# Project Milestone 1: Personal Finance Tracker 💰

**Goal:** Build a robust console-based application to track income and expenses.
**Scope:** Covers topics from **Folder 1 (Variables)** to **Folder 8 (Typedef)**.

## 📋 Project Requirements

You must implement a system that satisfies the following criteria, ensuring you use the specific Dart features listed:

### 1. Data Structure (Records & Typedefs)
*   **Typedef:** Define a type alias `Transaction` for a Record that looks like: `({int id, String title, double amount, bool isExpense})`.
*   **Typedef:** Define a type alias `TransactionList` for `List<Transaction>`.

### 2. Storage (Generics & Collections)
*   **Generics:** Create a class `DataStore<T>` that acts as a storage wrapper.
    *   It should hold a `List<T>` internally.
    *   Methods: `addItem(T item)`, `getAll()`, `removeItem(T item)`.
*   **Collections:** Use your `DataStore<Transaction>` to store the finance data.

### 3. Logic & Operations (Variables, Operators, Types)
*   **Variables:** Use `final` and `const` where appropriate.
*   **Operators:**
    *   Calculate the **Total Balance** (Income - Expenses).
    *   Calculate **Total Income** and **Total Expense** separately.
*   **Built-in Types:** Ensure correct usage of `int` for IDs, `double` for money, and `String` for text.

### 4. Functionality
*   **Add Transaction:** Allow adding a new record.
*   **View All:** Print all transactions formatted nicely.
*   **Summary:** Print the calculated totals.
*   **Filter:** (Bonus) Use a function to filter expenses > $100.

### 5. Documentation (Comments)
*   **Comments:** Add `///` documentation comments for your class and methods.
*   **Comments:** Use `//` inside methods to explain complex logic (like the balance calculation).

---

## 💻 Example Usage Flow

```dart
void main() {
  // 1. Initialize Store
  var financeStore = DataStore<Transaction>();

  // 2. Add Data
  financeStore.addItem((id: 1, title: 'Salary', amount: 5000.0, isExpense: false));
  financeStore.addItem((id: 2, title: 'Rent', amount: 1200.0, isExpense: true));
  financeStore.addItem((id: 3, title: 'Groceries', amount: 350.50, isExpense: true));

  // 3. Print Summary
  printFinanceReport(financeStore.getAll());
}
```

**Expected Console Output:**
```
--- Finance Report ---
[+] Salary: $5000.0
[-] Rent: $1200.0
[-] Groceries: $350.5

Total Income: $5000.0
Total Expense: $1550.5
----------------------
Net Balance: $3449.5
```
