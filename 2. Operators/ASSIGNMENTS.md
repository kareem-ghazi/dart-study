# Assignments: Operators

## Assignment 1: The Bill Splitter (Basic)
**Objective:**
Practice using arithmetic operators to calculate costs.
(التدرب على استخدام المعاملات الحسابية لحساب التكاليف.)

**Instructions:**
1.  Create a program that defines a total bill amount (e.g., `50.0`) and the number of people splitting it (e.g., `2`).
2.  Calculate the split amount per person using division.
3.  Calculate the remaining amount if it were to be split as integers (using integer division and modulo) just to see the difference.
4.  Print the results.
(قم بإنشاء برنامج يحدد إجمالي الفاتورة وعدد الأشخاص. احسب المبلغ لكل شخص. احسب الباقي إذا تم التقسيم كأعداد صحيحة.)

**Expected Output:**
```
Total: 50.0
Split: 25.0
Integer Split: 25
Remainder: 0
```

---

## Assignment 2: Access Control (Intermediate)
**Objective:**
Use logical (`&&`, `||`, `!`) and relational (`>`, `==`) operators.
(استخدام المعاملات المنطقية والعلاقية.)

**Instructions:**
1.  Define three variables: `age` (int), `hasId` (bool), and `isBanned` (bool).
2.  Write a boolean expression checking if a person can enter a club.
3.  Rules: They must be 18 or older AND have an ID, AND they must NOT be banned.
4.  Store the result in a variable `canEnter` and print it.
(عرف متغيرات للعمر، وجود الهوية، والحظر. اكتب تعبيراً منطقياً للتحقق مما إذا كان الشخص يمكنه الدخول: يجب أن يكون 18 أو أكبر، لديه هوية، وليس محظوراً.)

**Expected Output:**
```
Age: 20, Has ID: true, Banned: false
Can enter: true
```

---

## Assignment 3: Profile Settings (Advanced)
**Objective:**
Use conditional expressions (`? :`) and null-aware operators (`??`, `??=`).
(استخدام التعبيرات الشرطية ومعاملات null.)

**Instructions:**
1.  Define a nullable string variable `username` (set it to null initially).
2.  Define a variable `defaultName` as "Guest".
3.  Use the `??` operator to assign a final display name to a variable `displayName`.
4.  Use the `??=` operator to assign "User123" to `username` (simulating a user setting their name later).
5.  Use the ternary operator `? :` to print "Welcome back!" if `username` is now not null, or "Please log in" otherwise.
(عرف متغيراً للاسم (null). استخدم `??` لتعيين اسم عرض افتراضي. استخدم `??=` لتعيين قيمة للاسم. استخدم العامل الثلاثي لطباعة رسالة ترحيب.)

**Expected Output:**
```
Display Name: Guest
User updated name...
Welcome back!
```

---

## Assignment 4: Cascade Builder (Advanced)

**Objective:**
Use the Cascade Operator (`..`) to configure objects fluently.
*(الهدف: استخدام معامل التتابع `..` لتهيئة الكائنات بسلاسة.)*

**Instructions:**
1. Create a class `Request` with properties: `String url`, `String method`, `Map<String, String> headers`.
2. In `main`, instantiate `Request`.
3. Use the cascade operator `..` to set `url` to 'https://api.example.com', `method` to 'GET', and add a header 'Authorization' with value 'Bearer 123'.
4. Print the object's properties to verify.

**Expected Output:**
```
Request(url: https://api.example.com, method: GET, headers: {Authorization: Bearer 123})
```

---

## Assignment 5: Custom Encryption System (Expert)

**Objective:**
Use Bitwise XOR (`^`) and shifting (`<<`, `>>`) to create a symmetric encryption algorithm.
*(الهدف: استخدام XOR الثنائي (`^`) والإزاحة (`<<`، `>>`) لإنشاء خوارزمية تشفير متماثلة.)*

**Instructions:**
1.  Define an integer `key` (e.g., `12345`).
2.  Create a function `encrypt(String text, int key)`.
    *   Iterate through each character code unit.
    *   XOR the character code with the `key`.
    *   (Optional) Apply a bitwise shift for complexity.
    *   Return the list of encrypted integers.
3.  Create a function `decrypt(List<int> encrypted, int key)` that reverses the logic.
4.  In `main`, encrypt the string "Hello Dart" and then decrypt it back to verify.

**Expected Output:**
```
Original: Hello Dart
Encrypted: [7221, 10121, ...] (Example values)
Decrypted: Hello Dart
```

---

## Solutions

### Solution 1: The Bill Splitter

```dart
void main() {
  double totalBill = 50.0;
  int people = 2;

  double split = totalBill / people;
  int intSplit = totalBill.toInt() ~/ people;
  int remainder = totalBill.toInt() % people;

  print('Total: $totalBill');
  print('Split: $split');
  print('Integer Split: $intSplit');
  print('Remainder: $remainder');
}
```

### Solution 2: Access Control

```dart
void main() {
  int age = 20;
  bool hasId = true;
  bool isBanned = false;

  // Logic: (Age >= 18) AND (Has ID) AND (NOT Banned)
  bool canEnter = (age >= 18) && hasId && !isBanned;

  print('Age: $age, Has ID: $hasId, Banned: $isBanned');
  print('Can enter: $canEnter');
}
```

### Solution 3: Profile Settings

```dart
void main() {
  String? username;
  String defaultName = "Guest";

  // Use default if username is null
  String displayName = username ?? defaultName;
  print('Display Name: $displayName');

  // Update username only if it is null (it is)
  username ??= "User123";
  print('User updated name...');

  // Ternary check
  String message = (username != null) ? "Welcome back!" : "Please log in";
  print(message);
}
```

### Solution 4: Cascade Builder

```dart
class Request {
  String url = '';
  String method = '';
  Map<String, String> headers = {};
  
  @override
  String toString() => 'Request(url: $url, method: $method, headers: $headers)';
}

void main() {
  var req = Request()
    ..url = 'https://api.example.com'
    ..method = 'GET'
    ..headers['Authorization'] = 'Bearer 123';
    
  print(req);
}
```

### Solution 5: Custom Encryption System

```dart
List<int> encrypt(String text, int key) {
  List<int> encrypted = [];
  for (int charCode in text.codeUnits) {
    // XOR with key
    encrypted.add(charCode ^ key);
  }
  return encrypted;
}

String decrypt(List<int> encrypted, int key) {
  List<int> decryptedCodes = [];
  for (int code in encrypted) {
    // XOR again reverses the operation
    decryptedCodes.add(code ^ key);
  }
  return String.fromCharCodes(decryptedCodes);
}

void main() {
  int key = 987654321;
  String original = "Hello Dart";
  
  print('Original: $original');
  
  List<int> encryptedData = encrypt(original, key);
  print('Encrypted: $encryptedData');
  
  String decryptedText = decrypt(encryptedData, key);
  print('Decrypted: $decryptedText');
}
```
