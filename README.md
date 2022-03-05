# JS-code-style

### 1. Where to break

The prime directive of line-wrapping is: prefer to break at a **higher syntactic level**.
The primary goal for line wrapping is to have clear code, not necessarily code that fits in the smallest number of lines.

#### Good
``` js
currentEstimate =
    calc(currentEstimate + x * currentEstimate) /
        2.0;
```
#### Bad
``` js
currentEstimate = calc(currentEstimate + x *
    currentEstimate) / 2.0;
```
In the preceding example, the syntactic levels from highest to lowest are as follows: assignment, division, function call, parameters, number constant.

Operators are wrapped as follows:

When a line is broken at an operator the break comes after the symbol. This does not apply to the dot (.), which is not actually an operator.
A method or constructor name stays attached to the open parenthesis (() that follows it.
A comma (,) stays attached to the token that precedes it.

### 2. Horizontal alignment

Horizontal alignment is the practice of adding a variable number of additional spaces in your code with the goal of making certain tokens appear directly below certain other tokens on previous lines.
Alignment can aid readability, but it creates problems for future maintenance. Consider a future change that needs to touch just one line. This change may leave the formerly-pleasing formatting mangled, and that is allowed. More often it prompts the coder (perhaps you) to adjust whitespace on nearby lines as well, possibly triggering a cascading series of reformattings. That one-line change now has a blast radius. This can at worst result in pointless busywork, but at best it still corrupts version history information, slows down reviewers and exacerbates merge conflicts.

#### Good
``` js
  tiny: 42,
  longer: 435,
};
```
#### Bad
``` js
{
  tiny:   42,
  longer: 435,
};
```

### 3. Block comment style

Block comments are indented at the same level as the surrounding code. They may be in `/* … */` or `//`-style. For multi-line `/* … */` comments, subsequent lines must start with `*` aligned with the `*` on the previous line, to make comments obvious with no extra context.
#### Good
``` js
/*
 * This is
 * okay.
 */
// And so
// is this.
/* This is fine, too. */
```
Comments are not enclosed in boxes drawn with asterisks or other characters. Do not use JSDoc (`/** … */`) for implementation comments.
#### Bad
``` js
/**
This is bad
*/
```

### 4. Use const and let

Declare all local variables with either const or let. Use const by default, unless a variable needs to be reassigned. The var keyword must not be used.
#### Good
``` js
const name = 'John';
let age = 27;
```
#### Bad
``` js
var name = 'Pete';
```

#### 5. One variable per declaration

Every local variable declaration declares only one variable:
#### Good
``` js
let a = 1;
let b = 2;
```
#### Bad
``` js
let a = 1, b = 2;
```
#### 6. Use trailing commas

Include a trailing comma whenever there is a line break between the final element and the closing bracket.
Example:
``` js
const values = [
  'first value',
  'second value',
];
```

#### 7. Spread operator

Array literals may include the spread operator (`...`) to flatten elements out of one or more other iterables. The spread operator should be used instead of more awkward constructs with `Array.prototype`. There is no space after the `...`.
Example:
``` js
[...foo]   // preferred over Array.prototype.slice.call(foo)
[...foo, ...bar]   // preferred over foo.concat(bar)
```

#### 8. Constructors

Constructors are optional. Subclass constructors must call `super()` before setting any fields or otherwise accessing `this`. Interfaces should declare non-method properties in the constructor.

#### 9. with

Do not use the `with` keyword. It makes your code harder to understand and has been banned in strict mode since ES5.

#### 10. Omitting `()` when invoking a constructor

Never invoke a constructor in a new statement without using parentheses `()`.
#### Good
``` js
new Foo();
```
#### Bad
``` js
new Foo;
```
Omitting parentheses can lead to subtle mistakes. These two lines are not equivalent:
``` js
new Foo().Bar();
new Foo.Bar();
```
