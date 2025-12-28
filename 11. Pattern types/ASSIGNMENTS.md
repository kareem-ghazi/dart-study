# Assignments: Pattern Types

Explore the specific pattern types like Relational, Logical, and Collection patterns.

## Assignment 1: Relational & Logical Patterns
**Objective:** specific criteria using relational (`<`, `>`) and logical (`&&`, `||`) patterns.
*(الهدف: استخدام الأنماط العلائقية والمنطقية لتصنيف القيم.)*

**Instructions:**
1.  Write a function `checkTemperature(int temp)` that prints a message based on the temperature:
    *   **Cold:** Less than 0.
    *   **Freezing point:** Exactly 0.
    *   **Nice:** Between 15 and 25 (inclusive).
    *   **Hot:** Greater than 30.
    *   **Normal:** Anything else.
2.  Use a `switch` statement with relational and logical patterns (e.g., `> 30`, `>= 15 && <= 25`).
3.  Test it with values: -5, 0, 20, 35, 10.

**Expected Output:**
```
-5 is Cold
0 is Freezing point
20 is Nice
35 is Hot
10 is Normal
```

---

## Assignment 2: Collection & Rest Patterns
**Objective:** Match lists of varying lengths using the Rest element (`...`).
*(الهدف: مطابقة قوائم ذات أطوال متغيرة باستخدام عنصر الباقي `...`.)*

**Instructions:**
1.  Write a function `analyzeList(List<int> numbers)`.
2.  Use a `switch` statement to handle these cases:
    *   Empty list: `[]`.
    *   List with exactly one element: `[var a]`.
    *   List starting with 0: `[0, ...]`.
    *   List ending with 99: `[..., 99]`.
    *   Anything else: `_`.
3.  Print a descriptive message for each case.
4.  Test with: `[]`, `[5]`, `[0, 1, 2]`, `[1, 2, 99]`, `[5, 5]`.

**Expected Output:**
```
Empty list
Single element: 5
Starts with zero
Ends with 99
Unknown list format
```

---

## Assignment 3: Object & Null-Check Patterns
**Objective:** Destructure objects and handle nulls safely in patterns.
*(الهدف: تفكيك الكائنات والتعامل مع القيم الفارغة بأمان.)*

**Instructions:**
1.  Define a class `User` with fields `String? name` and `int age`.
2.  Create a list of users, some with null names.
    *   `User('Ali', 25)`
    *   `User(null, 30)`
    *   `User('Sara', 20)`
3.  Loop through the list using `for`.
4.  Inside the loop, use a `switch` on the user object.
    *   **Case 1:** Name is NOT null and age is > 18. Pattern: `User(name: var n?, age: > 18)`. Print "Adult: [name]".
    *   **Case 2:** Name is null. Pattern: `User(name: null)`. Print "Anonymous User".
    *   **Default:** Print "Minor".
5.  Observe how `var n?` checks for non-null values.

**Expected Output:**
```
Adult: Ali
Anonymous User
Adult: Sara
```

---

## Assignment 4: Validation Logic with Logical Patterns (Advanced)

**Objective:**
Combine Logical-AND (`&&`) and Logical-OR (`||`) to validate complex data.
*(الهدف: دمج AND و OR المنطقيين للتحقق من صحة البيانات المعقدة.)*

**Instructions:**
1. Create a `Map<String, dynamic>` representing a user: `{'age': 20, 'role': 'admin'}`.
2. Use a switch statement (or `if-case`) to validate access.
3. Case: Age must be >= 18 AND Role must be 'admin' OR 'mod'.
   * Pattern: `{'age': >= 18, 'role': 'admin' || 'mod'}`.
4. Print "Access Granted" if matched, else "Access Denied".
5. Test with an admin user and a guest user.

**Expected Output:**
```
Access Granted
```

---

## Assignment 5: Advanced Data Validator (Expert)

**Objective:**
Validate a complex nested JSON structure for a user profile using a single pattern.
*(الهدف: التحقق من صحة هيكل JSON متداخل معقد لملف تعريف المستخدم باستخدام نمط واحد.)*

**Instructions:**
1.  Define a map `json` representing a user response:
    ```dart
    var json = {
      'meta': {'version': 1},
      'payload': [
        {'type': 'user', 'info': {'name': 'Alice', 'active': true}},
        {'type': 'user', 'info': {'name': 'Bob', 'active': false}}
      ]
    };
    ```
2.  Use a `switch` or `if-case` pattern to validate that:
    *   `meta` has `version: 1`.
    *   `payload` is a list.
    *   The first item in payload has `type: 'user'` and an `active` user (`active: true`).
3.  Bind the user's name to a variable `name` and print "Found active user: [name]".
4.  Print "Invalid data" otherwise.

**Expected Output:**
```
Found active user: Alice
```

---

## Solutions

### Solution 1: Relational & Logical Patterns

```dart
void checkTemperature(int temp) {
  switch (temp) {
    case < 0:
      print('$temp is Cold');
    case 0:
      print('$temp is Freezing point');
    case >= 15 && <= 25:
      print('$temp is Nice');
    case > 30:
      print('$temp is Hot');
    default:
      print('$temp is Normal');
  }
}

void main() {
  checkTemperature(-5);
  checkTemperature(0);
  checkTemperature(20);
  checkTemperature(35);
  checkTemperature(10);
}
```

### Solution 2: Collection & Rest Patterns

```dart
void analyzeList(List<int> numbers) {
  switch (numbers) {
    case []:
      print('Empty list');
    case [var a]:
      print('Single element: $a');
    case [0, ...]:
      print('Starts with zero');
    case [..., 99]:
      print('Ends with 99');
    default:
      print('Unknown list format');
  }
}

void main() {
  analyzeList([]);
  analyzeList([5]);
  analyzeList([0, 1, 2]);
  analyzeList([1, 2, 99]);
  analyzeList([5, 5]);
}
```

### Solution 3: Object & Null-Check Patterns

```dart
class User {
  final String? name;
  final int age;
  User(this.name, this.age);
}

void main() {
  var users = [
    User('Ali', 25),
    User(null, 30),
    User('Sara', 20),
    User('Kid', 10)
  ];

  for (var user in users) {
    switch (user) {
      case User(name: var n?, age: > 18):
        print('Adult: $n');
      case User(name: null):
        print('Anonymous User');
      default:
        print('Minor');
    }
  }
}
```

### Solution 4: Validation Logic with Logical Patterns

```dart
void checkAccess(Map<String, dynamic> user) {
  switch (user) {
    case {'age': >= 18, 'role': 'admin' || 'mod'}:
      print('Access Granted');
    default:
      print('Access Denied');
  }
}

void main() {
  checkAccess({'age': 20, 'role': 'admin'});
  checkAccess({'age': 16, 'role': 'admin'});
  checkAccess({'age': 25, 'role': 'guest'});
}
```

### Solution 5: Advanced Data Validator

```dart
void main() {
  var json = {
    'meta': {'version': 1},
    'payload': [
      {'type': 'user', 'info': {'name': 'Alice', 'active': true}},
      {'type': 'user', 'info': {'name': 'Bob', 'active': false}}
    ]
  };

  // Complex single-pattern validation
  switch (json) {
    case {
        'meta': {'version': 1},
        'payload': [
          {'type': 'user', 'info': {'name': String name, 'active': true}},
          ... // Allow other items in payload
        ]
      }:
      print('Found active user: $name');
      
    default:
      print('Invalid data');
  }
}
```