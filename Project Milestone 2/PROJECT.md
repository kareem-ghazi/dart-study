# Project Milestone 2: DartMart CLI 🛒

**Objective:**
Build a robust, modular **Command-Line Interface (CLI) E-Commerce Inventory System**.
This project integrates **all** concepts learned so far, with a specific focus on **Functions**, **Error Handling**, **Libraries**, and **Patterns**.

**Goal:**
Create a system where a store manager can:
1.  Manage Inventory (Add/Remove items).
2.  Process Orders (Add to cart, Checkout).
3.  Search/Filter Products.
4.  Handle errors gracefully (e.g., out of stock, invalid input).

---

## 🎯 Requirements & Topics Used

### 1. Architecture (Topic 17: Libraries & Imports)
*   Split your code into at least **two files**:
    *   `lib/dart_mart_core.dart`: Contains the logic, classes, and types.
    *   `bin/main.dart`: Contains the `main()` function and user interaction loop.
*   Use the `library`, `part`, or `import` directives correctly.

### 2. Data Structures (Topic 4, 5, 6, 7: Types, Records, Collections, Generics)
*   **Product Class:** Should have properties like `id`, `name`, `price`, `stock`.
*   **Inventory:** Use a `Map<int, Product>` or `List<Product>` to store items.
*   **Cart:** A collection to hold items the user wants to buy.
*   **Generics:** Create a generic `Repository<T>` class that can store and retrieve items (Products, Users, etc.).
*   **Records:** Use a Record `(bool success, String message)` as a return type for operations like "AddToCart".

### 3. Logic & Control Flow (Topic 10, 12, 13: Patterns, Loops, Branches)
*   **CLI Loop:** Use a `while` loop to keep the program running until the user types "exit".
*   **Switch Expression/Pattern:** Use a `switch` statement or expression to handle user commands (`add`, `list`, `buy`, `search`).
*   **Pattern Matching:** Use pattern matching (e.g., `if (product case Product(stock: > 0))`) to validate availability.

### 4. Safety & Robustness (Topic 14, 15: Error Handling, Functions)
*   **Custom Exception:** Create an `OutOfStockException` and throw it when buying more than available.
*   **Try-Catch:** Wrap user input parsing (`int.parse`) and business logic in `try-catch` blocks to prevent crashes.
*   **Functions:**
    *   Use **Named Parameters** for product creation.
    *   Use **Arrow Syntax** for short getters.
    *   Use a **typedef** for a "FilterFunction" (e.g., filter by price < X).

### 5. Meta-programming (Topic 16: Metadata)
*   Mark an old method (e.g., `checkoutLegacy()`) as `@Deprecated` and suggest the new one.
*   Use `@override` for `toString()` methods in your classes.

---

## 📝 Expected User Interaction

```text
--- Welcome to DartMart 🛒 ---
Commands: [list] [add] [cart] [checkout] [exit]

> add
Enter Product (Name, Price, Stock): Apple, 1.5, 100
Success: Added Apple.

> list
1. Apple ($1.5) - Stock: 100

> buy
Enter Product ID: 1
Enter Quantity: 10
Added to cart.

> checkout
Total: $15.0
Receipt generated.

> buy
Enter Product ID: 1
Enter Quantity: 200
Error: OutOfStockException: Only 90 items left of Apple!
```

## 🚀 Hints
1.  **Start with the Core:** Build your `Product` class and `Repository` in the library file first.
2.  **Mock the Library:** If you are running in a single-file environment (like DartPad), you can put everything in one file but conceptually separate them with comments. For this project, try to simulate the structure or actually create the files if working locally.
3.  **Records are powerful:** Use them to return multiple values without creating a new class.

Good luck! 💙
