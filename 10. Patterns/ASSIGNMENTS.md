# Assignments: Patterns

Practice using patterns for matching and destructuring data in Dart.

## Assignment 1: Basic Destructuring
**Objective:** Learn how to extract values from Lists and Maps using patterns.
*(الهدف: تعلم كيفية استخراج القيم من القوائم والخرائط باستخدام الأنماط.)*

**Instructions:**
1.  Create a List containing three colors: `'Red'`, `'Green'`, `'Blue'`.
2.  Use a pattern variable declaration to destructure this list into three variables: `c1`, `c2`, `c3`.
3.  Create a Map representing a book: `{'title': 'Dart Guide', 'price': 29.99}`.
4.  Use a pattern to destructure the map into variables `title` and `price`.
5.  Print all the extracted variables.

**Expected Output:**
```
Colors: Red, Green, Blue
Book: Dart Guide costs $29.99
```

---

## Assignment 2: Switch Expression with Patterns
**Objective:** Use patterns in a switch expression to classify data.
*(الهدف: استخدام الأنماط في تعبير `switch` لتصنيف البيانات.)*

**Instructions:**
1.  Write a function `classify(int number)` that returns a String.
2.  Use a `switch` expression to return:
    *   "Zero" if the number is 0.
    *   "Small Positive" if the number is between 1 and 10 (inclusive).
    *   "Negative" if the number is less than 0.
    *   "Large" for anything else.
3.  Call the function with -5, 0, 5, and 100 and print the results.

**Expected Output:**
```
-5 is Negative
0 is Zero
5 is Small Positive
100 is Large
```

---

## Assignment 3: JSON Validation & Extraction
**Objective:** Validate and destructure nested JSON-like data using `if-case`.
*(الهدف: التحقق من صحة البيانات المتداخلة (JSON-like) وتفكيكها باستخدام `if-case`.)*

**Instructions:**
1.  Simulate a JSON response from an API:
    ```dart
    var response = {
      'status': 200,
      'data': {
        'username': 'dart_master',
        'roles': ['admin', 'editor']
      }
    };
    ```
2.  Write an `if-case` statement that checks:
    *   `status` is 200.
    *   `data` contains a `username` (String) and `roles` (List of Strings).
3.  Inside the `if` block, print the username and the first role found in the list.
4.  Add an `else` block to print "Invalid Response" if the pattern doesn't match.

**Hint:** You can nest patterns like `data: {'username': var u, ...}`.

**Expected Output:**
```
User: dart_master
Primary Role: admin
```

---

## Assignment 4: Object Destructuring with Guard Clauses (Advanced)

**Objective:**
Match specific object shapes and apply conditions using `when`.
*(الهدف: مطابقة أشكال كائنات محددة وتطبيق شروط باستخدام `when`.)*

**Instructions:**
1. Create a class `Shape` with properties `width` and `height`.
2. Create a function `describe(Shape s)` that uses a switch statement.
3. Case 1: Match `Shape(width: w, height: h)` when `w == h`. Return "Square".
4. Case 2: Match any `Shape`. Return "Rectangle".
5. Call it with `Shape(10, 10)` and `Shape(10, 20)`.

**Expected Output:**
```
Square
Rectangle
```

---

## Assignment 5: JSON List Iteration (Advanced)

**Objective:**
Destructure objects directly inside a `for-in` loop.
*(الهدف: تفكيك الكائنات مباشرة داخل حلقة `for-in`.)*

**Instructions:**
1. Create a list of maps: `var users = [{'id': 1, 'name': 'A'}, {'id': 2, 'name': 'B'}]`.
2. Write a `for` loop that iterates over `users`.
3. Use the pattern `{'id': id, 'name': name}` directly in the loop definition (e.g., `for (var {...} in users)`).
4. Print "User [name] has ID [id]".

**Expected Output:**
```
User A has ID 1
User B has ID 2
```

---

## Solutions

### Solution 1: Basic Destructuring

```dart
void main() {
  // List destructuring
  var colors = ['Red', 'Green', 'Blue'];
  var [c1, c2, c3] = colors;
  print('Colors: $c1, $c2, $c3');

  // Map destructuring
  var book = {'title': 'Dart Guide', 'price': 29.99};
  // Using explicit key names to bind to variables
  var {'title': title, 'price': price} = book;
  print('Book: $title costs \$$price');
}
```

### Solution 2: Switch Expression with Patterns

```dart
String classify(int number) {
  return switch (number) {
    0 => 'Zero',
    >= 1 && <= 10 => 'Small Positive',
    < 0 => 'Negative',
    _ => 'Large',
  };
}

void main() {
  var numbers = [-5, 0, 5, 100];
  for (var n in numbers) {
    print('$n is ${classify(n)}');
  }
}
```

### Solution 3: JSON Validation & Extraction

```dart
void main() {
  var response = {
    'status': 200,
    'data': {
      'username': 'dart_master',
      'roles': ['admin', 'editor']
    }
  };

  // Validating nested structure
  if (response case {'status': 200, 'data': {'username': String u, 'roles': [String r1, ...]} }) {
    print('User: $u');
    print('Primary Role: $r1');
  } else {
    print('Invalid Response');
  }
}
```

### Solution 4: Object Destructuring with Guard Clauses

```dart
class Shape {
  final int width;
  final int height;
  Shape(this.width, this.height);
}

String describe(Shape s) {
  return switch (s) {
    Shape(width: var w, height: var h) when w == h => 'Square',
    Shape() => 'Rectangle',
  };
}

void main() {
  print(describe(Shape(10, 10)));
  print(describe(Shape(10, 20)));
}
```

### Solution 5: JSON List Iteration

```dart
void main() {
  var users = [
    {'id': 1, 'name': 'A'},
    {'id': 2, 'name': 'B'}
  ];
  
  for (var {'id': id, 'name': name} in users) {
    print('User $name has ID $id');
  }
}
```
