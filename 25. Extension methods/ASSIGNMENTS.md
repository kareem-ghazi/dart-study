# Assignments: Extension Methods

## Assignment 1: String Extensions (Basic)
**Objective:** Add a useful method to `String`.
(إضافة دالة مفيدة لـ `String`.)

**Instructions:**
1.  Create an extension `StringOps` on `String`.
2.  Add a method `capitalize()` that capitalizes the first letter of the string.
3.  In `main`, print `'hello'.capitalize()`.

**Expected Output:**
```
Hello
```

---

## Assignment 2: Number Extensions (Intermediate)
**Objective:** Add getters to `int`.
(إضافة جوالب لـ `int`.)

**Instructions:**
1.  Create an extension `MathOps` on `int`.
2.  Add a getter `squared` that returns `this * this`.
3.  Add a getter `cubed` that returns `this * this * this`.
4.  In `main`, print `5.squared` and `3.cubed`.

**Expected Output:**
```
25
27
```

---

## Assignment 3: List Extensions (Intermediate)
**Objective:** Extend `List<int>` specifically.
(توسيع `List<int>` تحديداً.)

**Instructions:**
1.  Create an extension `IntListOps` on `List<int>`.
2.  Add a getter `sum` that returns the sum of all integers in the list.
3.  In `main`, calculate the sum of `[1, 2, 3, 4]`.

**Expected Output:**
```
Sum: 10
```

---

## Assignment 4: Generic Extensions (Advanced)
**Objective:** Extend any List.
(توسيع أي قائمة.)

**Instructions:**
1.  Create an extension `ListPrinter<T>` on `List<T>`.
2.  Add a method `printAll()` that loops through and prints each item.
3.  In `main`, call it on a list of Strings and a list of Ints.

**Expected Output:**
```
apple
banana
10
20
```

---

## Assignment 5: Conflict Resolution (Expert)
**Objective:** Handle two extensions with the same method name.
(التعامل مع توسعتين لهما نفس اسم الدالة.)

**Instructions:**
1.  Create extension `Ext1` on `String` with method `exclaim()` returning `"$this!"`.
2.  Create extension `Ext2` on `String` with method `exclaim()` returning `"$this!!!"`.
3.  In `main`, try to call `'Hi'.exclaim()`. Note the error (or simulate it mentally).
4.  Use explicit syntax to call `Ext2`'s version.

**Expected Output:**
```
Hi!!!
```

---

## Solutions

```dart
// Assignment 1: String Extensions
extension StringOps on String {
  String capitalize() {
    if (isEmpty) return this;
    return this[0].toUpperCase() + substring(1);
  }
}

// Assignment 2: Number Extensions
extension MathOps on int {
  int get squared => this * this;
  int get cubed => this * this * this;
}

// Assignment 3: List Extensions
extension IntListOps on List<int> {
  int get sum {
    int total = 0;
    for (var n in this) total += n;
    return total;
  }
}

// Assignment 4: Generic Extensions
extension ListPrinter<T> on List<T> {
  void printAll() {
    for (var item in this) {
      print(item);
    }
  }
}

// Assignment 5: Conflict Resolution
extension Ext1 on String {
  String exclaim() => 
    '$this!';
}

extension Ext2 on String {
  String exclaim() => 
    '$this!!!';
}

void main() {
  print('--- Assignment 1 ---');
  print('hello'.capitalize());

  print('\n--- Assignment 2 ---');
  print('5 squared: ${5.squared}');
  print('3 cubed: ${3.cubed}');

  print('\n--- Assignment 3 ---');
  print('Sum: ${[1, 2, 3, 4].sum}');

  print('\n--- Assignment 4 ---');
  ['apple', 'banana'].printAll();
  [10, 20].printAll();

  print('\n--- Assignment 5 ---');
  // 'Hi'.exclaim(); // Error: Ambiguous
  print(Ext2('Hi').exclaim());
}
```
