# Statements, Declarations, and Variables

Most code in a software project is made up of
[*statements*](https://en.wikipedia.org/wiki/Statement_(computer_science)). A
statement can be thought of as a single coherent instruction or group of
instructions. Sometimes a statement is very short. Sometimes a statement is a
block of a lot of other statements. We'll go the most common statements in Java
in this lesson.

A declaration ties a name to something. That something can be a piece of data, a
type, a function, a package, etc. They are so fundamental, it's hard to explain
it without using it, so we'll go over that as we explain statements and
variables.

Variables are the data that live inside the program. Without variables, a
program would just be an exhibition of performance, and would not actually do
anything useful. The hello world program is such a program. Even though you
don't declare any variables in the program, you actually are using variables!

## Declaring a variable

To declare a variable in Java, we use the syntax `Type name`. A [type](https://en.wikipedia.org/wiki/Data_type) is a
way of telling the compiler what kind of thing we want to declare.

Java has many builtin types (the most basic things you can declare). It also
allows you to declare your own types (classes), which we will cover in a later
lesson.

Probably the most basic type that Java (and many programming languages have) is
an [*integer*](https://en.wikipedia.org/wiki/Integer_(computer_science)). In java, we call this `int`.

Let's declare an `int` named `age`:

```java
int age;
```

Note the semicolon at the end tells the compiler we are done with the
declaration.

What this declaration says to the compiler is, "I want you to find some memory,
and in the memory I want to put an integer. Call that piece of memory 'age'".

`age` is called a [*variable*](https://en.wikipedia.org/wiki/Variable_(computer_science)). A variable in Java is a named, typed piece
of data we can manipulate (i.e. vary)[^1].

[^1]: Actually, even data that you can't and don't vary are still variables. It
    has come to mean essentially a named piece of data.

If we want the variable to start with a default value, we can add an
[initializer](https://en.wikipedia.org/wiki/Initialization_(programming)) to the variable declaration:

```java
int age = 42;
```

## Printing a value

We're going to cover functions in more detail later, but to have some
interesting programs to work with, we want to be able to examine the values of
things. The easiest way to do this is to *print* the value to the screen.

So just like in the hello world program, let's use `System.out.println` to show
our variable:

```java
System.out.println(age);
```

If you follow this pattern, you can display any variable data you have (as long
as its a basic type).

Let's look at a complete program:

```java
public class App {
    public static void main(String[] args) {
        int age = 42;
        System.out.println(age);
    }
}
```

output:

```console
42
```

## Assignment

What if we want to modify or vary the variable? We use an *assignment*
statement.

If we wanted to assign the value `24` to `age`, it looks like this in Java:

```java
age = 24;
```

Let's dive bit deeper into this code. There are actually three parts to this
statement. The most important piece is the [operator](https://en.wikipedia.org/wiki/Operator_(computer_programming)) `=`. This is the
functional piece of the statement. The left side of the operator states what is
to be assigned, and the right side states the value that should be assigned.

If you print the variable `age` after this statement, you will see it has changed its value.

```java
public class App {
    public static void main(String[] args) {
        int age = 42;
        System.out.println(age);
        age = 24;
        System.out.println(age);
    }
}
```

output:

```console
42
24
```

## Math operations

Assignment is not the only operator. We also have math operations in Java.

If we want to subtract `10` from age, we can use the `-` operator:

```java
age = age - 10;
```

Note we used 2 operators here. On the right side of the assignment operator,
instead of a value, we have an [*expression*](https://en.wikipedia.org/wiki/Expression_(computer_science)). An expression is a sequence
of symbols and names that evaluates to something. In this case, the sequence
`age - 10`, if `age` is currently `24`, will evaluate to `14`. We then take the
result of this expression, and assign it back to `age`.

So the right side is the expression, the left side is the variable to assign to.

It is important to note that the left side must *always* evaluate to a variable.
It cannot be an arbitrary expression. The compiler will not do your algebra
homework for you!

```java
/* this is an error */
age + 10 = age;
/* we can't redefine what numbers mean */
5 = 4;
```

There are more operations for math that are important to note. You probably can
guess `-` for subtraction and `+` for addition. Division is somewhat
recognizable as `/`. However, multiplication looks too close to an `x`, which is
a name. So for programming in almost any language, we use the asterisk `*` for
multiplication.

## Other types

There are many other basic types in Java. However, the most common types for
robot programming are:

* `int` - An integer value
* `long` - An integer value with a wider range
* `float` - A floating point value
* `double` - A floating point value with double precision
* `String` - A string of characters (text)
* `boolean` - A value of `true` or `false`.

What does "wider range" mean? Essentially, the larger or more precise types use
more space to store data, so they can have a larger range of values[^2]. For
example, an `int` can store the values `−2,147,483,648` to `2,147,483,647`.
However, a `long` can store the values `−9,223,372,036,854,775,808` to
`9,223,372,036,854,775,807`. Using a larger type gets more precision, but at the
cost of higher memory usage, and in some cases, slower execution.

[^2]: The range of values is dictated by the *bits* that each type uses. an
    `int` in Java is 32-bits, and a `long` is 64-bits. You may notice that the
    values here are 2^31 and 2^63. Why not all the bits? Because one bit is
    used for the sign of the value.

What does [floating point](https://en.wikipedia.org/wiki/Floating-point_arithmetic) mean? It's a bit complex, but essentially, this
is a number with a decimal place, like `3.14159`. Integers cannot be assigned a
floating point number, but floating point numbers can be assigned an integer.

## Statements

So far, we have been using declarations and statements. Both are very similar,
but have distinct uses.

A declaration generally does *not* execute during the program. It is a note to
the compiler defining a new name.

A statement *does* execute during the program. The statement gets directly
translated to machine code that the CPU then runs when yhou run your program.

We have used 2 different statements in this lesson, assignment statements and
function call statements. In further lessons we will be using more
statements, including larger compound statements.[^3]

[^3]: In reality, you have written just ONE type of statement -- an expression
    statement. An expression statement is an expression which simply ends in a
    semicolon. Assigments and function calls are both expressions, and can be
    combined with each other in various ways.

## Summary

In this lesson we learned how to declare a variable, how to assign that
variable, and how some simple math can be performed.

## Exercise

Try using more math on variables. Maybe try using a floating point variable.

See what will happen when you divide a number that doesn't go evenly into an
integer. As an example, try:

```java
int age = 42;
age = age / 5;
```
