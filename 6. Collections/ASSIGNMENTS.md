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

## Solutions

```dart
void main() {
  // --- Assignment 1 Solution ---
  print('--- Assignment 1 ---');
  var shoppingList = ['Milk', 'Bread', 'Eggs'];
  shoppingList.add('Apples');
  shoppingList.remove('Bread');
  
  print('First item: ${shoppingList[0]}');
  print('Total items: ${shoppingList.length}');
  print('\n');

  // --- Assignment 2 Solution ---
  print('--- Assignment 2 ---');
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
  print('\n');

  // --- Assignment 3 Solution ---
  print('--- Assignment 3 ---');
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