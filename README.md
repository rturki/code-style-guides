# Code style guides
Code style guides for various programming languages

## Table of contents

* [All languages](#all-languages)
* [CoffeeScript](#coffeescript)
* [Ruby](#ruby)
* [Python](#python)
* [JavaScript](#javascript)
* [Scala](#scala)
* [Erlang](#erlang)
* [Other](#other)
* [License](#license)

### All languages
* Readability counts.
* Be consistent.
* [Don't repeat yourself](http://en.wikipedia.org/wiki/Don't_repeat_yourself).
* Flat is better than nested.
* Beautiful is better than ugly.
* Simple is better than complex.
* Add blank line to the end of every file.
* Limit lines to 80 symbols.

### CoffeeScript
* Follow
[polarmobile/coffeescript-style-guide](https://github.com/polarmobile/coffeescript-style-guide).
* Follow [TomDoc](http://tomdoc.org/) as a documentation specification.
* Limit lines to 80 chars.
* Write code in a functional style. Less side effects == less errors. Examples:
    * Use array methods (`Array::forEach`, `Array::filter` etc.) instead of
    `for..in` loops. `for` loops don't create scope so it's easier to
    introduce bugs. `Object.keys()` are preferred to `for..of`.
    * Avoid `break`-s and `continue`-s.
    * Try to not redefine vars where it's possible.
    * Same applies to JavaScript.

### Ruby
* Follow [bbatsov/ruby-style-guide](https://github.com/bbatsov/ruby-style-guide).
* Follow [TomDoc](http://tomdoc.org/) as a documentation specification.

### Python
* Follow [PEP8](http://www.python.org/dev/peps/pep-0008/).

### JavaScript
* Two spaces indentation.
* Single quotes are preferred over double. Reason: HTML uses double quotes.
* Use `void 0` instead of `undefined`, because `undefined` could have been
redefined.
* Write code in functional style with minimum side effects. See coffeescript
section for more info.
* Don't use function statements. Instead, create anonymous functions and
assing them to vars for consistency with other vars.

    ```javascript
    // No
    function doThing(a, b) {return a * b;}

    // Yes
    var doThing = function(a, b) {return a * b;};
    ```

* Avoid global vars where you can. If you use them, specify it explicitly.

    ```javascript
    window.globalVar = ...;
    ```

* Use one `var` per variable.

    ```javascript
    var a = 5;
    var b = 6;
    var $this = $(this);
    // Exception.
    var a, b, c, d, $this;
    ```

* Use '_this' variable to push current context to the closures.

    ```javascript
    var a = {
     b: function() {
       var _this = this;
       $(some).click(function(event) {
         _this.c();
       });
     }
    };
    ```

* Event callback should name event data variable as 'event', not 'e' etc.

    ```javascript
    $('#item').click(function(event) {
      $.storage.set('item', $(this).val());
    });
    ```

* Do not use quotes in object keys.

    ```javascript
    // No
    {'a': 'testtest'}

    // Yes
    {a: 'testtest'}
    ```

* Use '===' for comparing instead of '=='. JavaScript is weakly typed
language, so 5 == '5'. This ambiguity could lead to hard-to-find bugs.

    ```javascript
    if (a === 5) {
      ...
    }
    if ($(this).val() === 'something') {
      ...
    }
    if (typeof a === 'undefined') {
      ...
    }

    // Exception: this compares both to 'null' and 'undefined'.
    if (item == null) {

    }
    ```

* Cache list length into a variable. You could afford 2x loop performance
increase with this on some browsers.

    ```javascript
    for (var i = 0, length = someList.length; i < length; i++) {
      doSomething(someList[i]);
    }
    ```

* Avoid bitwise operators if possible.
* Avoid `with` & implied typecasting.

### HTML
* Two spaces indentation.

### CSS
* Two spaces indentation.
* Use hex or rgb colors (e.g. #fff) instead of color names (e.g. white).
* [Use `* {box-sizing: border-box;}`](http://paulirish.com/2012/box-sizing-border-box-ftw/).
* Don't use inline styling.
* Use only classes for styling most of the time (no #ids, elems etc).
* Profile your selectors with webkit inspector.
* Use tree-style indentation.

    ```css
    .signup-page {
      background: #0d0; }
      .signup-button {
        padding: 10px;
        background-image: url("../img/signup.png"); }

    /* This looks cool if you use Stylus etc. */
    .chat-page {
      font-size: 0.9em; }
      .identity {
        margin-bottom: 20px; }
        .identity-profile {
          height: 4em; }
        .identity-nickname {
          float: left;
          width: 165px; }
        .identity-avatar {
          float: right; }
        .identity-updates {
          margin-top: 10px; }
        .identity-status {
          height: 30px; }
        .identity-current-mood {
          padding-left: 5px; }
        .identity-button {
          float: right; }
    ```

* Use this sequence of properties

    ```css
    .item {
      position: static;
      z-index: 0;
      top: 0;
      right: 0;
      bottom: 0;
      left: 0;

      display: block;
      visibility: hidden;
      float: none;
      clear: none;
      overflow: hidden;
      clip: rect(0 0 0 0);

      box-sizing: content-box;
      width: auto;
      min-width: 0;
      max-width: 0;
      height: auto;
      min-height: 0;
      max-height: 0;
      margin: 0;
      padding: 0;

      table-layout: fixed;
      empty-cells: show;
      border-spacing: 0;
      border-collapse: collapse;
      list-style: none;

      font: 1em sans-serif;
      font-family: Arial, sans-serif;
      font-size: 1em;
      font-weight: normal;
      font-style: normal;
      font-variant: normal;

      content: "";
      cursor: default;
      text-align: left;
      vertical-align: top;
      line-height: 1;
      white-space: normal;
      text-decoration: none;
      text-indent: 1;
      text-transform: uppercase;
      letter-spacing: 1;
      word-spacing: normal;

      opacity: 1;
      color: #d00;
      text-shadow: 5px 5px 5px #d59;
      border: 1px solid #d00;
      border-radius: 15px;
      box-shadow: inset 1px 0 0 #fff;
      background: #fff url("../i/bg.png") no-repeat 0 0; }
    ```

### Scala
* Follow [official language style guide](http://docs.scala-lang.org/style/).

### Erlang
* Follow the official [Programming Rules and Conventions](http://www.erlang.se/doc/programming_rules.shtml).
* Use types and function specifications and discrepancy analysis.
* Avoid if-s, throw-s and catch-es whenever possible.
* Always consider time and memory complexity.

    ```erlang
    %% DO NOT
    %% Since the ++ operator copies its left operand, the result will be copied again and again and again...
    %% leading to quadratic complexity.
    naive_reverse([H|T]) ->
        naive_reverse(T)++[H];
    naive_reverse([]) ->
        [].

    %% OK
    naive_but_ok_reverse([H|T], Acc) ->
        naive_but_ok_reverse(T, [H]++Acc);
    naive_but_ok_reverse([], Acc) ->
        Acc.

    %% DO
    %% This is slightly more efficient because you don't build a list element only to directly copy it.
    vanilla_reverse([H|T], Acc) ->
        vanilla_reverse(T, [H|Acc]);
    vanilla_reverse([], Acc) ->
        Acc.
    ```

### Git
* Keep your repository clean. Don’t commit big files unless they absolutely
  require git. Even in this case, prefer storing all big files in a separate
  submodule. That’s because git history can become very big and it will be pain
  for others to use the repo.
* Structure your commit message like this:

    ```
    One line summary (less than 50 characters)

    Longer description (wrap at 72 characters)
    ```

* Commit summary:
    * Less than 50 characters
    * What was changed
    * Imperative present tense (fix, add, change): ("Fix bug 123", "Add
    'foobar' command, "Change default timeout to 123")
    * End with period
* Commit description:
    * Wrap at 72 characters
    * Why, explain intention and implementation approach
    * Present tense
* Commit atomicity:
    * Break up logical changes
    * Make whitespace changes separately
* Use namespaces in git branches:
    * Use `versions/x.y` namespace for supporting old versions.
    Examples: `versions/1.0`, `versions/2.1`.
    * Use `topics/topic-name` namespace every time you
    want to create a pull request and just in everyday. Examples:
    `topics/fix-fs-utils`, `topics/add-reddit-button`.

## License
The MIT License (MIT)

Copyright (c) 2012 Paul Miller (http://paulmillr.com)

Permission is hereby granted, free of charge, to any person obtaining a copy of
this software and associated documentation files (the "Software"), to deal in
the Software without restriction, including without limitation the rights to
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies
of the Software, and to permit persons to whom the Software is furnished to do
so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
