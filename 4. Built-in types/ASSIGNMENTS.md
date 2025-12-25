# Assignments: Built-in Types

## Assignment 1: The Simple Receipt (Basic)

**Objective:**
Practice declaring `int`, `double`, and `String` variables and using string interpolation.
(التدرب على تعريف متغيرات من نوع أعداد صحيحة وعشرية ونصوص، واستخدام دمج النصوص.)

**Instructions:**
1.  Create a `String` variable named `item` with the value `'Coffee'`.
2.  Create a `double` variable named `price` with the value `3.50`.
3.  Create an `int` variable named `quantity` with the value `2`.
4.  Calculate the `total` (price * quantity) and store it in a variable.
5.  Print a message in this format: "You bought 2 Coffee(s) for $7.0".

**Expected Output:**
```
You bought 2 Coffee(s) for $7.0
```

---

## Assignment 2: String Parsing & Formatting (Intermediate)

**Objective:**
Practice converting Strings to numbers and formatting numbers as Strings.
(التدرب على تحويل النصوص إلى أرقام وتنسيق الأرقام كنصوص.)

**Instructions:**
1.  Define a `String` variable `strPrice` with the value `'12.99'`.
2.  Define a `String` variable `strTax` with the value `'0.85'`.
3.  Parse both strings into `double` variables.
4.  Add them together to get the total cost.
5.  Convert the total cost back to a String, fixed to exactly 1 decimal place (use `toStringAsFixed`).
6.  Print the result.

**Expected Output:**
```
Total cost: 13.8
```

---

## Assignment 3: Emoji Encoder (Advanced)

**Objective:**
Work with `Runes` and Unicode characters to handle special symbols.
(العمل مع `Runes` ورموز Unicode للتعامل مع الرموز الخاصة.)

**Instructions:**
1.  Define a variable `heart` using the Unicode hex code `\u2665`.
2.  Define a variable `laugh` using the Unicode hex code `\u{1f606}`.
3.  Create a sentence string combining text and these emojis (e.g., "I [heart] Dart [laugh]").
4.  Print the sentence.
5.  **Challenge:** Print the number of UTF-16 code units in the sentence (using `.length`) vs the number of Runes (using `.runes.length`).

**Expected Output:**
```
I ♥ Dart 😆
Code units: 13
Runes: 12
```
*(Note: Output numbers may vary slightly depending on your exact sentence text)*

---

## Assignment 4: List Basics (List type)

**Objective:**
Practice basic List operations.
*(الهدف: التدرب على عمليات القائمة الأساسية.)*

**Instructions:**
1. Create a list of integers `numbers = [1, 2, 3]`.
2. Add the number 4 to the list.
3. Remove the number 2.
4. Print the final list.

**Expected Output:**
```
[1, 3, 4]
```

---

## Assignment 5: Boolean Logic (Bool type)

**Objective:**
Practice working with boolean values.
*(الهدف: التدرب على العمل مع القيم المنطقية.)*

**Instructions:**
1. Define `bool isRaining = true`.
2. Define `bool hasUmbrella = false`.
3. Create a variable `willGetWet` that is true if it is raining AND you do not have an umbrella.
4. Print "Will I get wet? [result]".

**Expected Output:**
```
Will I get wet? true
```

---

## Solutions

### Solution 1: The Simple Receipt
```dart
void main() {
  String item = 'Coffee';
  double price = 3.50;
  int quantity = 2;
  
  // Calculate total
  double total = price * quantity;
  
  // Use string interpolation $variable
  print('You bought $quantity $item(s) for \$$total');
  // Note: \$ is used to print the actual dollar sign
}
```

### Solution 2: String Parsing & Formatting
```dart
void main() {
  String strPrice = '12.99';
  String strTax = '0.85';
  
  // Parse strings to double
  double price = double.parse(strPrice);
  double tax = double.parse(strTax);
  
  double total = price + tax;
  
  // Format to 1 decimal place
  String formattedTotal = total.toStringAsFixed(1);
  
  print('Total cost: $formattedTotal');
}
```

### Solution 3: Emoji Encoder
```dart
void main() {
  var heart = '\u2665';
  var laugh = '\u{1f606}';
  
  String sentence = 'I $heart Dart $laugh';
  
  print(sentence);
  
  // .length counts UTF-16 code units
  print('Code units: ${sentence.length}');
  
  // .runes.length counts the actual Unicode points
  print('Runes: ${sentence.runes.length}');
}
```

### Solution 4: List Basics
```dart
void main() {
  List<int> numbers = [1, 2, 3];
  numbers.add(4);
  numbers.remove(2);
  print(numbers);
}
```

### Solution 5: Boolean Logic
```dart
void main() {
  bool isRaining = true;
  bool hasUmbrella = false;
  
  bool willGetWet = isRaining && !hasUmbrella;
  print('Will I get wet? $willGetWet');
}
```