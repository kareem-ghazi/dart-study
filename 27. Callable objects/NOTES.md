# Callable Objects

## Overview
Dart allows you to treat an object instance like a function. If you can write `obj()`, it's a callable object. This is sometimes called a "Functor".
(تسمح لك Dart بمعاملة نسخة الكائن كدالة. إذا كنت تستطيع كتابة `obj()`، فهو كائن قابل للاستدعاء. يسمى هذا أحياناً "Functor".)

---

## The `call()` Method

### Concept
Simply name a method `call`. Dart automatically routes any attempt to "run" the object to this method.
(ببساطة سمِّ الدالة `call`. تقوم Dart تلقائياً بتوجيه أي محاولة "لتشغيل" الكائن إلى هذه الدالة.)

### Code Example
```dart
class Greeter {
  void call(String name) => print('Hello $name!');
}

var g = Greeter();
g('Ali'); // Equivalent to g.call('Ali')
```
**Explanation:** We invoke `g` as if it were a function name.
(**الشرح:** نستدعي `g` كما لو كان اسم دالة.)

### Analogy
**Walkie-Talkie Button.** The object is the walkie-talkie. The `call` method is the big side button. When you squeeze the whole object (call it), the button activates.
(**زر الجهاز اللاسلكي.** الكائن هو الجهاز. دالة `call` هي الزر الجانبي الكبير. عندما تضغط على الكائن بالكامل (تستدعيه)، يتم تفعيل الزر.)

---

## Key Takeaways

1.  **Cleaner Syntax:** Useful for classes that have one main purpose (like a validator or converter).
2.  **Stateful Functions:** Unlike a normal function, a callable object can store data (fields) between calls.
3.  **Type Signature:** The object can be passed where a `Function` is expected if the signature matches.

---

## Glossary

| Term | Definition | Arabic Meaning | Example |
| :--- | :--- | :--- | :--- |
| **Callable Object** | An object invoked like a function. | كائن قابل للاستدعاء | `var x = Class(); x();` |
| **call()** | The magic method name for callables. | دالة الاستدعاء | `void call() { ... }` |
