# Assignments: Dot Shorthands

## Assignment 1: Enum Shorthand (Basic)
**Objective:** Use shorthands in a switch statement.
(استخدام الاختصارات في جملة switch.)

**Instructions:**
1.  Create an enum `Light` { `red`, `green`, `yellow` }.
2.  Create a function `action(Light l)` returning a String.
3.  Use a switch expression with dot shorthands (`.red`, etc.) to return "Stop", "Go", "Caution".
4.  In `main`, call it with `.green`.

**Expected Output:**
```
Go
```

---

## Assignment 2: Constructor Shorthand (Intermediate)
**Objective:** Use `.new` and named constructors.
(استخدام `.new` والمنشئات المسماة.)

**Instructions:**
1.  Create a class `Vector` with `x, y`.
2.  Add a named constructor `Vector.zero() : x=0, y=0`.
3.  In `main`, declare explicitly: `Vector v1 = .new(1, 2)`.
4.  Declare explicitly: `Vector v2 = .zero()`.
5.  Print them.

**Expected Output:**
```
1, 2
0, 0
```

---

## Assignment 3: Static Methods (Intermediate)
**Objective:** Call static methods using shorthand.
(استدعاء الدوال الساكنة باستخدام الاختصار.)

**Instructions:**
1.  In `main`, define a variable `double d`.
2.  Assign it using `.parse('3.14')`.
3.  Print it.

**Expected Output:**
```
3.14
```

---

## Assignment 4: List Initialization (Advanced)
**Objective:** Use shorthands in collection literals.
(استخدام الاختصارات في تجميعات البيانات.)

**Instructions:**
1.  Create a class `Item` with `id`.
2.  In `main`, create a `List<Item>` named `items`.
3.  Initialize it with 3 items using `.new(1)`, `.new(2)`, `.new(3)`.
4.  Print the length of the list.

**Expected Output:**
```
3
```

---

## Assignment 5: Equality Rules (Expert)
**Objective:** Correctly use shorthands in conditions.
(استخدام الاختصارات بشكل صحيح في الشروط.)

**Instructions:**
1.  Create an enum `Role` { `admin`, `user` }.
2.  Create a variable `Role r = .admin`.
3.  Write an `if` statement checking if `r` is `admin` using shorthand.
4.  Write another `if` checking if `r` is NOT `user` using shorthand.
5.  Print "Is Admin" if both pass.

**Expected Output:**
```
Is Admin
```

---

## Solutions

```dart
// Assignment 1: Enum Shorthand
enum Light { red, green, yellow }

String action(Light l) {
  return switch (l) {
    .red => 'Stop',
    .green => 'Go',
    .yellow => 'Caution',
  };
}

// Assignment 2: Constructor Shorthand
class Vector {
  int x, y;
  Vector(this.x, this.y);
  Vector.zero() : x = 0, y = 0;
  
  @override
  String toString() => '$x, $y';
}

// Assignment 4: List Initialization
class Item {
  int id;
  Item(this.id);
}

// Assignment 5: Equality Rules
enum Role { admin, user }

void main() {
  print('--- Assignment 1 ---');
  print(action(Light.green)); // Can pass .green if inferred, but here argument type inference applies

  print('\n--- Assignment 2 ---');
  Vector v1 = .new(1, 2);
  Vector v2 = .zero();
  print(v1);
  print(v2);

  print('\n--- Assignment 3 ---');
  double d = .parse('3.14');
  print(d);

  print('\n--- Assignment 4 ---');
  List<Item> items = [.new(1), .new(2), .new(3)];
  print(items.length);

  print('\n--- Assignment 5 ---');
  Role r = .admin;
  if (r == .admin) {
    if (r != .user) {
      print('Is Admin');
    }
  }
}
```
