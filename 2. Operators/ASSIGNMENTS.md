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

## Assignment 5: Bitwise Permissions (Advanced)

**Objective:**
Use Bitwise operators (`|`, `&`, `<<`) to manage permission flags.
*(الهدف: استخدام المعاملات الثنائية `|`، `&`، `<<` لإدارة أعلام الصلاحيات.)*

**Instructions:**
1. Define constants for permissions using bit shifts: `READ = 1` (001), `WRITE = 2` (010), `EXECUTE = 4` (100).
2. Create a variable `userPerms` and assign it `READ | WRITE` (Binary 011 = 3).
3. Check if `userPerms` has `WRITE` permission using `&` (i.e., `(userPerms & WRITE) != 0`).
4. Toggle `WRITE` permission off using XOR `^` or complex logic, then check again. (Simplest: just check the first part).
5. Print "Has Write: true" or false.

**Expected Output:**
```
User Permissions: 3
Has Write Access: true
Has Execute Access: false
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

### Solution 5: Bitwise Permissions

```dart
void main() {
  const int READ = 1;      // 001
  const int WRITE = 2;     // 010
  const int EXECUTE = 4;   // 100
  
  // Grant READ and WRITE
  int userPerms = READ | WRITE; // 011 = 3
  
  print('User Permissions: $userPerms');
  
  bool hasWrite = (userPerms & WRITE) == WRITE; // or != 0
  print('Has Write Access: $hasWrite');
  
  bool hasExecute = (userPerms & EXECUTE) == EXECUTE;
  print('Has Execute Access: $hasExecute');
}
```
