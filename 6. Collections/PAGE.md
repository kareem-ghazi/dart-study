# Collections

Dart has built-in support for list, set, and map [collections](https://dart.dev/libraries/dart-core#collections).

## Lists

Perhaps the most common collection in nearly every programming language is the _array_, or ordered group of objects. In Dart, arrays are [`List`](https://api.dart.dev/dart-core/List-class.html) objects, so most people just call them _lists_.

Dart list literals are denoted by a comma-separated list of elements enclosed in square brackets (`[]`). Each element is usually an expression. Here's a simple Dart list:

```dart
var list = [1, 2, 3];
```

You can add a comma after the last item in a Dart collection literal. This _trailing comma_ doesn't affect the collection, but it can help prevent copy-paste errors.

```dart
var list = ['Car', 'Boat', 'Plane'];
```

Lists use zero-based indexing, where 0 is the index of the first element and `list.length - 1` is the index of the last element. You can get a list's length using the `.length` property and access a list's elements using the subscript operator (`[]`):

```dart
var list = [1, 2, 3];
assert(list.length == 3);
assert(list[1] == 2);

list[1] = 1;
assert(list[1] == 1);
```

To create a list that's a compile-time constant, add `const` before the list literal:

```dart
var constantList = const [1, 2, 3];
// constantList[1] = 1; // This line will cause an error.
```

## Sets

A set in Dart is an unordered collection of unique elements. Dart support for sets is provided by set literals and the [`Set`](https://api.dart.dev/dart-core/Set-class.html) type.

Here is a simple Dart set, created using a set literal:

```dart
var halogens = {'fluorine', 'chlorine', 'bromine', 'iodine', 'astatine'};
```

To create an empty set, use `{}` preceded by a type argument, or assign `{}` to a variable of type `Set`:

```dart
var names = <String>{};
// Set<String> names = {}; // This works, too.
// var names = {}; // Creates a map, not a set.
```

Add items to an existing set using the `add()` or `addAll()` methods:

```dart
var elements = <String>{};
elements.add('fluorine');
elements.addAll(halogens);
```

Use `.length` to get the number of items in the set:

```dart
var elements = <String>{};
elements.add('fluorine');
elements.addAll(halogens);
assert(elements.length == 5);
```

To create a set that's a compile-time constant, add `const` before the set literal:

```dart
final constantSet = const {
  'fluorine',
  'chlorine',
  'bromine',
  'iodine',
  'astatine',
};
// constantSet.add('helium'); // This line will cause an error.
```

## Maps

In a map, each element is a key-value pair. Each key within a pair is associated with a value, and both keys and values can be any type of object. Each key can occur only once, although the same value can be associated with multiple different keys. Dart support for maps is provided by map literals and the [`Map`](https://api.dart.dev/dart-core/Map-class.html) type.

Here are a couple of simple Dart maps, created using map literals:

```dart
var gifts = {
  // Key:    Value
  'first': 'partridge',
  'second': 'turtledoves',
  'fifth': 'golden rings',
};

var nobleGases = {2: 'helium', 10: 'neon', 18: 'argon'};
```

You can create the same objects using a Map constructor:

```dart
var gifts = Map<String, String>();
gifts['first'] = 'partridge';
gifts['second'] = 'turtledoves';
gifts['fifth'] = 'golden rings';

var nobleGases = Map<int, String>();
nobleGases[2] = 'helium';
nobleGases[10] = 'neon';
nobleGases[18] = 'argon';
```

Add a new key-value pair to an existing map using the subscript assignment operator (`[]=`):

```dart
var gifts = {'first': 'partridge'};
gifts['fourth'] = 'calling birds'; // Add a key-value pair
```

Retrieve a value from a map using the subscript operator (`[]`):

```dart
var gifts = {'first': 'partridge'};
assert(gifts['first'] == 'partridge');
```

If you look for a key that isn't in a map, you get `null` in return:

```dart
var gifts = {'first': 'partridge'};
assert(gifts['fifth'] == null);
```

Use `.length` to get the number of key-value pairs in the map:

```dart
var gifts = {'first': 'partridge'};
gifts['fourth'] = 'calling birds';
assert(gifts.length == 2);
```

To create a map that's a compile-time constant, add `const` before the map literal:

```dart
final constantMap = const {2: 'helium', 10: 'neon', 18: 'argon'};

// constantMap[2] = 'Helium'; // This line will cause an error.
```

## Collection Elements

A collection literal contains a series of elements. These elements fall into two main categories: leaf elements and control flow elements.

### Spread Elements

The spread element iterates over a given sequence and inserts all of the resulting values into the surrounding collection.

A spread element has the following syntax:

```dart
...<sequence_expression>
```

In the following example, the elements in a list called `a` are added to a list called `items`.

```dart
var a = [1, 2, null, 4];
var items = [0, ...a, 5]; // [0, 1, 2, null, 4, 5]
```

### Null-aware Spread Elements

The null-aware spread element is similar to the spread element, but allows the collection to be `null` and inserts nothing if it is.

A null-aware spread element has this syntax:

```dart
...?<sequence_expression>
```

Example:

```dart
List<int>? a = null;
var b = [1, null, 3];
var items = [0, ...?a, ...?b, 4]; // [0, 1, null, 3, 4]
```

### If Elements

An `if` element conditionally evaluates an inner element based on given a condition expression, and optionally evaluates another `else` element if the condition is false.

```dart
var includeItem = true;
var items = [0, if (includeItem) 1, 2, 3]; // [0, 1, 2, 3]
```

```dart
var name = 'apple';
var items = [0, if (name == 'orange') 1 else 10, 2, 3]; // [0, 10, 2, 3]
```

### For Elements

A `for` element iterates and repeatedly evaluates a given inner element, inserting zero or more resulting values.

```dart
var numbers = [2, 3, 4];
var items = [1, for (var n in numbers) n * n, 7]; // [1, 4, 9, 16, 7]
```

### Nesting Control Flow Elements

You can nest control flow elements within each other. This is a powerful alternative to list comprehensions.

```dart
var numbers = [1, 2, 3, 4, 5, 6, 7];
var items = [
  0,
  for (var n in numbers)
    if (n.isEven) n,
  8,
]; // [0, 2, 4, 6, 8]
```
