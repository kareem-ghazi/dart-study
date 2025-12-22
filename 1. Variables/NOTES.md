# Variables

## Overview
This page explains how to declare and use variables in Dart, including type inference, null safety, and creating constants.
*(تشرح هذه الصفحة كيفية تعريف واستخدام المتغيرات في Dart، بما في ذلك استنتاج النوع، أمان القيم الفارغة، وإنشاء الثوابت.)*

---

## Variable Declaration

- **Inference (`var`):** Dart usually figures out the type of a variable from its value.
  *(الاستنتاج: عادة ما تعرف Dart نوع المتغير من قيمته.)*

- **Explicit Type:** You can specify the type if you want to be precise.
  *(النوع الصريح: يمكنك تحديد النوع إذا كنت تريد أن تكون دقيقًا.)*

```dart
var name = 'Bob'; // Inferred as String (تم استنتاجه كنص)
String nickname = 'Bobby'; // Explicitly typed (تم تحديد النوع صراحة)
Object flexible = 'Bob'; // Can accept any type (يقبل أي نوع)
```

💡 *Analogy:*
*Using `var` is like asking a packer to box an item; they choose the right box size for you. Explicit typing is like handing them a specific box and saying "put it in this one".*
*(تشبيه: استخدام `var` مثل الطلب من عامل التغليف وضع غرض في صندوق؛ هو يختار الحجم المناسب. تحديد النوع مثل إعطائه صندوقًا محددًا والقول "ضعه في هذا".)*

---

## Null Safety

Null safety prevents errors caused by accessing variables that don't have a value (`null`).
*(يمنع نظام أمان القيم الفارغة الأخطاء الناتجة عن الوصول إلى متغيرات ليس لها قيمة.)*

- **Non-nullable (Default):** Variables cannot be `null` unless you say so.
  *(غير قابل للفراغ: لا يمكن للمتغيرات أن تكون `null` إلا إذا سمحت بذلك.)*

- **Nullable (`?`):** Add `?` to the type to allow `null`.
  *(قابل للفراغ: أضف `?` للنوع للسماح بـ `null`.)*

```dart
String name = 'Bob'; // Cannot be null (لا يمكن أن يكون null)
String? nullableName; // Can be null (يمكن أن يكون null)
```

---

## Default Value

- **Uninitialized Nullable Variables:** Default to `null`.
  *(المتغيرات القابلة للفراغ غير المهيأة: قيمتها الافتراضية `null`.)*

- **Non-nullable Variables:** Must be initialized before use.
  *(المتغيرات غير القابلة للفراغ: يجب تهيئتها قبل الاستخدام.)*

```dart
int? lineCount;
assert(lineCount == null); // True
```

---

## Late Variables

The `late` keyword is used in two cases:
1. **Delayed Initialization:** You promise Dart you will initialize the variable before using it.
   *(التهيئة المؤجلة: تعد Dart بأنك ستقوم بتهيئة المتغير قبل استخدامه.)*
2. **Lazy Initialization:** The variable is calculated only when accessed for the first time.
   *(التهيئة الكسولة: يتم حساب قيمة المتغير فقط عند الوصول إليه لأول مرة.)*

```dart
late String description;

void main() {
  description = 'Feijoada!'; // Initialized here (تمت التهيئة هنا)
  print(description);
}
```

💡 *Analogy:*
*`late` is like telling a waiter "I'll choose my order later". You promise to order before eating, or the chef (Dart) will be confused (throw an error).*
*(تشبيه: `late` مثل إخبار النادل "سأختار طلبي لاحقًا". أنت تعد بالطلب قبل الأكل، وإلا سيصاب الطاهي (Dart) بالارتباك ويحدث خطأ.)*

---

## Final and Const

Use these for variables that should not change.
*(استخدم هذه الكلمات للمتغيرات التي لا ينبغي أن تتغير.)*

- **`final`:** Set once. Can be set at runtime (e.g., current time).
  *(يتم تعيينه مرة واحدة. يمكن تحديده أثناء التشغيل، مثل الوقت الحالي.)*

- **`const`:** Compile-time constant. Must be known *before* the program runs.
  *(ثابت وقت التجميع. يجب أن تكون قيمته معروفة *قبل* تشغيل البرنامج.)*

```dart
final name = 'Bob'; // Set once (يحدد مرة واحدة)
const bar = 1000000; // Fixed forever (ثابت للأبد)
```

💡 *Analogy:*
*`final` is like writing a message in permanent marker; once written, it can't be changed. `const` is like carving it into stone; it's set in stone before you even start.*
*(تشبيه: `final` مثل الكتابة بقلم ثابت؛ بمجرد الكتابة لا يمكن التغيير. `const` مثل النحت في الحجر؛ محدد وثابت قبل أن تبدأ حتى.)*

---

## Wildcard Variables

- **Placeholder (`_`):** Use `_` when you don't need the variable's value or name.
  *(عنصر نائب `_`: استخدم `_` عندما لا تحتاج إلى قيمة المتغير أو اسمه.)*

```dart
for (var _ in list) {
  print('Item found!'); // Value ignored (تم تجاهل القيمة)
}
```

---

## Key Takeaways

- Prefer `var` for local variables.
  *(فضل استخدام `var` للمتغيرات المحلية.)*
- Dart is Null Safe by default; use `?` for nullable types.
  *(Dart آمنة من Null افتراضيًا؛ استخدم `?` للأنواع التي تقبل Null.)*
- Variables must be initialized before use.
  *(يجب تهيئة المتغيرات قبل استخدامها.)*
- Use `late` for variables initialized after declaration.
  *(استخدم `late` للمتغيرات التي تتم تهيئتها بعد التعريف.)*
- Use `final` for single-assignment variables and `const` for compile-time constants.
  *(استخدم `final` للمتغيرات التي تُعين مرة واحدة و `const` للثوابت المعروفة قبل التشغيل.)*

---

## Glossary

| Term | Definition | Arabic Meaning | Example |
| :--- | :--- | :--- | :--- |
| **Variable** | Stores a reference to a value. | متغير | `var x = 5;` |
| **Type Inference** | Compiler guesses the type. | استنتاج النوع | `var s = "Hi";` |
| **Nullable** | Type that can hold `null`. | قابل للفراغ | `int? x;` |
| **Late** | Delays variable initialization. | متأخر / مؤجل | `late String s;` |
| **Final** | Value set once (runtime). | نهائي | `final now = DateTime.now();` |
| **Const** | Value set at compile-time. | ثابت | `const pi = 3.14;` |
| **Wildcard** | A placeholder variable (`_`). | متغير بدل / مجهول | `for (var _ in list)` |
