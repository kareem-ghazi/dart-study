1.   [Language](https://dart.dev/language)
2.   [Collections](https://dart.dev/language/collections)

Summary of the different types of collections in Dart.

Dart has built-in support for list, set, and map [collections](https://dart.dev/libraries/dart-core#collections). To learn more about configuring the types collections contain, check out [Generics](https://dart.dev/language/generics).

Perhaps the most common collection in nearly every programming language is the _array_, or ordered group of objects. In Dart, arrays are [`List`](https://api.dart.dev/dart-core/List-class.html) objects, so most people just call them _lists_.

Dart list literals are denoted by a comma-separated list of elements enclosed in square brackets (`[]`). Each element is usually an expression. Here's a simple Dart list:

dart

```
var list = [1, 2, 3];
```

[](https://dart.dev/language/collections) You can add a comma after the last item in a Dart collection literal. This _trailing comma_ doesn't affect the collection, but it can help prevent copy-paste errors.

dart

```
var list = ['Car', 'Boat', 'Plane'];
```

Lists use zero-based indexing, where 0 is the index of the first element and `list.length - 1` is the index of the last element. You can get a list's length using the `.length` property and access a list's elements using the subscript operator (`[]`):

dart

```
var list = [1, 2, 3];
assert(list.length == 3);
assert(list[1] == 2);
​
list[1] = 1;
assert(list[1] == 1);
```

To create a list that's a compile-time constant, add `const` before the list literal:

dart

```
var constantList = const [1, 2, 3];
// constantList[1] = 1; // This line will cause an error.
```

For more information about lists, refer to the Lists section of the [`dart:core` documentation](https://dart.dev/libraries/dart-core#lists).

A set in Dart is an unordered collection of unique elements. Dart support for sets is provided by set literals and the [`Set`](https://api.dart.dev/dart-core/Set-class.html) type.

Here is a simple Dart set, created using a set literal:

dart

```
var halogens = {'fluorine', 'chlorine', 'bromine', 'iodine', 'astatine'};
```

To create an empty set, use `{}` preceded by a type argument, or assign `{}` to a variable of type `Set`:

dart

```
var names = <String>{};
// Set<String> names = {}; // This works, too.
// var names = {}; // Creates a map, not a set.
```

Add items to an existing set using the `add()` or `addAll()` methods:

dart

```
var elements = <String>{};
elements.add('fluorine');
elements.addAll(halogens);
```

Use `.length` to get the number of items in the set:

dart

```
var elements = <String>{};
elements.add('fluorine');
elements.addAll(halogens);
assert(elements.length == 5);
```

To create a set that's a compile-time constant, add `const` before the set literal:

dart

```
final constantSet = const {
  'fluorine',
  'chlorine',
  'bromine',
  'iodine',
  'astatine',
};
// constantSet.add('helium'); // This line will cause an error.
```

For more information about sets, refer to the Sets section of the [`dart:core` documentation](https://dart.dev/libraries/dart-core#sets).

In a map, each element is a key-value pair. Each key within a pair is associated with a value, and both keys and values can be any type of object. Each key can occur only once, although the same value can be associated with multiple different keys. Dart support for maps is provided by map literals and the [`Map`](https://api.dart.dev/dart-core/Map-class.html) type.

Here are a couple of simple Dart maps, created using map literals:

dart

```
var gifts = {
  // Key:    Value
  'first': 'partridge',
  'second': 'turtledoves',
  'fifth': 'golden rings',
};
​
var nobleGases = {2: 'helium', 10: 'neon', 18: 'argon'};
```

You can create the same objects using a Map constructor:

dart

```
var gifts = Map<String, String>();
gifts['first'] = 'partridge';
gifts['second'] = 'turtledoves';
gifts['fifth'] = 'golden rings';
​
var nobleGases = Map<int, String>();
nobleGases[2] = 'helium';
nobleGases[10] = 'neon';
nobleGases[18] = 'argon';
```

Add a new key-value pair to an existing map using the subscript assignment operator (`[]=`):

dart

```
var gifts = {'first': 'partridge'};
gifts['fourth'] = 'calling birds'; // Add a key-value pair
```

Retrieve a value from a map using the subscript operator (`[]`):

dart

```
var gifts = {'first': 'partridge'};
assert(gifts['first'] == 'partridge');
```

If you look for a key that isn't in a map, you get `null` in return:

dart

```
var gifts = {'first': 'partridge'};
assert(gifts['fifth'] == null);
```

Use `.length` to get the number of key-value pairs in the map:

dart

```
var gifts = {'first': 'partridge'};
gifts['fourth'] = 'calling birds';
assert(gifts.length == 2);
```

To create a map that's a compile-time constant, add `const` before the map literal:

dart

```
final constantMap = const {2: 'helium', 10: 'neon', 18: 'argon'};
​
// constantMap[2] = 'Helium'; // This line will cause an error.
```

For more information about maps, refer to the Maps section of the [`dart:core` documentation](https://dart.dev/libraries/dart-core#maps).

Collection elements
-------------------

[#](https://dart.dev/language/collections#collection-elements)

A collection literal contains a series of elements. During runtime, each element is evaluated, producing zero or more values that are then inserted into the resulting collection. These elements fall into two main categories: leaf elements and control flow elements.

*   Leaf element: Inserts an individual item into a collection literal.

    *   Expression element: Evaluates a single expression and inserts the resulting value into the collection.

    *   Map entry element: Evaluates a pair of key and value expressions and inserts the resulting entry into the collection.

*   Control flow element: Conditionally or iteratively adds zero or more values to the surrounding collection.

    *   Null-aware element: Evaluates an expression and if the result is not `null`, inserts the value into the surrounding collection.

    *   Spread element: Iterates over a given sequence (collection expression) and inserts all of the resulting values into the surrounding collection.

    *   Null-aware spread element: Similar to the spread element, but allows the collection to be `null` and inserts nothing if it is.

    *   If element: Conditionally evaluates an inner element based on given a condition expression, and optionally evaluates another `else` element if the condition is false.

    *   For element: Iterates and repeatedly evaluates a given inner element, inserting zero or more resulting values.

To learn more about collection elements, see the following sections.

### Expression elements

[#](https://dart.dev/language/collections#expression-element)

An expression element evaluates a single expression and inserts the resulting value into a collection. This expression can encompass various constructs like literals, variables, operators, function calls, and constructor calls.

An expression element has this syntax in a collection:

dart

```
<expression>
```

### Map entry elements

[#](https://dart.dev/language/collections#map-entry-element)

A map entry element evaluates a pair of key and value expressions and inserts the resulting entry into a collection. Both the key and the value within this pair can be expressions.

A map entry element has this syntax in a collection:

dart

```
<key_expression>: <value_expression>
```

### Null-aware elements

[#](https://dart.dev/language/collections#null-aware-element)

A null-aware element evaluates an expression and if the result is not `null`, inserts the value into the surrounding collection.

A null-aware element has the following syntax in an expression element:

dart

```
?<expression>
```

A null-aware element has the following syntax in a map entry element:

dart

```
// key is a null-aware element
?<key_expression>: <value_expression>
```

dart

```
// value is a null-aware element
<key_expression>: ?<value_expression>
```

dart

```
// key and value are null-aware elements
?<key_expression>: ?<value_expression>
```

In the following example, the result for the null-aware element `?a` is not added to a list called `items` because `a` is `null`:

dart

```
int? absentValue = null;
int? presentValue = 3;
var items = [
  1,
  ?absentValue,
  ?presentValue,
  absentValue,
  5,
]; // [1, 3, null, 5]
```

The following example illustrates various ways that you can use null-aware elements inside of map entry elements:

dart

```
String? presentKey = 'Apple';
String? absentKey = null;
​
int? presentValue = 3;
int? absentValue = null;
​
var itemsA = {presentKey: absentValue}; // {Apple: null}
var itemsB = {presentKey: ?absentValue}; // {}
​
var itemsC = {absentKey: presentValue}; // {null: 3}
var itemsD = {?absentKey: presentValue}; // {}
​
var itemsE = {absentKey: absentValue}; // {null: null}
var itemsF = {?absentKey: ?absentValue}; // {}
```

The spread element iterates over a given sequence and inserts all of the resulting values into the surrounding collection.

A spread element has the following syntax in a collection. The sequence expression can represent any expression that evaluates to an object that implements `Iterable`:

dart

```
...<sequence_expression>
```

In the following example, the elements in a list called `a` are added to a list called `items`.

dart

```
var a = [1, 2, null, 4];
var items = [0, ...a, 5]; // [0, 1, 2, null, 4, 5]
```

If you are spreading an expression that might evaluate to `null` and you want to ignore the `null` (and insert no elements), use a [null-aware spread element](https://dart.dev/language/collections#null-spread-element).

To learn more about the spread operator, see [Spread operator](https://dart.dev/language/operators/#spread-operators).

### Null-aware spread elements

[#](https://dart.dev/language/collections#null-spread-element)

The null-aware spread element is similar to the spread element, but allows the collection to be `null` and inserts nothing if it is.

A null-aware spread element has this syntax in a collection:

dart

```
...?<sequence_expression>
```

In the following example, a list called `a` is ignored because it's null, but the elements in a list called `b` are added to a list called `items`. Notice that if a collection itself is not `null`, but it contains elements that are, those `null` elements are still added to the result.

dart

```
List<int>? a = null;
var b = [1, null, 3];
var items = [0, ...?a, ...?b, 4]; // [0, 1, null, 3, 4]
```

Because of null safety, you can't perform a spread operation (`...`) on a value that might be null. The following example produces a compile-time error because the `extraOptions` parameter is nullable and the spread operator used on `extraOptions` is not null-aware.

static analysis: failure dart

```
List<String> buildCommandLine(
  String executable,
  List<String> options, [
  List<String>? extraOptions,
]) {
  return [
    executable,
    ...options,
    ...extraOptions, // <-- Error
  ];
}
​
// Usage:
//   buildCommandLine('dart', ['run', 'my_script.dart'], null);
// Result:
//   Compile-time error
```

If you want to spread a nullable collection, use a null-aware spread element. The following example is valid because the null-aware spread operator is used on `extraOptions`.

dart

```
List<String> buildCommandLine(
  String executable,
  List<String> options, [
  List<String>? extraOptions,
]) {
  return [
    executable,
    ...options,
    ...?extraOptions, // <-- OK now.
  ];
}
​
// Usage:
//   buildCommandLine('dart', ['run', 'my_script.dart'], null);
// Result:
//   [dart, run, my_script.dart]
```

To learn more about the null-aware spread operator, see [Spread operator](https://dart.dev/language/operators/#spread-operators).

An `if` element conditionally evaluates an inner element based on given a condition expression, and optionally evaluates another `else` element if the condition is false.

The `if` element has a few syntax variations:

dart

```
// If the bool expression is true, include the result.
if (<bool_expression>) <result>
```

dart

```
// If the expression matches the pattern, include the result.
if (<expression> case <pattern>) <result>
```

dart

```
// If the operation resolves as true, include the first
// result, otherwise, include the second result.
if (<bool_expression>) <result> else <result>
```

dart

```
// If the operation resolves as true, include the first
// result, otherwise, include the second result.
if (<expression> case <pattern>) <result> else <result>
```

The following examples illustrate various ways that you can use an `if` element inside of a collection with a boolean expression:

dart

```
var includeItem = true;
var items = [0, if (includeItem) 1, 2, 3]; // [0, 1, 2, 3]
```

dart

```
var includeItem = true;
var items = [0, if (!includeItem) 1, 2, 3]; // [0, 2, 3]
```

dart

```
var name = 'apple';
var items = [0, if (name == 'orange') 1 else 10, 2, 3]; // [0, 10, 2, 3]
```

dart

```
var name = 'apple';
var items = [
  0,
  if (name == 'kiwi') 1 else if (name == 'pear') 10,
  2,
  3,
]; // [0, 2, 3]
```

The following examples illustrate various ways that you can use an `if` element with a `case` part inside of a collection:

dart

```
Object data = 123;
var typeInfo = [
  if (data case int i) 'Data is an integer: $i',
  if (data case String s) 'Data is a string: $s',
  if (data case bool b) 'Data is a boolean: $b',
  if (data case double d) 'Data is a double: $d',
]; // [Data is an integer: 123, Data is a double: 123]
```

dart

```
var word = 'hello';
var items = [
  1,
  if (word case String(length: var wordLength)) wordLength,
  3,
]; // [1, 5, 3]
```

dart

```
var orderDetails = ['Apples', 12, ''];
var summary = [
  'Product: ${orderDetails[0]}',
  if (orderDetails case [_, int qty, _]) 'Quantity: $qty',
  if (orderDetails case [_, _, ''])
    'Delivery: Not Started'
  else
    'Delivery: In Progress',
]; // [Product: Apples, Quantity: 12, Delivery: Not Started]
```

You can mix different `if` operations with an `else if` part. For example:

dart

```
var a = 'apple';
var b = 'orange';
var c = 'mango';
var items = [
  0,
  if (a == 'apple') 1 else if (a case 'mango') 10,
  if (b case 'pear') 2 else if (b == 'mango') 20,
  if (c case 'apple') 3 else if (c case 'mango') 30,
  4,
]; // [0, 1, 30, 4]
```

To learn more about the `if` conditional, see [`if` statement](https://dart.dev/language/branches#if). To learn more about the `if-case` conditional, see [`if-case` statement](https://dart.dev/language/branches#if-case).

A `for` element iterates and repeatedly evaluates a given inner element, inserting zero or more resulting values.

A `for` element has this syntax in a collection:

dart

```
for (<expression> in <collection>) <result>
```

dart

```
for (<initialization_clause>; <condition_clause>; <increment_clause>) <result>
```

The following examples illustrate various ways that you can use a `for` element inside of a collection:

dart

```
var numbers = [2, 3, 4];
var items = [1, for (var n in numbers) n * n, 7]; // [1, 4, 9, 16, 7]
```

dart

```
var items = [1, for (var x = 5; x > 2; x--) x, 7]; // [1, 5, 4, 3, 7]
```

dart

```
var items = [1, for (var x = 2; x < 4; x++) x, 7]; // [1, 2, 3, 7]
```

To learn more about the `for` loop, see [`for` loops](https://dart.dev/language/loops/#for-loops).

### Nest control flow elements

[#](https://dart.dev/language/collections#nesting-elements)

You can nest control flow elements within each other. This is a powerful alternative to list comprehensions in other languages.

In the following example, only the even numbers in `numbers` are included in `items`.

dart

```
var numbers = [1, 2, 3, 4, 5, 6, 7];
var items = [
  0,
  for (var n in numbers)
    if (n.isEven) n,
  8,
]; // [0, 2, 4, 6, 8]
```

It's common and idiomatic to use a spread on a collection literal immediately inside of an `if` or `for` element. For example:

dart

```
var items = [
  if (condition) oneThing(),
  if (condition) ...[multiple(), things()],
]; // [oneThing, [multiple_a, multiple_b], things]
```

You can nest all kinds of elements arbitrarily deep. In the following example, `if`, `for` and spread elements are nested within each other in a collection:

dart

```
var nestItems = true;
var ys = [1, 2, 3, 4];
var items = [
  if (nestItems) ...[
    for (var x = 0; x < 3; x++)
      for (var y in ys)
        if (x < y) x + y * 10,
  ],
]; // [10, 20, 30, 40, 21, 31, 41, 32, 42]
```
