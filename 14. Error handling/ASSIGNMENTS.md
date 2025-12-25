# Assignments: Error Handling

Practice making your Dart programs robust and crash-proof.

## Assignment 1: Safe Division
**Objective:** Handle the specific "IntegerDivisionByZeroException".
*(الهدف: معالجة استثناء "القسمة الصحيحة على صفر".)*

**Instructions:**
1.  Write a function `divide(int a, int b)`.
2.  Inside, print the result of integer division `a ~/ b`.
3.  Wrap the division logic in a `try-catch` block.
4.  Use `on IntegerDivisionByZeroException` to catch division by zero errors and print "Cannot divide by zero!".
5.  Call the function with `(10, 2)` and `(10, 0)`.

**Expected Output:**
```
5
Cannot divide by zero!
```

---

## Assignment 2: Custom Authentication Error
**Objective:** Throw and catch a custom exception with `rethrow`.
*(الهدف: رمي والتقاط استثناء مخصص مع استخدام `rethrow`.)*

**Instructions:**
1.  Create a custom exception class `AuthException` that implements `Exception`. give it a `String message`.
2.  Write a function `login(String password)`.
3.  If the password is NOT "secret123", `throw AuthException('Wrong password')`.
4.  Write a `main` function with a `try-catch` block calling `login`.
5.  Catch the `AuthException` and print its message.

**Expected Output:**
```
Authentication Failed: Wrong password
```

---

## Assignment 3: Development Checks (Assert)
**Objective:** Use `assert` to validate constructor data.
*(الهدف: استخدام `assert` للتحقق من صحة بيانات البناء.)*

**Instructions:**
1.  Create a class `Person` with a final `int age`.
2.  Create a constructor `Person(this.age)`.
3.  Add an `assert` in the initializer list to ensure `age >= 0`. Add a message "Age must be positive".
4.  In `main`, try creating `Person(-5)`.
5.  **Note:** You must run this code with assertions enabled (usually default in debug mode) to see the error. If running normally, it might just proceed. Try catching the `AssertionError` if possible, or just observe the crash.

**Expected Output (Debug Mode):**
```
Uncaught Error: Assertion failed: "Age must be positive"
```

---

## Assignment 4: Rethrowing with StackTrace (Advanced)

**Objective:**
Catch an error, log it, and rethrow it preserving the stack trace.
*(الهدف: التقاط خطأ، تسجيله، وإعادة رميه مع الحفاظ على تتبع المكدس.)*

**Instructions:**
1. Create a function `riskyOperation()` that throws `Exception("Crash")`.
2. Wrap it in a `try-catch` block that catches both the error object `e` and the stack trace `s`.
3. Print "Log: Error occurred".
4. Use `rethrow` to propagate the error.
5. In `main`, call this function inside another try-catch to finally handle it and print "Handled in main".

**Expected Output:**
```
Log: Error occurred
Handled in main
```

---

## Assignment 5: Custom Exception Hierarchy (Advanced)

**Objective:**
Create and handle a hierarchy of custom exceptions.
*(الهدف: إنشاء ومعالجة تسلسل هرمي للاستثناءات المخصصة.)*

**Instructions:**
1. Create a base class `NetworkException` implements `Exception`.
2. Create a subclass `TimeoutException` extends `NetworkException`.
3. Create a function `fetchData()` that throws `TimeoutException()`.
4. In `main`, use `try-catch`.
5. Add a `on TimeoutException` block to print "Request timed out".
6. Add a `on NetworkException` block to print "General network error" (to show it catches subclasses if checked first, but here put it second).
7. Add a generic `catch` block.

**Expected Output:**
```
Request timed out
```

---

## Solutions

### Solution 1: Safe Division

```dart
void divide(int a, int b) {
  try {
    print(a ~/ b);
  } on IntegerDivisionByZeroException {
    print('Cannot divide by zero!');
  } catch (e) {
    print('Unknown error: $e');
  }
}

void main() {
  print('--- Safe Division ---');
  divide(10, 2);
  divide(10, 0);
}
```

### Solution 2: Custom Authentication Error

```dart
class AuthException implements Exception {
  final String message;
  AuthException(this.message);
  
  @override
  String toString() => 'AuthException: $message';
}

void login(String password) {
  if (password != 'secret123') {
    throw AuthException('Wrong password');
  }
  print('Login success!');
}

void main() {
  print('\n--- Auth System ---');
  try {
    login('guest');
  } on AuthException catch (e) {
    print('Authentication Failed: ${e.message}');
  }
}
```

### Solution 3: Development Checks

```dart
class Person {
  final int age;
  Person(this.age) : assert(age >= 0, 'Age must be positive');
}

void main() {
  print('\n--- Assert Check ---');
  try {
    var p = Person(-5);
    print('Person created with age ${p.age}');
  } catch (e) {
    print('Caught assertion error: $e');
  }
}
```

### Solution 4: Rethrowing with StackTrace

```dart
void riskyOperation() {
  try {
    throw Exception("Crash");
  } catch (e, s) {
    print("Log: Error occurred");
    // print(s); // Optional: print stack trace
    rethrow;
  }
}

void main() {
  try {
    riskyOperation();
  } catch (e) {
    print("Handled in main");
  }
}
```

### Solution 5: Custom Exception Hierarchy

```dart
class NetworkException implements Exception {}
class TimeoutException extends NetworkException {}

void fetchData() {
  throw TimeoutException();
}

void main() {
  try {
    fetchData();
  } on TimeoutException {
    print("Request timed out");
  } on NetworkException {
    print("General network error");
  } catch (e) {
    print("Unknown error");
  }
}
```
