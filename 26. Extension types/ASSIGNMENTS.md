# Assignments: Extension Types

## Assignment 1: Safe ID Wrapper (Basic)
**Objective:** Create an opaque extension type for an ID.
(إنشاء نوع توسعة معتم لمعرف.)

**Instructions:**
1.  Create `extension type UserID(int id)`.
2.  In `main`, create a `UserID`.
3.  Try to add 10 to it (comment out the error line).
4.  Print the ID using the implicit getter `.id`.

**Expected Output:**
```
ID: 12345
```

---

## Assignment 2: Transparent Wrapper (Intermediate)
**Objective:** Extend `int` but keep its functionality.
(توسيع `int` لكن مع الاحتفاظ بوظائفه.)

**Instructions:**
1.  Create `extension type FancyInt(int val) implements int`.
2.  Add a method `isEvenAndPositive()` returning bool.
3.  In `main`, create a `FancyInt`.
4.  Call `.abs()` (inherited from int) and `.isEvenAndPositive()` (new).

**Expected Output:**
```
Abs: 10
Is Special: true
```

---

## Assignment 3: Constructors (Intermediate)
**Objective:** Add named constructors to extension types.
(إضافة منشئات مسماة لأنواع التوسعة.)

**Instructions:**
1.  Create `extension type Email(String address)`.
2.  Add a named constructor `Email.admin()` that sets address to "admin@app.com".
3.  In `main`, create an admin email and print it.

**Expected Output:**
```
admin@app.com
```

---

## Assignment 4: Operator Replacement (Advanced)
**Objective:** Redefine operators for domain logic.
(إعادة تعريف المعاملات لمنطق المجال.)

**Instructions:**
1.  Create `extension type Score(int points)`.
2.  Implement `operator +` to add two Scores together returning a new Score.
3.  Ensure `operator +` behaves normally (`s1 + s2`).
4.  In `main`, add two scores.

**Expected Output:**
```
Total Score: 150
```

---

## Assignment 5: Runtime Checks (Expert)
**Objective:** Prove type erasure.
(إثبات محو النوع.)

**Instructions:**
1.  Create `extension type Wrapper(String s)`.
2.  In `main`, create an instance `w = Wrapper('hi')`.
3.  Check `if (w is String)` and print "It is a String".
4.  Check `if (w is Wrapper)` (this works in Dart 3.3+ but effectively checks the representation).
5.  Print `w.runtimeType`.

**Expected Output:**
```
It is a String
String
```

---

## Solutions

```dart
// Assignment 1: Safe ID Wrapper
extension type UserID(int id) {}

// Assignment 2: Transparent Wrapper
extension type FancyInt(int val) implements int {
  bool isEvenAndPositive() => val > 0 && val.isEven;
}

// Assignment 3: Constructors
extension type Email(String address) {
  Email.admin() : address = 'admin@app.com';
}

// Assignment 4: Operator Replacement
extension type Score(int points) {
  Score operator +(Score other) => Score(points + other.points);
}

// Assignment 5: Runtime Checks
extension type Wrapper(String s) {}

void main() {
  print('--- Assignment 1 ---');
  var uid = UserID(12345);
  // print(uid + 10); // Error
  print('ID: ${uid.id}');

  print('\n--- Assignment 2 ---');
  var fi = FancyInt(-10);
  print('Abs: ${fi.abs()}');
  var fi2 = FancyInt(10);
  print('Is Special: ${fi2.isEvenAndPositive()}');

  print('\n--- Assignment 3 ---');
  var admin = Email.admin();
  print(admin.address);

  print('\n--- Assignment 4 ---');
  var s1 = Score(50);
  var s2 = Score(100);
  var total = s1 + s2;
  print('Total Score: ${total.points}');

  print('\n--- Assignment 5 ---');
  var w = Wrapper('hi');
  if (w is String) print('It is a String');
  print(w.runtimeType);
}
```