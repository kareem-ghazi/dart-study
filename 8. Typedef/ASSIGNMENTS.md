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

## Solutions

```dart
// --- Assignment 1 Typedef ---
typedef Prices = List<double>;

// --- Assignment 2 Typedef ---
typedef Classroom = Map<String, List<String>>;

// --- Assignment 3 Typedef ---
typedef MathOp = int Function(int a, int b);

// --- Assignment 3 Functions ---
int multiply(int a, int b) => a * b;
int divide(int a, int b) => a ~/ b;

void perform(int x, int y, MathOp op) {
  print('Result: ${op(x, y)}');
}

void main() {
  // --- Assignment 1 Solution ---
  print('--- Assignment 1 ---');
  Prices cart = [10.5, 20.0, 5.99];
  print('Prices: $cart');
  print('\n');

  // --- Assignment 2 Solution ---
  print('--- Assignment 2 ---');
  Classroom myClass = {
    'Mr. Smith': ['John', 'Jane', 'Doe']
  };
  print('Students of Mr. Smith: ${myClass['Mr. Smith']}');
  print('\n');

  // --- Assignment 3 Solution ---
  print('--- Assignment 3 ---');
  perform(10, 2, multiply);
  perform(10, 2, divide);
}
```