# Assignments: Records

## Assignment 1: User Profile (Basic)

**Objective:**
Learn how to create records with both positional and named fields and access their values.
**(تعلم كيفية إنشاء سجلات تحتوي على حقول معتمدة على الموقع وحقول مسماة والوصول إلى قيمها.)**

**Instructions:**
1.  Create a record named `userProfile` that stores the following:
    *   Positional field 1: First Name (String, e.g., "John")
    *   Positional field 2: Last Name (String, e.g., "Doe")
    *   Named field `age`: Age (int, e.g., 30)
    *   Named field `isAdmin`: Role status (bool, e.g., true)
2.  Print a formatted string using these values.
**(1. أنشئ سجلاً باسم `userProfile` يخزن البيانات التالية: الاسم الأول، اسم العائلة (كمواقع)، العمر، وهل هو مسؤول أم لا (كمسميات). 2. اطبع نصاً منسقاً باستخدام هذه القيم.)**

**Expected Output:**
```
User: John Doe
Age: 30
Admin: true
```

---

## Assignment 2: Coordinate Converter (Intermediate)

**Objective:**
Practice returning multiple values from a function using records and destructuring them.
**(ممارسة إرجاع قيم متعددة من دالة باستخدام السجلات وتفكيكها.)**

**Instructions:**
1.  Write a function called `getLatLong` that accepts a `String` city name.
2.  If the city is "Cairo", return a record `(lat: 30.0444, long: 31.2357)`.
3.  If the city is "London", return `(lat: 51.5074, long: -0.1278)`.
4.  For any other city, return `(lat: 0.0, long: 0.0)`.
5.  In the `main` function, call `getLatLong` for "Cairo" and destructure the result into variables `latitude` and `longitude`.
6.  Print the result.
**(1. اكتب دالة باسم `getLatLong` تقبل اسم مدينة. 2. إذا كانت "Cairo"، أرجع إحداثياتها. 3. إذا كانت "London"، أرجع إحداثياتها. 4. لأي مدينة أخرى، أرجع أصفاراً. 5. في الدالة الرئيسية، استدعِ الدالة لمدينة "Cairo" وقم بتفكيك النتيجة إلى متغيرات. 6. اطبع النتيجة.)**

**Expected Output:**
```
City: Cairo
Latitude: 30.0444
Longitude: 31.2357
```

---

## Assignment 3: Product Inventory Comparator (Advanced)

**Objective:**
Understand record equality and shape.
**(فهم مساواة السجلات وشكلها.)**

**Instructions:**
1.  Define two records, `warehouseItem` and `storeShelfItem`.
2.  Both should have the shape `({int id, String name, double price})`.
3.  Initialize `warehouseItem` with `id: 101, name: "Laptop", price: 999.99`.
4.  Initialize `storeShelfItem` with the exact same values but change the order of named fields (e.g., put price before name).
5.  Check if `warehouseItem` is equal to `storeShelfItem` and print the result.
6.  Create a third record `newItem` with a different shape (e.g., positional fields instead of named) but same values. Try to compare it with `warehouseItem` (Observe the result or error, but here just print "Not comparable" if types differ).
**(1. عرّف سجلين `warehouseItem` و `storeShelfItem` بنفس الشكل والقيم ولكن بترتيب مختلف للحقول المسماة. 2. تحقق مما إذا كانا متساويين واطبع النتيجة. 3. أنشئ سجلاً ثالثاً بشكل مختلف وحاول مقارنته.)**

**Expected Output:**
```
Items are equal: true
```

---

## Assignment 4: Pattern Matching in Switch (Advanced)

**Objective:**
Use records and patterns in switch statements (Dart 3+).
*(الهدف: استخدام السجلات والأنماط في عبارات switch (Dart 3+).)*

**Instructions:**
1. Create a function `executeCommand((String, int) command)`.
2. Use a `switch` statement on the record:
   - Case `('create', var id)`: Print "Creating ID: $id".
   - Case `('delete', var id)`: Print "Deleting ID: $id".
   - Case `(_, _)` (Wildcard): Print "Unknown command".
3. Call it with `('create', 50)` and `('update', 10)`.

**Expected Output:**
```
Creating ID: 50
Unknown command
```

---

## Assignment 5: API Response Handler (Expert)

**Objective:**
Use records to handle complex API return states (Success, Error, Loading) generically.
*(الهدف: استخدام السجلات لمعالجة حالات إرجاع API المعقدة (نجاح، خطأ، تحميل) بشكل عام.)*

**Instructions:**
1.  Define a generic function `fetchData<T>(bool success, T data, String errorMsg)`.
2.  It should return a Record `({bool isSuccess, T? data, String? error})`.
3.  In `main`, call this function twice:
    *   Once representing a success (success: true, data: "User Data", error: "").
    *   Once representing a failure (success: false, data: null, error: "404 Not Found").
4.  Use **destructuring** inside an `if` statement to handle the result:
    *   If `isSuccess`, print "Data: [data]".
    *   Else, print "Error: [error]".

**Expected Output:**
```
Data: User Data
Error: 404 Not Found
```

---

## Solutions

### Solution 1: User Profile

```dart
void main() {
  // Creating the record
  var userProfile = ('John', 'Doe', age: 30, isAdmin: true);

  // Accessing fields ($1 and $2 for positional, .age and .isAdmin for named)
  print('User: ${userProfile.$1} ${userProfile.$2}');
  print('Age: ${userProfile.age}');
  print('Admin: ${userProfile.isAdmin}');
}
```

### Solution 2: Coordinate Converter

```dart
void main() {
  // Function returning a record with named fields
  ({double lat, double long}) getLatLong(String city) {
    if (city == 'Cairo') return (lat: 30.0444, long: 31.2357);
    if (city == 'London') return (lat: 51.5074, long: -0.1278);
    return (lat: 0.0, long: 0.0);
  }

  // Destructuring using named pattern matching
  var (:lat, :long) = getLatLong('Cairo');
  // OR: var result = getLatLong('Cairo'); var lat = result.lat;
  
  print('City: Cairo');
  print('Latitude: $lat');
  print('Longitude: $long');
}
```

### Solution 3: Product Inventory Comparator

```dart
void main() {
  // Record 1
  var warehouseItem = (id: 101, name: "Laptop", price: 999.99);
  
  // Record 2: Same fields and values, different order
  // Named field order doesn't matter for shape or equality
  var storeShelfItem = (price: 999.99, id: 101, name: "Laptop");

  // Comparison
  bool areEqual = warehouseItem == storeShelfItem;
  print('Items are equal: $areEqual');

  // Record 3: Different shape (positional)
  var newItem = (101, "Laptop", 999.99);
  // warehouseItem == newItem; // Error: Different types
}
```

### Solution 4: Pattern Matching in Switch

```dart
void executeCommand((String, int) command) {
  switch (command) {
    case ('create', var id):
      print('Creating ID: $id');
    case ('delete', var id):
      print('Deleting ID: $id');
    case (_, _):
      print('Unknown command');
  }
}

void main() {
  executeCommand(('create', 50));
  executeCommand(('update', 10));
}
```

### Solution 5: API Response Handler

```dart
({bool isSuccess, T? data, String? error}) fetchData<T>(bool success, T? data, String? errorMsg) {
  if (success) {
    return (isSuccess: true, data: data, error: null);
  } else {
    return (isSuccess: false, data: null, error: errorMsg);
  }
}

void main() {
  // Test Case 1: Success
  var response1 = fetchData<String>(true, "User Data", null);
  
  if (response1.isSuccess) {
    // Note: Dart flow analysis might still see data as T?, so we check or bang (!)
    print("Data: ${response1.data}");
  }

  // Test Case 2: Failure
  var response2 = fetchData<String>(false, null, "404 Not Found");
  
  // Destructuring pattern
  var (:isSuccess, :data, :error) = response2;
  
  if (!isSuccess) {
    print("Error: $error");
  }
}
```
