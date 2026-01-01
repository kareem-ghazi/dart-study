Callable objects
================

Learn how to create and use callable objects in Dart.

more_vert

*   copy Copy link
*   [docs View source](https://github.com/dart-lang/site-www/blob/main/src/content/language/callable-objects.md)
*   [bug_report Report issue](https://github.com/dart-lang/site-www/issues/new?template=1_page_issue.yml&page-url=https://dart.dev/language/callable-objects&page-source=https://github.com/dart-lang/site-www/blob/main/src/content/language/callable-objects.md)

To allow an instance of your Dart class to be called like a function, implement the `call()` method.

The `call()` method allows an instance of any class that defines it to emulate a function. This method supports the same functionality as normal [functions](https://dart.dev/language/functions) such as parameters and return types.

In the following example, the `WannabeFunction` class defines a `call()` function that takes three strings and concatenates them, separating each with a space, and appending an exclamation. Click **Run** to execute the code.

```
class WannabeFunction {
  String call(String a, String b, String c) => '$a $b $c!';
}

var wf = WannabeFunction();
var out = wf('Hi', 'there,', 'gang');

void main() => print(out);
```