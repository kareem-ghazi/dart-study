# Solution: Personal Finance Tracker

```dart
// --- Folder 8: Typedef ---
// Defining a type alias for our Record
typedef Transaction = ({int id, String title, double amount, bool isExpense});

// Defining a type alias for a list of transactions
typedef TransactionList = List<Transaction>;

// --- Folder 7: Generics ---
/// A generic storage class to handle any type of data [T].
/// (Folder 3: Documentation Comments)
class DataStore<T> {
  // Folder 6: Collections (List)
  final List<T> _items = [];

  /// Adds an item to the store.
  void addItem(T item) {
    _items.add(item);
  }

  /// Removes an item from the store.
  void removeItem(T item) {
    _items.remove(item);
  }

  /// Returns a list of all items.
  List<T> getAll() {
    // Return a copy to be safe
    return [..._items];
  }
}

// --- Logic Functions ---

void printFinanceReport(TransactionList transactions) {
  // Folder 1: Variables (double, double)
  double totalIncome = 0.0;
  double totalExpense = 0.0;

  print('--- Finance Report ---');

  // Folder 6: Collections (for-in loop)
  for (var tx in transactions) {
    // Folder 13 (Branches) / Folder 5 (Records Access)
    if (tx.isExpense) {
      // Folder 2: Operators (+=)
      totalExpense += tx.amount;
      print('[-] ${tx.title}: \$${tx.amount}');
    } else {
      totalIncome += tx.amount;
      print('[+] ${tx.title}: \$${tx.amount}');
    }
  }

  // Folder 2: Operators (Subtraction)
  double netBalance = totalIncome - totalExpense;

  print('\nTotal Income: \$$totalIncome');
  print('Total Expense: \$$totalExpense');
  print('----------------------');
  print('Net Balance: \$$netBalance');
}

void main() {
  // Initialize our Generic Store for Transactions
  var financeStore = DataStore<Transaction>();

  // Folder 4: Built-in Types & Folder 5: Records
  // Adding records directly
  financeStore.addItem((id: 1, title: 'Salary', amount: 5000.0, isExpense: false));
  financeStore.addItem((id: 2, title: 'Rent', amount: 1200.0, isExpense: true));
  financeStore.addItem((id: 3, title: 'Groceries', amount: 350.50, isExpense: true));
  financeStore.addItem((id: 4, title: 'Freelance', amount: 450.0, isExpense: false));

  // Get data
  var allData = financeStore.getAll();

  // Run Report
  printFinanceReport(allData);

  // Bonus: Filter usage (Folder 6 .where)
  /*
  var bigExpenses = allData.where((t) => t.isExpense && t.amount > 1000);
  print('\nBig Expenses: $bigExpenses');
  */
}
```