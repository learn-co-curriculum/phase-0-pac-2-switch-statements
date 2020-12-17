# Selection with Conditional: the 'switch' Statement

## Learning Goals

* Learn to use the `switch` statement

## Introduction

In this lesson we'll learn about the third tool available in JavaScript to use
_selection_, the `switch` statement. It provides an alternate way of expressing
conditional code that is less repetitive in cases where you want to test
multiple conditions against a single value.

![Seelection Image](https://curriculum-content.s3.amazonaws.com/programming-univbasics-2/sequence-and-comments/Selection_thick.png)

## Learn to Use the Switch Statement

Let's say we have a program that includes a variable containing a person's name
and we want to execute certain code depending on what that person's name is.
Using an `if...else if` construction, that might look like this:

```js
const name = "Alice";
let greeting;

if (name === "Alice") {
  greeting = "Hello, Alice!"
} else if (name === "The White Rabbit") {
  greeting = "Don't be late, White Rabbit"
} else if (name === "The Mad Hatter") {
  greeting = "Welcome to the tea party, Mad Hatter"
} else if (name === "The Queen of Hearts") {
  greeting = "Please don't chop off my head!"
} else {
  greeting = "Whoooo are you?"
}

greeting;
//=> "Hello, Alice!"
```

As we can see, there's quite a bit of repetition here: We always test name and
we always compare with `===`. This is a pretty common selection need. It's so
standard, that the `switch` statement was created to cut down the typing, but do
the same thing. Here's the `switch` version of the code above:

```js
const name = "Alice";
let greeting;

switch (name) {
  case "Alice":
    greeting = "Hello, Alice!";
    break;
  case "The White Rabbit":
    greeting = "Don't be late, White Rabbit";
    break;
  case "The Mad Hatter":
    greeting = "Welcome to the tea party, Mad Hatter";
    break;
  case "The Queen of Hearts":
    greeting = "Please don't chop off my head!";
    break;
  default:
    greeting = "Whoooo are you?";
}

greeting;
// => "Hello, Alice!"
```

The JavaScript engine compares the value passed in to the `switch` statement
(here, `name`) against each of the `case` values _using strict equality_
(`===`). When a match is found, the statements nested under that `case` are
executed. In this example, by using the `switch` statement, we avoid the need to
repeat the `if (name === _____)` line for each possibility.

We can also assign the same set of statements to multiple cases:

```js
const name = "Grumpy";
let characterType;

switch (name) {
  case "Sleepy":
  case "Sneezy":
  case "Happy":
  case "Grumpy":
  case "Bashful":
  case "Dopey":
  case "Doc":
    characterType = "dwarf";
    break;
  case "Handsome Prince":
    characterType = "hero";
    break;
  case "Evil Queen":
    characterType = "villain";
    break;
  case "Snow White":
    characterType = "heroine";
    break;
  default:
    characterType = "minor character";
}

characterType;
//=> "dwarf"
```

In the above example, if the `name` variable matches the names of any of the
dwarves, the `characterType` variable will be set to "dwarf".

The `default` and `break` keywords are both _optional_ in `switch` statements,
but can be useful. In more complicated statements, they become necessary to
ensure the correct flow.

### `default`

The `default` keyword is similar to the `else` clause in an `if...else`
construction. It specifies a set of statements to run after all of the `switch`
statement's `case`s have been checked. However, it is different from an `else`
in that **the only time it does _not_ run is if the engine hits a `break` in one
of the `case` statements**. If you only want one code block in your `switch`
statement to execute, it is safest to always include the `break` keyword.

### `break`

In the previous example, `break` is used to stop the `switch` statement from
continuing to look at case statements once it finds a match. If we left out the
`break` keyword, the "Grumpy" case would match and "dwarf" would be assigned to
`characterType`. However, since we didn't break after that assignment, the code
continues to execute and `characterType` winds up being reset to "minor
character." To keep that from happening, we use `break` to tell the JavaScript
engine to stop executing the `switch` statement as soon as it finds a match. You
will often see switch statements where `break` is used in every case as a way to
ensure there is no unexpected behavior from multiple cases executing.

**Advanced:** Sometimes we _want_ to potentially match multiple cases, and we
will need to leave out `break` in order to do this. Let's revisit an example
from the lesson on `if` statements:

```js
const age = 20;
let isAdult, canWork, canEnlist, canDrink;

if (age >= 21) {
  isAdult = true;
  canWork = true;
  canEnlist = true;
  canDrink = true;
} else if (age >= 18) {
  isAdult = true;
  canWork = true;
  canEnlist = true;
} else if (age >= 16) {
  canWork = true;
}
// => true

isAdult;
// => true

canWork;
// => true

canEnlist;
// => true

canDrink;
// => undefined
```

We can refactor the above `if...else if...else` chain as a more compact, less
repetitious `switch` statement. To make it work, we can will employ a neat
little trick: we'll use comparisons for our `case` statements instead of a
simple value.

```js
const age = 21;
let isAdult, canWork, canEnlist, canDrink;

switch (true) {
  case age >= 21:
    canDrink = true;
  case age >= 18:
    isAdult = true;
    canEnlist = true;
  case age >= 16:
    canWork = true;
}
// => true

isAdult;
// => true

canWork;
// => true

canEnlist;
// => true

canDrink;
// => undefined
```

We specified `true` as the value to `switch` on. All of our `case`s are
_comparison expressions_ that return `true` or `false`. If the comparison
returns `true` its statements will be run. Because we did not include any
`break` statements, once _one_ case statement matches, all subsequent statements
will execute. This is what we want here: if `age` is greater than 21, it's also
greater than 18 and 16, so we want *all* the assignments to run.

If we set `age` to `20` in the above example, the first `case`, `age >= 21`,
returns `false` and so the assignment of `canDrink` never happens. The engine
then proceeds to the next `case`, `age >= 18`, which returns `true`, assigning
the value `true` to `isAdult` and `canEnlist`. Since it encounters no `break`
statement, it then proceeds to the last case statement where `canWork` is set to
true as well.

## Conclusion

You now have three different tools available to you to use _selection_ in
JavaScript: the `if` statement, the `ternary` expression, and the `switch`
statement. The `if` statement is the one you will use most often &mdash; in
fact, you can _always_ construct your conditional code using `if`, `if...else`,
or `if...else if...else`. It may not be the most efficient way to write the code, but you can always get it to work.

As a rule of thumb, you may find it makes sense to start with `if` statements
and, once that's working, consider refactoring to use a ternary or switch
statement if they're better suited for what you need to do.

## Resources

* MDN
  * [`switch` statement](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/switch)
