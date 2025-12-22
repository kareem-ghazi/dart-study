Comments
========

The different comment types in Dart.

more_vert

*   copy Copy link
*   [docs View source](https://github.com/dart-lang/site-www/blob/main/src/content/language/comments.md)
*   [bug_report Report issue](https://github.com/dart-lang/site-www/issues/new?template=1_page_issue.yml&page-url=https://dart.dev/language/comments&page-source=https://github.com/dart-lang/site-www/blob/main/src/content/language/comments.md)

Dart supports single-line comments, multi-line comments, and documentation comments.

Single-line comments
--------------------

[#](https://dart.dev/language/comments#single-line-comments)

A single-line comment begins with `//`. Everything between `//` and the end of line is ignored by the Dart compiler.

dart
```
void main() {
  // TODO: refactor into an AbstractLlamaGreetingFactory?
  print('Welcome to my Llama farm!');
}
```
content_copy

Multi-line comments
-------------------

[#](https://dart.dev/language/comments#multi-line-comments)

A multi-line comment begins with `/*` and ends with `*/`. Everything between `/*` and `*/` is ignored by the Dart compiler (unless the comment is a documentation comment; see the next section). Multi-line comments can nest.

dart
```
void main() {
  /*
   * This is a lot of work. Consider raising chickens.
​
  Llama larry = Llama();
  larry.feed();
  larry.exercise();
  larry.clean();
   */
}
```
content_copy

Documentation comments
----------------------

[#](https://dart.dev/language/comments#documentation-comments)

Documentation comments are multi-line or single-line comments that begin with `///` or `/**`. Using `///` on consecutive lines has the same effect as a multi-line doc comment.

Inside a documentation comment, the analyzer ignores all text unless it is enclosed in brackets. Using brackets, you can refer to classes, methods, fields, top-level variables, functions, and parameters. The names in brackets are resolved in the lexical scope of the documented program element.

Here is an example of documentation comments with references to other classes and arguments:

dart
```
/// A domesticated South American camelid (Lama glama).
///
/// Andean cultures have used llamas as meat and pack
/// animals since pre-Hispanic times.
///
/// Just like any other animal, llamas need to eat,
/// so don't forget to [feed] them some [Food].
class Llama {
  String? name;
​
  /// Feeds your llama [food].
  ///
  /// The typical llama eats one bale of hay per week.
  void feed(Food food) {
    // ...
  }
​
  /// Exercises your llama with an [activity] for
  /// [timeLimit] minutes.
  void exercise(Activity activity, int timeLimit) {
    // ...
  }
}
```
content_copy

In the class's generated documentation, `[feed]` becomes a link to the docs for the `feed` method, and `[Food]` becomes a link to the docs for the `Food` class.

To parse Dart code and generate HTML documentation, you can use Dart's documentation generation tool, [`dart doc`](https://dart.dev/tools/dart-doc). For an example of generated documentation, see the [Dart API documentation.](https://api.dart.dev/) For advice on how to structure your comments, see [Effective Dart: Documentation.](https://dart.dev/effective-dart/documentation)
