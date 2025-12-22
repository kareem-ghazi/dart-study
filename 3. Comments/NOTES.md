# Comments

## Overview
Comments are non-executable text in your code used to explain logic, leave notes for developers, or generate documentation. The compiler completely ignores them.
(التعليقات هي نصوص غير قابلة للتنفيذ في الكود تستخدم لشرح المنطق، ترك ملاحظات للمطورين، أو إنشاء التوثيق. يتجاهلها المترجم تماماً.)

---

## Single-line Comments (التعليقات ذات السطر الواحد)
Used for brief explanations or notes on a specific line of code.
(تستخدم للشروحات المختصرة أو الملاحظات على سطر معين من الكود.)

```dart
// TODO: refactor into an AbstractLlamaGreetingFactory?
print('Welcome to my Llama farm!');
```

**Explanation:**
Starts with `//`. Everything after these slashes on the same line is invisible to the program.
(تبدأ بـ `//`. كل شيء بعد هاتين الشرطتين في نفس السطر يكون غير مرئي للبرنامج.)

**Analogy:**
Like writing a sticky note and putting it on a page of a book. It helps you remember something, but it's not part of the story.
(مثل كتابة ملاحظة لاصقة ووضعها على صفحة في كتاب. تساعدك على تذكر شيء ما، لكنها ليست جزءاً من القصة.)

---

## Multi-line Comments (التعليقات متعددة الأسطر)
Used for longer explanations or for temporarily disabling chunks of code.
(تستخدم للشروحات الطويلة أو لتعطيل أجزاء من الكود مؤقتاً.)

```dart
/*
 * This is a lot of work. Consider raising chickens.
 Llama larry = Llama();
 larry.feed();
 */
```

**Explanation:**
Starts with `/*` and ends with `*/`. Can span multiple lines. Unlike many other languages, Dart supports **nested** multi-line comments.
(تبدأ بـ `/*` وتنتهي بـ `*/`. يمكن أن تمتد لعدة أسطر. على عكس العديد من اللغات الأخرى، يدعم Dart التعليقات متعددة الأسطر **المتداخلة**.)

---

## Documentation Comments (تعليقات التوثيق)
Specially formatted comments used to generate API documentation (HTML pages).
(تعليقات منسقة بشكل خاص تستخدم لإنشاء توثيق API (صفحات HTML).)

```dart
/// A domesticated South American camelid (Lama glama).
///
/// Just like any other animal, llamas need to eat,
/// so don't forget to [feed] them some [Food].
class Llama { ... }
```

**Explanation:**
- Starts with `///` (preferred) or `/**`.
- Uses square brackets `[...]` to link to other classes, methods, or parameters.
- Tools like `dart doc` read these comments to build official documentation.
(تبدأ بـ `///` (المفضلة) أو `/**`. تستخدم الأقواس المربعة `[...]` للربط بفئات، طرق، أو معاملات أخرى. أدوات مثل `dart doc` تقرأ هذه التعليقات لبناء التوثيق الرسمي.)

**Analogy:**
This is like writing the "Instruction Manual" for your code. If you buy a TV, you get a manual explaining what buttons do. `///` comments are that manual for other developers using your code.
(هذا مثل كتابة "دليل التعليمات" للكود الخاص بك. إذا اشتريت تلفازاً، تحصل على دليل يشرح وظائف الأزرار. تعليقات `///` هي ذلك الدليل للمطورين الآخرين الذين يستخدمون الكود الخاص بك.)

---

## Important Notes & Warnings
*   **Don't Over-comment:** Good code should explain itself. Use comments for "Why", not "What".
    (لا تفرط في التعليق. الكود الجيد يشرح نفسه. استخدم التعليقات لـ "لماذا"، وليس "ماذا".)
*   **TODOs:** Using `// TODO:` is a standard convention to mark things that need to be done later. IDEs often highlight these.
    (استخدام `// TODO:` هو عرف قياسي لتمييز الأشياء التي يجب القيام بها لاحقاً. بيئات التطوير غالباً ما تميز هذه.)
*   **Documentation:** Always document public classes and functions so others (and your future self) know how to use them.
    (قم دائماً بتوثيق الفئات والدوال العامة حتى يعرف الآخرون (وأنت في المستقبل) كيفية استخدامها.)

---

## Key Takeaways
*   `//` for single lines.
*   `/* ... */` for blocks (can nest).
*   `///` for documentation (supports `[links]`).
*   Comments are ignored by the compiler.
*   Use comments to explain complex logic or intent.

---

## Glossary

| Term | Definition | Arabic Meaning | Example |
| --- | --- | --- | --- |
| **Comment** | Text ignored by the compiler, meant for humans. | تعليق | `// Hello` |
| **Single-line** | A comment occupying only the rest of the line. | سطر واحد | `// ...` |
| **Multi-line** | A comment spanning multiple lines. | متعدد الأسطر | `/* ... */` |
| **Documentation** | Comments used to generate external docs. | توثيق | `/// ...` |
| **Nesting** | Placing a comment inside another comment. | التداخل | `/* /* inner */ outer */` |
| **Compiler** | The program that converts code to executable instructions. | المترجم | It ignores comments. |
