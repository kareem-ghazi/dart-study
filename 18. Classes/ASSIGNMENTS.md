# Assignments: Classes

## Assignment 1: The Person Class (Basic)
**Objective:** Create a simple class with properties and a method.
(إنشاء فئة بسيطة مع خصائص ودالة.)

**Instructions:**
1.  Create a class named `Person`.
2.  Add two properties: `name` (String) and `age` (int).
3.  Create a constructor to initialize these properties.
4.  Add a method `introduce()` that prints "Hi, my name is [name] and I am [age] years old.".
5.  In `main`, create a `Person` object and call `introduce()`.

**Expected Output:**
```
Hi, my name is Ali and I am 25 years old.
```

---

## Assignment 2: Named Constructors (Intermediate)
**Objective:** Learn to use named constructors for specific initialization logic.
(تعلم استخدام المنشئات المسماة لمنطق تهيئة محدد.)

**Instructions:**
1.  Create a class `Rectangle`.
2.  Add properties `width` and `height` (double).
3.  Create a standard constructor `Rectangle(this.width, this.height)`.
4.  Create a named constructor `Rectangle.square(double side)` that sets both width and height to `side`.
5.  Add a method `area()` that returns the area.
6.  In `main`, create a rectangle and a square (using the named constructor) and print their areas.

**Expected Output:**
```
Rectangle Area: 50.0
Square Area: 16.0
```

---

## Assignment 3: Implicit Interfaces (Advanced)
**Objective:** Use a class as an interface.
(استخدام الفئة كواجهة.)

**Instructions:**
1.  Create a class `Shape` with a method `area()` that returns 0.
2.  Create a class `Circle` that `implements` `Shape`.
3.  Add a `radius` property to `Circle` and implement `area()` to return `3.14 * radius * radius`.
4.  Create a class `Square` that `implements` `Shape`.
5.  Add a `side` property to `Square` and implement `area()`.
6.  In `main`, create a list of `Shape` containing a circle and a square, loop through it, and print areas.

**Expected Output:**
```
Area: 78.5
Area: 100.0
```

---

## Assignment 4: Static Members (Advanced)
**Objective:** Understand static variables and methods.
(فهم المتغيرات والدوال الساكنة.)

**Instructions:**
1.  Create a class `Calculator`.
2.  Add a static constant `pi = 3.14159`.
3.  Add a static method `circleArea(double radius)` that uses `Calculator.pi` to calculate the area.
4.  In `main`, call `Calculator.circleArea(10)` without creating an instance of Calculator.

**Expected Output:**
```
Area of circle: 314.159
```

---

## Assignment 5: Smart Home System (Expert)
**Objective:** Combine const constructors, final fields, and encapsulation.
(دمج المنشئات الثابتة، الحقول النهائية، والتغليف.)

**Instructions:**
1.  Create a class `SmartDevice`.
2.  Add a `final String id` and `final String type`.
3.  Create a `const` constructor.
4.  Create a class `HomeHub`.
5.  Add a list of `SmartDevice`.
6.  In `main`, create two devices using `const` (e.g., "Light1", "Bulb"). Check if two identical const devices are the same instance using `identical()`.
7.  Add them to the hub and print the count.

**Expected Output:**
```
Are identical: true
Devices in hub: 2
```

---

## Solutions

```dart
// Assignment 1: The Person Class
class Person {
  String name;
  int age;

  Person(this.name, this.age);

  void introduce() {
    print('Hi, my name is $name and I am $age years old.');
  }
}

// Assignment 2: Named Constructors
class Rectangle {
  double width;
  double height;

  Rectangle(this.width, this.height);

  // Named constructor for a square
  Rectangle.square(double side) : width = side, height = side;

  double area() => width * height;
}

// Assignment 3: Implicit Interfaces
class Shape {
  double area() => 0;
}

class Circle implements Shape {
  double radius;
  Circle(this.radius);

  @override
  double area() => 3.14 * radius * radius;
}

class Square implements Shape {
  double side;
  Square(this.side);

  @override
  double area() => side * side;
}

// Assignment 4: Static Members
class Calculator {
  static const double pi = 3.14159;

  static double circleArea(double radius) {
    return pi * radius * radius;
  }
}

// Assignment 5: Smart Home System
class SmartDevice {
  final String id;
  final String type;

  const SmartDevice(this.id, this.type);
}

class HomeHub {
  List<SmartDevice> devices = [];

  void addDevice(SmartDevice device) {
    devices.add(device);
  }
}

void main() {
  print('--- Assignment 1 ---');
  var p = Person('Ali', 25);
  p.introduce();

  print('\n--- Assignment 2 ---');
  var rect = Rectangle(10, 5);
  var sq = Rectangle.square(4);
  print('Rectangle Area: ${rect.area()}');
  print('Square Area: ${sq.area()}');

  print('\n--- Assignment 3 ---');
  List<Shape> shapes = [Circle(5), Square(10)];
  for (var s in shapes) {
    print('Area: ${s.area()}');
  }

  print('\n--- Assignment 4 ---');
  print('Area of circle: ${Calculator.circleArea(10)}');

  print('\n--- Assignment 5 ---');
  var d1 = const SmartDevice('L1', 'Light');
  var d2 = const SmartDevice('L1', 'Light');
  print('Are identical: ${identical(d1, d2)}');
  
  var hub = HomeHub();
  hub.addDevice(d1);
  hub.addDevice(d2); // Adding same instance logic-wise
  print('Devices in hub: ${hub.devices.length}');
}
```