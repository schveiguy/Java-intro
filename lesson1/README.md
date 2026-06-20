# Introduction to Java

Java is a compiled, statically typed, Object-oriented, garbage collected
programming language. It is used in over 75% of FRC teams to program their
robots for competition. 4H Alarm uses it as well.

This lesson will introduce basic concepts of programming using Java. If you
already know programming concepts with another programming language, it still
might be useful to skim through the items here to get familiar with the syntax.

## What is a compiler?

Computers understand one language -- binary instruction code. The exact codes
used to tell the computer what to do are different depending on your computer
CPU. For example, the binary code for an ARM CPU is very different from an
Intel CPU.

These binary codes are extremely difficult to write and understand for humans,
so we invented [programming languages](url) for humans to write and understand.
Keep in mind, a programming language is an *exact* language. It is not like
English, with subtle semantics based on context. And we need it to be this way!
We do not want robots deciding on their own what you "really meant", they need
to behave exactly as instructed -- no room for ambiguity.

A [compiler](url) is a computer program which reads in a program that is
written in a programming language, and produces a binary instruction file which
the computer can execute.[^1]

[^1]: The Java compiler technically compiles code into a simpler binary code
    called [bytecode](url). Bytecode is not directly understood byh the CPU, but
    it is easily interpreted using a virtual machine (called the Java Virtual
    Machine, or JVM). While not as fast as [native code](url), the Java
    interpreter can use techniques to get the interpreted code to run as fast or
    nearly as fast as native code.

The Java compiler is called javac. This accepts a Java file (a file with
extension `.java`) and produces a binary file (a file with extension `.class`).
The class file can be executed by the Java Virtual Machine (JVM).

Most of what we will do in programming takes care of these steps, but it is
useful to understand how the process works to produce usable code from Java
files.

## What is static typing?

"Static" is a term used a lot in programming. It means "unchanging", but has
slightly nuanced other meanings in different contexts. A statically typed
language means that a piece of data, once assigned a type, can never change its
type. It will always be that type.

The opposite of this is called [dynamic typing](url). A dynamically typed
language such as Python can have a piece of data change types from one part of
the code to the next. While this power can make for shorter code or less
boilerplate, the drawback is that the compiler cannot know whether something is
correct until it is executing. This makes it much easier to have latent bugs in
dynamically typed languages that will be rejected by the compiler of a
statically typed language.

Typically, statically typed languages are *compiled*, whereas dynamically typed
lanugages are *interpreted*. This is not a hard rule though.

## What does Object oriented mean?

[Object oriented programming](url) is a style of programming which is centered
around objects, or bundles of code and data.

OO programming is a large *paradigm* of programming that can produce intuitive
organization of code and data. We will learn some of the aspects of OO
programming in this class, but for the most part, you don't have to learn most
of it to effectively program a robot.

## What is garbage collection?

Garbage collection is a form of automatic memory management where you do not
need to worry about deallocation of dynamic data. Languages like C++ do not have
a garbage collector, and this means you must remember to free your resources or
you will quickly accumulate memory leaks.

It is important to note that GC is *not* a magic bullet for all memory problems.
You can still leak memory with a GC, and there is a certain level of
nondeterministic behavior which can cause problems in certain applications
(hello, loop overruns!). In practice, we accept these drawbacks because of the
convenience of not worrying about memory errors.

Trust me when I say, as someone learning programming, you should be very happy
to avoid memory errors regardless of the drawbacks!

# Setting up your environment

[WPILib](url), the programming framework for building robots, uses a program
called [Visual Studio Code](url) to build and debug your robot programs. We are
going to use their installation of VSCode to build and test all programs in this
class.

To install, use [this link](url) to download and run the installer. This will be
different based on which operating system you are using, make sure to download
the correct one.

Once installed, you will have a special icon for WPILib in your launch/start
menu. Always use this icon to start VSCode, even if you also have a version of
VSCode elsewhere. Always use the version linked to the *year* of the season. For
example, the 2026 season should say "WPILib 2026", and have a WPILib icon.
Running VSCode from a prior season will not work with the latest robot
libraries.

Note that when running VSCode, you will know you you are running the right
version if you see the WPILib icon in your side-bar:

image here

If you do not see this icon, you are not running the right version, and you will
not have access to the correct build systems that WPILib requires.

# Your first Java program

All programming languages provide a program which displays on the screen the
text "Hello, world!". This is known as a [hello world program](url). This will
be no different!

## Create a new project

Using VSCode, create a new project using the command pallete (`shift-ctrl-p` on
Windows, `shift-cmd-p` on Mac), and finding the command `Java: Create Java
Project`.[^2]

[^2]: While creating a java project is not strictly necessary to learn Java, or
    build and run Java, we will use this opportunity to get used to the VSCode
    and gradle project systems.

Select [Gradle](url) as the build system. It may ask you to install the plugin
for gradle.

Select a new folder where your project will live. I recommend creating a
`Programming` or `Robotics` folder under your Documents folder, and then a
subfolder named `Hello`

Gradle will ask you the [DSL](url) you want to use for the build. Select
`Groovy`, as that is what WPILib uses.

Name the project "Hello" (should be the default)

Gradle will create your project. Then ask if you want to open it. Say yes.

It also may ask for trusting the gradle.jar file. Say yes to this as well.

## The default project

The default project actually *is* the hello world project. However, it does
things in a slightly more complex way than we are ready for.

Delete all the code in the `App.java` file, and replace it with:

```java
/*
 * The initial hello world program!
 */
package hello;

public class App {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

## Remove default testing harness

The `AppTest.java` harness will test that the application functions work as
designed. You can remove that test (Called `appHasAGreeting`. This test checks
that the code functions as designed. However, we will remove the test, since
we aren't going to be using test harnesses in this class.

Delete the entire AppTest.java file.

## Run the project

Above the main function, you will see 2 buttons "Run" and "Debug". Click the
"Run" button, and you should see output similar to this:

```console
steves@Steves-Macbook-Pro-M4 Hello %  /usr/bin/env /Users/steves/.gradle/jdks/eclipse_adoptium-21-x86_64-os_x.2/jdk-21.0.3+9/Contents/Home/bin/java @/var/folders/bj/cyphtfm55697b66dpw85yc1c0000gn/T/cp_2caw2xn6nvezk3pbu98a6igp2.argfile hello.App 
Hello, World!
```

The first line is VSCode executing your project. The `java` command is the java
interpreter for java bytecode.

The second line is the output from your program! If you see this, you have
successfully built and run your first Java program. If the build fails, then it
should tell you the problem with the code. Try to ensure you type in or copy
*exactly* the code above. See if there are any differences that you missed. Even
one small character difference (even names that are capitalized differently) can
cause the build to fail.

# Anatomy of hello, world

This is a quick introduction of everything in this file. We are going to go
through all the lines, and don't worry if you don't quite understand everything
being discussed. There is a lot even in this one little file.

In future lessons we will cover in depth the different things identified here.

## Comment

```java
/*
 * The initial hello world program!
 */
```

A comment in Java is any text which starts with `/*` and ends with `*/`. Any
text between these lines is *ignored* by the compiler[^3], and is not part of your
program. The purpose of a comment is to document the surrounding code for human
consumption.

[^3]: Not all programs ignore comments. For example, the [javadoc](url) program
    which can generate very pretty web pages documenting all your code using
    specially formed comments.

## `package` statement

```java
package hello;
```

Java files always need a package statement if they are in a package. A package
is the directory your source file is located in. Because the gradle hello world
project places your App.java file under `hello/` folder, it needs to have the
`package hello;` line.

For the most part, VSCode will handle this for you.

## `class` declaration

```java
public class App {
    ...
}
```

This declares a class called `App`, which is publicly visible to code outside
this file. The curly braces denote the beginning and end of the class
declaration.

All code in java *must* be located inside a class. Java is an "Object Oriented
First" programming language.

The name `App` must match the name of the file `App.java`. This is mostly
managed by VSCode[^4] and is a rule which you probably will never run afoul of.

[^4]: Try changing the class name and save the file, and see what happens!

## Function `main` declaration

```java
    public static void main(String[] args) {
        ...
    }
```

There is a lot to unpack here.

First, what is a [*function*](url)? A function is a collection of instructions
which executed in order, gives the CPU something to do. A function *declaration*
announces to the compiler a function, and what it's name is. All names in Java
are [*case sensitive*](url). All functions are invoked using the name.

The `public` attribute means code outside the `App` class can call this function

The `static` attribute means that the function `main` is meant to be called
without an *instance* of the `App` object (we will talk about this later).

The `main` name is the name of the function. The name is special in Java in that
it serves as the *entry point* of your program. Although code runs before and
after the `main` function executes, for all intents and purposes, the call to
`main` is the beginning.

Inside the parentheses, you see `String[] args`. We will talk a whole lot about
this syntax later, but I will identify that `String` is a *type* in Java, and
represents a "string of characters" (text). The square brackets signify an array
of strings, not just one. `args` is the name of the *parameter*.

When your program is started, `main` is called, and all parameters sent to the
program are passed to your `args` parameter.

## println function call

```java
        System.out.println("Hello, World!");
```

This line is a [*statement*](url), or an instruction of what the computer should
do. In this case, it is a *function call* to the function
[`System.out.println`](url). You might be able to guess what this does.

The `System` part of the call is the name of the class which will contain the
appropriate function.

`out` stands for "output", or "standard output".

`println` is the actual name of the function. This function accepts a single
arugment and renders it as text to the screen on the output stream. This is the
function which actually says "Hello, world!" in your terminal.

The `println` function ends with `ln` because it prints its arugment as a single
line. There is also the `print` function, which does not do this.

The `"Hello, World!"` argument. This is what is called a *string
expression*, and actually gets turned into a `String` value. We will talk more
about expressions and literals later.

And finally, the semi-colon is an important part of Java code. This tells the
compiler that the statement is over, and it should expect more statements or the
end of the function next. Because Java does not have [*significant
whitespace*](url), it uses semi-colons to provide anchor points during
compilation to help disambiguate instructions and diagnose errors. There are
many different languages which also use semi-colons for this purpose.

# Summary

We learned about Java, built our first Java program, and executed it. This is a
great first step towards understanding and writing robot code! There isn't a lot
more to say here, as you are just learning.

## Exercise

Try changing the text printed in the greeting, and adding more lines of text to
print!
