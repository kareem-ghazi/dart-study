# Assignments: Typedefs

## Assignment 1: Simple Alias (Basic)

**Objective:**
Create a simple type alias for a list of doubles.
**(إنشاء اسم مستعار بسيط لقائمة من الأعداد العشرية.)**

**Instructions:**
1.  Define a typedef `Prices` that is an alias for `List<double>`.
2.  In `main`, declare a variable `cart` of type `Prices`.
3.  Add 10.5, 20.0, and 5.99 to it.
4.  Print the list.
**(1. عرّف typedef باسم `Prices` كاسم مستعار لـ `List<double>`. 2. في `main`، صرح عن متغير `cart` من النوع `Prices`. 3. أضف القيم 10.5، 20.0، و 5.99. 4. اطبع القائمة.)**

**Expected Output:**
```
Prices: [10.5, 20.0, 5.99]
```

---

## Assignment 2: Nested Collection Alias (Intermediate)

**Objective:**
Simplify a complex map structure using typedef.
**(تبسيط هيكل خريطة معقد باستخدام typedef.)**

**Instructions:**
1.  Define a typedef `Classroom` which represents `Map<String, List<String>>` (Teacher Name -> List of Student Names).
2.  Create a variable `myClass` of type `Classroom`.
3.  Add one entry: Key "Mr. Smith", Value `['John', 'Jane', 'Doe']`.
4.  Print the students of "Mr. Smith".
**(1. عرّف typedef باسم `Classroom` يمثل خريطة تربط اسم المعلم بقائمة أسماء الطلاب. 2. أنشئ متغيراً `myClass` من هذا النوع. 3. أضف إدخالاً واحداً. 4. اطبع طلاب "Mr. Smith".)**

**Expected Output:**
```
Students of Mr. Smith: [John, Jane, Doe]
```

---

## Assignment 3: Math Operation Alias (Advanced)

**Objective:**
Use function typedefs to pass logic around.
**(استخدام typedef للدوال لتمرير المنطق.)**

**Instructions:**
1.  Define a typedef `MathOp` for a function that takes two integers and returns an integer.
2.  Write two functions matching this signature: `multiply(int a, int b)` and `divide(int a, int b)` (use integer division `~/`).
3.  Write a function `perform(int x, int y, MathOp op)` that executes the operation and prints the result.
4.  Call `perform` with 10, 2, and `multiply`.
5.  Call `perform` with 10, 2, and `divide`.
**(1. عرّف typedef باسم `MathOp` لدالة تأخذ عددين صحيحين وترجع عدداً صحيحاً. 2. اكتب دالتين `multiply` و `divide` تطابقان هذا التوقيع. 3. اكتب دالة `perform` تنفذ العملية وتطبع النتيجة. 4. استدعِ `perform` مع الضرب والقسمة.)**

**Expected Output:**
```
Result: 20
Result: 5
```

---

## Assignment 4: Generic Typedef Callback (Advanced)

**Objective:**
Create a Generic typedef that can handle different types.
*(الهدف: إنشاء typedef عام يمكنه التعامل مع أنواع مختلفة.)*

**Instructions:**
1. Define a generic typedef `Mapper<T, R>` as a function that takes `T` and returns `R`.
2. Create a function `List<R> transform<T, R>(List<T> items, Mapper<T, R> mapper)`.
3. Inside, iterate over items, apply the mapper, and return the new list.
4. Call it to transform `[1, 2, 3]` (int) to `["1", "2", "3"]` (String).

**Expected Output:**
```
Transformed: [1, 2, 3]
```

---

## Assignment 5: Event System Architecture (Expert)

**Objective:**
Design a type-safe event handler system using generic typedefs.
*(الهدف: تصميم نظام معالجة أحداث آمن النوع باستخدام typedefs العامة.)*

**Instructions:**
1.  Define a generic typedef `EventHandler<T>` as `void Function(T event)`.
2.  Create a class `EventManager`.
    *   It should allow registering handlers for specific event types. (Hint: `Map<Type, List<Function>>`).
    *   `void subscribe<T>(EventHandler<T> handler)`.
    *   `void publish<T>(T event)`.
3.  Create two event classes: `LoginEvent` (String username) and `LogoutEvent`.
4.  In `main`, subscribe to both.
5.  Publish a login event and a logout event.

**Expected Output:**
```
[Log] User Alice logged in.
[Log] User logged out.
```

---

## Solutions

### Solution 1: Simple Alias

```dart
typedef Prices = List<double>;

void main() {
  Prices cart = [10.5, 20.0, 5.99];
  print('Prices: $cart');
}
```

### Solution 2: Nested Collection Alias

```dart
typedef Classroom = Map<String, List<String>>;

void main() {
  Classroom myClass = {
    'Mr. Smith': ['John', 'Jane', 'Doe']
  };
  print('Students of Mr. Smith: ${myClass['Mr. Smith']}');
}
```

### Solution 3: Math Operation Alias

```dart
typedef MathOp = int Function(int a, int b);

int multiply(int a, int b) => a * b;
int divide(int a, int b) => a ~/ b;

void perform(int x, int y, MathOp op) {
  print('Result: ${op(x, y)}');
}

void main() {
  perform(10, 2, multiply);
  perform(10, 2, divide);
}
```

### Solution 4: Generic Typedef Callback

```dart
typedef Mapper<T, R> = R Function(T item);

List<R> transform<T, R>(List<T> items, Mapper<T, R> mapper) {
  var result = <R>[];
  for (var item in items) {
    result.add(mapper(item));
  }
  return result;
}

void main() {
  var nums = [1, 2, 3];
  var strings = transform(nums, (int n) => n.toString());
  print('Transformed: $strings');
}
```

### Solution 5: Event System Architecture

```dart
typedef EventHandler<T> = void Function(T event);

class EventManager {
  final Map<Type, List<Function>> _subscribers = {};

  void subscribe<T>(EventHandler<T> handler) {
    _subscribers.putIfAbsent(T, () => []).add(handler);
  }

  void publish<T>(T event) {
    var handlers = _subscribers[T];
    if (handlers != null) {
      for (var handler in handlers) {
        // Cast the generic function back to the specific type
        (handler as EventHandler<T>)(event);
      }
    }
  }
}

class LoginEvent {
  final String username;
  LoginEvent(this.username);
}

class LogoutEvent {}

void main() {
  var events = EventManager();

  // Subscribe to Login
  events.subscribe<LoginEvent>((e) => print('[Log] User ${e.username} logged in.'));

  // Subscribe to Logout
  events.subscribe<LogoutEvent>((e) => print('[Log] User logged out.'));

  // Fire events
  events.publish(LoginEvent('Alice'));
  events.publish(LogoutEvent());
}
```
