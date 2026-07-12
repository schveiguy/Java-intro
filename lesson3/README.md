# Flow Control

So far, the code we have written is sequential. That is, the instructions are a
list of things to do, and the computer does them.

But this isn't very interesting. Most programs need to alter what they do
based on *input*. This includes robots! Even during autonomous mode, FRC robots
need to adjust their outputs based on sensor data to deal with real world
issues, such as collisions or timing differences.

For this, we need to take different code paths based on information we receive
from the inputs.

The alteration of execution based on input is called [flow control](https://en.wikipedia.org/wiki/Control_flow).

## if statements

An `if` statement checks a boolean (true/false) value, and if the value is true,
then it executes a certain block of code. If it is false, it executes a
different block of code.

Each of those blocks can consist any number of statements.

The syntax for an if statement is as follows:

```java
if (x > 5) {
    System.out.println("x is big");
} else {
    System.out.println("x is small");
}
```

The `if` keyword begins the statement followed by the *condition*. The condition
*must* be wrapped in parentheses.

### condition

A condition expression is an expression which always results in a "truthy"
value. That is, a value which has an obvious mapping to `true` or `false`.

A *comparison expression* such as `x > 5` results in `true` if the variable `x` is greater
than 5. Otherwise, it results in `false`.

### statement block

A statement block is a list of statements wrapped in a set of curly braces `{`
and `}`. The entire block can be treated as one, when deciding which code to
execute.

In reality, the if statement block can be one statement, and then you do not
need the curly braces. For example, the above can be written:

```java
if (x > 5)
    System.out.println("x is big");
else
    System.out.println("x is small");
```

However, remember that whitespace is not significant in the Java language, so if
you do want to execute multiple statements for one branch of an if statement,
you must use the curly braces.

### else

The `else` keyword says what to execute when the condition is *false*. This
portion of the statement is optional (in the case where you don't need to
execute something when it is false).

### else if

If you have more than one condition to test, you can use an `else if`
construction.

Technically, there is no special "else if" keyword. It's just a normal `else`,
where the statement to execute is another `if` statement.

i.e. you may write:

```java
if (x > 10) {
    System.out.println("x is big");
} else {
    if (x > 5) {
        System.out.println("x is medium");
    } else {
        System.out.println("x is small");
    }
}
```

the statement inside the `else` block is just another `if-else` statement.

But since we are executing exactly one statement (an if-else statement), we can
remove the curly braces. And since white space is insignificant, we can paste
the `if` onto the same line as the `else`:

```java
if (x > 10) {
    System.out.println("x is big");
} else if (x > 5) {
    System.out.println("x is medium");
} else {
    System.out.println("x is small");
}
```

This is what's known as an [*if-else chain*](https://en.wikipedia.org/wiki/Conditional_(computer_programming)#Chaining).

Notice how we do not need to test that x is less than or equal to 10 in the
middle, because we know that x must already not be greater than 10. Only one
block of statements will execute in an if-else chain. subsequent conditions can
be implicitly thought of as including the *negation* of all the previous
conditions (they all must be false to reach the chained `else` statements).

## boolean logic

Sometimes, we *do* want to test multiple things to determine whether to execute
a statement block. For that we need to combine multiple tests into one
expression.

The three boolean operators are:

* AND operator: `a && b` is true if `a` is true and `b` is true
* OR operator: `a || b` is true if `a` is true or `b` is true.
* NOT operator: `!a` is true if `a` is false

So lets use this in an if condition:

```java
if (x >= 5 && x < 10) {
    System.out.println("x is just right");
}
```

Notice the new comparison operator. The comparison operators are as follows:

* `a < b` : true if `a` is less than `b`
* `a > b` : true if `a` is greater than `b`
* `a <= b` : true if `a` is less than OR equal to `b`
* `a >= b` : true if `a` is greater than OR equal to `b`
* `a == b` : true if `a` is equal to `b`
* `a != b` : true if `a` is NOT equal to `b`

I'll point out a typically confusing operator here is the equality operator.
This is two equal signs instead of one because remember that a single equal sign
means *assignment*!

Note that you can combine comparison operators and logic operators by using
parentheses:

`!(a > b && a < c)` : false if `a` is greater than `b` AND `a` is less than `c`,
true otherwise.

## While loop

What if we want to execute a block of statements multiple times? For that, we
need a [loop](https://en.wikipedia.org/wiki/Control_flow#Loops)!

Let's say we want to count down a timer for liftoff. First we will need a
variable to store the timer.

```java
int timer = 10;
```

Now, we need to print the timer value, and decrease it until it reaches 0. For
that, we need a loop.

```java
while (timer > 0) {
    System.out.println(timer);
    timer -= 1;
}
System.out.println("Lift off!");
```

As you can probably guess, a while loop executes a block of code *while* a
condition is true. It is possible for a while loop to be one statement, in which
case the curly braces aren't necessary.

## For loop

Did you notice how we created a variable, initialized it, checked it every loop,
and then modified it at the end of the loop? This is such a common construct,
that Java has a special type of loop designed to handle it.

```java
for(int timer = 10; timer > 0; timer -= 1)
    System.out.println(timer);

System.out.println("Lift off!");
```

This is equivalent to the previous `while` loop.

`for` loop syntax has 3 clauses -- the initializer clause, the conditional
clause, and the increment clause.[^1]

[^1]: Even though we aren't incrementing in the loop, this is still known as the
    increment clause.

### for each statement

In addition to the regular for-loop syntax, there is a specialized for statement
that operates on sequences of data. This is typically known as a "for each" or
"for in" statement.

This only works on certain data types, such as arrays.

```java
int[] array = new int[]{1, 2, 3, 4, 5};
for(int v : array)
    System.out.println(v);
```

## Exiting a loop body

Sometimes, you want to quit the loop entirely because some condition was
detected in the middle of executing the loop.

If you want to exit just that single loop iteration, you can use the `continue`
statement.

```java
for(int floor = 1; floor < 20; floor += 1) {
   if(floor == 13) continue; // skip unlucky numbers
   System.out.print("Floor ");
   System.out.println(floor);
}
```

If you want to exit the entire loop, you can use the `break` statement.

These statements are useful when a loop has no natural beginning or end point at
which to check the conditional. Or it might have multiple points at which to
check various conditions.

## Switch statement

A switch statement is like a very long if-else chain. While it may seem very
bizarre to have a specialized statement for this, you will likely see this
statement in real java code, so it will be good to understand what it means.

```java
int value = 42;
switch(value) {
    case 1:
        System.out.println("The value is 1");
        break;
    case 2:
        System.out.println("The value is 2");
        break;
    case 42:
        System.out.println("The value is 42");
        break;
    default:
        System.out.println("The value is something other than 1, 2 or 42");
        break;
}
```

Note that every clause, instead of using curly braces, uses a colon, followed by
a list of statements, and then requires a `break;` statement.

The `default:` case is executed if none of the other cases match.

What happens if you omit the `break;` statement? Then the execution continues to
the statements in the next clause.

Switch statements are typically used with a *discriminate value*, or a value
which must have one of a finite number of values. This can be something like a
robot state.

## Summary

We learned about all forms of flow control in Java, if statements, loop
statements, and switch statements. These are the statements which implement the
*logic* of your program, and allow your program to do different things with
different inputs.

## Exercise

TODO

---

[Previous: Statements, Declarations, and Variables](../lesson2/README.md)
