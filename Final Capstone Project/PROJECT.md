# Final Capstone Project: Real-Time Stock Trading Engine 📈

## 🎯 Objective
Build a high-performance **Real-Time Stock Trading Simulation Engine** that mimics a financial exchange. This project is the ultimate test of your Dart skills, integrating **Object-Oriented Programming**, **Functional Programming features**, **Advanced Typing**, and **Concurrency**.

You will build a system where users can place buy/sell orders, stock prices update in real-time via streams, and heavy market analysis calculations are offloaded to background isolates to keep the "main thread" responsive.

## 🛠️ Requirements

### 1. Core Data Models (OOP & Typing)
*   **Enums:** Define `OrderType` (Buy, Sell) and `MarketStatus` (Open, Closed, Halted). Use **enhanced enums** to add properties (e.g., a display string).
*   **Classes & Inheritance:**
    *   `abstract class Asset`: Base class for anything tradable.
    *   `class Stock extends Asset`: Represents a specific stock (Symbol, Price, Company Name).
    *   `class User`: Represents a trader with a portfolio and balance.
*   **Mixins:** Create a `Loggable` mixin that adds a `logTransaction()` method to classes that need audit trails.
*   **Records:** Use records to return multiple values (e.g., a trade result containing `(bool success, double executionPrice, DateTime timestamp)`).
*   **Typedefs:** Define a `typedef PriceUpdateCallback = void Function(double newPrice)`.
*   **Extension Types:** Create a wrapper around `double` called `Money` to ensure type safety for financial calculations (preventing accidental addition of money + distance, for example).
*   **Class Modifiers:** Use `sealed` for a `TransactionResult` class hierarchy (`Success`, `Failure`, `Pending`) to enforce exhaustive switch handling.

### 2. Market Logic (Logic & Collections)
*   **Collections:**
    *   Use a `Map<String, Stock>` to store the market registry.
    *   Use a `Queue<Order>` to manage the order book.
*   **Generics:** Create a generic `Portfolio<T>` class that can hold any subtype of `Asset`.
*   **Callable Objects:** Create a class `TradeExecutor` that can be called like a function `executor(order)` to process a trade.
*   **Extension Methods:** Add an extension on `double` to format it as currency (e.g., `100.0.toCurrency()`).

### 3. Concurrency & Asynchrony (The Heavy Lifting)
*   **Streams:** The Stock Market should emit a `Stream<Stock>` of price updates. Randomly fluctuate prices every second.
*   **Async/Await:** Create an `async` function `placeOrder()` that simulates a network delay (using `Future.delayed`) before confirming the trade.
*   **Isolates:** Implement a `MarketAnalyzer` that runs in a separate **Isolate**.
    *   It should accept a large list of historical price data (generate a list of 1,000,000 random doubles).
    *   It should calculate the **Moving Average** without blocking the main trading thread.
    *   Use `Isolate.run` for this computation.

### 4. Application Flow (Control Flow & Error Handling)
1.  Initialize the market with a set of dummy stocks.
2.  Start the "Market Clock" (Stream).
3.  Create a User with a starting balance.
4.  The user places multiple orders (some valid, some invalid due to insufficient funds).
5.  Use **Pattern Matching** (Topic 10) to destructure the `TransactionResult` and print appropriate messages.
6.  Trigger the background `Isolate` analysis to report market trends periodically.
7.  Handle errors gracefully using `try-catch` blocks (e.g., invalid ticker symbols, negative amounts).

## 📝 Implementation Steps

1.  **Define Models:** Set up your `Stock`, `User`, and `Order` classes using the specified OOP features.
2.  **Setup Extensions & Mixins:** Implement `Money` extension type and `Loggable` mixin.
3.  **Build the Market:** Create the `StockMarket` class that manages the stream of prices.
4.  **Implement Trading Logic:** Write the `TradeExecutor` and `placeOrder` logic.
5.  **Add Concurrency:** Implement the `Isolate` for market analysis.
6.  **Main Simulation:** Write the `main()` function to tie it all together, simulating a 10-second trading session.

## 🔍 Expected Output

```
[Market] Status: Open
[Stream] AAPL price updated: $150.25
[User] Placing BUY order for 10 AAPL...
[Trade] Processing...
[Success] Bought 10 AAPL at $150.25. Remaining Balance: $8,497.50
[Isolate] Analyzing 1,000,000 data points...
[Stream] GOOG price updated: $2,800.00
[Error] Insufficient funds for buying 5 GOOG.
[Isolate] Analysis Complete. Moving Average: 149.8
[Market] Status: Closed
```

## 💡 Hints
*   Remember that `await for` is used to loop through streams.
*   Use `switch` expressions with your `sealed` class for clean result handling.
*   Don't forget to close your streams and ports!
