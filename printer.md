# Pretty-Printer

## Objectives

-  To use Bison to construct a complete Abstract Syntax Tree.
-  To learn techniques for traversing the AST.
-  To use compiler techniques to perform source-code manipulations.
-  To gain experience in incremental software engineering.

## Overview

The third step in building a compiler is to construct the Abstract Syntax Tree (AST).
Building upon the previous assignment, you will use Bison rules to construct
elements of the AST as each component of the grammar is constructed.
Once the AST is constructed, you will verify its correctness by using it
to print the program back out, except this time consistently formatted,
much like the tool `/usr/bin/indent`.

## Requirements

Please review the [general instructions](general.md) for assignments.
To keep the class reasonably synchronized, you must use the
[B-Minor Starter Code](https://github.com/dthain-courses/compiler-starter-code) as the basis for the AST, although you are welcome
to add or adjust fields in the structures as necessary.

The prior stages of the compiler should continue to work as they did before:
```
./bminor --scan sourcefile.bminor
./bminor --parse sourcefile.bminor
```

For this stage, your program will be invoked as follows:
```
./bminor --print sourcefile.bminor
```

And it should behave as follows:

-  If the input does not scan correctly, then `bminor` must emit `scan error:` followed by a reasonable error message and exit with status 1.
-  If the input does not parse correctly, then `bminor` must emit `parse error:` followed by a reasonable error message and exit with status 1.
-  If the input has valid B-minor syntax, then `bminor` must display the pretty-printed output and exit with status 0.

## Approach

Continuing from the previous assignment, add functions to build the
parts of the AST, and then modify the grammar to invoke those actions
appropriately:

```
expr : expr TOKEN_ADD expr
          { $$ = expr_create( EXPR_ADD, $1, $3 ); }
     | expr TOKEN_SUB expr
          { $$ = expr_create( EXPR_SUB, $1, $3 ); }
     ...
     ;
```

To make this work, you will need to declare a `union`
type at the top, indicating which productions generate which
types in the AST:

```
%union {
	struct decl *decl;
	struct stmt *stmt;
	struct expr *expr;
	. . .
};
```

And then follow it with `%type` declarations that inform
Bison which member of the union to use for each production:

```
%type <decl> program decl_list decl
%type <stmt> stmt stmt_list
%type <expr> expr expr_list and_expr or_expr . . .
. . .
```

Finally, write the code which will pretty-print the AST back out:

```
decl_print( struct decl *d );
stmt_print( struct stmt *s );
expr_print( struct expr *e );
...
```

## Output Format

Your output must be a valid B-minor program that is logically
equivalent to the B-minor input code, with the following differences:

-  All comments and extraneous whitespace are removed.
-  Every declaration and statement starts on a new line.
-  Expressions should have no whitespace between tokens and operators, unless needed for correctness.
-  All code within braces should be indented by an additional level.
-  Expressions should have no more parentheses than strictly needed for correctness.  (Put another way, if the input program has excess parentheses, they should be removed.)

For example, this messy input code:

```
/* Display fibonnaci numbers from 0 to 45. */
fib: function integer ( x: integer ) = {
if( x<1 ) { return 0; } else {
if((x<2)) { return 1; } else {
return fib((x)-1) + fib((x-2)); // recursive step
} }}
```

Should be reformatted like this:
```
fib: function integer ( x: integer ) =
{
	if(x<1) {
		return 0;
	} else {
		if(x<2) {
			return 1;
		} else {
			return fib(x-1)+fib(x-2);
		}
	}
}
```

You can exercise your judgement on the remaining details not specified,
as long as your output is *consistent*.  For example, we don't care
whether you ident by tabs or spaces (or how many spaces). 

## Testing

As with the previous step, create <s>ten</s> **twenty** good test cases named `test/printer/good[0-10].bminor`
that consist of valid B-minor programs <s>and ten bad test cases `test/printer/bad[0-10].bminor`
that contain at least one parsing error.</s>
We will evaluate your code using these and some other hidden test cases.

**Because the output of the pretty-printer must be a valid B-minor program,
an excellent way to test your work is to run the output of the pretty
printer back through the compiler a second time, to ensure that the
output is parseable, and the output is identical that second time.**

As always, exercise good style in programming by choosing sensible
variable names, breaking complex tasks down into smaller functions,
and using constructive comments where appropriate.

Ensure that `make clean`, `make`, and `make test`, and continue to work properly.

## Grading

To turn in via github, please review the [general instructions for assignments](general)  Make sure that your code is tagged as a release named **printer**.

For this assignment, your grade will be based upon the following:

-  (20 points) General correctess of the code.
-  (30 points) Construction of the abstract syntax tree and coverage of all language elements.
-  (20 points) Correctness of your submitted test cases.
-  (20 points) Correctness on the instructors' hidden test cases.
-  (10 points) Good programming style.  Each of the program components (main, scanner, parser) should be cleanly separated into multiple source files, complex or repetitive tasks should be broken into multiple functions, identifiers should be sensibly chosen, and the code generally commented and readable.

This assignment is due **Monday, October 30th at 11:59PM**.  Late assignments are not accepted.

## Frequently Asked Questions

See the bottom of the [B-Minor Language Guide](bminor.md) for some FAQs about printing.

