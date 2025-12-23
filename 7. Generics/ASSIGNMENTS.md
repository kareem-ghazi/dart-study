# Assignments: Generics

## Assignment 1: Type-Safe List (Basic)

**Objective:**
Understand how to use Generics to create type-safe collections.
**(فهم كيفية استخدام Generics لإنشاء مجموعات آمنة النوع.)**

**Instructions:**
1.  Create a list of integers named `scores`.
2.  Try to add a generic `dynamic` value to it (commented out) to see the error, or just ensure you define it strictly as `List<int>`.
3.  Add numbers 90, 85, 77.
4.  Write a function `calculateAverage` that takes `List<int>` and returns a `double`.
5.  Print the average score.
**(1. أنشئ قائمة أعداد صحيحة باسم `scores`. 2. تأكد من تعريفها كـ `List<int>`. 3. أضف الأرقام. 4. اكتب دالة لحساب المتوسط تقبل قائمة أعداد صحيحة وترجع عدداً عشرياً. 5. اطبع المتوسط.)**

**Expected Output:**
```
Average: 84.0
```

---

## Assignment 2: Generic Box (Intermediate)

**Objective:**
Create a Generic class that can hold any type of value.
**(إنشاء فئة عامة يمكنها حمل أي نوع من القيم.)**

**Instructions:**
1.  Create a class named `Box<T>`.
2.  It should have a private field `_value` of type `T` and methods `put(T value)` and `T get()`.
3.  In `main`, create a `Box<String>` and store "Hello".
4.  Create a `Box<int>` and store 123.
5.  Retrieve and print both values.
**(1. أنشئ فئة باسم `Box<T>`. 2. يجب أن تحتوي على حقل خاص `_value` من النوع `T` وطرق `put` و `get`. 3. في `main`، أنشئ صندوقاً للنصوص وخزن "Hello". 4. أنشئ صندوقاً للأرقام وخزن 123. 5. استرجع واطبع القيمتين.)**

**Expected Output:**
```
String Box: Hello
Int Box: 123
```

---

## Assignment 3: Generic Swapper (Advanced)

**Objective:**
Write a generic method to process distinct types dynamically.
**(كتابة دالة عامة لمعالجة أنواع متميزة ديناميكياً.)**

**Instructions:**
1.  Write a generic function called `swapValues<T>` that accepts a `List<T>` and two indices (index1, index2).
2.  The function should swap the elements at those indices in the list.
3.  Test it with a `List<String>` `['A', 'B', 'C']` swapping 0 and 2.
4.  Test it with a `List<int>` `[1, 2, 3]` swapping 1 and 2.
5.  Print the modified lists.
**(1. اكتب دالة عامة `swapValues<T>` تقبل قائمة ومؤشرين. 2. يجب أن تقوم الدالة بتبديل العناصر في هذين الموقعين. 3. جربها مع قائمة نصوص. 4. جربها مع قائمة أرقام. 5. اطبع القوائم المعدلة.)**

**Expected Output:**
```
Swapped Strings: [C, B, A]
Swapped Ints: [1, 3, 2]
```

---

## Solutions

```dart
// --- Assignment 2 Class ---
class Box<T> {
  late T _value;

  void put(T value) {
    _value = value;
  }

  T get() {
    return _value;
  }
}

// --- Assignment 1 Helper ---
double calculateAverage(List<int> scores) {
  if (scores.isEmpty) return 0.0;
  var sum = 0;
  for (var score in scores) {
    sum += score;
  }
  return sum / scores.length;
}

// --- Assignment 3 Helper ---
void swapValues<T>(List<T> list, int i1, int i2) {
  if (i1 >= 0 && i1 < list.length && i2 >= 0 && i2 < list.length) {
    var temp = list[i1];
    list[i1] = list[i2];
    list[i2] = temp;
  }
}

void main() {
  // --- Assignment 1 Solution ---
  print('--- Assignment 1 ---');
  List<int> scores = [90, 85, 77];
  // scores.add("text"); // Error!
  print('Average: ${calculateAverage(scores)}');
  print('\n');

  // --- Assignment 2 Solution ---
  print('--- Assignment 2 ---');
  var stringBox = Box<String>();
  stringBox.put("Hello");
  print('String Box: ${stringBox.get()}');

  var intBox = Box<int>();
  intBox.put(123);
  print('Int Box: ${intBox.get()}');
  print('\n');

  // --- Assignment 3 Solution ---
  print('--- Assignment 3 ---');
  var letters = ['A', 'B', 'C'];
  swapValues(letters, 0, 2);
  print('Swapped Strings: $letters');

  var numbers = [1, 2, 3];
  swapValues(numbers, 1, 2);
  print('Swapped Ints: $numbers');
}
```