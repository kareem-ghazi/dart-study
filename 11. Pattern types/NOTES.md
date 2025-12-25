# Pattern Types

**Overview:**
There are many types of patterns in Dart, each acting like a specific tool or filter to check values. You can combine these simple tools to build complex validation and extraction logic.

**(نظرة عامة):**
هناك العديد من أنواع الأنماط في Dart، يعمل كل منها كأداة أو مرشح (filter) محدد لفحص القيم. يمكنك دمج هذه الأدوات البسيطة لبناء منطق معقد للتحقق والاستخراج.

---

## 1. Logical Patterns (الأنماط المنطقية)

Used to combine or chain other patterns.

*   **Logical-OR (`||`):** Matches if *either* side is true.
    *   *(مطابقة إذا كان أحد الطرفين صحيحاً.)*
    *   Example: `case 1 || 2:` (Matches 1 or 2)
*   **Logical-AND (`&&`):** Matches if *both* sides are true.
    *   *(مطابقة إذا كان كلا الطرفين صحيحين.)*
    *   Example: `case > 10 && < 20:` (Matches numbers between 10 and 20)

---

## 2. Relational Patterns (الأنماط العلائقية)

Used to compare values using operators like `==`, `<`, `>`, `<=`, `>=`.

*   **Usage:** Very useful for checking ranges of numbers.
*   *(الاستخدام: مفيد جدًا للتحقق من نطاقات الأرقام.)*
*   Example: `case < 0:` (Matches negative numbers)

---

## 3. Casting & Null Handling (التحويل ومعالجة القيم الفارغة)

Tools to handle types and nullability within a pattern.

*   **Cast (`as`):** Change the type before matching.
    *   `var (x as int)`
*   **Null-Check (`?`):** Matches if value is *not* null.
    *   `case var s?:` (Matches if `s` is not null)
*   **Null-Assert (`!`):** Forces a match to be non-null (throws error if null).
    *   `var (x!) = (null);` (Throws error)

---

## 4. Collection Patterns (أنماط المجموعات)

Match the structure of Lists, Maps, and Records.

*   **List (`[]`):** Matches a list and its elements positionally.
    *   `case [1, 2]:`
    *   **Rest Element (`...`):** Matches any remaining elements.
        *   `case [1, ..., 99]:` (Starts with 1, ends with 99, anything in between)
*   **Map (`{}`):** Matches a map by keys.
    *   `case {'name': 'Ali'}:`
*   **Record (`()`):** Matches a record's fields.
    *   `case (1, 2):` or `case (x: 1):`

---

## 5. Object & Wildcard Patterns (أنماط الكائنات وأحرف البدل)

*   **Object:** Checks the type and properties of a class instance.
    *   `case Circle(radius: var r):` (Is it a Circle? If so, get its radius).
    *   *(كائن: هل هو Circle؟ إذا كان كذلك، احصل على نصف قطره.)*
*   **Wildcard (`_`):** Matches anything but ignores it (doesn't save to a variable).
    *   `case [_, 2]:` (First element can be anything, second must be 2).
    *   *(حرف البدل: يطابق أي شيء ولكنه يتجاهله.)*

---

## Key Takeaways

*   **Precedence:** Patterns like `||` are evaluated after `&&`. Use parentheses `()` to group them if needed.
*   **Rest Element (`...`)**: Extremely powerful for list matching where you only care about the start or end.
*   **Object Patterns**: Allow you to "peer inside" an object and grab its properties in one step.
*   **Relational Patterns**: Make range checks (`0...10`) readable without verbose `if` statements.

---

## Glossary (English-Arabic)

| Term | Definition | Arabic Meaning | Example |
| :--- | :--- | :--- | :--- |
| **Logical-OR** | Matches if any sub-pattern matches. | "أو" المنطقية | `1 || 2` |
| **Relational** | Compares value using operators (`<`, `>`). | علائقي / مقارنة | `> 5` |
| **Cast Pattern** | Changes type during matching. | نمط التحويل | `x as int` |
| **Null-Assert** | Throws if value is null. | تأكيد عدم الفراغ | `x!` |
| **Rest Element** | Represents "the rest" of a list. | عنصر الباقي | `[1, ...]` |
| **Wildcard** | Matches anything, stores nothing. | حرف بدل / رمز عام | `_` |
