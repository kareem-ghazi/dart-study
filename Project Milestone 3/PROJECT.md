# Project Milestone 3: Smart Home Automation System 🏠

**Goal:** Build a robust, object-oriented system to simulate a Smart Home environment. This project integrates advanced Dart concepts including **Classes, Inheritance, Mixins, Extension Types, and Callable Objects**.

---

## 🎯 Objectives
You will create a system where a central **Hub** manages various **Smart Devices**. You must use specific Dart features to ensure type safety, reusability, and clean syntax.

### Included Topics:
*   **OOP:** Classes (18), Constructors (19), Methods (20), Inheritance (21).
*   **Advanced OOP:** Mixins (22), Enums (23), Extension Methods (25).
*   **Modern Dart:** Records (5), Patterns (10), Dot Shorthands (24).
*   **Type Safety:** Extension Types (26), Generics (7), Error Handling (14).
*   **Functional-Like:** Callable Objects (27), Typedefs (8).

---

## 📝 Requirements

### 1. Enums & Extension Types
*   Create an enum `DeviceStatus` with values: `active`, `idle`, `offline`, `error`.
*   Create an **Extension Type** `Watts(double value)` to safely represent power usage. It should implement `double` (transparent) or simply wrap it to prevent mixing with other units (e.g., Volts).

### 2. Mixins for Capabilities
*   Create a mixin `BatteryOperated`.
    *   Field: `int batteryLevel` (0-100).
    *   Method: `charge()` that sets level to 100.
*   Create a mixin `Networked`.
    *   Field: `String? ipAddress`.
    *   Method: `connect(String ip)` to set the address.

### 3. Base Class & Inheritance
*   Create an `abstract class SmartDevice`.
    *   Properties: `String id`, `DeviceStatus status`.
    *   Abstract Method: `operate()` which returns a `Record` of `(bool success, String message)`.
    *   Constructor: Standard constructor initializing `id` and setting status to `idle`.

### 4. Concrete Classes
*   **`SmartLight`**: Extends `SmartDevice` and uses `Networked`.
    *   Field: `double brightness` (0.0 to 1.0).
    *   Constructor: Named constructor `SmartLight.dimmable(String id)` starting at 0.5 brightness.
*   **`SecurityCamera`**: Extends `SmartDevice` and uses `BatteryOperated`, `Networked`.
    *   Field: `bool isRecording`.
    *   Method: `toggleRecording()`.

### 5. Extension Methods
*   Create an extension on `SmartDevice` called `StatusChecker`.
*   Add a getter `isCritical` that returns `true` if status is `offline` or `error`.

### 6. Callable Object (The Automation)
*   Create a class `AutomationRoutine`.
*   Field: `String name`.
*   It should be a **Callable Object** (`call` method) that takes a `SmartDevice` and executes a specific action (e.g., turning lights on or checking camera battery).

### 7. The Hub (Generics & Collections)
*   Create a class `DeviceHub<T extends SmartDevice>`.
*   Field: `List<T> devices`.
*   Method: `addDevice(T device)`.
*   Method: `runDiagnostics()`:
    *   Iterate through devices.
    *   Use **Switch Expressions** with **Dot Shorthands** on `status` to print a summary.
    *   Use **Pattern Matching** to destructure the result of `operate()`.

---

## 🧪 Example Scenario (main.dart)
1.  Initialize a `DeviceHub`.
2.  Create a `SmartLight` using a named constructor.
3.  Create a `SecurityCamera`.
4.  Connect devices to network (Mixin method).
5.  Create an `AutomationRoutine` named "Morning Protocol" that sets lights to full brightness.
6.  Call the routine on the light: `morningRoutine(livingRoomLight)`.
7.  Add devices to Hub and run diagnostics.

---

## 🏆 Success Criteria
*   Code compiles without errors.
*   All specified features (Mixins, Extension Types, Callables, etc.) are used correctly.
*   Output demonstrates the hierarchy and logic flow.
