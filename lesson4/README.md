# Functions

A *function* in Java is a sequence of statements that are executed in the order
they appear. We have already been writing functions, the `main` function in our
Hello World example is a function.

But functions serve as an [*abstraction*](https://en.wikipedia.org/wiki/Abstraction_(computer_science)) of functionality that can be reused
multiple times in a program. They also help us take on reasonable sizes of
functionality without having to do everything at once.

An example of such an abstraction is the `System.out.println` function. The job
of this function is to take the thing you give it, and display it on the screen.
You do not have to remember, or even know, the low level commands and statements
that will do this. It's all handled by the function. And that's all it has to
handle.

Using functions, we can construct a complex and rich program while designing the
program from a much higher level.

## Function declarations

Because Java is Object-oriented-first, all functions *must* be contained within a
class. So far, we have only created one class called `App`, and this class' only
purpose is to contain our function.

Let's create another simple function, one that takes a parameter and returns a
value. Note that this must go inside your class, so let's show the entire code
for now.

```java
package hello;

public class App {
    static int square(int num) {
        return num * num;
    }
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

If we run this code, it builds, but nothing is different about the result. We
still just see "Hello, World!" on the screen.

What we have done, however, is declare a *new function* called `square`.
Remember that a declaration does not execute code. It simply assigns a name to
something. In this case, we implemented a function, and assigned the name
`square`.

This function declaration is slightly different from `main`. It is not `public`,
and it returns `int` instead of `void`. This is significant -- a function is
allowed to return *one* thing. In the case of `main`, nothing is returned. But
in the case of `square`, we return an `int`.

Like `main`, the function accepts a *parameter*. This parameter is one `int`,
and we named that parameter `num`.

And finally, like `main`, we declared it to be `static`, which means you do not
need an object to run this function (more on that later).

## Implementation block

An implementation block is a block of statements that implement the function.
When the function is entered, each statement is executed in order until the end
of the block is reached, or a `return` statement is executed.

In this case, the function is very simple, one statement. The statement is a
`return` statement. Return statements are very straightforward, they look like:

```java
return expression;
```

Where `expression` must be a valid Java expression that evaluates to a value of the
provided *return type*.

In the case of this function, the return type is `int`, and the expression is
`num * num`. The type of multiplying two `int`s together is also `int`, and
so this function compiles correctly.

If instead, we tried to return `"hello"`, the compiler would complain that the
type `String` cannot be returned to an `int`.

## Calling a function

Defining a function without using it is pretty boring. So let's call it!

```java
public static void main(String[] args) {
    int num = square(42);
    System.out.println(num);
}
```

Now, instead of printing Hello, World, we print 1764.

Using a function's identifier followed by parentheses and the required number and
type of arguments calls the function. The `square` function accepts an `int`
and returns the square of that `int`. So for the declaration of `num`, we
assign it the value of 42<sup>2</sup>.

The second line calls `println` with the value stored in `num`.

Notice how we used `num` inside `main` *and* inside `square`. It is important to
note that these are two *different* variables. A function's locally declared
variables are unique to that call of that function, and similar names outside of
the function have no relationship to that variable.

## Functions to implement functions

Let's write a `power` function, which is like `square`, but accepts a second
parameter which is the power to raise the first parameter to.

```java
static int power(int num, int exp) {
    int result = 1;
    while(exp > 0) {
        result *= num;
        exp -= 1;
    }
    return result;
}
```

This function uses a while loop as we learned in the last lesson, and keeps
multiplying the result by the number until we have reached the correct value.

We have used the `exp` parameter as a counter, and note how because the function
itself has its own unique copy of it, it will not affect anything outside the
function.

Now, we can replace our `square` function call with this:

```java
int num = power(42, 2);
```

This will produce the exact same output. If we change the exponent to `3`, then
we get 42<sup>3</sup>, or 74088.

We can even replace the definition of square to be in terms of this function,
since this function is more general:

```java
static int square(int num) {
    return power(num, 2);
}
```

Why is it good to define functions in terms of other functions? Because you only
then have to implement functionality once. If something changes in the
implementation, you likely only have to change one place.[^1]

[^1]: In this case, the functionality is so simple as to never need changing.
    But this is not always the case.

In many cases, you will have more than one function where some of the function
implementations are the same. Adding another function with that similar portion
is called *factoring* the function into its more simple components. A factored
function can often make everything easier to understand and implement.

## Recursion

What about using a function to implement itself? This is called *recursion*. A
recursive definition for a function allows a function to be defined in terms of
itself.

In the case of `power`, we can simplify the function into three lines:

```java
static int power(int num, int exp) {
    if(exp == 0)
        return 1;
    return num * power(num, exp - 1);
}
```

Notice the call to `power` within the `power` function. When `power` calls
itself, it generates a *different* call, one that is independent of the first
call. In this new call, `exp` is one less.[^2]

[^2]: It is important that a recursive function never calls itself in a way to
    repeat the same exact code paths. This will cause an "infinite" recursion,
    and likely will exhaust your stack.

The `if` statement represents the "base case" of the recursive function -- any
number raised to the 0 power is 1. This terminates the recursion.

The recursive definition of a power function is:

> N<sup>0</sup> = 1; N<sup>a</sup> = N × N<sup>a-1</sup>

This is almost exactly how we typed it out.

One more note: there are two `return` statements. Only one of these can execute
each time a function is called. Once a `return` statement is executed, the
function is ended, and the value specified is returned. This is why we did not
need to enclose the second `return` statement in an `else` clause.

What happens when we call `power(42, 3)`? Let's follow the execution in our
mind:

1. The `power(42, 3)` function call checks, is `3 == 0`? It is not.
2. It then calls `power(42, 2)`.
3. `power(42, 2)` function checks is `2 == 0`? It is not.
4. It then calls `power(42, 1)`.
5. `power(42, 1)` similarly calls `power(42, 0)`.

Note: At this point, you have four calls to `power`, each with their own version of
`num` and `exp`. These all exist on a [*call stack*](https://en.wikipedia.org/wiki/Call_stack), where the compiler can
allocate memory for each of the variables.

6. `power(42, 0)` checks is `0 == 0`? It *is*!
7. It returns `1`.

The return brings execution back to the `power(42, 1)` call. Here, the
expression `power(42, 0)` has been replaced with the return value `1`.

8. `power(42, 1)` then multiplies that value (`1`) by `num` (`42`), and returns
   that value
9. `power(42, 2)` has now received that value (`42`) and substituted it for the
   call to `power(42, 1)`. It multiplies this value by `num` (`42`) and returns
   that value (`1764`).
10. `power(42, 3)` receives that value, and likewise multiplies it by `num`
    (`42`), to return that value (`74088`).
11. `main` receives that value, and assigns that to it's own `num` variable.

All of this happens so fast you can consider it happens almost instantly.
Computers can do these kinds of tasks millions of times a second.

## Summary

We learned about functions, how to declare them with a return type and
parameters. We learned about recursion and factoring of functions, two important
mechanisms to improve your code.

## Exercise

A very common recursive function is called `factorial`. A factorial of a number
`N` in mathematics is written `N!`.

The definition of `N!` is:

> N × (N - 1) × (N - 2) × ... × 1

Can you devise a `factorial` function which accepts a `long N` and returns the
factorial of that number as a `long`? You can try using loops or recursion.

Some values to test: 

> 5! = 5 × 4 × 3 × 2 × 1 = 120

> 10! = 3628800

> 15! = 1307674368000

---

[Previous: Flow Control](../lesson3/README.md) | [Next: Classes](../lesson5/README.md)
