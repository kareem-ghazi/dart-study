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

## Assignment 5: Matrix Spiral Traversal (Expert)

**Objective:**
Use complex loop logic (nested `while` or `for`) to traverse a 2D matrix in a spiral order.
*(الهدف: استخدام منطق تكرار معقد (متداخل `while` أو `for`) لاجتياز مصفوفة ثنائية الأبعاد بترتيب حلزوني.)*

**Instructions:**
1.  Define a 3x3 matrix (List of Lists): `[[1, 2, 3], [4, 5, 6], [7, 8, 9]]`.
2.  Write an algorithm to print elements in spiral order: Right -> Down -> Left -> Up.
    *   Maintain boundaries: `top`, `bottom`, `left`, `right`.
    *   Use a `while` loop that runs as long as `left <= right` and `top <= bottom`.
3.  Print the sequence.

**Expected Output:**
```
1 2 3 6 9 8 7 4 5
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

### Solution 5: Matrix Spiral Traversal

```dart
void main() {
  List<List<int>> matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
  ];
  
  List<int> result = [];
  int top = 0;
  int bottom = matrix.length - 1;
  int left = 0;
  int right = matrix[0].length - 1;

  while (top <= bottom && left <= right) {
    // 1. Right
    for (int i = left; i <= right; i++) result.add(matrix[top][i]);
    top++;

    // 2. Down
    for (int i = top; i <= bottom; i++) result.add(matrix[i][right]);
    right--;

    // 3. Left
    if (top <= bottom) {
      for (int i = right; i >= left; i--) result.add(matrix[bottom][i]);
      bottom--;
    }

    // 4. Up
    if (left <= right) {
      for (int i = bottom; i >= top; i--) result.add(matrix[i][left]);
      left++;
    }
  }
  
  print(result.join(' '));
}
```
