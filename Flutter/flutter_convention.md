# Effective Dart: Style

A surprisingly important part of good code is good style. Consistent naming, ordering, and formatting helps code that *is* the same *look* the same. It takes advantage of the powerful pattern-matching hardware most of us have in our ocular systems.  If we use a consistent style across the entire Dart ecosystem, it makes it easier for all of us to learn from and contribute to each others' code.

## Identifiers

Identifiers come in three flavors in Dart.

*   `UpperCamelCase` names capitalize the first letter of each word, including
    the first.

*   `lowerCamelCase` names capitalize the first letter of each word, *except*
    the first which is always lowercase, even if it's an acronym.

*   `lowercase_with_underscores` names use only lowercase letters,
    even for acronyms,
    and separate words with `_`.

### DO name types using `UpperCamelCase`.

Classes, enum types, typedefs, and type parameters should capitalize the first letter of each word (including the first word), and use no separators.

```dart
good
class SliderMenu { ... }

class HttpRequest { ... }

typedef Predicate<T> = bool Function(T value);
```

This even includes classes intended to be used in metadata annotations.

```dart
good
class Foo {
  const Foo([Object? arg]);
}

@Foo(anArg)
class A { ... }

@Foo()
class B { ... }
```

If the annotation class's constructor takes no parameters, you might want to create a separate `lowerCamelCase` constant for it.

```dart
good
const foo = Foo();

@foo
class C { ... }
```

### DO name extensions using `UpperCamelCase`.

Like types, [extensions](https://dart.dev/guides/language/extension-methods) should capitalize the first letter of each word (including the first word),
and use no separators.

```dart
extension MyFancyList<T> on List<T> { ... }

extension SmartIterable<T> on Iterable<T> { ... }
```

### DO name libraries, packages, directories, and source files using `lowercase_with_underscores`. 

Some file systems are not case-sensitive, so many projects require filenames to be all lowercase. Using a separating character allows names to still be readable in that form. Using underscores as the separator ensures that the name is still a valid Dart identifier, which may be helpful if the language later supports symbolic imports.

```dart
good
library peg_parser.source_scanner;

import 'file_system.dart';
import 'slider_menu.dart';
```

```dart
bad
library pegparser.SourceScanner;

import 'file-system.dart';
import 'SliderMenu.dart';
```

### Do name import prefixes using lowercase_with_underscores

```dart
good
import 'dart:math' as math;
import 'package:angular_components/angular_components'
    as angular_components;
import 'package:js/js.dart' as js;
```

```dart
bad
import 'dart:math' as Math;
import 'package:angular_components/angular_components'
    as angularComponents;
import 'package:js/js.dart' as JS;
```

### DO name other identifiers using lowerCamelCase.

Class members, top-level definitions, variables, parameters, and named parameters should capitalize the first letter of each word except the first word, and use no separators.

```dart
good
var count = 3;

HttpRequest httpRequest;

void align(bool clearItems) {
  // ...
}
```

### PREFER using lowerCamelCase for constant names.

In new code, use lowerCamelCase for constant variables, including enum values.

```dart
good
const pi = 3.14;
const defaultTimeout = 1000;
final urlScheme = RegExp('^([a-z]+):');

class Dice {
  static final numberGenerator = Random();
}
```

```dart
bad
const PI = 3.14;
const DefaultTimeout = 1000;
final URL_SCHEME = RegExp('^([a-z]+):');

class Dice {
  static final NUMBER_GENERATOR = Random();
}
```

You may use `SCREAMING_CAPS` for consistency with existing code, as in the following cases:

- When adding code to a file or library that already uses `SCREAMING_CAPS`.
- When generating Dart code that’s parallel to Java code — for example, in enumerated types generated from [protobufs.](https://pub.dev/packages/protobuf)

```
Note: We initially used Java’s SCREAMING_CAPS style for constants. We changed for a few reasons:

SCREAMING_CAPS looks bad for many cases, particularly enum values for things like CSS colors.
Constants are often changed to final non-const variables, which would necessitate a name change.
The values property automatically defined on an enum type is const and lowercase.
```

### DO capitalize acronyms and abbreviations longer than two letters like words.

Capitalized acronyms can be hard to read, and multiple adjacent acronyms can lead to ambiguous names. For example, given a name that starts with `HTTPSFTP`, there’s no way to tell if it’s referring to HTTPS FTP or HTTP SFTP.

To avoid this, acronyms and abbreviations are capitalized like regular words.

**Exception**: Two-letter acronyms like IO (input/output) are fully capitalized: `IO`. On the other hand, two-letter abbreviations like ID (identification) are still capitalized like regular words: `Id`.

```dart
good
class HttpConnection {}
class DBIOPort {}
class TVVcr {}
class MrRogers {}

var httpRequest = ...
var uiHandler = ...
Id id;
```

```dart
bad
class HTTPConnection {}
class DbIoPort {}
class TvVcr {}
class MRRogers {}

var hTTPRequest = ...
var uIHandler = ...
ID iD;
```

### PREFER using _, __, etc. for unused callback parameters.

Sometimes the type signature of a callback function requires a parameter, but the callback implementation doesn’t use the parameter. In this case, it’s idiomatic to name the unused parameter _. If the function has multiple unused parameters, use additional underscores to avoid name collisions: __, ___, etc.

```dart
good
futureOfVoid.then((_) {
  print('Operation complete.');
});
```

This guideline is only for functions that are both anonymous and local. These functions are usually used immediately in a context where it’s clear what the unused parameter represents. In contrast, top-level functions and method declarations don’t have that context, so their parameters must be named so that it’s clear what each parameter is for, even if it isn’t used.

### DON’T use a leading underscore for identifiers that aren’t private.

Dart uses a leading underscore in an identifier to mark members and top-level declarations as private. This trains users to associate a leading underscore with one of those kinds of declarations. They see “_” and think “private”.

There is no concept of “private” for local variables, parameters, local functions, or library prefixes. When one of those has a name that starts with an underscore, it sends a confusing signal to the reader. To avoid that, don’t use leading underscores in those names.

DON’T use prefix letters.

### DON’T use prefix letters.

[Hungarian notation](https://en.wikipedia.org/wiki/Hungarian_notation) and other schemes arose in the time of BCPL, when the compiler didn’t do much to help you understand your code. Because Dart can tell you the type, scope, mutability, and other properties of your declarations, there’s no reason to encode those properties in identifier names.

```dart
good
defaultTimeout
```

```bad
kDefaultTimeout
```

### Ordering

To keep the preamble of your file tidy, we have a prescribed order that directives should appear in. Each “section” should be separated by a blank line.

A single linter rule handles all the ordering guidelines: [directives_ordering](https://dart-lang.github.io/linter/lints/directives_ordering.html).

### DO place “dart:” imports before other imports.

```dart
good
import 'dart:async';
import 'dart:html';

import 'package:bar/bar.dart';
import 'package:foo/foo.dart';
```

### DO place “package:” imports before relative imports.

```dart
good
import 'package:bar/bar.dart';
import 'package:foo/foo.dart';

import 'util.dart';
```

### DO specify exports in a separate section after all imports.

```dart
good
import 'src/error.dart';
import 'src/foo_bar.dart';

export 'src/error.dart';
```

```dart
bad
import 'src/error.dart';
export 'src/error.dart';
import 'src/foo_bar.dart';
```

### DO sort sections alphabetically.

```dart
good
import 'package:bar/bar.dart';
import 'package:foo/foo.dart';

import 'foo.dart';
import 'foo/foo.dart';
```

```dart
bad
import 'package:foo/foo.dart';
import 'package:bar/bar.dart';

import 'foo/foo.dart';
import 'foo.dart';
```

## Formatting

Like many languages, Dart ignores whitespace. However, humans don’t. Having a consistent whitespace style helps ensure that human readers see code the same way the compiler does.

### DO format your code using `dart format`.

Formatting is tedious work and is particularly time-consuming during refactoring. Fortunately, you don’t have to worry about it. We provide a sophisticated automated code formatter called [dart format](https://dart.dev/tools/dart-format) that does it for you. We have [some documentation](https://github.com/dart-lang/dart_style/wiki/Formatting-Rules) on the rules it applies, but the official whitespace-handling rules for Dart are whatever `dart format` produces.

The remaining formatting guidelines are for the few things `dart format` cannot fix for you.

### CONSIDER changing your code to make it more formatter-friendly.

The formatter does the best it can with whatever code you throw at it, but it can’t work miracles. If your code has particularly long identifiers, deeply nested expressions, a mixture of different kinds of operators, etc. the formatted output may still be hard to read.

When that happens, reorganize or simplify your code. Consider shortening a local variable name or hoisting out an expression into a new local variable. In other words, make the same kinds of modifications that you’d make if you were formatting the code by hand and trying to make it more readable. Think of `dart format` as a partnership where you work together, sometimes iteratively, to produce beautiful code.

### AVOID lines longer than 80 characters.

Readability studies show that long lines of text are harder to read because your eye has to travel farther when moving to the beginning of the next line. This is why newspapers and magazines use multiple columns of text.

If you really find yourself wanting lines longer than 80 characters, our experience is that your code is likely too verbose and could be a little more compact. The main offender is usually `VeryLongCamelCaseClassNames`. Ask yourself, “Does each word in that type name tell me something critical or prevent a name collision?” If not, consider omitting it.

Note that `dart format` does 99% of this for you, but the last 1% is you. It does not split long string literals to fit in 80 columns, so you have to do that manually.

**Exception**: When a URI or file path occurs in a comment or string (usually in an import or export), it may remain whole even if it causes the line to go over 80 characters. This makes it easier to search source files for a path.

**Exception**: Multi-line strings can contain lines longer than 80 characters because newlines are significant inside the string and splitting the lines into shorter ones can alter the program.

### DO use curly braces for all flow control statements.

Doing so avoids the [dangling else](https://en.wikipedia.org/wiki/Dangling_else) problem.

```dart
good
if (isWeekDay) {
  print('Bike to work!');
} else {
  print('Go dancing or read a book!');
}
```

**Exception**: When you have an `if` statement with no `else` clause and the whole `if` statement fits on one line, you can omit the braces if you prefer:

```dart
good
if (arg == null) return defaultValue;
```

If the body wraps to the next line, though, use braces:

```dart
good
if (overflowChars != other.overflowChars) {
  return overflowChars < other.overflowChars;
}
```

```dart
bad
if (overflowChars != other.overflowChars)
  return overflowChars < other.overflowChars;
```

# Effective Dart: Documentation

It’s easy to think your code is obvious today without realizing how much you rely on context already in your head. People new to your code, and even your forgetful future self won’t have that context. A concise, accurate comment only takes a few seconds to write but can save one of those people hours of time.

We all know code should be self-documenting and not all comments are helpful. But the reality is that most of us don’t write as many comments as we should. It’s like exercise: you technically can do too much, but it’s a lot more likely that you’re doing too little. Try to step it up.

## Comments

The following tips apply to comments that you don’t want included in the generated documentation.

### DO format comments like sentences.

```dart
good
// Not if there is nothing before it.
if (_chunks.isEmpty) return false;
```

Capitalize the first word unless it’s a case-sensitive identifier. End it with a period (or “!” or “?”, I suppose). This is true for all comments: doc comments, inline stuff, even TODOs. Even if it’s a sentence fragment.

### DON’T use block comments for documentation.

```dart
good
void greet(String name) {
  // Assume we have a valid name.
  print('Hi, $name!');
}
```

```dart
bad
void greet(String name) {
  /* Assume we have a valid name. */
  print('Hi, $name!');
}
```

You can use a block comment (/* ... */) to temporarily comment out a section of code, but all other comments should use //.

### Doc comments

Doc comments are especially handy because [dartdoc](https://github.com/dart-lang/dartdoc) parses them and generates [beautiful doc pages](https://api.dart.dev/stable/2.14.3/index.html) from them. A doc comment is any comment that appears before a declaration and uses the special /// syntax that dartdoc looks for.

### DO use /// doc comments to document members and types.

Using a doc comment instead of a regular comment enables [dartdoc](https://github.com/dart-lang/dartdoc) to find it and generate documentation for it.

```dart
good
/// The number of characters in this chunk when unsplit.
int get length => ...
```

```dart
bad
// The number of characters in this chunk when unsplit.
int get length => ...
```

For historical reasons, dartdoc supports two syntaxes of doc comments: /// (“C# style”) and /** ... */ (“JavaDoc style”). We prefer /// because it’s more compact. /** and */ add two content-free lines to a multiline doc comment. The /// syntax is also easier to read in some situations, such as when a doc comment contains a bulleted list that uses * to mark list items.

If you stumble onto code that still uses the JavaDoc style, consider cleaning it up.

### PREFER writing doc comments for public APIs.

You don’t have to document every single library, top-level variable, type, and member, but you should document most of them.

### CONSIDER writing a library-level doc comment.

Unlike languages like Java where the class is the only unit of program organization, in Dart, a library is itself an entity that users work with directly, import, and think about. That makes the `library` directive a great place for documentation that introduces the reader to the main concepts and functionality provided within. Consider including:

- A single-sentence summary of what the library is for.
- Explanations of terminology used throughout the library.
- A couple of complete code samples that walk through using the API.
- Links to the most important or most commonly used classes and functions.
- Links to external references on the domain the library is concerned with.

You document a library by placing a doc comment right above the `library` directive at the start of the file. If the library doesn’t have a `library` directive, you can add one just to hang the doc comment off of it.

### CONSIDER writing doc comments for private APIs.

Doc comments aren’t just for external consumers of your library’s public API. They can also be helpful for understanding private members that are called from other parts of the library.

### DO start doc comments with a single-sentence summary.

Start your doc comment with a brief, user-centric description ending with a period. A sentence fragment is often sufficient. Provide just enough context for the reader to orient themselves and decide if they should keep reading or look elsewhere for the solution to their problem.

```dart
good
/// Deletes the file at [path] from the file system.
void delete(String path) {
  ...
}
```

```dart
bad
/// Depending on the state of the file system and the user's permissions,
/// certain operations may or may not be possible. If there is no file at
/// [path] or it can't be accessed, this function throws either [IOError]
/// or [PermissionError], respectively. Otherwise, this deletes the file.
void delete(String path) {
  ...
}
```

### DO separate the first sentence of a doc comment into its own paragraph.
Add a blank line after the first sentence to split it out into its own paragraph. If more than a single sentence of explanation is useful, put the rest in later paragraphs.

This helps you write a tight first sentence that summarizes the documentation. Also, tools like dartdoc use the first paragraph as a short summary in places like lists of classes and members.

```dart
/// Deletes the file at [path].
///
/// Throws an [IOError] if the file could not be found. Throws a
/// [PermissionError] if the file is present but could not be deleted.
void delete(String path) {
  ...
}
```

```dart
bad
/// Deletes the file at [path]. Throws an [IOError] if the file could not
/// be found. Throws a [PermissionError] if the file is present but could
/// not be deleted.
void delete(String path) {
  ...
}
```

### AVOID redundancy with the surrounding context.

The reader of a class’s doc comment can clearly see the name of the class, what interfaces it implements, etc. When reading docs for a member, the signature is right there, and the enclosing class is obvious. None of that needs to be spelled out in the doc comment. Instead, focus on explaining what the reader doesn’t already know.

```dart
good
class RadioButtonWidget extends Widget {
  /// Sets the tooltip to [lines], which should have been word wrapped using
  /// the current font.
  void tooltip(List<String> lines) {
    ...
  }
}
```

```dart
bad
class RadioButtonWidget extends Widget {
  /// Sets the tooltip for this radio button widget to the list of strings in
  /// [lines].
  void tooltip(List<String> lines) {
    ...
  }
}
```

If you really don’t have anything interesting to say that can’t be inferred from the declaration itself, then omit the doc comment. It’s better to say nothing than waste a reader’s time telling them something they already know.

### PREFER starting function or method comments with third-person verbs.

The doc comment should focus on what the code does.

```dart
good
/// Returns `true` if every element satisfies the [predicate].
bool all(bool predicate(T element)) => ...

/// Starts the stopwatch if not already running.
void start() {
  ...
}
```

### PREFER starting variable, getter, or setter comments with noun phrases.

The doc comment should stress what the property is. This is true even for getters which may do calculation or other work. What the caller cares about is the result of that work, not the work itself.

```dart
good
/// The current day of the week, where `0` is Sunday.
int weekday;

/// The number of checked buttons on the page.
int get checkedCount => ...
```

If a property has both a getter and a setter, then create a doc comment for only one of them. Dartdoc treats the getter and setter like a single field, and if both the getter and the setter have doc comments, then dartdoc discards the setter’s doc comment.

### PREFER starting library or type comments with noun phrases.

Doc comments for classes are often the most important documentation in your program. They describe the type’s invariants, establish the terminology it uses, and provide context to the other doc comments for the class’s members. A little extra effort here can make all of the other members simpler to document.

```dart
good
/// A chunk of non-breaking output text terminated by a hard or soft newline.
///
/// ...
class Chunk { ... }
```

### CONSIDER including code samples in doc comments.

```dart
good
/// Returns the lesser of two numbers.
///
///
/// min(5, 3) == 3
///
num min(num a, num b) => ...
```

Humans are great at generalizing from examples, so even a single code sample makes an API easier to learn.

### DO use square brackets in doc comments to refer to in-scope identifiers.

If you surround things like variable, method, or type names in square brackets, then dartdoc looks up the name and links to the relevant API docs. Parentheses are optional, but can make it clearer when you’re referring to a method or constructor.

```dart
good
/// Throws a [StateError] if ...
/// similar to [anotherMethod()], but ...
```

To link to a member of a specific class, use the class name and member name, separated by a dot:

```dart
good
/// Similar to [Duration.inDays], but handles fractional days.
```

The dot syntax can also be used to refer to named constructors:

```dart
good
/// To create a point from polar coordinates, use [Point.polar()].
```

### DO use prose to explain parameters, return values, and exceptions.

Other languages use verbose tags and sections to describe what the parameters and returns of a method are.

```dart
bad
/// Defines a flag with the given name and abbreviation.
///
/// @param name The name of the flag.
/// @param abbr The abbreviation for the flag.
/// @returns The new flag.
/// @throws ArgumentError If there is already an option with
///     the given name or abbreviation.
Flag addFlag(String name, String abbr) => ...
```

The convention in Dart is to integrate that into the description of the method and highlight parameters using square brackets.

```dart
good
/// Defines a flag.
///
/// Throws an [ArgumentError] if there is already an option named [name] or
/// there is already an option using abbreviation [abbr]. Returns the new flag.
Flag addFlag(String name, String abbr) => ...

```

### DO put doc comments before metadata annotations.

```dart
good
/// A button that can be flipped on and off.
@Component(selector: 'toggle')
class ToggleComponent {}
```

```dart
bad
@Component(selector: 'toggle')
/// A button that can be flipped on and off.
class ToggleComponent {}
```

### Markdown

You are allowed to use most [markdown](https://daringfireball.net/projects/markdown/) formatting in your doc comments and dartdoc will process it accordingly using [the markdown package](https://pub.dev/packages/markdown).

There are tons of guides out there already to introduce you to Markdown. Its universal popularity is why we chose it. Here’s just a quick example to give you a flavor of what’s supported:

```dart
/// This is a paragraph of regular text.
///
/// This sentence has *two* _emphasized_ words (italics) and **two**
/// __strong__ ones (bold).
///
/// A blank line creates a separate paragraph. It has some `inline code`
/// delimited using backticks.
///
/// * Unordered lists.
/// * Look like ASCII bullet lists.
/// * You can also use `-` or `+`.
///
/// 1. Numbered lists.
/// 2. Are, well, numbered.
/// 1. But the values don't matter.
///
///     * You can nest lists too.
///     * They must be indented at least 4 spaces.
///     * (Well, 5 including the space after `///`.)
///
/// Code blocks are fenced in triple backticks:
///
/// this.code
///     .will
///     .retain(its, formatting);
/// 
///
/// The code language (for syntax highlighting) defaults to Dart. You can
/// specify it by putting the name of the language after the opening backticks:
///
/// 
/// <h1>HTML is magical!</h1>
/// 
///
/// Links can be:
///
/// * https://www.just-a-bare-url.com
/// * [with the URL inline](https://google.com)
/// * [or separated out][ref link]
///
/// [ref link]: https://google.com
///
/// # A Header
///
/// ## A subheader
///
/// ### A subsubheader
///
/// #### If you need this many levels of headers, you're doing it wrong
```

### AVOID using markdown excessively.

When in doubt, format less. Formatting exists to illuminate your content, not replace it. Words are what matter.

### AVOID using HTML for formatting.

It may be useful to use it in rare cases for things like tables, but in almost all cases, if it’s too complex to express in Markdown, you’re better off not expressing it.

### PREFER backtick fences for code blocks.

Markdown has two ways to indicate a block of code: indenting the code four spaces on each line, or surrounding it in a pair of triple-backtick “fence” lines. The former syntax is brittle when used inside things like Markdown lists where indentation is already meaningful or when the code block itself contains indented code.

The backtick syntax avoids those indentation woes, lets you indicate the code’s language, and is consistent with using backticks for inline code.

```dart
good
/// You can use [CodeBlockExample] like this:
///
///
/// var example = CodeBlockExample();
/// print(example.isItGreat); // "Yes."
/// 
```

```dart
bad
/// You can use [CodeBlockExample] like this:
///
///     var example = CodeBlockExample();
///     print(example.isItGreat); // "Yes."
```

### Writing

We think of ourselves as programmers, but most of the characters in a source file are intended primarily for humans to read. English is the language we code in to modify the brains of our coworkers. As for any programming language, it’s worth putting effort into improving your proficiency.

This section lists a few guidelines for our docs. You can learn more about best practices for technical writing, in general, from articles such as [Technical writing style](https://en.wikiversity.org/wiki/Technical_writing/Style).

### PREFER brevity.

Be clear and precise, but also terse.

### AVOID abbreviations and acronyms unless they are obvious.

Many people don’t know what “i.e.”, “e.g.” and “et al.” mean. That acronym that you’re sure everyone in your field knows may not be as widely known as you think.

### PREFER using “this” instead of “the” to refer to a member’s instance.

When documenting a member for a class, you often need to refer back to the object the member is being called on. Using “the” can be ambiguous.

```dart
good
class Box {
  /// The value this wraps.
  Object? _value;

  /// True if this box contains a value.
  bool get hasValue => _value != null;
```

# Effective Dart: Usage

You can use these guidelines every day in the bodies of your Dart code. _Users_ of your library may not be able to tell that you’ve internalized the ideas here, but _maintainers_ of it sure will.

### Libraries

These guidelines help you compose your program out of multiple files in a consistent, maintainable way. To keep these guidelines brief, they use “import” to cover `import` and `export` directives. The guidelines apply equally to both.

### DO use strings in `part of` directives.

Many Dart developers avoid using `part` entirely. They find it easier to reason about their code when each library is a single file. If you do choose to use part to split `part` of a library out into another file, Dart requires the other file to in turn indicate which library it’s a part of. For legacy reasons, Dart allows this `part of` directive to use the name of the library it’s a part of. That makes it harder for tools to physically find the main library file, and can make it ambiguous which library the part is actually part of.

The preferred, modern syntax is to use a URI string that points directly to the library file, just like you use in other directives. If you have some library, `my_library.dart`, that contains:

```dart
library my_library;

part 'some/other/file.dart';
```

Then the part file should look like:

```dart
good
part of '../../my_library.dart';
```

and not

```dart
bad
part of my_library;
```

### DON’T import libraries that are inside the src directory of another package.

The src directory under `lib` [is specified](https://dart.dev/tools/pub/package-layout) to contain libraries private to the package’s own implementation. The way package maintainers version their package takes this convention into account. They are free to make sweeping changes to code under src without it being a breaking change to the package.

That means that if you import some other package’s private library, a minor, theoretically non-breaking point release of that package could break your code.

### DON’T allow an import path to reach into or out of `lib`.

A `package`: import lets you access a library inside a package’s `lib` directory without having to worry about where the package is stored on your computer. For this to work, you cannot have imports that require the `lib` to be in some location on disk relative to other files. In other words, a relative import path in a file inside lib can’t reach out and access a file outside of the `lib` directory, and a library outside of `lib` can’t use a relative path to reach into the `lib` directory. Doing either leads to confusing errors and broken programs.

For example, say your directory structure looks like this:

```dart
my_package
└─ lib
   └─ api.dart
   test
   └─ api_test.dart
```

And say `api_test.dart` imports `api.dart` in two ways:

```dart
bad
import 'package:my_package/api.dart';
import '../lib/api.dart';
```

Dart thinks those are imports of two completely unrelated libraries. To avoid confusing Dart and yourself, follow these two rules:

- Don’t use `/lib/` in import paths.
- Don’t use `../` to escape the `lib` directory.

Instead, when you need to reach into a package’s `lib` directory (even from the same package’s `test` directory or any other top-level directory), use a `package`: import.

```dart
good
import 'package:my_package/api.dart';
```

A package should never reach out of its lib directory and import libraries from other places in the package.

### PREFER relative import paths.

Whenever the previous rule doesn’t come into play, follow this one. When an import does not reach across lib, prefer using relative imports. They’re shorter. For example, say your directory structure looks like this:

```dart
my_package
└─ lib
   ├─ src
   │  └─ stuff.dart
   │  └─ utils.dart
   └─ api.dart
   test
   │─ api_test.dart
   └─ test_utils.dart
```

Here is how the various libraries should import each other:

**lib/api.dart:**

```dart
good
import 'src/stuff.dart';
import 'src/utils.dart';
```

**lib/src/utils.dart:**

```dart
import '../api.dart';
import 'stuff.dart';
```

**test/api_test.dart:**

```dart
import 'package:my_package/api.dart'; // Don't reach into 'lib'.

import 'test_utils.dart'; // Relative within 'test' is fine.
```

## Null

### DON’T explicitly initialize variables to null.

If a variable has a non-nullable type, Dart reports a compile error if you try to use it before it has been definitely initialized. If the variable is nullable, then it is implicitly initialized to `null` for you. There’s no concept of “uninitialized memory” in Dart and no need to explicitly initialize a variable to `null` to be “safe”.

```dart
good
Item? bestDeal(List<Item> cart) {
  Item? bestItem;

  for (var item in cart) {
    if (bestItem == null || item.price < bestItem.price) {
      bestItem = item;
    }
  }

  return bestItem;
}
```

```dart
bad
Item? bestDeal(List<Item> cart) {
  Item? bestItem = null;

  for (var item in cart) {
    if (bestItem == null || item.price < bestItem.price) {
      bestItem = item;
    }
  }

  return bestItem;
}
```

### DON’T use an explicit default value of null.

If you make a nullable parameter optional but don’t give it a default value, the language implicitly uses null as the default, so there’s no need to write it.

```dart
good
void error([String? message]) {
  stderr.write(message ?? '\n');
}
```

```dart
bad
void error([String? message = null]) {
  stderr.write(message ?? '\n');
}
```

### PREFER using ?? to convert null to a boolean value.

This rule applies when an expression can evaluate to `true`, `false`, or `null`, and you need to pass the result to something that expects a non-nullable boolean value. A common case is using the result of a null-aware method call as a condition. You can “convert” `null` to `true` or `false` using`==, but we recommend using `??`:

```dart
good
// If you want null to be false:
if (optionalThing?.isEnabled ?? false) {
  print('Have enabled thing.');
}

// If you want null to be true:
if (optionalThing?.isEnabled ?? true) {
  print('Have enabled thing or nothing.');
}
```

```dart
bad
// If you want null to be false:
if (optionalThing?.isEnabled == true) {
  print('Have enabled thing.');
}

// If you want null to be true:
if (optionalThing?.isEnabled != false) {
  print('Have enabled thing or nothing.');
}
```

Both operations produce the same result and do the right thing, but `??` is preferred for three main reasons:

- The `??` operator signals that the code has something to do with `null`.
- The `==` true looks like a common mistake where the equality operator is redundant and can be removed. That’s true when the boolean expression on the left will not produce `null`, but not when it can.
- The `??` false and `??` true clearly show what value will be used when the expression is `null`. With `==` true, you have to think through the boolean logic to realize that means that a `null` gets converted to false.


**Exception**: Using a null-aware operator on a variable inside a condition doesn’t promote the variable to a non-nullable type. If you want the variable to be promoted inside the body of the if statement, it might be better to use an explicit `!= null` check instead of `?.` followed by `??`:

```dart
good
int measureMessage(String? message) {
  if (message != null && message.isNotEmpty) {
    // message is promoted to String.
    return message.length;
  }

  return 0;
}
```

```dart
bad
int measureMessage(String? message) {
  if (message?.isNotEmpty ?? false) {
    // message is not promoted to String.
    return message!.length;
  }

  return 0;
}
```

### AVOID late variables if you need to check whether they are initialized.

Dart offers no way to tell if a `late` variable has been initialized or assigned to. If you access it, it either immediately runs the initializer (if it has one) or throws an exception. Sometimes you have some state that’s lazily initialized where `late` might be a good fit, but you also need to be able to tell if the initialization has happened yet.

Although you could detect initialization by storing the state in a `late` variable and having a separate boolean field that tracks whether the variable has been set, that’s redundant because Dart internally maintains the initialized status of the `late` variable. Instead, it’s usually clearer to make the variable non-late and nullable. Then you can see if the variable has been initialized by checking for `null`.

Of course, if `null` is a valid initialized value for the variable, then it probably does make sense to have a separate boolean field.

### CONSIDER copying a nullable field to a local variable to enable type promotion.

Checking that a nullable variable is not equal to null promotes the variable to a non-nullable type. That lets you access members on the variable and pass it to functions expecting a non-nullable type. Unfortunately, promotion is only sound for local variables and parameters, so fields and top-level variables aren’t promoted.

One pattern to work around this is to copy the field’s value to a local variable. Null checks on that variable do promote, so you can safely treat it as non-nullable.

```dart
good
class UploadException {
  final Response? response;

  UploadException([this.response]);

  @override
  String toString() {
    var response = this.response;
    if (response != null) {
      return 'Could not complete upload to ${response.url} '
          '(error code ${response.errorCode}): ${response.reason}.';
    }

    return 'Could not upload (no response).';
  }
}
```

Copying to a local variable can be cleaner and safer than using ! every place the field or top-level variable is used:

```dart
bad
class UploadException {
  final Response? response;

  UploadException([this.response]);

  @override
  String toString() {
    if (response != null) {
      return 'Could not complete upload to ${response!.url} '
          '(error code ${response!.errorCode}): ${response!.reason}.';
    }

    return 'Could not upload (no response).';
  }
}
```

Be careful when using a local copy. If you need to write back to the field, then make sure you do so, and don’t just write to the local variable. Also, if the field might change while the local is still in scope, then the local might have a stale value. Sometimes it’s best to simply use ! on the field.

## Strings

Here are some best practices to keep in mind when composing strings in Dart.

### DO use adjacent strings to concatenate string literals.

If you have two string literals—not values, but the actual quoted literal form—you do not need to use + to concatenate them. Just like in C and C++, simply placing them next to each other does it. This is a good way to make a single long string that doesn’t fit on one line.

```dart
good
raiseAlarm(
    'ERROR: Parts of the spaceship are on fire. Other '
    'parts are overrun by martians. Unclear which are which.');
```

```dart
bad
raiseAlarm('ERROR: Parts of the spaceship are on fire. Other ' +
    'parts are overrun by martians. Unclear which are which.');
```

### PREFER using interpolation to compose strings and values.

If you’re coming from other languages, you’re used to using long chains of + to build a string out of literals and other values. That does work in Dart, but it’s almost always cleaner and shorter to use interpolation:

```dart
good
'Hello, $name! You are ${year - birth} years old.';
```

```dart
bad
'Hello, ' + name + '! You are ' + (year - birth).toString() + ' y...';
```

### AVOID using curly braces in interpolation when not needed.

If you’re interpolating a simple identifier not immediately followed by more alphanumeric text, the {} should be omitted.

```dart
good
var greeting = 'Hi, $name! I love your ${decade}s costume.';
```

```dart
bad
var greeting = 'Hi, ${name}! I love your ${decade}s costume.';
```

## Collections

Out of the box, Dart supports four collection types: lists, maps, queues, and sets. The following best practices apply to collections.

### DO use collection literals when possible.

Dart has three core collection types: List, Map, and Set. The Map and Set classes have unnamed constructors like most classes do. But because these collections are used so frequently, Dart has nicer built-in syntax for creating them:

```dart
good
var points = <Point>[];
var addresses = <String, Address>{};
var counts = <int>{};
```

```dart
bad
var addresses = Map<String, Address>();
var counts = Set<int>();
```

Note that this guideline doesn’t apply to the named constructors for those classes. `List.from(), Map.fromIterable()`, and friends all have their uses. (The List class also has an unnamed constructor, but it is prohibited in null safe Dart.)

Collection literals are particularly powerful in Dart because they give you access to the [spread operator](https://dart.dev/guides/language/language-tour#spread-operator) for including the contents of other collections, and [if and for](https://dart.dev/guides/language/language-tour#collection-operators) for performing control flow while building the contents:

```dart
good
var arguments = [
  ...options,
  command,
  ...?modeFlags,
  for (var path in filePaths)
    if (path.endsWith('.dart'))
      path.replaceAll('.dart', '.js')
];
```

```dart
bad
var arguments = <String>[];
arguments.addAll(options);
arguments.add(command);
if (modeFlags != null) arguments.addAll(modeFlags);
arguments.addAll(filePaths
    .where((path) => path.endsWith('.dart'))
    .map((path) => path.replaceAll('.dart', '.js')));
```

### DON’T use .length to see if a collection is empty.

The [Iterable](https://api.dart.dev/stable/dart-core/Iterable-class.html) contract does not require that a collection know its length or be able to provide it in constant time. Calling `.length` just to see if the collection contains anything can be painfully slow.

Instead, there are faster and more readable getters: `.isEmpty` and `.isNotEmpty`. Use the one that doesn’t require you to negate the result.

```dart
good
if (lunchBox.isEmpty) return 'so hungry...';
if (words.isNotEmpty) return words.join(' ');
```

```dart
bad
if (lunchBox.length == 0) return 'so hungry...';
if (!words.isEmpty) return words.join(' ');
```

### AVOID using `Iterable.forEach()` with a function literal.

`forEach()` functions are widely used in JavaScript because the built in for-in loop doesn’t do what you usually want. In Dart, if you want to iterate over a sequence, the idiomatic way to do that is using a loop.

```dart
good
for (var person in people) {
  ...
}
```

```dart
bad
people.forEach((person) {
  ...
});
```

Note that this guideline specifically says “function literal”. If you want to invoke some already existing function on each element, forEach() is fine.

```dart
good
people.forEach(print);
```

Also note that it’s always OK to use `Map.forEach()`. Maps aren’t iterable, so this guideline doesn’t apply.

### DON’T use `List.from()` unless you intend to change the type of the result.

Given an Iterable, there are two obvious ways to produce a new List that contains the same elements:

```dart
var copy1 = iterable.toList();
var copy2 = List.from(iterable);
```

The obvious difference is that the first one is shorter. The important difference is that the first one preserves the type argument of the original object:

```dart
good
// Creates a List<int>:
var iterable = [1, 2, 3];

// Prints "List<int>":
print(iterable.toList().runtimeType);
```

```dart
bad
// Creates a List<int>:
var iterable = [1, 2, 3];

// Prints "List<dynamic>":
print(List.from(iterable).runtimeType);
```

If you want to change the type, then calling `List.from()` is useful:

```dart
good
var numbers = [1, 2.3, 4]; // List<num>.
numbers.removeAt(1); // Now it only contains integers.
var ints = List<int>.from(numbers);
```

But if your goal is just to copy the iterable and preserve its original type, or you don’t care about the type, then use toList().

### DO use whereType() to filter a collection by type.

Let’s say you have a list containing a mixture of objects, and you want to get just the integers out of it. You could use where() like this:

```dart
bad
var objects = [1, 'a', 2, 'b', 3];
var ints = objects.where((e) => e is int);
```

This is verbose, but, worse, it returns an iterable whose type probably isn’t what you want. In the example here, it returns an `Iterable<Object>` even though you likely want an `Iterable<int>` since that’s the type you’re filtering it to.

Sometimes you see code that “corrects” the above error by adding `cast()`:

```dart
bad
var objects = [1, 'a', 2, 'b', 3];
var ints = objects.where((e) => e is int).cast<int>();
```

That’s verbose and causes two wrappers to be created, with two layers of indirection and redundant runtime checking. Fortunately, the core library has the `whereType()` method for this exact use case:

```dart
good
var objects = [1, 'a', 2, 'b', 3];
var ints = objects.whereType<int>();
```

Using `whereType()` is concise, produces an [Iterable](https://api.dart.dev/stable/dart-core/Iterable-class.html) of the desired type, and has no unnecessary levels of wrapping.

### DON’T use `cast()` when a nearby operation will do.

Often when you’re dealing with an iterable or stream, you perform several transformations on it. At the end, you want to produce an object with a certain type argument. Instead of tacking on a call to `cast()`, see if one of the existing transformations can change the type.

If you’re already calling `toList()`, replace that with a call to [List<T>.from()](https://api.dart.dev/stable/dart-core/List/List.from.html) where T is the type of resulting list you want.

```dart
good
var stuff = <dynamic>[1, 2];
var ints = List<int>.from(stuff);
```

```dart
bad
var stuff = <dynamic>[1, 2];
var ints = stuff.toList().cast<int>();
```

If you are calling `map()`, give it an explicit type argument so that it produces an iterable of the desired type. Type inference often picks the correct type for you based on the function you pass to `map()`, but sometimes you need to be explicit.

```dart
good
var stuff = <dynamic>[1, 2];
var reciprocals = stuff.map<double>((n) => 1 / n);
```

```dart
bad
var stuff = <dynamic>[1, 2];
var reciprocals = stuff.map((n) => 1 / n).cast<double>();
```

### AVOID using cast().

This is the softer generalization of the previous rule. Sometimes there is no nearby operation you can use to fix the type of some object. Even then, when possible avoid using `cast()` to “change” a collection’s type.

Prefer any of these options instead:

- **Create it with the right type**. Change the code where the collection is first created so that it has the right type.
- **Cast the elements on access**. If you immediately iterate over the collection, cast each element inside the iteration.
- **Eagerly cast using `List.from()`**. If you’ll eventually access most of the elements in the collection, and you don’t need the object to be backed by the original live object, convert it using `List.from()`.

The `cast()` method returns a lazy collection that checks the element type on every operation. If you perform only a few operations on only a few elements, that laziness can be good. But in many cases, the overhead of lazy validation and of wrapping outweighs the benefits.

Here is an example of **creating it with the right type**:

```dart
good
List<int> singletonList(int value) {
  var list = <int>[];
  list.add(value);
  return list;
}
```

```dart
bad
List<int> singletonList(int value) {
  var list = []; // List<dynamic>.
  list.add(value);
  return list.cast<int>();
}
```

Here is **casting each element on access**:

```dart
good
void printEvens(List<Object> objects) {
  // We happen to know the list only contains ints.
  for (var n in objects) {
    if ((n as int).isEven) print(n);
  }
}
```

```dart
bad
void printEvens(List<Object> objects) {
  // We happen to know the list only contains ints.
  for (var n in objects.cast<int>()) {
    if (n.isEven) print(n);
  }
}
```

Here is **casting eagerly using `List.from()`**:

```dart
good
int median(List<Object> objects) {
  // We happen to know the list only contains ints.
  var ints = List<int>.from(objects);
  ints.sort();
  return ints[ints.length ~/ 2];
}
```

```dart
bad
int median(List<Object> objects) {
  // We happen to know the list only contains ints.
  var ints = objects.cast<int>();
  ints.sort();
  return ints[ints.length ~/ 2];
}
```

These alternatives don’t always work, of course, and sometimes cast() is the right answer. But consider that method a little risky and undesirable—it can be slow and may fail at runtime if you aren’t careful.

## Functions

In Dart, even functions are objects. Here are some best practices involving functions.

### DO use a function declaration to bind a function to a name.

Modern languages have realized how useful local nested functions and closures are. It’s common to have a function defined inside another one. In many cases, this function is used as a callback immediately and doesn’t need a name. A function expression is great for that.

But, if you do need to give it a name, use a function declaration statement instead of binding a lambda to a variable.

```dart
good
void main() {
  void localFunction() {
    ...
  }
}
```

```dart
bad
void main() {
  var localFunction = () {
    ...
  };
}
```

### DON’T create a lambda when a tear-off will do.

If you refer to a method on an object but omit the parentheses, Dart gives you a “tear-off”—a closure that takes the same parameters as the method and invokes it when you call it.

If you have a function that invokes a method with the same arguments as are passed to it, you don’t need to manually wrap the call in a lambda.

```dart
good
names.forEach(print);
```

```dart
bad
names.forEach((name) {
  print(name);
});
```

### DO use = to separate a named parameter from its default value.

For legacy reasons, Dart allows both : and = as the default value separator for named parameters. For consistency with optional positional parameters, use =.

```dart
good
void insert(Object item, {int at = 0}) { ... }
```

```dart
bad
void insert(Object item, {int at: 0}) { ... }
```

## Variables

The following best practices describe how to best use variables in Dart.

### DO follow a consistent rule for `var` and `final` on local variables.

Most local variables shouldn’t have type annotations and should be declared using just var or final. There are two rules in wide use for when to use one or the other:

- Use `final` for local variables that are not reassigned and `var` for those that are.
- Use `var` for all local variables, even ones that aren’t reassigned. Never use `final` for locals. (Using final for fields and top-level variables is still encouraged, of course.)

Either rule is acceptable, but pick one and apply it consistently throughout your code. That way when a reader sees var, they know whether it means that the variable is assigned later in the function.

### AVOID storing what you can calculate.

When designing a class, you often want to expose multiple views into the same underlying state. Often you see code that calculates all of those views in the constructor and then stores them:

```dart
bad
class Circle {
  double radius;
  double area;
  double circumference;

  Circle(double radius)
      : radius = radius,
        area = pi * radius * radius,
        circumference = pi * 2.0 * radius;
}
```

This code has two things wrong with it. First, it’s likely wasting memory. The area and circumference, strictly speaking, are caches. They are stored calculations that we could recalculate from other data we already have. They are trading increased memory for reduced CPU usage. Do we know we have a performance problem that merits that trade-off?

Worse, the code is wrong. The problem with caches is invalidation—how do you know when the cache is out of date and needs to be recalculated? Here, we never do, even though `radius` is mutable. You can assign a different value and the `area` and `circumference` will retain their previous, now incorrect values.

To correctly handle cache invalidation, we would need to do this:

```dart
bad
class Circle {
  double _radius;
  double get radius => _radius;
  set radius(double value) {
    _radius = value;
    _recalculate();
  }

  double _area = 0.0;
  double get area => _area;

  double _circumference = 0.0;
  double get circumference => _circumference;

  Circle(this._radius) {
    _recalculate();
  }

  void _recalculate() {
    _area = pi * _radius * _radius;
    _circumference = pi * 2.0 * _radius;
  }
}
```

That’s an awful lot of code to write, maintain, debug, and read. Instead, your first implementation should be:

```dart
good
class Circle {
  double radius;

  Circle(this.radius);

  double get area => pi * radius * radius;
  double get circumference => pi * 2.0 * radius;
}
```

This code is shorter, uses less memory, and is less error-prone. It stores the minimal amount of data needed to represent the circle. There are no fields to get out of sync because there is only a single source of truth.

In some cases, you may need to cache the result of a slow calculation, but only do that after you know you have a performance problem, do it carefully, and leave a comment explaining the optimization.

## Members

In Dart, objects have members which can be functions (methods) or data (instance variables). The following best practices apply to an object’s members.

### DON’T wrap a field in a getter and setter unnecessarily.

In Java and C#, it’s common to hide all fields behind getters and setters (or properties in C#), even if the implementation just forwards to the field. That way, if you ever need to do more work in those members, you can without needing to touch the callsites. This is because calling a getter method is different than accessing a field in Java, and accessing a property isn’t binary-compatible with accessing a raw field in C#.

Dart doesn’t have this limitation. Fields and getters/setters are completely indistinguishable. You can expose a field in a class and later wrap it in a getter and setter without having to touch any code that uses that field.

```dart
good
class Box {
  Object? contents;
}
```

```dart
bad
class Box {
  Object? _contents;
  Object? get contents => _contents;
  set contents(Object? value) {
    _contents = value;
  }
}
```

### PREFER using a `final` field to make a read-only property.

If you have a field that outside code should be able to see but not assign to, a simple solution that works in many cases is to simply mark it `final`.

```dart
good
class Box {
  final contents = [];
}
```

```dart
bad
class Box {
  Object? _contents;
  Object? get contents => _contents;
}
```

Of course, if you need to internally assign to the field outside of the constructor, you may need to do the “private field, public getter” pattern, but don’t reach for that until you need to.

### CONSIDER using => for simple members.

In addition to using => for function expressions, Dart also lets you define members with it. That style is a good fit for simple members that just calculate and return a value.

```dart
good
double get area => (right - left) * (bottom - top);

String capitalize(String name) =>
    '${name[0].toUpperCase()}${name.substring(1)}';
```

People writing code seem to love =>, but it’s very easy to abuse it and end up with code that’s hard to read. If your declaration is more than a couple of lines or contains deeply nested expressions—cascades and conditional operators are common offenders—do yourself and everyone who has to read your code a favor and use a block body and some statements.

```dart
good
Treasure? openChest(Chest chest, Point where) {
  if (_opened.containsKey(chest)) return null;

  var treasure = Treasure(where);
  treasure.addAll(chest.contents);
  _opened[chest] = treasure;
  return treasure;
}
```

```dart
bad
Treasure? openChest(Chest chest, Point where) => _opened.containsKey(chest)
    ? null
    : _opened[chest] = (Treasure(where)..addAll(chest.contents));
```

You can also use => on members that don’t return a value. This is idiomatic when a setter is small and has a corresponding getter that uses =>.

```dart
num get x => center.x;
set x(num value) => center = Point(value, center.y);
```

### DON’T use this. except to redirect to a named constructor or to avoid shadowing.

JavaScript requires an explicit `this.` to refer to members on the object whose method is currently being executed, but Dart—like C++, Java, and C#—doesn’t have that limitation.

There are only two times you need to use `this.`. One is when a local variable with the same name shadows the member you want to access:

```dart
bad
class Box {
  Object? value;

  void clear() {
    this.update(null);
  }

  void update(Object? value) {
    this.value = value;
  }
}
```

```dart
good
class Box {
  Object? value;

  void clear() {
    update(null);
  }

  void update(Object? value) {
    this.value = value;
  }
}
```

The other time to use `this.` is when redirecting to a named constructor:

```dart
bad
class ShadeOfGray {
  final int brightness;

  ShadeOfGray(int val) : brightness = val;

  ShadeOfGray.black() : this(0);

  // This won't parse or compile!
  // ShadeOfGray.alsoBlack() : black();
}
```

```dart
good
class ShadeOfGray {
  final int brightness;

  ShadeOfGray(int val) : brightness = val;

  ShadeOfGray.black() : this(0);

  // But now it will!
  ShadeOfGray.alsoBlack() : this.black();
}
```

Note that constructor parameters never shadow fields in constructor initializer lists:

```dart
good
class Box extends BaseBox {
  Object? value;

  Box(Object? value)
      : value = value,
        super(value);
}
```

This looks surprising, but works like you want. Fortunately, code like this is relatively rare thanks to initializing formals.

### DO initialize fields at their declaration when possible.

If a field doesn’t depend on any constructor parameters, it can and should be initialized at its declaration. It takes less code and avoids duplication when the class has multiple constructors.

```dart
bad
class ProfileMark {
  final String name;
  final DateTime start;

  ProfileMark(this.name) : start = DateTime.now();
  ProfileMark.unnamed()
      : name = '',
        start = DateTime.now();
}
```

```dart
good
class ProfileMark {
  final String name;
  final DateTime start = DateTime.now();

  ProfileMark(this.name);
  ProfileMark.unnamed() : name = '';
}
```

Some fields can’t be initialized at their declarations because they need to reference `this` — to use other fields or call methods, for example. However, if the field is marked `late`, then the initializer can access `this`.

Of course, if a field depends on constructor parameters, or is initialized differently by different constructors, then `this` guideline does not apply.

## Constructors

The following best practices apply to declaring constructors for a class.

### DO use initializing formals when possible.

Many fields are initialized directly from a constructor parameter, like:

```dart
bad
class Point {
  double x, y;
  Point(double x, double y)
      : x = x,
        y = y;
}
```

We’ve got to type x four times here to define a field. We can do better:

```dart
good
class Point {
  double x, y;
  Point(this.x, this.y);
}
```

This `this.` syntax before a constructor parameter is called an “initializing formal”. You can’t always take advantage of it. Sometimes you want to have a named parameter whose name doesn’t match the name of the field you are initializing. But when you can use initializing formals, you should.

### DON’T use `late` when a constructor initializer list will do.

Sound null safety requires Dart to ensure that a non-nullable field is initialized before it can be read. Since fields can be read inside the constructor body, this means you get an error if you don’t initialize a non-nullable field before the body runs.

You can make this error go away by marking the field `late`. That turns the compile-time error into a runtime error if you access the field before it is initialized. That’s what you need in some cases, but often the right fix is to initialize the field in the constructor initializer list:

```dart
good
class Point {
  double x, y;
  Point.polar(double theta, double radius)
      : x = cos(theta) * radius,
        y = sin(theta) * radius;
}
```

```dart
bad
class Point {
  late double x, y;
  Point.polar(double theta, double radius) {
    x = cos(theta) * radius;
    y = sin(theta) * radius;
  }
}
```

The initializer list gives you access to constructor parameters and lets you initialize fields before they can be read. So, if it’s possible to use an initializer list, that’s better than making the field late and losing some static safety and performance.

### DO use ; instead of {} for empty constructor bodies.

In Dart, a constructor with an empty body can be terminated with just a semicolon. (In fact, it’s required for const constructors.)

```dart
good
class Point {
  double x, y;
  Point(this.x, this.y);
}
```

```dart
bad
class Point {
  double x, y;
  Point(this.x, this.y) {}
}
```

### DON'T use new

Dart 2 makes the new keyword optional. Even in Dart 1, its meaning was never clear because factory constructors mean a new invocation may still not actually return a new object.

The language still permits new in order to make migration less painful, but consider it deprecated and remove it from your code.

```dart
good
Widget build(BuildContext context) {
  return Row(
    children: [
      RaisedButton(
        child: Text('Increment'),
      ),
      Text('Click!'),
    ],
  );
}
```

```dart
bad
Widget build(BuildContext context) {
  return new Row(
    children: [
      new RaisedButton(
        child: new Text('Increment'),
      ),
      new Text('Click!'),
    ],
  );
}
```

### DON'T use `const` redundantly

In contexts where an expression must be constant, the `const` keyword is implicit, doesn’t need to be written, and shouldn’t. Those contexts are any expression inside:

- A const collection literal.
- A const constructor call
- A metadata annotation.
- The initializer for a const variable declaration.
- A switch case expression—the part right after `case` before the :, not the body of the case.

(Default values are not included in this list because future versions of Dart may support non-const default values.)

Basically, any place where it would be an error to write `new` instead of `const`, Dart 2 allows you to omit the `const`.

```dart
good
const primaryColors = [
  Color('red', [255, 0, 0]),
  Color('green', [0, 255, 0]),
  Color('blue', [0, 0, 255]),
];
```

```dart
bad
const primaryColors = const [
  const Color('red', const [255, 0, 0]),
  const Color('green', const [0, 255, 0]),
  const Color('blue', const [0, 0, 255]),
];
```

## Error handling

Dart uses exceptions when an error occurs in your program. The following best practices apply to catching and throwing exceptions.

### AVOID catches without on clauses.

A catch clause with no on qualifier catches anything thrown by the code in the try block. [Pokémon exception handling](https://blog.codinghorror.com/new-programming-jargon/) is very likely not what you want. Does your code correctly handle [StackOverflowError](https://api.dart.dev/stable/dart-core/StackOverflowError-class.html) or [OutOfMemoryError](https://api.dart.dev/stable/dart-core/OutOfMemoryError-class.html)? If you incorrectly pass the wrong argument to a method in that try block do you want to have your debugger point you to the mistake or would you rather that helpful [ArgumentError](https://api.dart.dev/stable/dart-core/ArgumentError-class.html) get swallowed? Do you want any `assert()` statements inside that code to effectively vanish since you’re catching the thrown [AssertionErrors](https://api.dart.dev/stable/2.14.3/dart-core/AssertionError-class.html)?

The answer is probably “no”, in which case you should filter the types you catch. In most cases, you should have an on clause that limits you to the kinds of runtime failures you are aware of and are correctly handling.

In rare cases, you may wish to catch any runtime error. This is usually in framework or low-level code that tries to insulate arbitrary application code from causing problems. Even here, it is usually better to catch [Exception](https://api.dart.dev/stable/dart-core/Exception-class.html) than to catch all types. Exception is the base class for all runtime errors and excludes errors that indicate programmatic bugs in the code.

### DON’T discard errors from catches without on clauses.

If you really do feel you need to catch everything that can be thrown from a region of code, do something with what you catch. Log it, display it to the user or rethrow it, but do not silently discard it.

### DO throw objects that implement Error only for programmatic errors.

The [Error](https://api.dart.dev/stable/dart-core/Error-class.html) class is the base class for programmatic errors. When an object of that type or one of its subinterfaces like [ArgumentError](https://api.dart.dev/stable/dart-core/ArgumentError-class.html) is thrown, it means there is a bug in your code. When your API wants to report to a caller that it is being used incorrectly throwing an Error sends that signal clearly.

Conversely, if the exception is some kind of runtime failure that doesn’t indicate a bug in the code, then throwing an Error is misleading. Instead, throw one of the core Exception classes or some other type.

### DON’T explicitly catch Error or types that implement it.

This follows from the above. Since an Error indicates a bug in your code, it should unwind the entire callstack, halt the program, and print a stack trace so you can locate and fix the bug.

Catching errors of these types breaks that process and masks the bug. Instead of adding error-handling code to deal with this exception after the fact, go back and fix the code that is causing it to be thrown in the first place.

### DO use rethrow to rethrow a caught exception.

If you decide to rethrow an exception, prefer using the rethrow statement instead of throwing the same exception object using `throw.rethrow` preserves the original stack trace of the exception. throw on the other hand resets the stack trace to the last thrown position.

```dart
bad
try {
  somethingRisky();
} catch (e) {
  if (!canHandle(e)) throw e;
  handle(e);
}
```

```dart
good
try {
  somethingRisky();
} catch (e) {
  if (!canHandle(e)) rethrow;
  handle(e);
}
```

## Asynchrony

Dart has several language features to support asynchronous programming. The following best practices apply to asynchronous coding.

### PREFER async/await over using raw futures.

Asynchronous code is notoriously hard to read and debug, even when using a nice abstraction like futures. The async/await syntax improves readability and lets you use all of the Dart control flow structures within your async code.

```dart
good
Future<int> countActivePlayers(String teamName) async {
  try {
    var team = await downloadTeam(teamName);
    if (team == null) return 0;

    var players = await team.roster;
    return players.where((player) => player.isActive).length;
  } catch (e) {
    log.error(e);
    return 0;
  }
}
```

```dart
bad
Future<int> countActivePlayers(String teamName) {
  return downloadTeam(teamName).then((team) {
    if (team == null) return Future.value(0);

    return team.roster.then((players) {
      return players.where((player) => player.isActive).length;
    });
  }).catchError((e) {
    log.error(e);
    return 0;
  });
}
```

### DON’T use async when it has no useful effect.

It’s easy to get in the habit of using async on any function that does anything related to asynchrony. But in some cases, it’s extraneous. If you can omit the async without changing the behavior of the function, do so.

```dart
good
Future<int> fastestBranch(
    Future<int> left, Future<int> right) {
  return Future.any([left, right]);
}
```

```dart
bad
Future<int> fastestBranch(Future<int> left, Future<int> right) async {
  return Future.any([left, right]);
}
```

Cases where `async` is useful include:

- You are using `await`. (This is the obvious one.)
- You are returning an error asynchronously. `async` and then throw is shorter than `return Future.error(...)`.
- You are returning a value and you want it implicitly wrapped in a future. async is shorter than `Future.value(...)`.

```dart
good
Future<void> usesAwait(Future<String> later) async {
  print(await later);
}

Future<void> asyncError() async {
  throw 'Error!';
}

Future<void> asyncValue() async => 'value';
```

### CONSIDER using higher-order methods to transform a stream.

This parallels the above suggestion on iterables. Streams support many of the same methods and also handle things like transmitting errors, closing, etc. correctly.

### AVOID using Completer directly.

Many people new to asynchronous programming want to write code that produces a future. The constructors in Future don’t seem to fit their need so they eventually find the Completer class and use that.

```dart
bad
Future<bool> fileContainsBear(String path) {
  var completer = Completer<bool>();

  File(path).readAsString().then((contents) {
    completer.complete(contents.contains('bear'));
  });

  return completer.future;
}
```

Completer is needed for two kinds of low-level code: new asynchronous primitives, and interfacing with asynchronous code that doesn’t use futures. Most other code should use async/await or [Future.then()](https://api.dart.dev/stable/dart-async/Future/then.html), because they’re clearer and make error handling easier.

```dart
good
Future<bool> fileContainsBear(String path) {
  return File(path).readAsString().then((contents) {
    return contents.contains('bear');
  });
}
```

```dart
Future<bool> fileContainsBear(String path) async {
  var contents = await File(path).readAsString();
  return contents.contains('bear');
}
```

### DO test for `Future<T>` when disambiguating a `FutureOr<T>` whose type argument could be Object.

Before you can do anything useful with a FutureOr<T>, you typically need to do an is check to see if you have a `Future<T>` or a bare T. If the type argument is some specific type as in `FutureOr<int>`, it doesn’t matter which test you use, is int or is `Future<int>`. Either works because those two types are disjoint.

However, if the value type is Object or a type parameter that could possibly be instantiated with Object, then the two branches overlap. `Future<Object>` itself implements `Object`, so is `Object` or is `T` where `T` is some type parameter that could be instantiated with `Object` returns true even when the object is a future. Instead, explicitly test for the `Future` case:

```dart
good
Future<T> logValue<T>(FutureOr<T> value) async {
  if (value is Future<T>) {
    var result = await value;
    print(result);
    return result;
  } else {
    print(value);
    return value;
  }
}
```

```dart
bad
Future<T> logValue<T>(FutureOr<T> value) async {
  if (value is T) {
    print(value);
    return value;
  } else {
    var result = await value;
    print(result);
    return result;
  }
}
```

In the bad example, if you pass it a Future<Object>, it incorrectly treats it like a bare, synchronous value.

# Effective Dart: Design

