## Parser Assignment

## Objectives

The objectives of this assignment are:
- To design a grammar for a non-trivial language.
- To solve grammar ambiguities through re-writing.
- To learn how to use Bison and Flex together.
- To gain experience in incremental software engineering.

## Overview

The next step in building a compiler is to construct a parser.
You will build upon the code from previous assignments and
use the [Bison Parser Generator](http://www.gnu.org/software/bison/manual)
to create a parser for [B-Minor Language](bminor.md).
It is up to you to carefully read this document and decide what all of the
relevant elements of B-Minor are.  Make sure that you include declarations,
definitions, statements, expressions, and any other program elements.

Make sure that you follow the [general instructions](general.md) for assignments,
so that your work runs correctly on the student machines.  We want you to 
have the benefit of using exactly the environment in which your work will be graded.

## Requirements

If your program is invoked like this:
```
./bminor --parse sourcefile.bminor
```

Then it should behave as follows:
-  If the input does not scan correctly, then `bminor` must emit `scan error:` followed by a reasonable error message and exit with status 1.
-  If the input does not parse correctly, then `bminor` must emit `parse error:` followed by a reasonable error message and exit with status 1.
-  If the input has valid B-minor syntax, then `bminor` must emit `parse successful` and exit with status 0.

If your program is invoked like this:

```
./bminor --scan sourcefile.bminor
```
Then it should continue to operate as in the previous assignment; this will facilitate debugging.
You may of course reorganize or move code around as long as the previous mode still works.

Use the scanner code from the prior assignment as your starting point.
If your scanner has any problems, then you should fix them before proceeding.
Make sure that the action of each rule is to return a symbolic token type (e.g. `TOKEN_INTEGER`)
so that `yylex()` has the proper return value to be used by `yyparse()`.
You can and should fix anything in your scanner
needed to get the entire scanner-parser combination working correctly.

## Approach

We recommend that you construct your grammar in stages and begin
by testing it on small examples, then proceeding to larger structures.
For example, start off by creating just arithmetic expressions, like this:

```
expr : expr TOKEN_ADD expr
     | expr TOKEN_SUB expr
     ...
     ;
```

Then, verify that your grammar has no shift-reduce or reduce-reduce
conflicts. If it does, look at the detailed output of Bison and re-write
your grammar rules to address them.  Once you have basic expressions working,
then start adding control-flow structures, and then declarations, until you
have constructed the complete grammar.

Note that Bison will tell you if your grammar has errors.
In particular, your grammar **must not have any shift-reduce or reduce-reduce conflicts**.  To eliminate them, you may **only re-write the production rules**, you may not apply disambiguating rules, operator precedence specifiers, or apply other "tricks" found in Bison.  (The purpose of this rule is to force you to fully understand the key ideas in LR parsing.)

It will take some time to think through the grammar problems.
Plan to work on this project over the course of several days,
so that you are able to work, then take a break to think, and
then return to the code with fresh thoughts.

## Testing

As with the previous step, create ten good test cases named `test/parser/good[0-10].bminor`
that consist of valid B-minor programs and ten bad test cases `test/parser/bad[0-10].bminor`
that scan correctly but contain parse errors.  Take the time to write thorough tests distinct from the scanner tests.

You can also try these [example test cases](https://github.com/dthain/compilerbook-examples/tree/master/tests/parser)
that come with the textbook but note that they don't cover the features specific to [B-Minor 2023](bminor).
We will evaluate your code using these and some other hidden test cases.

As always, exercise good style in programming by choosing sensible
variable names, breaking complex tasks down into smaller functions,
and using constructive comments where appropriate.

Ensure that `make clean`, `make`, and `make test`, and continue to work properly.

## Grading

To turn in via github, please review the [general instructions for turning in](general.md).   Make sure that your code is tagged as a release named `parser`.

For this assignment, your grade will be based upon the following:
-  (20 points) General correctness of the code.
-  (30 points) Correctness of the grammar, including elimination of shift-reduce and reduce-reduce conflicts by the re-writing of production rules.
-  (20 points) Correctness of your submitted test cases.
-  (20 points) Correctness on the instructors' hidden test cases.
-  (10 points) Good programming style.  Each of the program components (main, scanner, parser) should be cleanly separated into multiple source files, complex or repetitive tasks should be broken into multiple functions, identifiers should be sensibly chosen, and the code generally commented and readable.

This assignment is due on **Wednesday, October 11th at 11:59PM**.  Late assignments are not accepted.

## Frequently Asked Questions

See the bottom of the [B-Minor Language Guide](bminor.md) for some FAQs about parsing.
