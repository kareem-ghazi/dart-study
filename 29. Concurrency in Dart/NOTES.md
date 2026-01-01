# Concurrency in Dart

## Overview

Dart uses a unique model for concurrency. By default, it runs on a single thread using an **Event Loop** to handle asynchronous tasks (like waiting for data). For true parallelism (running code on multiple CPU cores at once), Dart uses **Isolates**.

(يستخدم Dart نموذجًا فريدًا للتزامن. بشكل افتراضي، يعمل على خيط واحد باستخدام **حلقة الأحداث** لمعالجة المهام غير المتزامنة (مثل انتظار البيانات). ولتحقيق توازٍ حقيقي (تشغيل الكود على عدة أنوية للمعالج في وقت واحد)، يستخدم Dart **العزلات**.)

## Event Loop

**Concept:** The mechanism that executes tasks one by one.
(الآلية التي تنفذ المهام واحدة تلو الأخرى.)

*   **English:** The event loop takes events (clicks, timers, data ready) from a queue and processes them sequentially. It never blocks.
*   **Arabic:** (تأخذ حلقة الأحداث الأحداث (نقرات، مؤقتات، بيانات جاهزة) من قائمة الانتظار وتعالجها بالتسلسل. هي لا تتوقف أبدًا.)
*   **Analogy:** A single waiter in a restaurant. He takes an order to the kitchen, then goes to the next table. He doesn't stand in the kitchen waiting for the food to cook.
    (تشبيه: نادل واحد في مطعم. يأخذ طلبًا إلى المطبخ، ثم يذهب إلى الطاولة التالية. لا يقف في المطبخ منتظرًا طهي الطعام.)

## Futures & Async/Await

**Concept:** Handling results that will arrive later.
(التعامل مع النتائج التي ستصل لاحقًا.)

```dart
Future<String> fetchUser() async {
  // Simulate network delay
  await Future.delayed(Duration(seconds: 2));
  return 'User 1';
}
```

*   **English:** `Future` is a placeholder for a value not yet ready. `async/await` makes reading this code look synchronous (step-by-step) even though it's not blocking the CPU.
*   **Arabic:** (`Future` هو مكان محجوز لقيمة ليست جاهزة بعد. `async/await` تجعل قراءة هذا الكود تبدو متزامنة (خطوة بخطوة) على الرغم من أنها لا تحجب المعالج.)

## Streams

**Concept:** A sequence of asynchronous events.
(تسلسل من الأحداث غير المتزامنة.)

```dart
Stream<int> countStream() async* {
  for (int i = 1; i <= 5; i++) {
    await Future.delayed(Duration(seconds: 1));
    yield i;
  }
}
```

*   **English:** Like a Future, but for multiple values over time. You use `await for` to listen to them.
*   **Arabic:** (مثل Future، ولكن لقيم متعددة بمرور الوقت. تستخدم `await for` للاستماع إليها.)
*   **Analogy:** A conveyor belt in a factory. Items (data) arrive one by one over time.
    (تشبيه: حزام ناقل في مصنع. العناصر (البيانات) تصل واحدة تلو الأخرى بمرور الوقت.)

## Isolates

**Concept:** True parallelism with isolated memory.
(توازي حقيقي مع ذاكرة معزولة.)

```dart
void heavyTask() async {
  // Runs on a separate thread
  await Isolate.run(() => complexCalculation());
}
```

*   **English:** Isolates are like separate little programs. They don't share memory (variables). They communicate by sending messages. This prevents "race conditions" where two threads fight over the same variable.
*   **Arabic:** (العزلات مثل برامج صغيرة منفصلة. لا تتشارك الذاكرة (المتغيرات). تتواصل عن طريق إرسال الرسائل. هذا يمنع "سباق البيانات" حيث يتنافس خيطان على نفس المتغير.)
*   **Analogy:** Two separate kitchens. Kitchen A can't touch ingredients in Kitchen B. They can only pass finished dishes through a window.
    (تشبيه: مطبخان منفصلان. المطبخ "أ" لا يمكنه لمس المكونات في المطبخ "ب". يمكنهم فقط تمرير الأطباق الجاهزة عبر نافذة.)

## Key Takeaways

*   **Event Loop**: Handles async tasks on a single thread.
*   **Non-blocking**: Dart code shouldn't block the loop (freeze the UI).
*   **`async/await`**: Syntactic sugar to make Futures easy to read.
*   **Isolates**: Use for heavy CPU work (parsing huge JSON, image processing) to keep the app smooth.
*   **No Shared Memory**: Isolates are safe because they don't share variables.

## Glossary

| Term | Definition | Arabic Meaning | Example |
| :--- | :--- | :--- | :--- |
| **Concurrency** | Doing multiple things during the same period | التزامن | Event Loop switching tasks |
| **Parallelism** | Doing multiple things exactly at the same time | التوازي | Multiple Isolates on multiple cores |
| **Future** | An object representing a delayed result | المستقبل | `Future<int>` |
| **Stream** | A source of asynchronous data events | تيار / مجرى | `Stream<int>` |
| **Isolate** | Independent worker with its own memory | عزلة | `Isolate.run(...)` |
