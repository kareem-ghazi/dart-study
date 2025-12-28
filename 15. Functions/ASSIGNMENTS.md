# Assignments: Functions

Practice creating and using functions in Dart.

## Assignment 1: Simple Greeting
**Objective:** Create a function with positional parameters.
*(الهدف: إنشاء دالة بمعاملات موضعية.)*

**Instructions:**
1.  Write a function named `greet` that takes two arguments: `String name` and `int age`.
2.  The function should print: "Hello [name], you are [age] years old.".
3.  Call this function from `main` with your name and age.

**Expected Output:**
```
Hello Alice, you are 25 years old.
```

---

## Assignment 2: Area Calculator (Named Parameters)
**Objective:** Use named parameters with default values.
*(الهدف: استخدام المعاملات المسماة مع القيم الافتراضية.)*

**Instructions:**
1.  Write a function `calculateArea` that calculates the area of a rectangle.
2.  Use named parameters for `width` and `height`.
3.  Set a default value of `1.0` for both.
4.  The function should return the area (double).
5.  Call it in `main` three times:
    *   No arguments.
    *   Only `width` provided (e.g., 5).
    *   Both provided (e.g., 4 and 3).
6.  Print the results.

**Expected Output:**
```
1.0
5.0
12.0
```

---

## Assignment 3: Arrow Functions & List Mapping
**Objective:** Use arrow syntax and anonymous functions with lists.
*(الهدف: استخدام صيغة السهم والدوال المجهولة مع القوائم.)*

**Instructions:**
1.  Create a list of numbers: `[1, 2, 3, 4, 5]`.
2.  Use the `map` method to create a new list where each number is squared (multiplied by itself).
3.  Use an arrow function `=>` inside the `map`.
4.  Convert the result back to a list using `.toList()` and print it.

**Expected Output:**
```
[1, 4, 9, 16, 25]
```

---

## Assignment 4: The Multiplier (Closure)
**Objective:** Create a function that returns another function (Closure).
*(الهدف: إنشاء دالة ترجع دالة أخرى (Closure).)*

**Instructions:**
1.  Write a function called `multiplier` that takes one integer argument `factor`.
2.  It should return a function.
3.  The returned function should take an integer `n` and return `n * factor`.
4.  In `main`, create a variable `triple` by calling `multiplier(3)`.
5.  Use `triple` to multiply 10 and print the result.

**Expected Output:**
```
30
```

---

## Assignment 5: Sequence Generator
**Objective:** Use a synchronous generator (`sync*`) to create a sequence.
*(الهدف: استخدام مولّد متزامن (`sync*`) لإنشاء تسلسل.)*

**Instructions:**
1.  Write a function `evenNumbers(int n)` marked with `sync*`.
2.  It should yield even numbers starting from 0 up to (but not including) `n`.
3.  Use a loop and the `yield` keyword.
4.  In `main`, iterate through `evenNumbers(10)` using a for-loop and print each number.

**Expected Output:**
```
0
2
4
6
8
```

---

## Solutions

### Solution 1: Simple Greeting

```dart
void greet(String name, int age) {
  print('Hello $name, you are $age years old.');
}

void main() {
  greet('Alice', 25);
}
```

### Solution 2: Area Calculator

```dart
double calculateArea({double width = 1.0, double height = 1.0}) {
  return width * height;
}

void main() {
  print(calculateArea()); // 1.0 * 1.0
  print(calculateArea(width: 5)); // 5.0 * 1.0
  print(calculateArea(width: 4, height: 3)); // 4.0 * 3.0
}
```

### Solution 3: Arrow Functions & List Mapping

```dart
void main() {
  var numbers = [1, 2, 3, 4, 5];
  var squares = numbers.map((n) => n * n).toList();
  print(squares);
}
```

### Solution 4: The Multiplier (Closure)

```dart
Function multiplier(int factor) {
  return (int n) => n * factor;
}

void main() {
  var triple = multiplier(3);
  print(triple(10)); // 10 * 3 = 30
}
```

### Solution 5: Sequence Generator

```dart
Iterable<int> evenNumbers(int n) sync* {
  for (int i = 0; i < n; i++) {
    if (i % 2 == 0) {
      yield i;
    }
  }
}

void main() {
  for (var num in evenNumbers(10)) {
    print(num);
  }
}
```
