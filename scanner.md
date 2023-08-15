# Scanner Assignment

The first step in building a compiler is to create a scanner.

You will use the [Flex Scanner Generator](https://westes.github.io/flex/manual/)
to construct a scanner generator for the [B-minor Language](bminor.md).
It is up to you to carefully read this document and decide what all of the
token types are, and define them carefully using flex regular expressions.
Make sure that you define all reserved words, identifiers, operators, constants,
statements, and any other program elements.
If you think that the specification is not clear, be sure to ask for
a clarification.

Make sure that you follow the [general instructions](general.md) for assignments,
so that your work runs on the student machines using `/usr/bin/gcc` and so forth.
We want you to have the benefit of using exactly the environment in which
your work will be graded.

Your program must be invoked as follows:
```
./bminor -scan sourcefile.bminor
```
It must output to the standard output using `printf` the
symbolic token types for each element of the input.
For literal values (integers, strings, characters) and identifiers, you
must also output the body of the token, with the quotes removed and
any escape codes translated.  If the input contains an invalid token,
then the program should print a message to the standard error stream (`fprintf(stderr,"...")`) and `exit(1);` immediately.  Otherwise,
the program should exit with return code zero.

For example, if the input looks like this:
```
string
1534
'a'
Notre Dame
"\'Notre Dame\'";
>=
@
```
then your output should be:
```
STRING
INTEGER_LITERAL 1534
CHARACTER_LITERAL a
IDENTIFIER Notre
IDENTIFIER Dame
STRING_LITERAL 'Notre Dame'
SEMICOLON
GE
scan error: @ is not a valid character
```

A compiler has many odd corner cases that you must carefully handle.
To encourage you to test thoroughly, we will
also require you to turn in twenty test cases.  Ten should be
named `good[0-9].bminor` and should contain valid tokens.
Ten should be named `bad[0-9].bminor` and should contain
at least one erroneous token.  We strongly recommend that you
also try these [example test cases](https://github.com/dthain/compilerbook-examples/tree/master/tests/scanner).
We will evaluate your code using these and some other hidden test cases.

As always, exercise good style in programming by choosing sensible
variable names, breaking complex tasks down into smaller functions,
and using constructive comments where appropriate.

To turn in via github, please review the [General Instructions for Turning In](general.md).  Make sure that your code is tagged as a release named "scan".

**This assignment is due on Wednesday, September 14th at 11:59PM  Late assignments are not accepted.**

