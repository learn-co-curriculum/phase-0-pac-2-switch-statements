# Selection with Conditionals: the 'switch' Statement

## Learning Goals

* Learn to use the `switch` statement

## Introduction

We've now learned about two of the three _selection_ tools available to us in
JavaScript: the `if` statement and the `ternary` expression. In this lesson,
we'll learn about a third: the `switch` statement. The `switch` statement
provides an alternate way of expressing conditional code that is less repetitive
in cases where you want to test multiple conditions against a single value.

![Selection Image](https://curriculum-content.s3.amazonaws.com/phase-0/pac-2-intro/Selection_thick.png)

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

As we can see, there's quite a bit of repetition here: we always test `name` and
we always compare with `===`. This is a pretty common selection need. It's so
standard that the `switch` statement was created to enable us to streamline our
code. Here's the `switch` version of the code above:

<iframe height="400px" width="100%" src="https://replit.com/@lizbur10/VastVividPreprocessor?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

The JavaScript engine compares the value passed in to the `switch` statement
(here, `name`) against each of the `case` values _using strict equality_
(`===`). When a match is found, the statements nested under that `case` are
executed. In this example, by using the `switch` statement, we avoid the need to
repeat the `if (name === _____)` line for each possibility.

We can also assign the same set of statements to multiple cases:

<iframe height="400px" width="100%" src="https://replit.com/@lizbur10/LatestAshamedStrategy?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

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
statement to execute, you should always include the `break` keyword.

### `break`

In the previous example, `break` is used to stop the `switch` statement from
continuing to look at case statements once it finds a match. If we left out the
`break` keywords, the JavaScript engine would first assign `characterType` to
"dwarf" when it reached the "Grumpy" case (as desired), but the code would
**continue to execute** and `characterType` would wind up being reset to
"minor character." To keep that from happening, we use `break` to tell the
JavaScript engine to stop executing the `switch` statement as soon as it finds
a match. You will often see switch statements where `break` is used in every
case as a way to ensure there is no unexpected behavior from multiple cases
executing.

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
repetitious `switch` statement. To make it work, we will employ a neat little
trick: we'll use comparisons for our `case` statements instead of a simple
value.

<iframe height="400px" width="100%" src="https://replit.com/@lizbur10/YummyThreadbareResource?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

We specified `true` as the value to `switch` on. All of our `case`s are
_comparison expressions_ that return `true` or `false`. Therefore, if a
comparison returns `true`, its statements will be run. Because we did not include
any `break` statements, once _one_ case statement matches, all subsequent
statements will execute. This is what we want here: if `age` is greater than 21,
it's also greater than 18 and 16, so we want *all* the assignments to be made.

If we set `age` to `20` in the above example, the first `case`, `age >= 21`,
returns `false` and the assignment of `canDrink` never happens. The engine then
proceeds to the next `case`, `age >= 18`, which returns `true`, assigning the
value `true` to `isAdult` and `canEnlist`. Since it encounters no `break`
statement, it then proceeds to the last case statement where `canWork` is set to
true as well.

## Conclusion

You now have three different tools available to you to use _selection_ in
JavaScript: the `if` statement, the `ternary` expression, and the `switch`
statement. The `if` statement is the one you will use most often — in
fact, you can _always_ construct your conditional code using some combination of
`if`, `else if`, and `else`. It may not be the most efficient way to write the
code, but it will always do the trick.

As a rule of thumb, you may find it makes sense to start with `if` statements
and, once you've got the code working, consider refactoring it to use a ternary
or switch statement if they're better suited for what you need to do.

## Resources

* MDN
  * [`switch` statement](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/switch)
