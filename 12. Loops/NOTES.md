# Loops

**Overview:**
Loops are control flow statements that allow you to repeat a block of code multiple times. This is essential for processing lists of items, repeating actions until a condition is met, or simply counting.

**(نظرة عامة):**
الحلقات (Loops) هي جمل تحكم في التدفق تسمح لك بتكرار كتلة من الكود عدة مرات. هذا ضروري لمعالجة قوائم العناصر، أو تكرار الإجراءات حتى يتم استيفاء شرط معين، أو ببساطة للعد.

---

## 1. Standard `for` Loop (حلقة for القياسية)

Use this when you know exactly how many times you want to loop (e.g., "5 times").

```dart
for (var i = 0; i < 5; i++) {
  print(i); // Prints 0, 1, 2, 3, 4
}
```
*   **Initialization (`var i = 0`):** Starts the counter.
*   **Condition (`i < 5`):** Checks if the loop should continue.
*   **Increment (`i++`):** Updates the counter after each loop.

---

## 2. `for-in` Loop (حلقة for-in)

The **best way** to loop through lists or collections. You don't need to manage an index variable (`i`).

```dart
var names = ['Ali', 'Sara', 'Zayn'];
for (var name in names) {
  print(name);
}
```
*   **Analogy:** Imagine picking items one by one from a basket until it's empty.
*   *(تشبيه: تخيل التقاط العناصر واحدًا تلو الآخر من سلة حتى تفرغ.)*

---

## 3. `while` Loop (حلقة while)

Use this when you don't know how many times to loop, but you know the **stop condition**. It checks the condition **before** running.

```dart
while (!isDone()) {
  keepWorking();
}
```
*   **Note:** If the condition is false initially, the loop never runs.
*   *(ملاحظة: إذا كان الشرط خطأ في البداية، فلن تعمل الحلقة أبدًا.)*

---

## 4. `do-while` Loop (حلقة do-while)

Similar to `while`, but checks the condition **after** running. It guarantees the code runs **at least once**.

```dart
do {
  print('Run once!');
} while (false);
```

---

## 5. Controlling Loops (التحكم في الحلقات)

*   **`break`**: Stops the loop completely and exits.
    *   *(يوقف الحلقة تمامًا ويخرج منها.)*
*   **`continue`**: Skips the current iteration and jumps to the next one.
    *   *(يتخطى التكرار الحالي وينتقل إلى التالي.)*

```dart
for (var i = 0; i < 10; i++) {
  if (i == 5) break; // Stop at 5
  if (i % 2 == 0) continue; // Skip even numbers
  print(i);
}
```

---

## Key Takeaways

*   Use `for-in` for Lists and Sets (it's cleaner).
*   Use `for` with index `i` if you need the position number.
*   Use `while` for indefinite waiting or logic checks.
*   Avoid **Infinite Loops**: Always ensure your loop condition eventually becomes false!
*   **Labels** allow you to break out of nested loops (loops inside loops).

---

## Glossary (English-Arabic)

| Term | Definition | Arabic Meaning | Example |
| :--- | :--- | :--- | :--- |
| **Iteration** | One single pass through the loop. | تكرار / دورة | Each print in a loop. |
| **Iterable** | A collection that can be looped over (List, Set). | قابل للتكرار | `[1, 2, 3]` |
| **Index** | The position number of an item (starts at 0). | فهرس / مؤشر | `list[0]` |
| **Infinite Loop** | A loop that never stops (often a bug). | حلقة لا نهائية | `while(true) ...` |
| **Nested Loop** | A loop inside another loop. | حلقة متداخلة | `for { for { ... } }` |
