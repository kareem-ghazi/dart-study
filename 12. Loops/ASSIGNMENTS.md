# Assignments: Loops

Practice controlling program flow with different types of loops.

## Assignment 1: The Even Counter
**Objective:** Use a standard `for` loop to filter numbers.
*(الهدف: استخدام حلقة `for` القياسية لتصفية الأرقام.)*

**Instructions:**
1.  Write a `for` loop that counts from 1 to 20.
2.  Inside the loop, check if the number is even (divisible by 2).
3.  Print only the even numbers.

**Expected Output:**
```
2
4
...
20
```

---

## Assignment 2: Summing a List
**Objective:** Use a `for-in` loop to process a collection.
*(الهدف: استخدام حلقة `for-in` لمعالجة مجموعة بيانات.)*

**Instructions:**
1.  Create a list of prices: `[12.5, 10.0, 5.5, 2.0]`.
2.  Create a variable `total` initialized to 0.
3.  Loop through the list using `for-in` and add each price to `total`.
4.  Print the final total.

**Expected Output:**
```
Total Price: 30.0
```

---

## Assignment 3: Guessing Game Simulation
**Objective:** Use `while` and `break` to simulate a process until a condition is met.
*(الهدف: استخدام `while` و `break` لمحاكاة عملية حتى يتم استيفاء شرط.)*

**Instructions:**
1.  Create a list of numbers representing "guesses": `[3, 7, 1, 9, 5]`.
2.  Set a `target` number (e.g., 9).
3.  Use a `while` loop to iterate through the guesses (you might need an index variable defined outside).
4.  If the current guess matches the target:
    *   Print "Found 9!"
    *   Use `break` to stop the loop.
5.  If not, print "Guessed X, trying again...".

**Hint:** You can also use `for-in` with `break`, but try doing it manually with `while` and an index `i` to practice.

**Expected Output:**
```
Guessed 3, trying again...
Guessed 7, trying again...
Guessed 1, trying again...
Found 9!
```

---

## Assignment 4: Nested Loops & Labels (Advanced)

**Objective:**
Control nested loops using labels and `break`.
*(الهدف: التحكم في الحلقات المتداخلة باستخدام التسميات و `break`.)*

**Instructions:**
1. Create a 2D grid: `var grid = [[1, 2], [3, 4], [5, 6]];`.
2. Write a nested loop to find the number `4`.
3. Use a label `outerLoop:` before the first loop.
4. When `4` is found, print "Found 4 at [$i][$j]" and `break outerLoop` to stop *both* loops immediately.
5. Print "Done" after the loops to verify it exited correctly.

**Expected Output:**
```
Checking 1...
Checking 2...
Checking 3...
Found 4 at [1][1]
Done
```

---

## Assignment 5: Async For-In (Advanced)

**Objective:**
Iterate over an asynchronous stream of data using `await for`.
*(الهدف: التكرار عبر تدفق بيانات غير متزامن باستخدام `await for`.)*

**Instructions:**
1. Create a function `Stream<int> countStream(int to) async*` that yields numbers from 1 to `to` with a 1-second delay between each.
2. In `main` (marked `async`), use `await for (var n in countStream(3))` to loop through the stream.
3. Print each number.

**Expected Output:**
```
1
(1 second delay)
2
(1 second delay)
3
```

---

## Solutions

### Solution 1: The Even Counter

```dart
void main() {
  print('--- Even Numbers ---');
  for (int i = 1; i <= 20; i++) {
    if (i % 2 == 0) {
      print(i);
    }
  }
}
```

### Solution 2: Summing a List

```dart
void main() {
  print('\n--- Summing List ---');
  List<double> prices = [12.5, 10.0, 5.5, 2.0];
  double total = 0;

  for (var price in prices) {
    total += price;
  }
  print('Total Price: $total');
}
```

### Solution 3: Guessing Game Simulation

```dart
void main() {
  print('\n--- Guessing Game ---');
  List<int> guesses = [3, 7, 1, 9, 5];
  int target = 9;
  int index = 0;

  // Using while loop to manually iterate
  while (index < guesses.length) {
    int currentGuess = guesses[index];
    
    if (currentGuess == target) {
      print('Found $target!');
      break; // Exit the loop immediately
    } else {
      print('Guessed $currentGuess, trying again...');
    }
    
    index++; // Move to next guess
  }
}
```

### Solution 4: Nested Loops & Labels

```dart
void main() {
  var grid = [
    [1, 2],
    [3, 4],
    [5, 6]
  ];

  outerLoop: // Label
  for (int i = 0; i < grid.length; i++) {
    for (int j = 0; j < grid[i].length; j++) {
      int num = grid[i][j];
      print('Checking $num...');
      
      if (num == 4) {
        print('Found 4 at [$i][$j]');
        break outerLoop; // Breaks the labeled loop (the outer one)
      }
    }
  }
  print('Done');
}
```

### Solution 5: Async For-In

```dart
import 'dart:async';

Stream<int> countStream(int to) async* {
  for (int i = 1; i <= to; i++) {
    await Future.delayed(Duration(seconds: 1));
    yield i;
  }
}

void main() async {
  print('Starting stream...');
  await for (var n in countStream(3)) {
    print(n);
  }
  print('Stream finished');
}
```
