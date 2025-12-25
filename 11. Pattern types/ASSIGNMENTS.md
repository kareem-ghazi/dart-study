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

## Assignment 4: Cast Pattern (as operator)

**Objective:**
Use the cast pattern to handle dynamic types safely.
*(الهدف: استخدام نمط التحويل للتعامل مع الأنواع الديناميكية بأمان.)*

**Instructions:**
1. Create a variable `dynamic d = 10`.
2. Use a switch statement on `d`.
3. Match it using `var i as int`.
4. Print "It is an integer: [i]".

**Expected Output:**
```
It is an integer: 10
```

---

## Assignment 5: Range Check (Relational)

**Objective:**
Use relational patterns to validate a score.
*(الهدف: استخدام الأنماط العلائقية للتحقق من الدرجة.)*

**Instructions:**
1. Create a function `isValidScore(int score)`.
2. Use a switch expression that returns `true` if score is `>= 0 && <= 100`, else `false`.
3. Print the result for 50 and 150.

**Expected Output:**
```
true
false
```

---

## Solutions

```dart
// Assignment 1
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

// Assignment 2
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

// Assignment 3
class User {
  final String? name;
  final int age;
  User(this.name, this.age);
}

void assignment3() {
  var users = [
    User('Ali', 25),
    User(null, 30),
    User('Sara', 20), // Adult
    User('Kid', 10)   // Minor
  ];

  for (var user in users) {
    switch (user) {
      // Matches if name is NOT null (?) AND age > 18
      case User(name: var n?, age: > 18):
        print('Adult: $n');
      
      // Matches if name IS null
      case User(name: null):
        print('Anonymous User');
      
      default:
        print('Minor');
    }
  }
}

// Assignment 4
void assignment4() {
  dynamic d = 10;
  switch (d) {
    case var i as int:
      print('It is an integer: $i');
  }
}

// Assignment 5
bool isValidScore(int score) => switch(score) {
  >= 0 && <= 100 => true,
  _ => false
};

void main() {
  print('--- Assignment 1 ---');
  checkTemperature(-5);
  checkTemperature(0);
  checkTemperature(20);
  checkTemperature(35);
  checkTemperature(10);

  print('\n--- Assignment 2 ---');
  analyzeList([]);
  analyzeList([5]);
  analyzeList([0, 1, 2]);
  analyzeList([1, 2, 99]);
  analyzeList([5, 5]);

  print('\n--- Assignment 3 ---');
  assignment3();

  print('\n--- Assignment 4 ---');
  assignment4();

  print('\n--- Assignment 5 ---');
  print(isValidScore(50));
  print(isValidScore(150));
}
