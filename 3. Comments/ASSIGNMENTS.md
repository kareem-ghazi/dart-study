# Assignments: Comments

## Assignment 1: The Explainer (Basic)
**Objective:**
Practice writing single-line comments to explain code logic.
(التدرب على كتابة تعليقات السطر الواحد لشرح منطق الكود.)

**Instructions:**
1.  Copy the code block below.
2.  Add `//` comments to explain what each line does.
3.  Add a `// TODO:` comment noting that the tax rate should be moved to a constant variable later.
(انسخ الكود أدناه. أضف تعليقات `//` لشرح كل سطر. أضف تعليق `// TODO:` يشير إلى أن معدل الضريبة يجب نقله إلى متغير ثابت لاحقاً.)

**Code to comment:**
```dart
void main() {
  double price = 100.0;
  double tax = price * 0.15;
  print(price + tax);
}
```

**Expected Output:**
(No change in program output, just the code file with comments).

---

## Assignment 2: The Debugger (Intermediate)
**Objective:**
Use multi-line comments `/* ... */` to temporarily disable a block of buggy code.
(استخدام التعليقات متعددة الأسطر لتعطيل كتلة من الكود المليء بالأخطاء مؤقتاً.)

**Instructions:**
1.  You have a function with some unfinished, crashing code in the middle.
2.  Wrap the "crashy" part in `/* ... */` so the program runs the good parts only.
3.  Ensure the "Start" and "End" messages still print.
(لديك دالة تحتوي على كود غير مكتمل ويسبب أعطالاً. قم بإحاطة الجزء "المعطل" بـ `/* ... */` ليعمل البرنامج. تأكد من طباعة رسالتي البداية والنهاية.)

**Code:**
```dart
void main() {
  print("Start");
  
  String x = null; // Error
  print(x.length); // Crash
  
  print("End");
}
```

**Expected Output:**
```
Start
End
```

---

## Assignment 3: The API Writer (Advanced)
**Objective:**
Write professional `///` documentation comments with references.
(كتابة تعليقات توثيق احترافية `///` مع مراجع.)

**Instructions:**
1.  Create a class `Calculator`.
2.  Add a method `add(int a, int b)`.
3.  Write documentation for the class explaining it is a "Simple math utility".
4.  Write documentation for the `add` method.
5.  Use square brackets `[...]` to refer to parameters `a` and `b` in the description.
(أنشئ فئة `Calculator`. أضف دالة `add`. اكتب توثيقاً للفئة والدالة. استخدم الأقواس المربعة للإشارة إلى المعاملات.)

**Expected Output:**
(Code compiles, doc comments are present).

---

## Assignment 4: Lint Suppression (Advanced)

**Objective:**
Use comments to interact with the analysis server (`ignore` rules).
*(الهدف: استخدام التعليقات للتفاعل مع خادم التحليل (تجاهل القواعد).)*

**Instructions:**
1. Define a local string variable `unusedVariable` inside `main` but do NOT use it.
2. Normally, Dart's linter warns about "Unused local variable".
3. Add a specific comment `// ignore: unused_local_variable` on the line above it to silence the warning.
4. Add another variable and use `// ignore_for_file: unused_local_variable` at the very top of the file to silence it for the whole file.

**Expected Output:**
(No output, but the analysis warning should disappear in your IDE).

---

## Assignment 5: Documentation Generator (Expert)

**Objective:**
Write a program that parses Dart code (as a string) and extracts documentation comments.
*(الهدف: كتابة برنامج يحلل كود Dart (كسلسلة نصية) ويستخرج تعليقات التوثيق.)*

**Instructions:**
1.  Define a multi-line string variable `sourceCode` containing a simulated class with `///` comments.
2.  Write a function `extractDocs(String code)` that:
    *   Splits the code into lines.
    *   Iterates through lines to find those starting with `///`.
    *   Cleans up the `///` and whitespace.
    *   Groups consecutive comment lines into a single "block".
    *   Returns a `List<String>` where each string is a full documentation block.
3.  In `main`, call the function and print the extracted docs nicely.

**Expected Output:**
```
Found Documentation:
[1] Represents a user in the system.
[2] Logs the user out.
    Clears the session token.
```
---

## Solutions

### Solution 1: The Explainer

```dart
void main() {
  // Define the base price of the item
  double price = 100.0;
  
  // TODO: Refactor 0.15 into a const TAX_RATE variable
  // Calculate tax amount (15%)
  double tax = price * 0.15;
  
  // Print the total cost including tax
  print(price + tax);
}
```

### Solution 2: The Debugger

```dart
void main() {
  print("Start");
  
  /* 
  Temporarily disabled because x cannot be assigned null 
  without 'String?' type, and it crashes on access.
  
  String x = null; 
  print(x.length); 
  */
  
  print("End");
}
```

### Solution 3: The API Writer

```dart
/// A simple math utility class.
/// 
/// Use this to perform basic arithmetic operations.
class Calculator {
  
  /// Adds two integers [a] and [b] together.
  /// 
  /// Returns the sum of [a] and [b].
  int add(int a, int b) {
    return a + b;
  }
}

void main() {
  Calculator calc = Calculator();
  print(calc.add(5, 3));
}
```

### Solution 4: Lint Suppression

```dart
// ignore_for_file: unused_local_variable

void main() {
  // This warning is ignored for the specific line
  // ignore: unused_local_variable
  var ignoredVar = "I am ignored";
  
  // This warning is ignored because of the file-level comment
  var fileIgnoredVar = "Me too";
}
```

### Solution 5: Documentation Generator

```dart
List<String> extractDocs(String code) {
  List<String> docs = [];
  StringBuffer currentBlock = StringBuffer();
  
  List<String> lines = code.split('\n');
  
  for (String line in lines) {
    String trimmed = line.trim();
    if (trimmed.startsWith('///')) {
      // Remove '///' and leading space
      String content = trimmed.substring(3).trim();
      if (currentBlock.isNotEmpty) {
        currentBlock.write('\n');
      }
      currentBlock.write(content);
    } else {
      // If we were building a block and hit non-comment code, save it
      if (currentBlock.isNotEmpty) {
        docs.add(currentBlock.toString());
        currentBlock.clear();
      }
    }
  }
  // Flush remaining
  if (currentBlock.isNotEmpty) {
    docs.add(currentBlock.toString());
  }
  
  return docs;
}

void main() {
  String sourceCode = """
  /// Represents a user in the system.
  class User {
    String name;
    
    /// Logs the user out.
    /// Clears the session token.
    void logout() {}
  }
  """;

  var extracted = extractDocs(sourceCode);
  
  print("Found Documentation:");
  for (int i = 0; i < extracted.length; i++) {
    print("[${i + 1}] ${extracted[i]}");
  }
}
```
