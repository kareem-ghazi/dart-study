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

## Assignment 4: Simple Destructuring

**Objective:**
Practice unpacking record fields into variables directly.
*(الهدف: التدرب على تفكيك حقول السجل إلى متغيرات مباشرة.)*

**Instructions:**
1. Create a record `(10, 20)`.
2. Destructure it into two variables `x` and `y` in one line.
3. Print `x` and `y`.

**Expected Output:**
```
x: 10, y: 20
```

---

## Assignment 5: Record Type Return

**Objective:**
Define a function that explicitly specifies a record return type.
*(الهدف: تعريف دالة تحدد صراحة نوع إرجاع السجل.)*

**Instructions:**
1. Write a function `swap((int, int) record)` that takes a record of two ints.
2. It should return a record `(int, int)` with the values swapped.
3. Call it with `(1, 2)` and print the result.

**Expected Output:**
```
(2, 1)
```

---

## Solutions

```dart
void main() {
  // --- Assignment 1 Solution ---
  print('--- Assignment 1 ---');
  // Creating the record
  var userProfile = ('John', 'Doe', age: 30, isAdmin: true);

  // Accessing fields ($1 and $2 for positional, .age and .isAdmin for named)
  print('User: ${userProfile.$1} ${userProfile.$2}');
  print('Age: ${userProfile.age}');
  print('Admin: ${userProfile.isAdmin}');
  
  print('\n');

  // --- Assignment 2 Solution ---
  print('--- Assignment 2 ---');
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

  print('\n');

  // --- Assignment 3 Solution ---
  print('--- Assignment 3 ---');
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
  // warehouseItem == newItem; // This would be a compile-time error or always false depending on context
  // Because they have different shapes (types).

  // --- Assignment 4 Solution ---
  print('--- Assignment 4 ---');
  var (x, y) = (10, 20);
  print('x: $x, y: $y');

  // --- Assignment 5 Solution ---
  print('--- Assignment 5 ---');
  (int, int) swap((int, int) record) {
    return (record.$2, record.$1);
  }
  print(swap((1, 2)));
}