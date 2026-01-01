# Isolates

## Overview

Isolates are Dart's way of doing multi-threading. Unlike threads in other languages that share memory (which causes bugs), Dart isolates are completely separate. They have their own memory and communicate by sending messages.

(العزلات هي طريقة Dart للقيام بتعدد الخيوط. على عكس الخيوط في اللغات الأخرى التي تشترك في الذاكرة (مما يسبب أخطاء)، فإن عزلات Dart منفصلة تمامًا. لديهم ذاكرتهم الخاصة ويتواصلون عن طريق إرسال الرسائل.)

## `Isolate.run` (Short-lived)

**Concept:** Run a function on another core and get the result.
(تشغيل دالة على نواة أخرى والحصول على النتيجة.)

```dart
final result = await Isolate.run(() => heavyTask());
```

*   **English:** Best for "one-off" tasks like parsing a large file. It starts, does the work, sends the result, and closes.
*   **Arabic:** (الأفضل للمهام "لمرة واحدة" مثل تحليل ملف كبير. تبدأ، وتقوم بالعمل، وترسل النتيجة، وتغلق.)
*   **Analogy:** Hiring a freelancer for one specific project. They do it and leave.

## `Isolate.spawn` (Long-lived)

**Concept:** Start a worker that stays alive to handle multiple messages.
(بدء عامل يبقى على قيد الحياة لمعالجة رسائل متعددة.)

```dart
await Isolate.spawn(workerFunction, receivePort.sendPort);
```

*   **English:** Useful if you have a continuous stream of heavy work (e.g., processing video frames). Requires setting up ports.
*   **Arabic:** (مفيد إذا كان لديك تدفق مستمر من العمل الثقيل (مثل معالجة إطارات الفيديو). يتطلب إعداد المنافذ.)
*   **Analogy:** Hiring a full-time employee. You need a dedicated line of communication.

## Ports (`SendPort` & `ReceivePort`)

**Concept:** The communication channel.
(قناة الاتصال.)

*   **`ReceivePort`**: The listening end (Mailbox).
*   **`SendPort`**: The sending end (Address).

*   **English:** You create a `ReceivePort` to listen. You give the `SendPort` to the other isolate so it can talk to you.
*   **Arabic:** (تقوم بإنشاء `ReceivePort` للاستماع. تعطي `SendPort` للعزلة الأخرى حتى تتمكن من التحدث إليك.)

## Key Takeaways

*   **No Shared Memory**: Variables in one isolate cannot be touched by another.
*   **Message Passing**: Use ports to send data back and forth.
*   **UI Unblocking**: Isolates keep the main thread free for UI updates.
*   **Overhead**: Creating an isolate takes time/memory. Don't use them for tiny tasks.

## Glossary

| Term | Definition | Arabic Meaning | Example |
| :--- | :--- | :--- | :--- |
| **Isolate** | Independent execution thread with own memory | عزلة | `Isolate.spawn` |
| **Main Isolate** | The default thread where `main()` runs | العزلة الرئيسية | UI thread |
| **Spawn** | To create and start a new isolate | تفريخ / إنشاء | `Isolate.spawn(...)` |
| **Port** | Communication endpoint | منفذ | `ReceivePort` |
| **Closure** | An anonymous function | دالة مجهولة / إغلاق | `() => print('hi')` |
