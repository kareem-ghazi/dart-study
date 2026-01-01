# Assignments: Methods

## Assignment 1: Instance Methods (Basic)
**Objective:** Create methods to manipulate object state.
(إنشاء دوال للتلاعب بحالة الكائن.)

**Instructions:**
1.  Create a class `BankAccount`.
2.  Add a property `balance` (double).
3.  Add a method `deposit(double amount)` that increases balance.
4.  Add a method `withdraw(double amount)` that decreases balance if sufficient funds exist, otherwise print "Insufficient funds".
5.  In `main`, test both methods.

**Expected Output:**
```
Deposited: 100.0, New Balance: 100.0
Insufficient funds
Withdrawn: 50.0, New Balance: 50.0
```

---

## Assignment 2: Getters and Setters (Intermediate)
**Objective:** Use getters and setters for computed properties.
(استخدام الجوالب والضوابط للخصائص المحسوبة.)

**Instructions:**
1.  Create a class `Temperature`.
2.  Add a private property `_celsius` (double).
3.  Add a getter `fahrenheit` that converts celsius to fahrenheit (`(c * 9/5) + 32`).
4.  Add a setter `fahrenheit` that converts fahrenheit to celsius and updates `_celsius`.
5.  In `main`, set temp in F and read it in C.

**Expected Output:**
```
Set F to 212.0
Celsius: 100.0
```

---

## Assignment 3: Operator Overloading (Advanced)
**Objective:** Define custom behavior for standard operators.
(تعريف سلوك مخصص للمعاملات القياسية.)

**Instructions:**
1.  Create a class `ComplexNumber` with `real` and `imag` (double).
2.  Overload the `+` operator to add two complex numbers (`(a+bi) + (c+di) = (a+c) + (b+d)i`).
3.  Overload `toString()` to print in "a + bi" format.
4.  In `main`, add two complex numbers and print the result.

**Expected Output:**
```
Result: 5.0 + 7.0i
```

---

## Assignment 4: Abstract Methods (Advanced)
**Objective:** Use abstract methods to enforce a contract.
(استخدام الدوال المجردة لفرض عقد.)

**Instructions:**
1.  Create an abstract class `Employee`.
2.  Add an abstract method `calculateSalary()`.
3.  Create a subclass `FullTime` with a fixed salary.
4.  Create a subclass `PartTime` with hourly rate and hours worked.
5.  Implement `calculateSalary` in both.
6.  In `main`, create a list of employees and print their salaries.

**Expected Output:**
```
FullTime Salary: 5000.0
PartTime Salary: 1000.0
```

---

## Assignment 5: Smart Cart Item (Expert)
**Objective:** Combine encapsulation, getters/setters, and logic.
(دمج التغليف، الجوالب/الضوابط، والمنطق.)

**Instructions:**
1.  Create a class `CartItem`.
2.  Properties: `name`, `price`, and `_quantity`.
3.  Create a getter for `quantity`.
4.  Create a setter for `quantity` that prevents negative values (sets to 0 if negative).
5.  Create a getter `totalPrice` (`price * quantity`).
6.  In `main`, try setting negative quantity, then valid quantity, and print total.

**Expected Output:**
```
Tried setting -5. Quantity is now: 0
Total: 0.0
Set quantity to 3. Total: 30.0
```

---

## Solutions

```dart
// Assignment 1: Instance Methods
class BankAccount {
  double balance = 0;

  void deposit(double amount) {
    balance += amount;
    print('Deposited: $amount, New Balance: $balance');
  }

  void withdraw(double amount) {
    if (balance >= amount) {
      balance -= amount;
      print('Withdrawn: $amount, New Balance: $balance');
    } else {
      print('Insufficient funds');
    }
  }
}

// Assignment 2: Getters and Setters
class Temperature {
  double _celsius = 0;

  double get celsius => _celsius;

  set fahrenheit(double f) {
    _celsius = (f - 32) * 5 / 9;
  }

  double get fahrenheit => (_celsius * 9 / 5) + 32;
}

// Assignment 3: Operator Overloading
class ComplexNumber {
  final double real;
  final double imag;

  ComplexNumber(this.real, this.imag);

  ComplexNumber operator +(ComplexNumber other) {
    return ComplexNumber(real + other.real, imag + other.imag);
  }

  @override
  String toString() => '$real + ${imag}i';
}

// Assignment 4: Abstract Methods
abstract class Employee {
  double calculateSalary();
}

class FullTime extends Employee {
  double salary;
  FullTime(this.salary);

  @override
  double calculateSalary() => salary;
}

class PartTime extends Employee {
  double hourlyRate;
  int hours;
  PartTime(this.hourlyRate, this.hours);

  @override
  double calculateSalary() => hourlyRate * hours;
}

// Assignment 5: Smart Cart Item
class CartItem {
  String name;
  double price;
  int _quantity = 1;

  CartItem(this.name, this.price);

  int get quantity => _quantity;

  set quantity(int val) {
    if (val < 0) {
      _quantity = 0;
    } else {
      _quantity = val;
    }
  }

  double get totalPrice => price * _quantity;
}

void main() {
  print('--- Assignment 1 ---');
  var acc = BankAccount();
  acc.deposit(100);
  acc.withdraw(150);
  acc.withdraw(50);

  print('\n--- Assignment 2 ---');
  var t = Temperature();
  t.fahrenheit = 212;
  print('Set F to 212.0');
  print('Celsius: ${t.celsius}');

  print('\n--- Assignment 3 ---');
  var c1 = ComplexNumber(2, 3);
  var c2 = ComplexNumber(3, 4);
  print('Result: ${c1 + c2}');

  print('\n--- Assignment 4 ---');
  List<Employee> emps = [FullTime(5000), PartTime(20, 50)];
  print('FullTime Salary: ${emps[0].calculateSalary()}');
  print('PartTime Salary: ${emps[1].calculateSalary()}');

  print('\n--- Assignment 5 ---');
  var item = CartItem('Apple', 10);
  item.quantity = -5;
  print('Tried setting -5. Quantity is now: ${item.quantity}');
  print('Total: ${item.totalPrice}');
  item.quantity = 3;
  print('Set quantity to 3. Total: ${item.totalPrice}');
}
