# Assignments: Constructors

## Assignment 1: Initializer List Basics (Basic)
**Objective:** Use an initializer list to calculate a property value.
(استخدام قائمة التهيئة لحساب قيمة خاصية.)

**Instructions:**
1.  Create a class `Triangle`.
2.  Add properties `base`, `height` (double) and a `final double area`.
3.  Create a constructor that takes `base` and `height`.
4.  In the initializer list, calculate `area` (`0.5 * base * height`).
5.  In `main`, create a triangle and print its area.

**Expected Output:**
```
Triangle Area: 25.0
```

---

## Assignment 2: Assertions in Constructors (Intermediate)
**Objective:** Use asserts to validate input data.
(استخدام التوكيدات (asserts) للتحقق من صحة البيانات المدخلة.)

**Instructions:**
1.  Create a class `User`.
2.  Add a property `age` (int).
3.  Create a constructor `User(this.age)`.
4.  Add an assertion in the initializer list to ensure `age` is 18 or older (`age >= 18`).
5.  In `main`, try to create a user with age 20 (success) and age 15 (should fail if checked mode is on, but just write the code). Print "Success" if valid.

**Expected Output:**
```
User created with age: 20
```

---

## Assignment 3: Superclass Constructors (Advanced)
**Objective:** Manually call a named superclass constructor.
(استدعاء منشئ مسمى للفئة الأب يدوياً.)

**Instructions:**
1.  Create a class `Appliance` with a constructor `Appliance.named(String name)`. It should print "Appliance: $name".
2.  Create a subclass `Toaster`.
3.  Create a constructor `Toaster(int slots)` that calls `super.named("Toaster")`.
4.  In `main`, create a `Toaster`.

**Expected Output:**
```
Appliance: Toaster
Toaster created with 2 slots
```

---

## Assignment 4: Super Parameters (Advanced)
**Objective:** Use the `super.` shorthand syntax.
(استخدام اختصار `super.`.)

**Instructions:**
1.  Create a class `Vehicle` with properties `make` and `model`.
2.  Create a standard constructor for `Vehicle`.
3.  Create a subclass `Car` with an extra property `doors` (int).
4.  Create a constructor for `Car` using `super.make` and `super.model`.
5.  In `main`, create a `Car` and print all details.

**Expected Output:**
```
Car: Toyota Camry, Doors: 4
```

---

## Assignment 5: Redirecting Constructors (Expert)
**Objective:** Redirect one constructor to another within the same class.
(إعادة توجيه منشئ إلى آخر داخل نفس الفئة.)

**Instructions:**
1.  Create a class `Color`.
2.  Add properties `red`, `green`, `blue` (int).
3.  Create a main constructor `Color(this.red, this.green, this.blue)`.
4.  Create a named constructor `Color.black()` that redirects to the main constructor with values (0, 0, 0).
5.  Create a named constructor `Color.white()` that redirects to the main constructor with values (255, 255, 255).
6.  In `main`, create black and white colors and print their values.

**Expected Output:**
```
Black: 0, 0, 0
White: 255, 255, 255
```

---

## Solutions

```dart
// Assignment 1: Initializer List Basics
class Triangle {
  double base;
  double height;
  final double area;

  Triangle(this.base, this.height) : area = 0.5 * base * height;
}

// Assignment 2: Assertions
class User {
  int age;

  User(this.age) : assert(age >= 18, 'User must be 18 or older');
}

// Assignment 3: Superclass Constructors
class Appliance {
  Appliance.named(String name) {
    print('Appliance: $name');
  }
}

class Toaster extends Appliance {
  int slots;

  Toaster(this.slots) : super.named('Toaster') {
    print('Toaster created with $slots slots');
  }
}

// Assignment 4: Super Parameters
class Vehicle {
  String make;
  String model;

  Vehicle(this.make, this.model);
}

class Car extends Vehicle {
  int doors;

  Car(super.make, super.model, this.doors);

  void display() {
    print('Car: $make $model, Doors: $doors');
  }
}

// Assignment 5: Redirecting Constructors
class Color {
  int red, green, blue;

  Color(this.red, this.green, this.blue);

  Color.black() : this(0, 0, 0);
  
  Color.white() : this(255, 255, 255);

  @override
  String toString() => '$red, $green, $blue';
}

void main() {
  print('--- Assignment 1 ---');
  var t = Triangle(10, 5);
  print('Triangle Area: ${t.area}');

  print('\n--- Assignment 2 ---');
  try {
    var u = User(20);
    print('User created with age: ${u.age}');
  } catch (e) {
    print(e);
  }

  print('\n--- Assignment 3 ---');
  Toaster(2);

  print('\n--- Assignment 4 ---');
  var c = Car('Toyota', 'Camry', 4);
  c.display();

  print('\n--- Assignment 5 ---');
  var black = Color.black();
  var white = Color.white();
  print('Black: $black');
  print('White: $white');
}
