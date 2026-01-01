# Asynchronous programming

## Overview

Asynchronous programming allows your program to perform long-running tasks (like fetching data from the internet) without freezing the entire application.

(تسمح البرمجة غير المتزامنة لبرنامجك بأداء مهام طويلة الأمد (مثل جلب البيانات من الإنترنت) دون تجميد التطبيق بأكمله.)

## Handling Futures

**Concept:** Waiting for a value that isn't ready yet.
(انتظار قيمة ليست جاهزة بعد.)

```dart
Future<String> getUser() async {
  await Future.delayed(Duration(seconds: 1));
  return 'Alice';
}

void main() async {
  print(await getUser());
}
```

*   **English:** Use `await` to pause execution until the `Future` completes. The function containing `await` must be marked `async`.
*   **Arabic:** (استخدم `await` لإيقاف التنفيذ مؤقتًا حتى يكتمل `Future`. يجب وضع علامة `async` على الدالة التي تحتوي على `await`.)
*   **Analogy:** Ordering a custom burger. You get a buzzer (Future). You wait (await) for it to buzz before you can eat (use the value).

## Error Handling

**Concept:** Catching errors in async code.
(اكتشاف الأخطاء في الكود غير المتزامن.)

```dart
try {
  await badNetworkCall();
} catch (e) {
  print('Error: $e');
}
```

*   **English:** Use standard `try-catch` blocks around `await` expressions to handle failures like network errors.
*   **Arabic:** (استخدم كتل `try-catch` القياسية حول تعبيرات `await` لمعالجة الإخفاقات مثل أخطاء الشبكة.)

## Declaring Async Functions

**Concept:** Converting sync functions to async.
(تحويل الدوال المتزامنة إلى غير متزامنة.)

```dart
// Sync
String getName() => 'Bob';

// Async
Future<String> getNameAsync() async => 'Bob';
```

*   **English:** Adding `async` automatically wraps the return value in a `Future`.
*   **Arabic:** (إضافة `async` تغلف قيمة الإرجاع تلقائيًا في `Future`.)

## Handling Streams (`await for`)

**Concept:** Looping through data arriving over time.
(التكرار عبر البيانات التي تصل بمرور الوقت.)

```dart
await for (var number in numberStream) {
  print(number);
}
```

*   **English:** Works like a standard `for-in` loop, but pauses for each new item from the stream.
*   **Arabic:** (تعمل مثل حلقة `for-in` القياسية، ولكنها تتوقف مؤقتًا لكل عنصر جديد من التيار.)
*   **Analogy:** Watching a conveyor belt. You pick up one item, process it, wait for the next, and so on.

## Key Takeaways

*   **`Future`**: Represents a single value available later.
*   **`async`**: Marks a function as asynchronous and allows using `await`.
*   **`await`**: Pauses the function execution until the Future completes.
*   **`Stream`**: Represents a sequence of values available later.
*   **`await for`**: Loops through a stream asynchronously.

## Glossary

| Term | Definition | Arabic Meaning | Example |
| :--- | :--- | :--- | :--- |
| **Async** | Non-blocking execution style | غير متزامن | `async` keyword |
| **Await** | Pause execution for a Future | انتظار | `await future` |
| **Future** | A placeholder for a potential value | مستقبل | `Future<String>` |
| **Stream** | A source of sequential events | تيار | `Stream<int>` |
| **Exception** | An error event | استثناء | `try-catch` |
