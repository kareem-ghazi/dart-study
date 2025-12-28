# Functions

## Overview
Functions are the building blocks of Dart applications. They wrap a piece of code that performs a specific task. Dart is a true object-oriented language, so even functions are objects and can be assigned to variables or passed to other functions.

(الدوال هي اللبنات الأساسية لتطبيقات Dart. فهي تغلف جزءًا من الكود الذي يؤدي مهمة محددة. Dart هي لغة كائنية التوجه حقيقية، لذا حتى الدوال هي كائنات ويمكن تعيينها لمتغيرات أو تمريرها لدوال أخرى.)

## Parameters

### Named parameters
Named parameters allow you to pass arguments by name, making function calls more readable. They are optional by default unless marked `required`.
(المعاملات المسماة تسمح لك بتمرير القيم بالاسم، مما يجعل استدعاء الدالة أكثر قابلية للقراءة. هي اختيارية افتراضيًا ما لم يتم وضع علامة `required` عليها.)

```dart
void enableFlags({bool? bold, bool? hidden}) {
  // ...
}
enableFlags(bold: true);
```
**Explanation:** `bold` and `hidden` are named parameters enclosed in `{}`. You call them using `parameterName: value`. `bold` takes `true`, while `hidden` remains `null`.
(الشرح: `bold` و `hidden` هي معاملات مسماة محاطة بـ `{}`. يتم استدعاؤها باستخدام `اسم_المعامل: القيمة`. `bold` يأخذ القيمة `true` بينما يبقى `hidden` بقيمة `null`.)

**Analogy:** Think of a form where fields have labels (e.g., "Name:", "Age:"). You fill them based on the label, not just the order.
(تشبيه: فكر في نموذج حيث الحقول لها تسميات (مثل "الاسم:"، "العمر:"). أنت تملأها بناءً على التسمية، وليس الترتيب فقط.)

### Optional positional parameters
Parameters wrapped in `[]` are optional and based on position.
(المعاملات المحاطة بـ `[]` هي اختيارية وتعتمد على الموقع.)

```dart
String say(String from, String msg, [String? device]) {
  // ...
}
```
**Explanation:** `device` is optional. If you provide a third argument, it goes to `device`; otherwise, `device` is null.
(الشرح: `device` اختياري. إذا قدمت معاملًا ثالثًا، فسيذهب إلى `device`؛ وإلا، فإن `device` سيكون null.)

## The main() function
Every app requires a top-level `main()` function as its entry point.
(كل تطبيق يتطلب دالة `main()` عالية المستوى كنقطة دخول.)

```dart
void main() {
  print('Hello, World!');
}
```
**Explanation:** This is where the program execution starts. It returns `void` (nothing).
(الشرح: هذا هو المكان الذي يبدأ فيه تنفيذ البرنامج. لا تُرجع أي شيء `void`.)

## Functions as first-class objects
Functions can be treated like any other variable.
(يمكن التعامل مع الدوال مثل أي متغير آخر.)

```dart
var loudify = (msg) => '!!! ${msg.toUpperCase()} !!!';
assert(loudify('hello') == '!!! HELLO !!!');
```
**Explanation:** Here, an anonymous function is assigned to the variable `loudify`. You can call `loudify` like a function.
(الشرح: هنا، تم تعيين دالة مجهولة للمتغير `loudify`. يمكنك استدعاء `loudify` مثل الدالة.)

**Analogy:** A function is like a recipe card. You can hold the card (assign to variable), give it to a friend (pass as argument), or put it in a box (store in list).
(تشبيه: الدالة مثل بطاقة الوصفة. يمكنك حمل البطاقة (تعيين لمتغير)، إعطاؤها لصديق (تمرير كمعامل)، أو وضعها في صندوق (تخزين في قائمة).)

## Anonymous functions
Functions without a name, also called lambdas or closures.
(دوال بدون اسم، تسمى أيضًا lambdas أو closures.)

```dart
var list = ['apples', 'bananas', 'oranges'];
list.forEach((item) {
  print('${list.indexOf(item)}: $item');
});
```
**Explanation:** The code inside `forEach` is an anonymous function defined right where it's used. It takes `item` as a parameter.
(الشرح: الكود داخل `forEach` هو دالة مجهولة تم تعريفها في مكان استخدامها مباشرة. تأخذ `item` كمعامل.)

## Lexical scope & Closures
Dart is lexically scoped, meaning variables are accessible based on code structure (curly braces). A **closure** is a function that has access to the parent scope, even when used outside of that scope.
(لغة Dart ذات نطاق معجمي، مما يعني أن المتغيرات يمكن الوصول إليها بناءً على هيكل الكود (الأقواس المعقوفة). **Closure** هي دالة لها حق الوصول إلى النطاق الأصلي، حتى عند استخدامها خارج ذلك النطاق.)

```dart
Function makeAdder(int addBy) {
  return (int i) => addBy + i;
}
var add2 = makeAdder(2);
print(add2(3)); // 5
```
**Explanation:** `makeAdder` returns a function. The returned function remembers `addBy` (2) even after `makeAdder` has finished executing.
(الشرح: `makeAdder` ترجع دالة. الدالة المرجعة تتذكر `addBy` (2) حتى بعد انتهاء تنفيذ `makeAdder`.)

## Tear-offs
Using a function name without parentheses creates a reference to it (a closure) instead of calling it.
(استخدام اسم الدالة بدون أقواس ينشئ مرجعًا لها (closure) بدلاً من استدعائها.)

```dart
var charCodes = [68, 97, 114, 116];
charCodes.forEach(print);
```
**Explanation:** We pass `print` itself to `forEach`, not the result of `print()`. `forEach` calls it for each item.
(الشرح: نمرر `print` نفسها إلى `forEach`، وليس نتيجة `print()`. `forEach` تستدعيها لكل عنصر.)

## Return values
All functions return a value. If no return is specified, they implicitly return `null`.
(جميع الدوال ترجع قيمة. إذا لم يتم تحديد إرجاع، فإنها ترجع `null` ضمنيًا.)

```dart
foo() {}
assert(foo() == null);
```

## Getters and setters
Special methods that provide read and write access to an object's properties.
(طرق خاصة توفر الوصول للقراءة والكتابة لخصائص الكائن.)

```dart
String get secret => _secret.toUpperCase();
set secret(String value) => _secret = value;
```
**Explanation:** `get secret` calculates a value when accessed. `set secret` executes code when a value is assigned.
(الشرح: `get secret` تحسب قيمة عند الوصول إليها. `set secret` تنفذ كودًا عند تعيين قيمة.)

## Generators
Functions that lazily produce a sequence of values. `sync*` returns an `Iterable`, `async*` returns a `Stream`.
(دوال تنتج سلسلة من القيم بشكل كسول. `sync*` ترجع `Iterable`، و `async*` ترجع `Stream`.)

```dart
Iterable<int> naturalsTo(int n) sync* {
  int k = 0;
  while (k < n) yield k++;
}
```
**Explanation:** `yield` delivers a value and pauses execution until the next value is requested.
(الشرح: `yield` تسلم قيمة وتوقف التنفيذ مؤقتًا حتى يتم طلب القيمة التالية.)

## Important Notes & Warnings
*   **Default Values:** Named and optional parameters default to `null` unless a default value is provided. (القيم الافتراضية: المعاملات المسماة والاختيارية تكون افتراضيًا `null` ما لم يتم توفير قيمة افتراضية.)
*   **Required Parameters:** Use the `required` keyword for named parameters that must not be null. (المعاملات المطلوبة: استخدم الكلمة المفتاحية `required` للمعاملات المسماة التي يجب ألا تكون null.)
*   **Arrow Syntax:** `=> expr` is shorthand for `{ return expr; }`. It only works with expressions, not statements (like `if` blocks). (صيغة السهم: `=> expr` هي اختصار لـ `{ return expr; }`. تعمل فقط مع التعبيرات، وليس الجمل البرمجية.)

## Key Takeaways
*   Functions in Dart are objects (`Function` type).
*   You can have positional (`f(a, b)`) or named (`f({a, b})`) parameters.
*   The `main()` function is the entry point.
*   Anonymous functions (lambdas) are useful for callbacks like `forEach`.
*   Closures capture variables from their surrounding scope.
*   Getters and Setters allow control over property access.
*   Generators (`sync*`/`async*`) produce sequences of data lazily using `yield`.

## Glossary

| Term | Definition | Arabic Meaning | Example |
| :--- | :--- | :--- | :--- |
| **Parameter** | Variable in function declaration. | معامل | `void func(int x)` |
| **Argument** | Value passed to function call. | وسيط / حجة | `func(5)` |
| **Closure** | Function object that accesses variables from its lexical scope. | إغلاق (دالة تحتفظ بنطاقها) | `(i) => addBy + i` |
| **Lambda** | Anonymous function. | دالة مجهولة (لامدا) | `() => print('hi')` |
| **Tear-off** | Referring to a function without calling it. | فصل الدالة (كمرجع) | `forEach(print)` |
| **Generator** | Function that yields multiple values. | مولّد | `sync*` function |
