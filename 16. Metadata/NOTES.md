# Metadata

## Overview
Metadata gives you a way to attach additional information to your code. This information can be used by the compiler, analyzer, or runtime. Annotations always start with `@`.
(البيانات الوصفية تعطيك طريقة لإرفاق معلومات إضافية بالكود الخاص بك. يمكن استخدام هذه المعلومات من قبل المترجم، المحلل، أو وقت التشغيل. التعليقات التوضيحية تبدأ دائمًا بـ `@`.)

## Built-in annotations

### @Deprecated
Use this to mark a function, class, or variable that should no longer be used. It helps developers know there is a newer, better way.
(استخدم هذا لتمييز دالة، فئة، أو متغير لا ينبغي استخدامه بعد الآن. يساعد المطورين على معرفة أن هناك طريقة أحدث وأفضل.)

```dart
@Deprecated('Use turnOn instead')
void activate() {
  turnOn();
}
```
**Explanation:** The `activate` method is marked as deprecated. The string message explains what to use instead (`turnOn`).
(الشرح: تم وضع علامة على طريقة `activate` بأنها مهملة. الرسالة النصية تشرح ما يجب استخدامه بدلاً منها (`turnOn`).)

**Analogy:** Putting a "Closed for Renovation" sign on an old bridge and directing traffic to the new bridge.
(تشبيه: وضع لافتة "مغلق للتجديد" على جسر قديم وتوجيه حركة المرور إلى الجسر الجديد.)

### @override
Indicates that a method is intended to replace (override) a method from a superclass.
(يشير إلى أن الطريقة تهدف إلى استبدال (تجاوز) طريقة من الفئة العليا.)

**Explanation:** This helps catch errors. If you misspell the method name, the analyzer will warn you that you aren't actually overriding anything.
(الشرح: هذا يساعد في اكتشاف الأخطاء. إذا أخطأت في كتابة اسم الطريقة، فسيحذرك المحلل بأنك لا تتجاوز أي شيء في الواقع.)

## Analyzer-supported annotations
These annotations usually come from `package:meta` and give hints to the analyzer to enforce certain rules.
(هذه التعليقات التوضيحية تأتي عادةً من `package:meta` وتعطي تلميحات للمحلل لفرض قواعد معينة.)

### @visibleForTesting
Marks a function or variable as "public" only so tests can access it. If normal code tries to use it, the analyzer warns.
(يميز دالة أو متغيرًا على أنه "عام" فقط لكي تتمكن الاختبارات من الوصول إليه. إذا حاول الكود العادي استخدامه، يقوم المحلل بالتحذير.)

## Custom annotations
You can create your own annotations by defining a class with a `const` constructor.
(يمكنك إنشاء تعليقات توضيحية خاصة بك عن طريق تعريف فئة مع منشئ ثابت `const`.)

```dart
class Todo {
  final String who;
  final String what;
  const Todo(this.who, this.what);
}

@Todo('Dash', 'Fix this')
void doWork() {}
```
**Explanation:** We define a `Todo` class. We can then use `@Todo(...)` to tag parts of our code.
(الشرح: نُعرف فئة `Todo`. يمكننا بعد ذلك استخدام `@Todo(...)` لوسم أجزاء من الكود الخاص بنا.)

**Analogy:** Like sticky notes you put on documents to remind yourself or others of tasks.
(تشبيه: مثل الملاحظات اللاصقة التي تضعها على المستندات لتذكير نفسك أو الآخرين بالمهام.)

## Important Notes & Warnings
*   **Const Constructors:** Annotation classes must have `const` constructors because metadata must be evaluated at compile-time. (المنشئات الثابتة: يجب أن تحتوي فئات التعليقات التوضيحية على منشئات `const` لأن البيانات الوصفية يجب تقييمها في وقت الترجمة.)
*   **Target:** You can restrict where your annotation can be used (e.g., only on functions) using `@Target`. (الهدف: يمكنك تقييد مكان استخدام تعليقك التوضيحي (مثلًا، فقط على الدوال) باستخدام `@Target`.)

## Key Takeaways
*   Metadata starts with `@`.
*   Common built-ins are `@Deprecated` and `@override`.
*   `@override` ensures you are correctly modifying inherited behavior.
*   You can create custom annotations using classes with `const` constructors.
*   Metadata doesn't change how code runs by default; it provides info for tools.

## Glossary

| Term | Definition | Arabic Meaning | Example |
| :--- | :--- | :--- | :--- |
| **Metadata** | Additional data about code. | بيانات وصفية | `@override` |
| **Annotation** | The syntactic form of metadata. | تعليق توضيحي | `@Deprecated(...)` |
| **Deprecated** | Status meaning "should not be used". | مهمل / مستنكر | `@Deprecated` |
| **Override** | Replacing a parent method. | تجاوز / إحلال | `@override` |
| **Compile-time** | The period when code is converted to executable. | وقت الترجمة | `const` values |
