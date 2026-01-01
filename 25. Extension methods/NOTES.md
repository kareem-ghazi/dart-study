# Extension Methods

## Overview
**Extension Methods** allow you to add new functionality to existing libraries or classes, even if you didn't write them. You can add methods to `String`, `int`, or even your own classes without modifying the original file.
(**دوال التوسعة (Extension Methods)** تسمح لك بإضافة وظائف جديدة للمكتبات أو الفئات الموجودة، حتى لو لم تقم بكتابتها. يمكنك إضافة دوال لـ `String`، `int`، أو حتى فئاتك الخاصة دون تعديل الملف الأصلي.)

---

## Basic Syntax

### Concept
Use `extension Name on Type` to define the new methods.
(استخدم `extension Name on Type` لتعريف الدوال الجديدة.)

### Code Example
```dart
extension StringExtensions on String {
  bool get isCapitalized => this[0] == this[0].toUpperCase();
}

print('Hello'.isCapitalized); // true
```
**Explanation:** We added a property `isCapitalized` to ALL strings in our project.
(**الشرح:** قمنا بإضافة خاصية `isCapitalized` لجميع النصوص في مشروعنا.)

### Analogy
**Phone Case with Battery.** The phone (String) works fine. You add a case (Extension) that gives it extra battery life (Method). The phone inside didn't change, but now it can do more.
(**غطاء هاتف ببطارية.** الهاتف (String) يعمل جيداً. تضيف غطاء (Extension) يعطيه عمر بطارية إضافي (Method). الهاتف بالداخل لم يتغير، لكنه الآن يمكنه فعل المزيد.)

---

## Static Resolution

### Concept
Extensions are resolved **statically** (at compile time). This means they **do not work on `dynamic`** types. Dart needs to know the exact type to find the extension.
(يتم حل التوسعات **بشكل ساكن** (وقت الترجمة). هذا يعني أنها **لا تعمل على الأنواع الديناميكية `dynamic`**. Dart بحاجة لمعرفة النوع الدقيق لإيجاد التوسعة.)

### Code Example
```dart
dynamic d = 'Hello';
// d.isCapitalized; // Error! Dart doesn't know 'd' is a String.
```

---

## Generic Extensions

### Concept
You can extend generic types like `List<T>`.
(يمكنك توسيع الأنواع العامة مثل `List<T>`.)

### Code Example
```dart
extension ListExt<T> on List<T> {
  T? get second => length >= 2 ? this[1] : null;
}
```

---

## API Conflicts

### Concept
If two extensions define the same method name, Dart gets confused. You can fix this by hiding one import or using explicit syntax.
(إذا قامت توسعتان بتعريف نفس اسم الدالة، ترتبك Dart. يمكنك إصلاح ذلك بإخفاء استيراد واحد أو استخدام الصيغة الصريحة.)

### Code Example
```dart
// Explicit syntax acts like a wrapper
ExtensionName(object).method(); 
```

---

## Important Notes & Warnings

*   **Helper Methods:** Extensions are great for utility functions specific to your app. (التوسعات رائعة لدوال المساعدة الخاصة بتطبيقك.)
*   **Don't Overuse:** If you own the class, it's usually better to add the method directly to the class. Use extensions for classes you can't control (like `DateTime` or `String`). (لا تفرط في الاستخدام: إذا كنت تملك الفئة، عادة ما يكون من الأفضل إضافة الدالة مباشرة للفئة. استخدم التوسعات للفئات التي لا يمكنك التحكم فيها.)
*   **Scope:** Extensions are only available if you import the file defining them. (التوسعات متاحة فقط إذا قمت باستيراد الملف الذي يعرفها.)

---

## Key Takeaways

1.  **Syntactic Sugar:** Calls look like normal methods (`obj.method()`) but are actually static helpers behind the scenes.
2.  **No Dynamic:** Never use extensions with `dynamic`.
3.  **On Any Type:** You can write extensions on any type, even `Function` or `Null`.

---

## Glossary

| Term | Definition | Arabic Meaning | Example |
| :--- | :--- | :--- | :--- |
| **Extension** | A construct to add members to a type. | توسعة | `extension E on String` |
| **Receiver** | The object the extension is called on (`this`). | المستقبل | `this.length` |
| **Explicit Extension** | Calling extension wrapper manually. | توسعة صريحة | `E(obj).method()` |
