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

## Assignment 4: Decrement Loop (Reverse for)

**Objective:**
Practice looping backwards.
*(الهدف: التدرب على التكرار العكسي.)*

**Instructions:**
1. Write a for loop that starts at 5 and goes down to 1.
2. Print each number.
3. Print "Liftoff!" after the loop.

**Expected Output:**
```
5
4
3
2
1
Liftoff!
```

---

## Assignment 5: Do-While Input (Simulation)

**Objective:**
Ensure a block runs at least once.
*(الهدف: التأكد من تشغيل الكتلة مرة واحدة على الأقل.)*

**Instructions:**
1. Define `int count = 0`.
2. Use a do-while loop that increments `count` and prints it.
3. The condition should be `count < 3`.

**Expected Output:**
```
1
2
3
```

---

## Solutions

```dart
// Assignment 1
void assignment1() {
  print('--- Even Numbers ---');
  for (int i = 1; i <= 20; i++) {
    if (i % 2 == 0) {
      print(i);
    }
  }
}

// Assignment 2
void assignment2() {
  print('\n--- Summing List ---');
  List<double> prices = [12.5, 10.0, 5.5, 2.0];
  double total = 0;

  for (var price in prices) {
    total += price;
  }
  print('Total Price: $total');
}

// Assignment 3
void assignment3() {
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

// Assignment 4
void assignment4() {
  print('\n--- Decrement Loop ---');
  for (int i = 5; i > 0; i--) {
    print(i);
  }
  print('Liftoff!');
}

// Assignment 5
void assignment5() {
  print('\n--- Do-While ---');
  int count = 0;
  do {
    count++;
    print(count);
  } while (count < 3);
}

void main() {
  assignment1();
  assignment2();
  assignment3();
  assignment4();
  assignment5();
}
```

```