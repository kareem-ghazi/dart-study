# Error handling

**Overview:**
Errors happen! Files might be missing, the internet might disconnect, or logic might fail. Error handling lets your program crash gracefully or fix the problem instead of stopping abruptly.

**(نظرة عامة):**
الأخطاء تحدث! قد تكون الملفات مفقودة، أو قد ينقطع الاتصال بالإنترنت، أو قد يفشل المنطق. تسمح معالجة الأخطاء لبرنامجك بالتوقف بسلام أو إصلاح المشكلة بدلاً من التوقف المفاجئ.

---

## 1. Exceptions (الاستثناءات)

An **Exception** is an event that disrupts the normal flow of the program. If you don't "catch" it, the program crashes.

*   **Throw:** Creating an error (raising the flag).
    *   *(Throw: إنشاء خطأ (رفع العلم).)*
*   **Catch:** Handling the error (lowering the flag).
    *   *(Catch: معالجة الخطأ (إنزال العلم).)*

---

## 2. `try`, `on`, `catch` (حاول، عند، التقط)

*   **`try`**: Wrap risky code here.
    *   *(حاول: ضع الكود الذي يحتمل الخطأ هنا.)*
*   **`on`**: Catch a *specific* type of error.
    *   *(عند: التقاط نوع محدد من الأخطاء.)*
*   **`catch`**: Catch *any* error (and get the error object `e`).
    *   *(التقط: التقاط أي خطأ (والحصول على كائن الخطأ `e`).)*

```dart
try {
  var result = 10 ~/ 0; // Division by zero!
} on IntegerDivisionByZeroException {
  print('Cannot divide by zero.');
} catch (e) {
  print('Unknown error: $e');
}
```

---

## 3. `finally` (أخيرًا)

Code inside `finally` runs **no matter what** (whether there was an error or not). It is used for cleanup (closing files, database connections).

```dart
try {
  openFile();
  processData();
} catch (e) {
  print('Error!');
} finally {
  closeFile(); // Always runs
}
```

---

## 4. `rethrow` (إعادة الرمي)

Sometimes you catch an error just to log it, but you still want the program to know there was an error. Use `rethrow` to pass it up the chain.

---

## 5. `assert` (التحقق / التوكيد)

Used **during development** to check for "impossible" situations. They are ignored in production code.

```dart
// Stops program if age is null (only in debug mode)
assert(age != null, 'Age cannot be null'); 
```

---

## Key Takeaways

*   Don't leave users with a crashed app; catch expected errors.
*   Use `on` if you know exactly what error might happen.
*   Use `finally` to clean up resources.
*   Assertions are your friends for catching bugs early while coding.

---

## Glossary (English-Arabic)

| Term | Definition | Arabic Meaning | Example |
| :--- | :--- | :--- | :--- |
| **Exception** | A runtime error event. | استثناء | `FormatException` |
| **Throw** | Triggering an error. | رمي / إثارة | `throw 'Error!'` |
| **Catch** | Intercepting an error. | التقاط | `catch (e) { ... }` |
| **Stack Trace** | The list of functions called before the error. | تتبع المكدس | Shows where error happened. |
| **Assert** | A debug-only check. | توكيد / تحقق | `assert(x > 0)` |
