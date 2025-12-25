# Assignments: Collections

## Assignment 1: Shopping List (Basic)

**Objective:**
Practice basic List operations: creating, adding, accessing, and removing items.
**(ممارسة عمليات القائمة الأساسية: الإنشاء، الإضافة، الوصول، والإزالة.)**

**Instructions:**
1.  Create a list of strings named `shoppingList` with initial items: "Milk", "Bread", "Eggs".
2.  Add "Apples" to the list.
3.  Remove "Bread" from the list.
4.  Print the first item in the list.
5.  Print the total number of items in the list.
**(1. أنشئ قائمة سلاسل نصية باسم `shoppingList` تحتوي على: "Milk", "Bread", "Eggs". 2. أضف "Apples". 3. احذف "Bread". 4. اطبع العنصر الأول. 5. اطبع العدد الكلي للعناصر.)**

**Expected Output:**
```
First item: Milk
Total items: 3
```

---

## Assignment 2: Unique Inventory (Intermediate)

**Objective:**
Use Sets to handle unique items and Maps to store related data.
**(استخدام المجموعات "Sets" للتعامل مع العناصر الفريدة والخرائط "Maps" لتخزين البيانات المرتبطة.)**

**Instructions:**
1.  Create a list of product IDs (integers) that contains duplicates: `[101, 102, 101, 103, 102, 104]`.
2.  Create a `Set` from this list to remove duplicates and print the unique IDs.
3.  Create a `Map` named `inventory` where the keys are the unique IDs and values are product names (e.g., 101: "Mouse", 102: "Keyboard", etc.).
4.  Print the product name for ID 103.
**(1. أنشئ قائمة بمعرفات المنتجات تحتوي على تكرارات. 2. أنشئ مجموعة `Set` من هذه القائمة لإزالة التكرارات واطبع المعرفات الفريدة. 3. أنشئ خريطة `Map` تربط المعرفات بأسماء المنتجات. 4. اطبع اسم المنتج للمعرف 103.)**

**Expected Output:**
```
Unique IDs: {101, 102, 103, 104}
Product 103: Monitor
```
*(Note: Product names may vary based on your choice).*

---

## Assignment 3: Filter and Merge (Advanced)

**Objective:**
Master collection operators: Spread (`...`), Collection If, and Collection For.
**(إتقان عوامل تشغيل المجموعات: النشر، الشرط، والتكرار داخل المجموعات.)**

**Instructions:**
1.  Define two lists of numbers: `listA = [1, 2, 3]` and `listB = [4, 5, 6]`.
2.  Define a boolean variable `addExtra` set to `true`.
3.  Create a new list `combinedList` that:
    *   Starts with 0.
    *   Includes all elements from `listA`.
    *   Includes elements from `listB` *only if* they are even numbers (use `for` with `if` inside the collection literal).
    *   Adds 99 at the end *only if* `addExtra` is true.
4.  Print the `combinedList`.
**(1. عرّف قائمتين من الأرقام. 2. عرّف متغيراً منطقياً `addExtra`. 3. أنشئ قائمة جديدة تبدأ بـ 0، تتضمن عناصر `listA`، تتضمن الأعداد الزوجية فقط من `listB`، وتضيف 99 إذا كان `addExtra` صحيحاً. 4. اطبع القائمة الناتجة.)**

**Expected Output:**
```
Combined List: [0, 1, 2, 3, 4, 6, 99]
```

---

## Assignment 4: Nested Collections Processing (Advanced)

**Objective:**
Work with complex nested data structures (Map of Lists).
*(الهدف: العمل مع هياكل البيانات المتداخلة المعقدة (خريطة قوائم).)*

**Instructions:**
1. Create a `Map<String, List<int>>` representing students and their grades:
   `{'Ali': [90, 85, 88], 'Bob': [70, 60, 75]}`.
2. Iterate through the map.
3. For each student, calculate their average score.
4. Print "Student: [Name], Average: [Value]".

**Expected Output:**
```
Student: Ali, Average: 87.6...
Student: Bob, Average: 68.3...
```

---

## Assignment 5: Functional Methods (Fold & Reduce) (Advanced)

**Objective:**
Use higher-order functions `fold` and `reduce` for aggregation.
*(الهدف: استخدام الدوال عالية المستوى `fold` و `reduce` للتجميع.)*

**Instructions:**
1. Create a list of item prices: `[10.0, 20.0, 5.0, 30.0]`.
2. Use `.fold(0, ...)` to calculate the total sum.
3. Use `.reduce(...)` to find the highest price (max value).
4. Print both results.

**Expected Output:**
```
Total Sum: 65.0
Highest Price: 30.0
```

---

## Solutions

### Solution 1: Shopping List

```dart
void main() {
  var shoppingList = ['Milk', 'Bread', 'Eggs'];
  shoppingList.add('Apples');
  shoppingList.remove('Bread');
  
  print('First item: ${shoppingList[0]}');
  print('Total items: ${shoppingList.length}');
}
```

### Solution 2: Unique Inventory

```dart
void main() {
  var rawIds = [101, 102, 101, 103, 102, 104];
  var uniqueIds = rawIds.toSet();
  print('Unique IDs: $uniqueIds');

  var inventory = {
    101: 'Mouse',
    102: 'Keyboard',
    103: 'Monitor',
    104: 'Webcam'
  };
  print('Product 103: ${inventory[103]}');
}
```

### Solution 3: Filter and Merge

```dart
void main() {
  var listA = [1, 2, 3];
  var listB = [4, 5, 6];
  var addExtra = true;

  var combinedList = [
    0,
    ...listA,
    for (var num in listB)
      if (num % 2 == 0) num,
    if (addExtra) 99
  ];

  print('Combined List: $combinedList');
}
```

### Solution 4: Nested Collections Processing

```dart
void main() {
  var grades = {
    'Ali': [90, 85, 88],
    'Bob': [70, 60, 75]
  };

  grades.forEach((name, scores) {
    double sum = 0;
    for (var score in scores) {
      sum += score;
    }
    double average = sum / scores.length;
    print('Student: $name, Average: $average');
  });
}
```

### Solution 5: Functional Methods (Fold & Reduce)

```dart
import 'dart:math'; // For max function if preferred, but manual reduce is fine too

void main() {
  var prices = [10.0, 20.0, 5.0, 30.0];
  
  // Fold: starts with initial value (0.0)
  double total = prices.fold(0.0, (prev, element) => prev + element);
  
  // Reduce: starts with first element
  double highest = prices.reduce((curr, next) => curr > next ? curr : next);
  
  print('Total Sum: $total');
  print('Highest Price: $highest');
}
```
