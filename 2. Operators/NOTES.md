# Operators

## Overview
Operators are special symbols that check, change, or combine values. They are the building blocks of expressions in Dart, allowing you to perform calculations, comparisons, and logic checks.
(المعاملات هي رموز خاصة تقوم بفحص أو تغيير أو دمج القيم. هي اللبنات الأساسية للتعبيرات في Dart، مما يتيح لك إجراء العمليات الحسابية، والمقارنات، والتحقق المنطقي.)

---

## Operator Precedence (أولوية المعاملات)
Operator precedence determines the order in which operators are evaluated. Just like in mathematics, multiplication happens before addition.
(تحدد أولوية المعاملات الترتيب الذي يتم به تقييم المعاملات. تماماً كما في الرياضيات، يتم الضرب قبل الجمع.)

```dart
// Parentheses improve readability.
if ((n % i == 0) && (d % i == 0)) {
  // ...
}

// Harder to read, but equivalent.
if (n % i == 0 && d % i == 0) {
  // ...
}
```

**Explanation:**
The first example uses parentheses to explicitly show the order of operations. The second relies on Dart's default precedence rules (where `%` happens before `==`, and `==` before `&&`).
(المثال الأول يستخدم الأقواس لتوضيح ترتيب العمليات بشكل صريح. الثاني يعتمد على قواعد الأولوية الافتراضية في Dart حيث يتم تنفيذ `%` قبل `==`، و `==` قبل `&&`.)

**Analogy:**
Think of PEMDAS in math class. You always solve what's in parentheses first, then exponents, multiplication/division, and finally addition/subtraction.
(فكر في ترتيب العمليات الحسابية في الرياضيات. تقوم دائماً بحل ما بداخل الأقواس أولاً، ثم الأسس، الضرب/القسمة، وأخيراً الجمع/الطرح.)

---

## Arithmetic Operators (المعاملات الحسابية)
These are used for basic mathematical calculations like addition, subtraction, multiplication, and division.
(تستخدم هذه لإجراء العمليات الحسابية الأساسية مثل الجمع، الطرح، الضرب، والقسمة.)

```dart
assert(2 + 3 == 5);
assert(2 - 3 == -1);
assert(2 * 3 == 6);
assert(5 / 2 == 2.5); // Result is a double
assert(5 ~/ 2 == 2); // Result is an int
assert(5 % 2 == 1); // Remainder
```

**Explanation:**
- `+`, `-`, `*`, `/`: Standard math operators.
- `~/`: Integer division (truncates the decimal part).
- `%`: Modulo (returns the remainder of division).
(الرموز القياسية للرياضيات. `~/` للقسمة الصحيحة (تحذف الجزء العشري). `%` باقي القسمة.)

**Analogy:**
- `5 / 2` is like sharing 5 apples between 2 people precisely (2.5 apples each).
- `5 ~/ 2` is like sharing whole apples only (each gets 2, 0.5 is ignored).
- `5 % 2` is the one apple left over.
(`5 / 2` مثل تقسيم 5 تفاحات على شخصين بالتساوي (2.5 لكل منهما). `5 ~/ 2` مثل تقسيم التفاح الكامل فقط (كل شخص يحصل على 2). `5 % 2` هي التفاحة المتبقية.)

---

## Increment and Decrement (الزيادة والنقصان)
Shortcuts to add or subtract 1 from a variable.
(اختصارات لإضافة أو طرح 1 من متغير.)

```dart
int a = 0;
int b = ++a; // Increment a before b gets its value.
assert(a == b); // 1 == 1

a = 0;
b = a++; // Increment a after b gets its value.
assert(a != b); // 1 != 0
```

**Explanation:**
- `++var` (Prefix): Increment, then use the value.
- `var++` (Postfix): Use the value, then increment.
(`++var` (بادئة): قم بالزيادة، ثم استخدم القيمة. `var++` (لاحقة): استخدم القيمة، ثم قم بالزيادة.)

---

## Equality and Relational Operators (معاملات المساواة والعلاقة)
Used to compare two values, resulting in a boolean (`true` or `false`).
(تستخدم لمقارنة قيمتين، وتكون النتيجة قيمة منطقية `true` أو `false`.)

```dart
assert(2 == 2);
assert(2 != 3);
assert(3 > 2);
assert(2 < 3);
```

**Explanation:**
- `==`: Checks if values are equal.
- `!=`: Checks if values are not equal.
- `>`, `<`, `>=`, `<=`: Standard comparisons.
(`==` يتحقق مما إذا كانت القيم متساوية. `!=` يتحقق مما إذا كانت القيم غير متساوية.)

---

## Type Test Operators (معاملات اختبار النوع)
Check the type of an object at runtime.
(التحقق من نوع الكائن أثناء التشغيل.)

```dart
if (employee is Person) {
  // Type check
  employee.firstName = 'Bob';
}
```

**Explanation:**
- `is`: Returns true if the object has the specified type.
- `as`: Casts an object to a specific type (throws error if invalid).
(`is`: ترجع true إذا كان الكائن من النوع المحدد. `as`: يحول الكائن إلى نوع معين.)

**Analogy:**
Checking `is Fruit` allows you to treat an object like a fruit safely. `as Fruit` forces it into a fruit box—if it's actually a rock, it breaks the box (error).
(التحقق باستخدام `is Fruit` يسمح لك بمعاملة الكائن كفاكهة بأمان. `as Fruit` يجبره على الدخول في صندوق الفاكهة—إذا كان صخرة، سيكسر الصندوق.)

---

## Assignment Operators (معاملات التعيين)
Assign values to variables.
(تعيين قيم للمتغيرات.)

```dart
a = value;
b ??= value; // Assign only if b is null
a += b;      // Same as a = a + b
```

**Explanation:**
- `=`: Basic assignment.
- `??=`: Assigns only if the variable is currently `null`.
- `+=`, `*=`, etc.: Perform an operation and assign the result.
(`=`: تعيين أساسي. `??=`: يعين فقط إذا كان المتغير `null`. `+=`، `*=`، إلخ: تنفذ عملية وتعين النتيجة.)

---

## Logical Operators (المعاملات المنطقية)
Combine or invert boolean values.
(دمج أو عكس القيم المنطقية.)

```dart
if (!done && (col == 0 || col == 3)) { ... }
```

**Explanation:**
- `!`: NOT (inverts value).
- `&&`: AND (both must be true).
- `||`: OR (at least one must be true).
(`!`: ليس (يعكس القيمة). `&&`: و (يجب أن يكون كلاهما صحيحاً). `||`: أو (يجب أن يكون أحدهما على الأقل صحيحاً).)

---

## Conditional Expressions (التعبيرات الشرطية)
Concise ways to handle conditions without full `if-else` blocks.
(طرق مختصرة للتعامل مع الشروط بدون استخدام كتل `if-else` الكاملة.)

```dart
var visibility = isPublic ? 'public' : 'private';
String playerName(String? name) => name ?? 'Guest';
```

**Explanation:**
- `condition ? expr1 : expr2`: If true, `expr1`; else `expr2`. (Ternary operator).
- `expr1 ?? expr2`: If `expr1` is not null, use it; else use `expr2`.
(`condition ? expr1 : expr2`: إذا كان الشرط صحيحاً، نفذ `expr1`؛ وإلا `expr2`. `expr1 ?? expr2`: إذا لم يكن `expr1` فارغاً، استخدمه؛ وإلا استخدم `expr2`.)

---

## Cascade Notation (تدوين التتابع)
Allows you to perform a sequence of operations on the same object.
(يسمح لك بإجراء سلسلة من العمليات على نفس الكائن.)

```dart
var paint = Paint()
  ..color = Colors.black
  ..strokeCap = StrokeCap.round
  ..strokeWidth = 5.0;
```

**Explanation:**
Instead of writing `paint.color = ...; paint.strokeCap = ...;`, you chain them with `..`.
(بدلاً من كتابة اسم الكائن مراراً وتكراراً، تقوم بربط العمليات باستخدام `..`.)

**Analogy:**
Like ordering at a restaurant: "I'll have the burger, ..with cheese, ..no onions, ..and fries." You don't say "I'll have the burger with cheese. I'll have the burger with no onions."
(مثل الطلب في مطعم: "سأطلب البرجر، ..مع جبن، ..بدون بصل، ..وبطاطس." لا تكرر "سأطلب البرجر" في كل مرة.)

---

## Important Notes & Warnings
*   **Integer Division:** Remember `~/` returns an integer. Normal `/` always returns a `double`.
    (تذكر أن `~/` ترجع عدداً صحيحاً. القسمة العادية `/` ترجع دائماً `double`.)
*   **Equality:** `==` works for value comparison. Don't use it to check if two variables point to the exact same memory location (use `identical()` for that, though rarely needed).
    (`==` تعمل لمقارنة القيم. لا تستخدمها للتحقق مما إذا كان متغيران يشيران إلى نفس موقع الذاكرة.)
*   **Null Safety:** Operators like `??`, `?.`, `??=`, and `!` are crucial for handling null values safely in Dart.
    (المعاملات المتعلقة بـ null ضرورية جداً للتعامل الآمن مع القيم الفارغة في Dart.)

---

## Key Takeaways
*   **Arithmetic:** Dart has standard math operators plus integer division `~/`.
*   **Precedence:** Multiplication/division happen before addition/subtraction.
*   **Increment:** `++i` (pre) increments immediately; `i++` (post) increments after use.
*   **Type Checking:** Use `is` to check types and `as` to cast types.
*   **Null Aware:** `??` provides a fallback for null values.
*   **Cascades:** `..` lets you chain method calls on one object.

---

## Glossary

| Term | Definition | Arabic Meaning | Example |
| --- | --- | --- | --- |
| **Operator** | A symbol performing an operation on values. | مُعامِل | `+`, `-`, `==` |
| **Operand** | The value an operator acts on. | المُعامَل (الطرف) | In `a + b`, `a` and `b` are operands. |
| **Precedence** | The priority rule for processing operators. | الأولوية | `*` is higher than `+`. |
| **Associativity** | Direction of processing (left-to-right or right-to-left). | الترابطية | `a = b = c` is right-associative. |
| **Unary** | An operator taking only one operand. | أحادي | `++`, `!`, `-` (negation). |
| **Binary** | An operator taking two operands. | ثنائي | `+`, `&&`, `==`. |
| **Ternary** | An operator taking three operands. | ثلاثي | `condition ? a : b`. |
