# Libraries & Imports

## Overview
Libraries in Dart are modular units of code. Every Dart file is implicitly a library. They allow you to share code and control visibility (privacy) using the underscore `_` prefix.
(المكتبات في Dart هي وحدات نمطية من الكود. كل ملف Dart هو مكتبة ضمنيًا. تسمح لك بمشاركة الكود والتحكم في الرؤية (الخصوصية) باستخدام بادئة الشرطة السفلية `_`.)

## Using libraries
To use code from another library, you use the `import` directive.
(لاستخدام كود من مكتبة أخرى، تستخدم توجيه `import`.)

```dart
import 'dart:math'; // Built-in library
import 'package:test/test.dart'; // Package library
import 'path/to/my_file.dart'; // Local file
```

### Specifying a library prefix
If two libraries have classes with the same name, use `as` to give one a prefix.
(إذا كان لمكتبتين فئات بنفس الاسم، استخدم `as` لإعطاء إحداهما بادئة.)

```dart
import 'package:lib1/lib1.dart';
import 'package:lib2/lib2.dart' as lib2;

Element e1 = Element();      // From lib1
lib2.Element e2 = lib2.Element(); // From lib2
```
**Explanation:** `lib2` acts as a namespace to access items from the second library, preventing conflicts.
(الشرح: `lib2` يعمل كمساحة اسم للوصول إلى العناصر من المكتبة الثانية، مما يمنع التعارضات.)

**Analogy:** Two students named "Ahmed" in the same class. You call one "Ahmed A." and the other "Ahmed B." to distinguish them.
(تشبيه: طالبان اسمهما "أحمد" في نفس الفصل. تنادي أحدهما "أحمد أ." والآخر "أحمد ب." لتمييزهما.)

### Importing only part of a library
You can choose to import only specific parts (`show`) or exclude specific parts (`hide`).
(يمكنك اختيار استيراد أجزاء محددة فقط (`show`) أو استبعاد أجزاء محددة (`hide`).)

```dart
import 'package:lib1/lib1.dart' show foo; // Only foo is visible
import 'package:lib2/lib2.dart' hide bar; // Everything except bar is visible
```
**Explanation:** This keeps your namespace clean and avoids accidental usage of internal classes.
(الشرح: هذا يحافظ على نظافة مساحة الاسم الخاصة بك ويتجنب الاستخدام العرضي للفئات الداخلية.)

### Lazily loading a library (Deferred Loading)
You can load a library only when it's needed using `deferred as`. This is useful for web apps to reduce initial download size.
(يمكنك تحميل مكتبة فقط عند الحاجة إليها باستخدام `deferred as`. هذا مفيد لتطبيقات الويب لتقليل حجم التنزيل الأولي.)

```dart
import 'package:greetings/hello.dart' deferred as hello;

Future<void> greet() async {
  await hello.loadLibrary();
  hello.printGreeting();
}
```
**Explanation:** The `await hello.loadLibrary()` pauses execution until the code is fetched.
(الشرح: `await hello.loadLibrary()` يوقف التنفيذ مؤقتًا حتى يتم جلب الكود.)

## The library directive
Used mainly for documentation or annotations at the file level.
(يستخدم بشكل أساسي للتوثيق أو التعليقات التوضيحية على مستوى الملف.)

```dart
/// Math helper library
library math_helpers;
```

## Important Notes & Warnings
*   **Privacy:** Anything starting with `_` (underscore) is private to its library. It cannot be imported. (الخصوصية: أي شيء يبدأ بـ `_` (شرطة سفلية) هو خاص بمكتبته. لا يمكن استيراده.)
*   **Schemes:** Use `dart:` for built-ins, `package:` for dependencies, and relative paths for local files. (المخططات: استخدم `dart:` للمضمنات، `package:` للاعتماديات، والمسارات النسبية للملفات المحلية.)
*   **Circular Imports:** Dart handles circular imports well, but try to avoid complex dependencies. (الاستيرادات الدائرية: Dart تتعامل مع الاستيرادات الدائرية جيدًا، لكن حاول تجنب التبعيات المعقدة.)

## Key Takeaways
*   Every Dart file is a library.
*   `import` brings code into your scope.
*   `as` creates a prefix to resolve naming conflicts.
*   `show` and `hide` control what is imported.
*   `deferred as` allows lazy loading (mostly for web).
*   Privacy is enforced via the `_` prefix.

## Glossary

| Term | Definition | Arabic Meaning | Example |
| :--- | :--- | :--- | :--- |
| **Library** | A unit of code (a file) in Dart. | مكتبة | `import 'dart:math'` |
| **Import** | Directive to use code from another library. | استيراد | `import '...'` |
| **Prefix** | A name used to namespace a library. | بادئة | `as myLib` |
| **Deferred Loading** | Loading code on demand (lazy loading). | تحميل مؤجل | `deferred as` |
| **Namespace** | A container for names to avoid conflicts. | مساحة اسم | `lib2.Element` |
