# Code Generation Assignment

## Objectives

- To build a native code generator for a procedural language.
- To demonstrate competence in X86-64 assembly language.
- To solve common problems in register allocation and expression translation.
- To gain experience in incremental software development.

## Overview

Finally, you will complete your compiler by adding a code generator!
We have discussed code generation extensively in class,
so this assignment won't specify it in too much detail.
The goal is simple: Your compiler must read in a B-minor program
as described by the [language guide](bminor.html)
and emit an 64-bit X86 assembly language program that can be
assembled, linked, and run correctly on the CSE student machines.

## Requirements

Please review the [general requirements](general.md) for assignments.
Your final submission must have a Makefile that generates an executable
called `bminor` that can be invoked like this:

```
% bminor -codegen program.bminor program.s
```

If the program passes all earlier phases of compiling
(scanning, parsing, resolving, and typechecking) then it should
write a valid assembly language program to the file specified in the third argument
and exit with status zero.
If some error is encountered along the way, then it must print a reasonable error and exit with status one.

Your compiled programs will need a runtime library to operate correctly.
Use the `library.c` provided with the B-minor starter files as a starting point.
Note that a print statement in B-Minor should result in one or more calls
to the C functions `print_string`, `print_integer`, etc, depending on the type of the expression
You may add additional additional runtime calls as you see fit.

To convert assembly code into a working executable, use GCC in assembly mode and include the B-minor standard library:

```
gcc -g myprogram.s library.c -o myprogram
```

Then execute the final program like this:

```
./myprogram
```

It's quite possible that this final stage of the project
will require you do go back and make a few changes to earlier stages.
Do what you need to do in order to get the code working!
The assembly code that you produce must work correctly, but it need not be simple, pretty, or optimal.

You may make the following simplifying assumptions in this final stage:
- Due to the large number of X86-64 registers, you may use a simple non-spilling register allocator,
and fail with an "out of registers" error on really complicated nested expressions.
- To keep the calling conventions simple, calls to functions with more than six arguments may fail with a "too many arguments" error.
- Only one-dimensional arrays of integers at global scope must be implemented.
Arrays of other types, or arrays as parameters or local variables may fail with an "array not implemented" error.

## Hints

Start by writing a bunch of *very* simple programs,
and then write just enough of the code generator to cover those cases.
For example, write a test that declares one variable (and nothing else),
or returns a single constant value from main.
Work up bit by bit to handle integer arithmetic, then control statements, function calls, and so forth.
When you are ready for a challenge, try these [complete example programs](https://github.com/dthain/compilerbook-examples/tree/master/tests/codegen)

## Turning In

Tag your submission with `codegen` in github to turn in.

Your submission will be tested on the CSE student Linux machines,
so make sure that your code works there. If you develop on your laptop or another computer,
leave plenty of time before final submission to debug any differences between your computer and ours.

As before, the options from the previous stage must continue to work correctly.
You must also turn in a set of twenty test programs named good[1-20].bminor.
Each one must be a valid B-minor program on which you produce working output.
Make sure that your test cases start with very simple examples and work up to
complex examples with complex expressions, control flow statements, and functions.
(You tested all the bad cases in previous stages, so you don't need to include bad cases now.)

Your grade on this project will be based upon:

- Continued correctness on previous stages. (10 percent)
- General structure and completeness of the code generation stage. (40 percent)
- Correctness of your test cases. (20 percent)
- Correctness on our test cases. (20 percent)
- Good programming style. (10 percent)
 
This assignment is due on Wednesday, December 7th by 11:59PM. Late assignments are not accepted.

