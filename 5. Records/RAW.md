1.   [Language](https://dart.dev/language)
2.   [Records](https://dart.dev/language/records)

Summary of the record data structure in Dart.

Records are an anonymous, immutable, aggregate type. Like other [collection types](https://dart.dev/language/collections), they let you bundle multiple objects into a single object. Unlike other collection types, records are fixed-sized, heterogeneous, and typed.

Records are real values; you can store them in variables, nest them, pass them to and from functions, and store them in data structures such as lists, maps, and sets.

_Records expressions_ are comma-delimited lists of named or positional fields, enclosed in parentheses:

dart

```
var record = ('first', a: 2, b: true, 'last');
```

_Record type annotations_ are comma-delimited lists of types enclosed in parentheses. You can use record type annotations to define return types and parameter types. For example, the following `(int, int)` statements are record type annotations:

dart

```
(int, int) swap((int, int) record) {
  var (a, b) = record;
  return (b, a);
}
```

Fields in record expressions and type annotations mirror how [parameters and arguments](https://dart.dev/language/functions#parameters) work in functions. Positional fields go directly inside the parentheses:

dart

```
// Record type annotation in a variable declaration:
(String, int) record;
​
// Initialize it with a record expression:
record = ('A string', 123);
```

In a record type annotation, named fields go inside a curly brace-delimited section of type-and-name pairs, after all positional fields. In a record expression, the names go before each field value with a colon after:

dart

```
// Record type annotation in a variable declaration:
({int a, bool b}) record;
​
// Initialize it with a record expression:
record = (a: 123, b: true);
```

The names of named fields in a record type are part of the [record's type definition](https://dart.dev/language/records#record-types), or its _shape_. Two records with named fields with different names have different types:

dart

```
({int a, int b}) recordAB = (a: 1, b: 2);
({int x, int y}) recordXY = (x: 3, y: 4);
​
// Compile error! These records don't have the same type.
// recordAB = recordXY;
```

In a record type annotation, you can also name the _positional_ fields, but these names are purely for documentation and don't affect the record's type:

dart

```
(int a, int b) recordAB = (1, 2);
(int x, int y) recordXY = (3, 4);
​
recordAB = recordXY; // OK.
```

This is similar to how positional parameters in a [function declaration or function typedef](https://dart.dev/language/functions#function-types) can have names but those names don't affect the signature of the function.

For more information and examples, check out [Record types](https://dart.dev/language/records#record-types) and [Record equality](https://dart.dev/language/records#record-equality).

Record fields are accessible through built-in getters. Records are immutable, so fields do not have setters.

Named fields expose getters of the same name. Positional fields expose getters of the name `$<position>`, skipping named fields:

dart

```
var record = ('first', a: 2, b: true, 'last');
​
print(record.$1); // Prints 'first'
print(record.a); // Prints 2
print(record.b); // Prints true
print(record.$2); // Prints 'last'
```

To streamline record field access even more, check out the page on [Patterns](https://dart.dev/language/patterns#destructuring-multiple-returns).

There is no type declaration for individual record types. Records are structurally typed based on the types of their fields. A record's _shape_ (the set of its fields, the fields' types, and their names, if any) uniquely determines the type of a record.

Each field in a record has its own type. Field types can differ within the same record. The type system is aware of each field's type wherever it is accessed from the record:

dart

```
(num, Object) pair = (42, 'a');
​
var first = pair.$1; // Static type `num`, runtime type `int`.
var second = pair.$2; // Static type `Object`, runtime type `String`.
```

Consider two unrelated libraries that create records with the same set of fields. The type system understands that those records are the same type even though the libraries are not coupled to each other.

Two records are equal if they have the same _shape_ (set of fields), and their corresponding fields have the same values. Since named field _order_ is not part of a record's shape, the order of named fields does not affect equality.

For example:

dart

```
(int x, int y, int z) point = (1, 2, 3);
(int r, int g, int b) color = (1, 2, 3);
​
print(point == color); // Prints 'true'.
```

dart

```
({int x, int y, int z}) point = (x: 1, y: 2, z: 3);
({int r, int g, int b}) color = (r: 1, g: 2, b: 3);
​
print(point == color); // Prints 'false'. Lint: Equals on unrelated types.
```

Records automatically define `hashCode` and `==` methods based on the structure of their fields.

Records allow functions to return multiple values bundled together. To retrieve record values from a return, [destructure](https://dart.dev/language/patterns#destructuring) the values into local variables using [pattern matching](https://dart.dev/language/patterns#destructuring-multiple-returns).

dart

```
// Returns multiple values in a record:
(String name, int age) userInfo(Map<String, dynamic> json) {
  return (json['name'] as String, json['age'] as int);
}
​
final json = <String, dynamic>{'name': 'Dash', 'age': 10, 'color': 'blue'};
​
// Destructures using a record pattern with positional fields:
var (name, age) = userInfo(json);
​
/* Equivalent to:
  var info = userInfo(json);
  var name = info.$1;
  var age  = info.$2;
*/
```

You can also destructure a record using its [named fields](https://dart.dev/language/records#record-fields), using the colon `:` syntax, which you can read more about on the [Pattern types](https://dart.dev/language/pattern-types#record) page:

dart

```
({String name, int age}) userInfo(Map<String, dynamic> json)
// ···
// Destructures using a record pattern with named fields:
final (:name, :age) = userInfo(json);
```

You can return multiple values from a function without records, but other methods come with downsides. For example, creating a class is much more verbose, and using other collection types like `List` or `Map` loses type safety.

Records as simple data structures
---------------------------------

[#](https://dart.dev/language/records#records-as-simple-data-structures)

Records only hold data. When that's all you need, they're immediately available and easy to use without needing to declare any new classes. For a simple list of data tuples that all have the same shape, a _list of records_ is the most direct representation.

Take this list of "button definitions", for example:

dart

```
final buttons = [
  (
    label: "Button I",
    icon: const Icon(Icons.upload_file),
    onPressed: () => print("Action -> Button I"),
  ),
  (
    label: "Button II",
    icon: const Icon(Icons.info),
    onPressed: () => print("Action -> Button II"),
  )
];
```

This code can be written directly without needing any additional declarations.

### Records and typedefs

[#](https://dart.dev/language/records#records-and-typedefs)

You can choose to use [typedefs](https://dart.dev/language/typedefs) to give the record type itself a name, and use that rather than writing out the full record type. This method allows you to state that some fields can be null (`?`), even if none of the current entries in the list have a null value.

dart

```
typedef ButtonItem = ({String label, Icon icon, void Function()? onPressed});
final List<ButtonItem> buttons = [
  // ...
];
```

Because record types are structural types, giving a name like `ButtonItem` only introduces an alias that makes it easier to refer to the structural type: `({String label, Icon icon, void Function()? onPressed})`.

Having all your code refer to a record type by its alias makes it easier to later change the record's implementation without needing to update every reference.

Code can work with the given button definitions the same way it would with simple class instances:

dart

```
List<Container> widget = [
  for (var button in buttons)
    Container(
      margin: const EdgeInsets.all(4.0),
      child: OutlinedButton.icon(
        onPressed: button.onPressed,
        icon: button.icon,
        label: Text(button.label),
      ),
    ),
];
```

You could even decide to later change the record type to a class type to add methods:

dart

```
class ButtonItem {
  final String label;
  final Icon icon;
  final void Function()? onPressed;
  ButtonItem({required this.label, required this.icon, this.onPressed});
  bool get hasOnpressed => onPressed != null;
}
```

Or to an [extension type](https://dart.dev/language/extension-types):

dart

```
extension type ButtonItem._(({String label, Icon icon, void Function()? onPressed}) _) {
  String get label => _.label;
  Icon get icon => _.icon;
  void Function()? get onPressed => _.onPressed;
  ButtonItem({required String label, required Icon icon, void Function()? onPressed})
      : this._((label: label, icon: icon, onPressed: onPressed));
  bool get hasOnpressed => _.onPressed != null;
}
```

And then create the list of button definitions using that type's constructors:

dart

```
final List<ButtonItem> buttons =  [
  ButtonItem(
    label: "Button I",
    icon: const Icon(Icons.upload_file),
    onPressed: () => print("Action -> Button I"),
  ),
  ButtonItem(
    label: "Button II",
    icon: const Icon(Icons.info),
    onPressed: () => print("Action -> Button II"),
  )
];
```

Again, all while not needing to change the code that uses that list.

Changing any type does require the code using it to be very careful about not making assumptions. A type alias does not offer any protection or guarantee, for the code using it as a reference, that the value being aliased is a record. Extension types, also, offer little protection. Only a class can provide full abstraction and encapsulation.