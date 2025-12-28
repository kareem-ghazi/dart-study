# Assignments: Generics

## Assignment 1: Type-Safe List (Basic)

**Objective:**
Understand how to use Generics to create type-safe collections.
**(فهم كيفية استخدام Generics لإنشاء مجموعات آمنة النوع.)**

**Instructions:**
1.  Create a list of integers named `scores`.
2.  Try to add a generic `dynamic` value to it (commented out) to see the error, or just ensure you define it strictly as `List<int>`.
3.  Add numbers 90, 85, 77.
4.  Write a function `calculateAverage` that takes `List<int>` and returns a `double`.
5.  Print the average score.
**(1. أنشئ قائمة أعداد صحيحة باسم `scores`. 2. تأكد من تعريفها كـ `List<int>`. 3. أضف الأرقام. 4. اكتب دالة لحساب المتوسط تقبل قائمة أعداد صحيحة وترجع عدداً عشرياً. 5. اطبع المتوسط.)**

**Expected Output:**
```
Average: 84.0
```

---

## Assignment 2: Generic Box (Intermediate)

**Objective:**
Create a Generic class that can hold any type of value.
**(إنشاء فئة عامة يمكنها حمل أي نوع من القيم.)**

**Instructions:**
1.  Create a class named `Box<T>`.
2.  It should have a private field `_value` of type `T` and methods `put(T value)` and `T get()`.
3.  In `main`, create a `Box<String>` and store "Hello".
4.  Create a `Box<int>` and store 123.
5.  Retrieve and print both values.
**(1. أنشئ فئة باسم `Box<T>`. 2. يجب أن تحتوي على حقل خاص `_value` من النوع `T` وطرق `put` و `get`. 3. في `main`، أنشئ صندوقاً للنصوص وخزن "Hello". 4. أنشئ صندوقاً للأرقام وخزن 123. 5. استرجع واطبع القيمتين.)**

**Expected Output:**
```
String Box: Hello
Int Box: 123
```

---

## Assignment 3: Generic Swapper (Advanced)

**Objective:**
Write a generic method to process distinct types dynamically.
**(كتابة دالة عامة لمعالجة أنواع متميزة ديناميكياً.)**

**Instructions:**
1.  Write a generic function called `swapValues<T>` that accepts a `List<T>` and two indices (index1, index2).
2.  The function should swap the elements at those indices in the list.
3.  Test it with a `List<String>` `['A', 'B', 'C']` swapping 0 and 2.
4.  Test it with a `List<int>` `[1, 2, 3]` swapping 1 and 2.
5.  Print the modified lists.
**(1. اكتب دالة عامة `swapValues<T>` تقبل قائمة ومؤشرين. 2. يجب أن تقوم الدالة بتبديل العناصر في هذين الموقعين. 3. جربها مع قائمة نصوص. 4. جربها مع قائمة أرقام. 5. اطبع القوائم المعدلة.)**

**Expected Output:**
```
Swapped Strings: [C, B, A]
Swapped Ints: [1, 3, 2]
```

---

## Assignment 4: Bounded Generics (Advanced)

**Objective:**
Restrict generic types using `extends` to ensure they support specific operations (like math).
*(الهدف: تقييد الأنواع العامة باستخدام `extends` للتأكد من أنها تدعم عمليات معينة (مثل الرياضيات).)*

**Instructions:**
1. Write a function `T sum<T extends num>(T a, T b)`.
2. Inside, return `(a + b) as T`. (Note: Dart math returns appropriate num type, casting might be needed for strict T).
3. Call it with two integers `10` and `20`.
4. Call it with two doubles `1.5` and `2.5`.
5. Try calling it with Strings (commented out) to see the compile error.

**Expected Output:**
```
Sum Int: 30
Sum Double: 4.0
```

---

## Assignment 5: Generic Storage Service (Expert)

**Objective:**
Simulate a generic repository with CRUD operations (Create, Read, Update, Delete).
*(الهدف: محاكاة مستودع عام مع عمليات CRUD (إنشاء، قراءة، تحديث، حذف).)*

**Instructions:**
1.  Define an abstract class `Identifiable` with a field `String id`.
2.  Create a class `User` extending `Identifiable` with a `name`.
3.  Create a class `Product` extending `Identifiable` with a `price`.
4.  Create a generic class `Storage<T extends Identifiable>`.
    *   Use a `List<T>` to store items.
    *   Add `save(T item)` (add or update if id exists).
    *   Add `delete(String id)`.
    *   Add `findById(String id)`.
5.  In `main`, create a storage for Users and another for Products. Perform operations and print results.

**Expected Output:**
```
User Saved: Alice
User Updated: Alice (New Name)
Found Product: Laptop
Deleted Product: Laptop
```

---

## Solutions

### Solution 1: Type-Safe List

```dart
double calculateAverage(List<int> scores) {
  if (scores.isEmpty) return 0.0;
  var sum = 0;
  for (var score in scores) {
    sum += score;
  }
  return sum / scores.length;
}

void main() {
  List<int> scores = [90, 85, 77];
  print('Average: ${calculateAverage(scores)}');
}
```

### Solution 2: Generic Box

```dart
class Box<T> {
  late T _value;

  void put(T value) {
    _value = value;
  }

  T get() {
    return _value;
  }
}

void main() {
  var stringBox = Box<String>();
  stringBox.put("Hello");
  print('String Box: ${stringBox.get()}');

  var intBox = Box<int>();
  intBox.put(123);
  print('Int Box: ${intBox.get()}');
}
```

### Solution 3: Generic Swapper

```dart
void swapValues<T>(List<T> list, int i1, int i2) {
  if (i1 >= 0 && i1 < list.length && i2 >= 0 && i2 < list.length) {
    var temp = list[i1];
    list[i1] = list[i2];
    list[i2] = temp;
  }
}

void main() {
  var letters = ['A', 'B', 'C'];
  swapValues(letters, 0, 2);
  print('Swapped Strings: $letters');

  var numbers = [1, 2, 3];
  swapValues(numbers, 1, 2);
  print('Swapped Ints: $numbers');
}
```

### Solution 4: Bounded Generics

```dart
T sum<T extends num>(T a, T b) {
  // Dart arithmetic on 'num' returns 'num'. 
  // We cast to T to satisfy the return type.
  return (a + b) as T; 
}

void main() {
  print('Sum Int: ${sum(10, 20)}');
  print('Sum Double: ${sum(1.5, 2.5)}');
  // sum("A", "B"); // Error: String doesn't extend num
}
```

### Solution 5: Generic Storage Service

```dart
abstract class Identifiable {
  String get id;
}

class User extends Identifiable {
  final String id;
  String name;
  User(this.id, this.name);
  
  @override
  String toString() => 'User(name: $name)';
}

class Product extends Identifiable {
  final String id;
  double price;
  Product(this.id, this.price);
  
  @override
  String toString() => 'Product(price: $price)';
}

class Storage<T extends Identifiable> {
  final List<T> _items = [];

  void save(T item) {
    int index = _items.indexWhere((e) => e.id == item.id);
    if (index >= 0) {
      _items[index] = item; // Update
      print("Updated item: $item");
    } else {
      _items.add(item); // Create
      print("Saved item: $item");
    }
  }

  void delete(String id) {
    _items.removeWhere((e) => e.id == id);
    print("Deleted item with ID: $id");
  }

  T? findById(String id) {
    try {
      return _items.firstWhere((e) => e.id == id);
    } catch (e) {
      return null;
    }
  }
}

void main() {
  var userStore = Storage<User>();
  var u1 = User('1', 'Alice');
  userStore.save(u1);
  
  u1.name = 'Alice Wonderland';
  userStore.save(u1); // Update
  
  var prodStore = Storage<Product>();
  prodStore.save(Product('p1', 999.0));
  
  var found = prodStore.findById('p1');
  print('Found Product: $found');
  
  prodStore.delete('p1');
}
```
