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

## Assignment 4: BigInt Factorial (Advanced)

**Objective:**
Handle numbers larger than the standard 64-bit integer limit using `BigInt`.
*(الهدف: التعامل مع أرقام أكبر من حد العدد الصحيح القياسي 64-بت باستخدام `BigInt`.)*

**Instructions:**
1. Try to calculate the factorial of 25 using standard `int` (it will overflow or be incorrect/negative).
2. Change the implementation to use `BigInt`.
3. Define `BigInt n = BigInt.from(25)`.
4. Use a loop to multiply `result` (starting at `BigInt.one`) by numbers down to 1.
5. Print the result.

**Expected Output:**
```
Factorial of 25: 15511210043330985984000000
```

---

## Assignment 5: Numeric Polymorphism (Advanced)

**Objective:**
Understand the `num` type and how to handle `int` and `double` generically.
*(الهدف: فهم النوع `num` وكيفية التعامل مع `int` و `double` بشكل عام.)*

**Instructions:**
1. Create a list `List<num> numbers = [10, 3.14, 5, 2.5]`.
2. Iterate through the list.
3. For each number, check `is int` or `is double`.
4. If it's an integer, print "Integer: [value]".
5. If it's a double, print "Double: [value] (Rounded: [round()])".
6. Calculate the sum of all numbers.

**Expected Output:**
```
Integer: 10
Double: 3.14 (Rounded: 3)
Integer: 5
Double: 2.5 (Rounded: 3)
Sum: 20.64
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

### Solution 4: BigInt Factorial
```dart
void main() {
  BigInt n = BigInt.from(25);
  BigInt result = BigInt.one;
  
  for (BigInt i = n; i > BigInt.zero; i = i - BigInt.one) {
    result = result * i;
  }
  
  print('Factorial of 25: $result');
}
```

### Solution 5: Numeric Polymorphism
```dart
void main() {
  List<num> numbers = [10, 3.14, 5, 2.5];
  num sum = 0;
  
  for (var n in numbers) {
    sum += n;
    if (n is int) {
      print('Integer: $n');
    } else if (n is double) {
      print('Double: $n (Rounded: ${n.round()})');
    }
  }
  print('Sum: $sum');
}
```
