# Typechecking Assignment

## Objectives

-  To implement binding of names to symbols in a nested language.
-  To reason carefully about type-safety in a strictly typed language.
-  To implement brilliantly helpful error messages in a typed language.
-  To gain experience in programming via recursive decomposition.
-  To gain further experience in incremental software engineering.

## Overview
 
The next step in building a compiler is to perform typechecking:
determine the type 
discovered during name resolutiong
correctness of the program, particularly focusing on name resolution
and type checking.  Both stages involve traversing the abstract
syntax tree recursively.  Name resolution involves matching every
unbound reference to a name (`x`) to the relevant variable
definition to which it refers (`x:integer=3;`).
Once that is accomplished, typechecking computes the type of each
expression and ensure that it is compatible with its destination.

## Requirements

Please review the [general instructions](general.md) for assignments.

If your program is invoked as follows:
```
bminor --scan sourcefile.bminor
bminor --parse sourcefile.bminor
bminor --print sourcefile.bminor
bminor --resolve sourcefile.bminor
```
... then it should continue to scan, parse, print, or resolve, as in previous assignments.

For this assignment, you will add the typechecking phase:

### Type Checking

If your program is invoked like this:

```
./bminor --typecheck sourcefile.bminor
```

then it should parse, construct the AST, resolve variable names,
and then perform typechecking, using `decl_typecheck`, `stmt_typecheck`,
etc, as discussed in the textbook.  In every place where type equivalence is required,
you must look for compatibility of types.  If an operation is not type-safe
(for example, adding a string to an integer), then you should emit a *very detailed*
error message that indicates the relevant expression(s), type(s), and
what was expected in that context.  For example:

```
type error: cannot add a string ("abc") to an integer (3+5)
type error: cannot return a boolean (x<5) in a function (fibonnacci) that returns integer
type error: declaration of array (a) must have a fixed size
```
					  
After encountering the first type or resolution error, *keep going* so that you can display all possible type errors at once, then exit with status 1 to indicate failure.  If no errors were encountered, exit with status zero.

There are many different places where typechecking must be performed.
Section 7.3 in the textbook summarizes the expected behavior of operators,
but you will have to examine the grammar carefully to find all places
where checks must be made.
Think carefully about function calls and definitions, array
definitions, etc.

The following "oddities" are not supported in B-minor, even though
it is possible to express them syntactically:

- Functions that return arrays or other functions.
- Functions as parameters to other functions.
- Arrays of functions.
- Non-constant initializers for global variables.
- Array initializers for local variables.

If these are encountered, emit a suitable error message indicating that they are not supported.

**Note** that [B-Minor 2023](bminor.md) does allow for floating point variables,
and so you should extend the typechecking rules to accommodate them.

## Hints

For typechecking, begin by building some helper functions related to types:

```
struct type * type_copy( struct type *t );
int type_compare( struct type *a, struct type *b );
void type_delete( struct type *t );
```

Then, implement typechecking operations on each of the key structures:
```
struct type * expr_typecheck( struct expr *e );
void stmt_typecheck( struct stmt *s );
void decl_typecheck( struct decl *d );
```

`expr_typecheck` should compute the type of an expression
recursively, and return a new type object to represent it.
(It should also check for errors within the expression.)
Then, write `stmt_typecheck` and `decl_typecheck`
to use the result of `expr_typecheck` and compare it
against expectations.

## Testing

As with the previous step, create ten good test cases named `test/typecheck/good[0-10].bminor`
that consist of valid B-minor programs and ten bad test cases `test/typecheck/bad[0-10].bminor`
that contain at least one typechecking error.
We will evaluate your code using these and some other hidden test cases.

As always, exercise good style in programming by choosing sensible
variable names, breaking complex tasks down into smaller functions,
and using constructive comments where appropriate.

Ensure that `make clean`, `make`, and `make test`, and continue to work properly.

## Grading

**Tag your submission with `typecheck` in github to turn in.**

For this assignment, your grade will be based upon the following:

-  Continued correctness of the --scan, --parse, --print, and --resolve options. (30 percent)
-  General correctness of the --typecheck option. (20 percent)
-  Correctness of your test cases. (20 percent)
-  Correctness on our test cases.  (20 percent)
-  Good programming style. (10 percent)

This assignment is due <s>**Thursday, November 16th at 11:59PM**</s> **Friday, November 17th at 11:59PM**.  Late assignments are not accepted.

## Frequently Asked Questions

See the bottom of the [B-Minor Language Guide](bminor.md) for some FAQs about typechecking.
