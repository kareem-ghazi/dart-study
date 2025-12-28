# Solution: DartMart CLI

This solution demonstrates a modular approach using two files.

## File 1: `lib/dart_mart_core.dart`
*Contains the business logic, data models, and helper classes.*

```dart
library dart_mart_core;

// --- Folder 16: Metadata ---
// Marking this library as experimental (simulation)
@deprecated
const String version = "1.0.0-beta";

// --- Folder 8: Typedef ---
// A function type for filtering products
typedef ProductFilter = bool Function(Product);

// --- Folder 14: Error Handling ---
class OutOfStockException implements Exception {
  final String message;
  OutOfStockException(this.message);
  
  @override
  String toString() => 'OutOfStockException: $message';
}

// --- Folder 4 & 5: Built-in Types & Records ---
class Product {
  final int id;
  final String name;
  final double price;
  int stock;

  Product({
    required this.id, 
    required this.name, 
    required this.price, 
    this.stock = 0
  });

  // --- Folder 16: Metadata ---
  @override
  String toString() => '[$id] $name - \$$price (Stock: $stock)';
}

// --- Folder 7: Generics ---
class Repository<T> {
  // --- Folder 6: Collections ---
  final List<T> _items = [];

  void add(T item) => _items.add(item);
  
  List<T> getAll() => [..._items];
  
  T? find(bool Function(T) test) {
    try {
      return _items.firstWhere(test);
    } catch (e) {
      return null;
    }
  }
}

class StoreService {
  final Repository<Product> inventory = Repository<Product>();
  final List<({Product product, int quantity})> cart = [];

  // --- Folder 15: Functions (Named parameters, Return Record) ---
  ({bool success, String message}) addToCart(int productId, int quantity) {
    var product = inventory.find((p) => p.id == productId);

    // --- Folder 10 & 13: Patterns & Branches ---
    if (product case Product(stock: var s) when s >= quantity) {
      cart.add((product: product, quantity: quantity));
      product.stock -= quantity;
      return (success: true, message: 'Added ${product.name} to cart.');
    } else if (product == null) {
      return (success: false, message: 'Product not found.');
    } else {
      // --- Folder 14: Error Handling ---
      throw OutOfStockException('Only ${product.stock} left of ${product.name}!');
    }
  }

  // --- Folder 16: Metadata ---
  @Deprecated('Use calculateTotal() instead')
  double oldCheckout() {
    return 0.0;
  }
  
  double calculateTotal() {
    // --- Folder 12: Loops ---
    double total = 0.0;
    for (var item in cart) {
      total += item.product.price * item.quantity;
    }
    cart.clear();
    return total;
  }
}
```

---

## File 2: `bin/main.dart`
*The entry point that interacts with the user.*

```dart
import 'dart:io';
// In a real project, you would import the relative file:
// import '../lib/dart_mart_core.dart';

// NOTE: For this single-file demonstration to work in some environments,
// you might need to copy the contents of 'dart_mart_core.dart' here 
// or run this in a project structure where the import resolves.
// For now, assume the classes above are available.

void main() {
  final store = StoreService();
  
  // Seed Data
  store.inventory.add(Product(id: 1, name: 'Laptop', price: 999.99, stock: 5));
  store.inventory.add(Product(id: 2, name: 'Mouse', price: 25.50, stock: 50));
  store.inventory.add(Product(id: 3, name: 'Keyboard', price: 45.00, stock: 0)); // Out of stock

  print('--- Welcome to DartMart 🛒 ---');
  print('Commands: list, add, cart, checkout, exit');

  bool running = true;

  // --- Folder 12: Loops ---
  while (running) {
    stdout.write('\n> ');
    String? input = stdin.readLineSync()?.toLowerCase().trim();

    // --- Folder 13: Branches (Switch Statement) ---
    switch (input) {
      case 'exit':
        running = false;
        print('Goodbye!');
        break;

      case 'list':
        print('--- Inventory ---');
        var items = store.inventory.getAll();
        if (items.isEmpty) {
          print('Empty.');
        } else {
          // --- Folder 15: Anonymous Function ---
          items.forEach((p) => print(p));
        }
        break;

      case 'add':
         // Simplified input parsing
         print('Simulating adding product... (Use code to implement full input parsing)');
         store.inventory.add(Product(id: 4, name: 'New Item', price: 10.0, stock: 10));
         print('Added "New Item" automatically.');
         break;

      case 'cart':
        print('--- Enter Product ID to buy ---');
        try {
          String? idStr = stdin.readLineSync();
          int id = int.parse(idStr ?? '0');
          
          print('--- Enter Quantity ---');
          String? qtyStr = stdin.readLineSync();
          int qty = int.parse(qtyStr ?? '0');

          // --- Folder 5: Records (Destructuring result) ---
          var result = store.addToCart(id, qty);
          
          if (result.success) {
            print('✅ ${result.message}');
          } else {
            print('❌ ${result.message}');
          }

        } on FormatException {
          print('❌ Error: Invalid number format.');
        } on OutOfStockException catch (e) {
          print('❌ Stock Error: ${e.message}');
        } catch (e) {
          print('❌ Unexpected Error: $e');
        }
        break;
        
      case 'checkout':
        double total = store.calculateTotal();
        print('💸 Total paid: \$${total.toStringAsFixed(2)}');
        break;

      default:
        print('Unknown command.');
    }
  }
}
```