# Classes

So far we have implemented everything in one *class*. But what is a class?

Remember way back in lesson 2 where we discussed the builtin types? Well, a
class is a *not*-builtin, or *custom* type.

Classes in Java are a definition of a custom type that is based on data and
functions to operate on that data. In whole, the class should carry *semantic
meaning* to the user reading the code. We can think of a class as a *model* or
an *abstraction* of a concept you want to implement.

## The class declaration

A class, or custom type, is defined by declaring one. This uses the special
keyword `class`. You have seen this every time we have been programming Java,
but now we will examine it more closely.

```java
public class App {
   ...
}
```

A `public` class is a type which can be used outside the package in which it is
declared. It is important to note that:

1. A java file must have *at most* one public class.
2. The public class defined in the file must match the name of the file.
3. A java file can have any number of non-public classes.

Visual studio code will take care of these details for you.

The name `App` can be decided by you. One thing that is almost universal in
programming is that *[naming things is hard](url)*. Not hard in that it's difficult to
type out, but finding an appropriate name can be challenging.

You want a name that captures the essence of what the class is meant to do.
Naming your classes `A`, `B`, `C` might make sense to you at the time you wrote
them, but will be difficult for other people, or even a later version of you, to
understand.

In this case, `App` stands for application, and is perfectly reasonable for the
class that just contains the main function.

Inside the class, there are any number of declarations. These declarations are
called *members* of the class. These members define what data the class carries
around, and what functionality the class has. We will focus on the two most
important member types: fields and methods.

## Class instances

So far, we have used a class as a sort of container for functions. All the
functions were `static`, and so you called the functions based on the class
itself.

Remember that a class is a custom *Type*. Therefore, we must be able to declare
variables of that type:

```java
App val;
```

This declares a variable named `val` with type `App`. However, class types are
what we call *reference* types. These do not store the data directly, but
instead store a reference to the data.

A class variable by default does not refer to anything. Using it is actually an
error.

If we want to create a real `App` value, we must allocated it with `new`. We saw
`new` previously with arrays. Incidentally arrays are *also* reference types.

```java
val = new App();
```

What does this do? The expression `new App()` allocates space in the garbage
collected [heap](url) for an `App` value and then initializes it. This thing
that got allocated is called an *instance*. We say it is an instance of `App`,
or `App` instance. These are also sometimes called *objects*, as that is the
base unit in object-oriented programming.

The parentheses look strange, but we will understand that a bit later.

The result of this expression (the instance) is then assigned to `val`, which is
a reference to an `App` instance. Therefore, we can say `val` is an `App`
instance.

The act of allocating and initializing an instance is called
*object instantiation*.

Until an object is instantiated, using it is usually an error, and usually will
cause a compilation error, or an Exception at runtime (generally a
`NullPointerException`). Therefore, it is quite common to always instantiate an
object variable when declaring it.

What can we do with an instance? For `App`, not much, all the functions are
static, and do not need an instance. But we will create objects that do have
interesting things we can do with them!

## Member fields

A field is like a variable, but instead of being inside a function, it is inside
a class. When you declare a field in a class, every instance of that class
contains one of those fields.

Let's start with some geometric types in 2 dimensions. The most basic type is a
point. Create a new java class in VS Code and call it Point (it will be added as
Point.java):

```java
package hello;

public class Point {
    public double x;
    public double y;
}
```

If you use the VS Code menu for adding a new Java class, it will provide all the
code above except for the fields. Add those in.

You might be able to see how we are modeling geometry here -- a `Point` object
represents a point in 2d space, with a floating point `x` coordinate, and a
floating point `y` coordinate.

Now, we can create instances of `Point` and assign their `x` and `y` values.
Edit your `App.java` main function and add the following code:

```java
public static void main(String[] args) {
    Point p1 = new Point();
    p1.x = 5;
    p1.y = 2.5;
    Point p2 = new Point();
    p2.x = 10;
    p2.y = 5;
}
```

Let's review what has happened here.
1. The variable `p1` has been instantiated as a `Point`.
2. When you write `p1.x` you are referring to the `x` member of that instance.
   So the `x` value of the `p1` instance of point is set to 5.
3. The `y` value of `p1` is set to 2.5.
4. A `Point` variable `p2` is instantiated.
5. `p2.x` is set to 10, and `p2.y` is set to 5.

We can read and print the fields by adding the following lines to the function:

```java
System.out.printf("p1 = (%s, %s)\n", p1.x, p1.y);
System.out.printf("p2 = (%s, %s)\n", p2.x, p2.y);
```

This new function `printf` is more powerful than `print` or `println`. Instead
of just printing one thing, we can print multiple things, by specifying in a
format string how data should be printed.

Inside the format string, special format specifiers that start with `%` indicate
a value should be printed here. The `%s` means "string", so the data is
converted to a string and printed. There are other types of format specifiers,
but for now we should just use `%s`.

The `\n` means "newline". There is no `ln` version of `printf`, and so we must
add the newline ourselves.

The number of format specifiers must match the remaining parameters. Each
parameter goes into the output at the specifier locations.

In this case, you should get the following output:

```
p1 = (5.0, 2.5)
p2 = (10.0, 5.0)
```

## Member functions (methods)

Object oriented programming does not just include data in custom types, but
functionality in them as well.

These are implemented via member functions or methods. We have already created
some static methods, including the `main` function. But what about non-static
methods?

A static method can be called using the class type. It does not need an
instance. A normal method, in contrast, needs an instance to call it. While
inside the method, all the fields of the instance are available to read and
write.

When you call a method, you use the dot operator `.` on an instance just like
you used to set and get the fields.

Let's create a function which adds one point to another point. The resulting
point will be stored in the instance that called the method.

```java
public class Point {
    public double x;
    public double y;

    void add(Point p2) {
        x += p2.x;
        y += p2.y;
    }
}
```

We can use it by calling it on one of our points:

```java
public static void main(String[] args) {
    Point p1 = new Point();
    p1.x = 5;
    p1.y = 2.5;
    Point p2 = new Point();
    p2.x = 10;
    p2.y = 5;
    System.out.printf("p1 = (%s, %s)\n", p1.x, p1.y);
    System.out.printf("p2 = (%s, %s)\n", p2.x, p2.y);

    // add the points
    p1.add(p2);
    System.out.printf("p1 = (%s, %s)\n", p1.x, p1.y);
    System.out.printf("p2 = (%s, %s)\n", p2.x, p2.y);        
}
```

The output should be:

```
p1 = (5.0, 2.5)
p2 = (10.0, 5.0)
p1 = (15.0, 7.5)
p2 = (10.0, 5.0)
```

## Constructors

A constructor is a special member function in a java class that initializes the
instance. This is called whenever you call `new Point()` or whatever your class
is called. 

By default, Java will create a constructor with no arguments which sets all
fields to their default values. If we define any constructors, that default
constructor is not provided, and you must call one of the given constructors.

A constructor is named the same as the class name:

```java
public class Point {
    public double x;
    public double y;

    // our first constructor
    Point(double x, double y) {
        this.x = x;
        this.y = y;
    }

    void add(Point p2) {
        x += p2.x;
        y += p2.y;
    }
}
```

Notice that the constructor is named `Point`, and has no return type. Also
notice that we now have something called `this`.

Inside any member function that is not static, `this` refers to the instance.
Why do we use it here? Because we have accepted parameters named `x`, and `y`.
If we wanted to assign `x = x;`, what would happen is we would assign the
parameter to itself! This phenomenon is called
[variable shadowing](https://en.wikipedia.org/wiki/Variable_shadowing). When we
create a symbol in a nested scope such as a member function that is named the
same as one in an outer scope such as the class, then the name itself switches
to the nested one, and the outer one is shadowed. In order to tell the compiler
we really mean the instance `x` value, we use the symbol `this`.

We can avoid shadowing by naming our parameters or our member variables
something different. However, the practice of using `this` to assign fields in a
constructor is extremely common and aids in preventing unintentional shadowing
bugs.

You will notice when you save this file, that you now have errors in your
`App.java` file. This is because the default constructor which takes no
parameters is no longer available. We now must call the defined constructor to
create a `Point`. But the new constructor syntax makes things a lot simpler!

```java
Point p1 = new Point(5, 2.5);
Point p2 = new Point(10, 5);
System.out.printf("p1 = (%s, %s)\n", p1.x, p1.y);
System.out.printf("p2 = (%s, %s)\n", p2.x, p2.y);
```

## Composing objects with other objects

It's not just builtin types that can be used for fields, you can also use other
objects as fields. Note that because instances are by default `null`, you
should only use the field objects after they have been instantiated.

Let's create a `Line` object which is composed of 2 `Point` objects:

```java
package hello;

public class Line {
    public Point p1;
    public Point p2;

    Line(Point p1, Point p2) {
        this.p1 = p1;
        this.p2 = p2;
    }
}
```

In this case, the instantiation of p1 and p2 occurs before you instantiate the
Line, and these objects are *referenced* from the `Line` instance.

What happens when you copy the reference but not duplicate the instance? Any
other references to the instance are still valid, and can modify the instance.

To demonstrate, let's play with the line points in `main`:

```java
public static void main(String[] args) {
    Point p1 = new Point(5, 2.5);
    Point p2 = new Point(10, 5);

    Line l1 = new Line(p1, p2);
    System.out.printf("l1 = (%s, %s) - (%s, %s)\n", l1.p1.x, l1.p1.y, l1.p2.x, l1.p2.y);        
    p1.add(p2);
    System.out.printf("l1 = (%s, %s) - (%s, %s)\n", l1.p1.x, l1.p1.y, l1.p2.x, l1.p2.y);        
}
```

The output:

```
l1 = (5.0, 2.5) - (10.0, 5.0)
l1 = (15.0, 7.5) - (10.0, 5.0)
```

Notice how we changed the `p1` variable in `main`, and it affected `l1.p1`. This
is because the two variables refer to the *same* instance.

In order to fix this, we should initialize `Line.p1` and `Line.p2` with new
points instead of reusing the points passed in:

```java
public class Line {
    public Point p1;
    public Point p2;

    Line(Point p1, Point p2) {
        // make new points, don't just refer to the parameters
        this.p1 = new Point(p1.x, p1.y);
        this.p2 = new Point(p2.x, p2.y);
    }
}
```

If we try running main again now, we get what was expected:

```
l1 = (5.0, 2.5) - (10.0, 5.0)
l1 = (5.0, 2.5) - (10.0, 5.0)
```

## Summary

We learned all about classes today, how to instantiate, how to add fields and
member functions, and how they are reference types. We also learned how to
compose classes using other classes.

## Exercise

TODO

---

[Previous: Functions](../lesson4/README.md)

