# Assignments: Callable Objects

## Assignment 1: Basic Greeter (Basic)
**Objective:** Create a simple callable class.
(إنشاء فئة بسيطة قابلة للاستدعاء.)

**Instructions:**
1.  Create a class `Greet`.
2.  Implement `call(String name)` to print "Welcome, $name".
3.  In `main`, create an instance and call it with "Ali".

**Expected Output:**
```
Welcome, Ali
```

---

## Assignment 2: Math Multiplier (Intermediate)
**Objective:** Use callable objects for math.
(استخدام الكائنات القابلة للاستدعاء للرياضيات.)

**Instructions:**
1.  Create a class `Multiplier`.
2.  It should have a `final int factor` initialized in constructor.
3.  Implement `call(int value)` returning `value * factor`.
4.  Create a doubler (factor 2) and tripler (factor 3). Call them.

**Expected Output:**
```
Doubled: 10
Tripled: 15
```

---

## Assignment 3: Stateful Callable (Intermediate)
**Objective:** Store state between calls.
(تخزين الحالة بين الاستدعاءات.)

**Instructions:**
1.  Create a class `Counter`.
2.  Have a private `_count` starting at 0.
3.  Implement `call()`: increment count and print "Count: $_count".
4.  Call the same instance 3 times.

**Expected Output:**
```
Count: 1
Count: 2
Count: 3
```

---

## Assignment 4: Password Validator (Advanced)
**Objective:** Encapsulate validation logic.
(تغليف منطق التحقق.)

**Instructions:**
1.  Create a class `PasswordValidator`.
2.  Constructor takes `minLength`.
3.  Implement `call(String password)` returning bool (true if length >= minLength).
4.  Create a validator for length 5. Test with "123" (false) and "12345" (true).

**Expected Output:**
```
Valid: false
Valid: true
```

---

## Assignment 5: Generic Transformer (Expert)
**Objective:** Generic callable class.
(فئة عامة قابلة للاستدعاء.)

**Instructions:**
1.  Create a class `Boxer<T>`.
2.  Implement `call(T value)` returning a `List<T>` containing just that value.
3.  Create a `Boxer<String>`. Call it with "Hello". Print the result.

**Expected Output:**
```
[Hello]
```

---

## Solutions

```dart
// Assignment 1: Basic Greeter
class Greet {
  void call(String name) => print('Welcome, $name');
}

// Assignment 2: Math Multiplier
class Multiplier {
  final int factor;
  Multiplier(this.factor);
  int call(int value) => value * factor;
}

// Assignment 3: Stateful Callable
class Counter {
  int _count = 0;
  void call() {
    _count++;
    print('Count: $_count');
  }
}

// Assignment 4: Password Validator
class PasswordValidator {
  final int minLength;
  PasswordValidator(this.minLength);
  bool call(String password) => password.length >= minLength;
}

// Assignment 5: Generic Transformer
class Boxer<T> {
  List<T> call(T value) => [value];
}

void main() {
  print('--- Assignment 1 ---');
  var greet = Greet();
  greet('Ali');

  print('\n--- Assignment 2 ---');
  var doubleIt = Multiplier(2);
  var tripleIt = Multiplier(3);
  print('Doubled: ${doubleIt(5)}');
  print('Tripled: ${tripleIt(5)}');

  print('\n--- Assignment 3 ---');
  var count = Counter();
  count();
  count();
  count();

  print('\n--- Assignment 4 ---');
  var validator = PasswordValidator(5);
  print('Valid: ${validator("123")}');
  print('Valid: ${validator("12345")}');

  print('\n--- Assignment 5 ---');
  var box = Boxer<String>();
  print(box('Hello'));
}
```
