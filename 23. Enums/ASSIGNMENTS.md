# Assignments: Enums

## Assignment 1: Simple Enum (Basic)
**Objective:** Declare and use a simple enum.
(تعريف واستخدام تعداد بسيط.)

**Instructions:**
1.  Create an enum `WeekDay` with values `monday`, `tuesday`, `wednesday`, `thursday`, `friday`, `saturday`, `sunday`.
2.  In `main`, create a variable `today` set to `WeekDay.friday`.
3.  Print "Today is: " followed by the enum value.

**Expected Output:**
```
Today is: WeekDay.friday
```

---

## Assignment 2: Switch on Enum (Intermediate)
**Objective:** Control flow based on enum values.
(التحكم في التدفق بناءً على قيم التعداد.)

**Instructions:**
1.  Use the `WeekDay` enum from Assignment 1.
2.  Create a function `getActivity(WeekDay day)`.
3.  Use a switch statement:
    *   Monday-Friday: return "Work".
    *   Saturday-Sunday: return "Relax".
4.  In `main`, print the activity for Monday and Sunday.

**Expected Output:**
```
Monday: Work
Sunday: Relax
```

---

## Assignment 3: Enhanced Enum (Advanced)
**Objective:** Add fields and constructors to an enum.
(إضافة حقول ومنشئات للتعداد.)

**Instructions:**
1.  Create an enum `SolarSystemBody`.
2.  Add a `final double mass` (relative to Earth).
3.  Add a `const` constructor to initialize mass.
4.  Define values: `mercury(0.055)`, `venus(0.815)`, `earth(1.0)`, `mars(0.107)`.
5.  In `main`, print "Mass of Mars relative to Earth: [mass]".

**Expected Output:**
```
Mass of Mars relative to Earth: 0.107
```

---

## Assignment 4: Methods in Enum (Advanced)
**Objective:** Add behavior to an enum.
(إضافة سلوك للتعداد.)

**Instructions:**
1.  Create an enum `TrafficLight` with values `red`, `yellow`, `green`.
2.  Add a method `next()` that returns the next light (Red -> Green -> Yellow -> Red).
    *   *Note: Standard sequence is usually Green->Yellow->Red->Green, but follow instructions or standard logic.* Let's do Red -> Green -> Yellow -> Red for simplicity or standard traffic flow (Red->Green).
    *   Let's stick to simple: Red -> Green -> Yellow -> Red.
3.  In `main`, start at Red and call `next()` 3 times, printing the light each time.

**Expected Output:**
```
Current: TrafficLight.red
Next: TrafficLight.green
Next: TrafficLight.yellow
Next: TrafficLight.red
```

---

## Assignment 5: Enum Implementing Interface (Expert)
**Objective:** Make an enum implement `Comparable`.
(جعل التعداد ينفذ واجهة `Comparable`.)

**Instructions:**
1.  Create an enum `Medal` implements `Comparable<Medal>`.
2.  Values: `gold(3)`, `silver(2)`, `bronze(1)`.
3.  Add `final int value` and const constructor.
4.  Override `compareTo` to compare based on `value`.
5.  In `main`, create a list `[bronze, gold, silver]`. Sort it and print.

**Expected Output:**
```
[Medal.bronze, Medal.silver, Medal.gold]
```

---

## Solutions

```dart
// Assignment 1 & 2
enum WeekDay { monday, tuesday, wednesday, thursday, friday, saturday, sunday }

String getActivity(WeekDay day) {
  switch (day) {
    case WeekDay.saturday:
    case WeekDay.sunday:
      return 'Relax';
    default:
      return 'Work';
  }
}

// Assignment 3: Enhanced Enum
enum SolarSystemBody {
  mercury(0.055),
  venus(0.815),
  earth(1.0),
  mars(0.107);

  final double mass;
  const SolarSystemBody(this.mass);
}

// Assignment 4: Methods in Enum
enum TrafficLight {
  red,
  yellow,
  green;

  TrafficLight next() {
    switch (this) {
      case TrafficLight.red:
        return TrafficLight.green;
      case TrafficLight.green:
        return TrafficLight.yellow;
      case TrafficLight.yellow:
        return TrafficLight.red;
    }
  }
}

// Assignment 5: Implementing Interface
enum Medal implements Comparable<Medal> {
  bronze(1),
  silver(2),
  gold(3);

  final int value;
  const Medal(this.value);

  @override
  int compareTo(Medal other) => value - other.value;
  
  @override
  String toString() => 'Medal.${name}';
}

void main() {
  print('--- Assignment 1 ---');
  var today = WeekDay.friday;
  print('Today is: $today');

  print('\n--- Assignment 2 ---');
  print('Monday: ${getActivity(WeekDay.monday)}');
  print('Sunday: ${getActivity(WeekDay.sunday)}');

  print('\n--- Assignment 3 ---');
  print('Mass of Mars relative to Earth: ${SolarSystemBody.mars.mass}');

  print('\n--- Assignment 4 ---');
  var light = TrafficLight.red;
  print('Current: $light');
  light = light.next();
  print('Next: $light');
  light = light.next();
  print('Next: $light');
  light = light.next();
  print('Next: $light');

  print('\n--- Assignment 5 ---');
  List<Medal> medals = [Medal.bronze, Medal.gold, Medal.silver];
  medals.sort();
  print(medals);
}
```