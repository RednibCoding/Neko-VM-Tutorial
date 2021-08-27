[🠔 INDEX](../readme.md)
#

# Control Flow

## Conditions

When `if` and `while` check their conditions, only the boolean `true` will be considered true. You can convert any value to a boolean using the `$istrue` function, which considers `0`, `false`, and `null` to be false, and all other values to be true. Alternatively, you may use `$not`, which does the opposite.

## If

If expressions evaluate a boolean condition and executes the given expression. Parentheses are not required, nor are braces for a single expression.

```js
if true $print("Condition was true.")

if(true) {
    $print("Condition was true.");
}
```

## If-else

If expressions can also have an else clause.

```js
if(false)
    $print("Condition was false.")
else
    $print("Condition was true.")
 
if(false) {
    // do stuff
}
else {
   // do lots of other stuff
}
```

Since if expressions are expressions, they can easily be chained together in if-else-if expressions.

```js
var x = 1;

if x == 0
    $print("X is zero")
else if x == 1
    $print("X is one.")
else if false {
    // do stuff
}
else {
    $print("X is something else.")
} 
```

They do not need to end in an else clause.


## While

While loops while the condition remains true.

```js
var x = 1;

while x < 10 {
    $print(x, "\n");
    x = x + 1; 
}
```

## Do-while

Do-while loops ensure the loop is executed at least once.

```js
var x = 1;

do {
    $print(x, "\n");
} while x != 1

do $print(x, "\n") while {
    x = x + 1;
    x < 10;
}
```

## Switch

The switch expression is a series of comparisons to a given expression. The results of the first match are returned, the default clause if there is no match, and `null` if there are no matches and no default clause.

Note the lack of semicolons after the clauses.

```js
switch 0 {
    0 => "Ah, zero."
    1 => "Hello, one."
    2 => { $print("This was two!"); "two" }
    default => $print("No number I know.")
}
```

## Goto

Goto can be used to jump to a particular label. Details of gotos and the stack is discussed [here](http://nekovm.org/specs#labels_and_gotos).

```js
$goto(lab)
$print("Won't see this")
lab:
$print("Hello")
```

## Try-catch

A try-catch expression can be used for error handling. If an error is thrown (using `$throw`) within the try block, the catch block will be passed the arguments from `$throw`.

```js
try {
    $throw("error");
}
catch e {
    $print(e);
}
```

There is also a `$rethrow` function which can be used within the catch block to throw the same error or a new one.

```js
try {
    $throw("error");
}
catch e {
    $print(e);
    $rethrow("Something bad happened!");
}
```

#
[🠔 INDEX](../readme.md)