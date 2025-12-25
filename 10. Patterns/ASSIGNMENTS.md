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

## Assignment 4: List Head/Tail (List pattern)

**Objective:**
Use list patterns to separate the first element from the rest.
*(الهدف: استخدام أنماط القائمة لفصل العنصر الأول عن الباقي.)*

**Instructions:**
1. Create a list `[10, 20, 30, 40]`.
2. Use a pattern `[head, ...tail]` to destructure it.
3. Print the head and the tail.

**Expected Output:**
```
Head: 10
Tail: [20, 30, 40]
```

---

## Assignment 5: Logic Check (Logical patterns)

**Objective:**
Use logical-or patterns in a switch.
*(الهدف: استخدام أنماط OR المنطقية في جملة switch.)*

**Instructions:**
1. Create a variable `command` with value "STOP".
2. Use a switch statement.
3. Match "STOP" or "EXIT" or "QUIT" in a single case using `||`.
4. Print "Stopping...".

**Expected Output:**
```
Stopping...
```

---

## Solutions

```dart
// Assignment 1
void assignment1() {
  // List destructuring
  var colors = ['Red', 'Green', 'Blue'];
  var [c1, c2, c3] = colors;
  print('Colors: $c1, $c2, $c3');

  // Map destructuring
  var book = {'title': 'Dart Guide', 'price': 29.99};
  // Using explicit key names to bind to variables
  var {'title': title, 'price': price} = book;
  print('Book: $title costs $$price');
}

// Assignment 2
String classify(int number) {
  return switch (number) {
    0 => 'Zero',
    >= 1 && <= 10 => 'Small Positive',
    < 0 => 'Negative',
    _ => 'Large',
  };
}

void assignment2() {
  var numbers = [-5, 0, 5, 100];
  for (var n in numbers) {
    print('$n is ${classify(n)}');
  }
}

// Assignment 3
void assignment3() {
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

// Assignment 4
void assignment4() {
  var list = [10, 20, 30, 40];
  var [head, ...tail] = list;
  print('Head: $head');
  print('Tail: $tail');
}

// Assignment 5
void assignment5() {
  var command = "STOP";
  switch (command) {
    case "STOP" || "EXIT" || "QUIT":
      print("Stopping...");
  }
}

void main() {
  print('--- Assignment 1 ---');
  assignment1();
  print('\n--- Assignment 2 ---');
  assignment2();
  print('\n--- Assignment 3 ---');
  assignment3();
  print('\n--- Assignment 4 ---');
  assignment4();
  print('\n--- Assignment 5 ---');
  assignment5();
}
```