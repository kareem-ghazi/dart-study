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

## Assignment 4: Format Exception (Parsing error)

**Objective:**
Handle errors when converting strings to numbers.
*(الهدف: معالجة الأخطاء عند تحويل النصوص إلى أرقام.)*

**Instructions:**
1. Create a function `parseNumber(String text)`.
2. Try to parse it using `int.parse(text)`.
3. Catch `FormatException` and return -1.
4. Call it with "123" and "abc".

**Expected Output:**
```
123
-1
```

---

## Assignment 5: Finally Cleanup (Resource management)

**Objective:**
Use the `finally` block.
*(الهدف: استخدام كتلة `finally`.)*

**Instructions:**
1. Write a try-catch-finally block.
2. In try, print "Opening file...".
3. In try, throw an exception "File corrupted".
4. In catch, print "Error detected".
5. In finally, print "Closing file...".

**Expected Output:**
```
Opening file...
Error detected
Closing file...
```

---

## Solutions

```dart
// Assignment 1
void divide(int a, int b) {
  try {
    print(a ~/ b);
  } on IntegerDivisionByZeroException {
    print('Cannot divide by zero!');
  } catch (e) {
    print('Unknown error: $e');
  }
}

void assignment1() {
  print('--- Safe Division ---');
  divide(10, 2);
  divide(10, 0);
}

// Assignment 2
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

void assignment2() {
  print('\n--- Auth System ---');
  try {
    login('guest');
  } on AuthException catch (e) {
    print('Authentication Failed: ${e.message}');
  }
}

// Assignment 3
class Person {
  final int age;
  Person(this.age) : assert(age >= 0, 'Age must be positive');
}

void assignment3() {
  print('\n--- Assert Check ---');
  try {
    var p = Person(-5);
    print('Person created with age ${p.age}');
  } catch (e) {
    print('Caught assertion error: $e');
  }
}

// Assignment 4
int parseNumber(String text) {
  try {
    return int.parse(text);
  } on FormatException {
    return -1;
  }
}

// Assignment 5
void assignment5() {
  try {
    print("Opening file...");
    throw Exception("File corrupted");
  } catch (e) {
    print("Error detected");
  } finally {
    print("Closing file...");
  }
}

void main() {
  assignment1();
  assignment2();
  // Note: Assertions might be disabled in production/some environments
  assignment3(); 
  
  print('\n--- Assignment 4 ---');
  print(parseNumber("123"));
  print(parseNumber("abc"));

  print('\n--- Assignment 5 ---');
  assignment5();
}
```