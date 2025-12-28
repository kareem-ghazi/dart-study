# Assignments: Introduction to Dart

## Assignment 1: Spacecraft Inventory (Basic)

**Objective:**
Practice defining variables, printing to the console, and creating a simple class.
*(الهدف: التدرب على تعريف المتغيرات، الطباعة على الشاشة، وإنشاء فئة بسيطة.)*

**Instructions:**
1. Create a class named `Spacecraft`.
2. Define two properties: `name` (String) and `launchYear` (int).
3. Create a constructor to initialize these properties.
4. In the `main` function, create an instance of `Spacecraft` (e.g., "Voyager I", 1977).
5. Print a message referencing the object's properties: "The spacecraft [name] was launched in [year]."

**Expected Output:**
```
The spacecraft Voyager I was launched in 1977.
```

---

## Assignment 2: Planet Classifier (Intermediate)

**Objective:**
Practice using Enums, Functions, and Control Flow (Switch/If-Else).
*(الهدف: التدرب على استخدام Enums، الدوال، والتحكم في سير البرنامج.)*

**Instructions:**
1. Define an enum named `PlanetType` with values: `terrestrial`, `gas`, `ice`.
2. Create a function named `classifyPlanet` that takes a `PlanetType` as an argument.
3. Inside the function, use a `switch` statement to print a description:
   - `terrestrial`: "Solid surface, rocky."
   - `gas`: "Gas giant, no solid surface."
   - `ice`: "Ice giant, very cold."
4. In `main`, call the function with different planet types.

**Expected Output:**
```
Solid surface, rocky.
Gas giant, no solid surface.
```

---

## Assignment 3: Mission Control (Advanced)

**Objective:**
Practice Collections (List/Map), Async/Await, and Exception Handling.
*(الهدف: التدرب على المجموعات، البرمجة غير المتزامنة، ومعالجة الاستثناءات.)*

**Instructions:**
1. Create a function `startCountdown(int seconds)` that is `async`.
2. Inside the function, use a loop to count down from `seconds` to 1.
3. Use `await Future.delayed` to wait 1 second between each number.
4. If `seconds` is greater than 5, throw an exception: "Countdown too long!".
5. In `main`, call `startCountdown` inside a `try-catch` block.
6. Test it with a valid number (3) and an invalid number (10).

**Expected Output (Example for 3 seconds):**
```
3...
2...
1...
Liftoff!
```

---

## Assignment 4: Recursive Factorial (Advanced)

**Objective:**
Understand functions, recursion, and stack depth.
*(الهدف: فهم الدوال، العودية، وعمق المكدس.)*

**Instructions:**
1. Create a function `factorial(int n)` that returns an `int`.
2. If `n` is 0 or 1, return 1 (Base case).
3. Otherwise, return `n * factorial(n - 1)`.
4. In `main`, calculate and print the factorial of 5.
5. **Bonus:** Add a check to throw an exception if `n` is negative.

**Expected Output:**
```
Factorial of 5 is 120
```

---

## Assignment 5: Solar System Simulation (Expert)

**Objective:**
Create a complex scenario combining classes, loops, state, and user interaction logic (simulated).
*(الهدف: إنشاء سيناريو معقد يجمع بين الفئات، الحلقات، الحالة، ومنطق تفاعل المستخدم (محاكى).)*

**Instructions:**
1.  Create a class `Planet` with `name`, `distanceFromSun` (AU), and `isHabitable`.
2.  Create a class `SolarSystem` that holds a list of planets.
3.  Add a method `addPlanet` to the system.
4.  Add a method `findHabitable()` that returns a list of habitable planets.
5.  In `main`, simulate a "scan":
    *   Create the system.
    *   Add Earth, Mars, Venus, and Jupiter with realistic properties.
    *   Print "Scanning system...".
    *   Find and print the names of all habitable planets found.
    *   **Challenge:** If no habitable planets are found, throw a custom exception `DoomException`.

**Expected Output:**
```
Scanning system...
Habitable planets found:
- Earth
- Mars
```

---

## Solutions

### Solution 1: Spacecraft Inventory

```dart
class Spacecraft {
  String name;
  int launchYear;

  Spacecraft(this.name, this.launchYear);
}

void main() {
  // Create an instance
  var voyager = Spacecraft('Voyager I', 1977);

  // Print details using string interpolation
  print('The spacecraft ${voyager.name} was launched in ${voyager.launchYear}.');
}
```

### Solution 2: Planet Classifier

```dart
enum PlanetType { terrestrial, gas, ice }

void classifyPlanet(PlanetType type) {
  switch (type) {
    case PlanetType.terrestrial:
      print('Solid surface, rocky.');
      break;
    case PlanetType.gas:
      print('Gas giant, no solid surface.');
      break;
    case PlanetType.ice:
      print('Ice giant, very cold.');
      break;
  }
}

void main() {
  classifyPlanet(PlanetType.terrestrial);
  classifyPlanet(PlanetType.gas);
}
```

### Solution 3: Mission Control

```dart
import 'dart:async';

Future<void> startCountdown(int seconds) async {
  if (seconds > 5) {
    throw Exception('Countdown too long!');
  }

  for (int i = seconds; i > 0; i--) {
    print('$i...');
    await Future.delayed(Duration(seconds: 1));
  }
  print('Liftoff!');
}

void main() async {
  // Test Case 1: Valid countdown
  try {
    print('--- Mission 1 ---');
    await startCountdown(3);
  } catch (e) {
    print('Error: $e');
  }

  // Test Case 2: Invalid countdown
  try {
    print('\n--- Mission 2 ---');
    await startCountdown(10);
  } catch (e) {
    print('Error: $e');
  }
}
```

### Solution 4: Recursive Factorial

```dart
int factorial(int n) {
  if (n < 0) throw Exception('Negative numbers not allowed');
  if (n <= 1) return 1;
  return n * factorial(n - 1);
}

void main() {
  try {
    int n = 5;
    print('Factorial of $n is ${factorial(n)}');
  } catch (e) {
    print(e);
  }
}
```

### Solution 5: Solar System Simulation

```dart
class DoomException implements Exception {
  String toString() => "DoomException: No hope for humanity.";
}

class Planet {
  String name;
  double distanceFromSun;
  bool isHabitable;

  Planet(this.name, this.distanceFromSun, this.isHabitable);
}

class SolarSystem {
  List<Planet> planets = [];

  void addPlanet(Planet p) {
    planets.add(p);
  }

  List<Planet> findHabitable() {
    // filtering the list
    return planets.where((p) => p.isHabitable).toList();
  }
}

void main() {
  var system = SolarSystem();
  
  // Adding planets (approximate data)
  system.addPlanet(Planet('Mercury', 0.4, false));
  system.addPlanet(Planet('Venus', 0.7, false));
  system.addPlanet(Planet('Earth', 1.0, true));
  system.addPlanet(Planet('Mars', 1.5, true)); // Optimistic!
  system.addPlanet(Planet('Jupiter', 5.2, false));

  print('Scanning system...');
  
  try {
    var habitable = system.findHabitable();
    if (habitable.isEmpty) {
      throw DoomException();
    }
    
    print('Habitable planets found:');
    for (var p in habitable) {
      print('- ${p.name}');
    }
  } catch (e) {
    print(e);
  }
}
```