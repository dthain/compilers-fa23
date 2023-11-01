# Typechecking Assignment

## Objectives

-  To implement binding of names to symbols in a nested language.
-  To reason carefully about type-safety in a strictly typed language.
-  To implement brilliantly helpful error messages in a typed language.
-  To gain experience in programming via recursive decomposition.
-  To gain further experience in incremental software engineering.

## Overview

The next step in building a compiler is to check the semantic
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
```
... then it should continue to scan, parse, or print out the AST, as in previous assignments.

For this assignment, you will add name resolution.

### Name Resolution

If your program is invoked as follows:
```
bminor --resolve sourcefile.bminor
```

then it should parse, construct the AST, and then resolve variable names to
symbols using `decl_resolve`, `stmt_resolve`, `expr_resolve`, as
discussed in the textbook.  As each variable declaration is encountered,
enter it into the symbol table, bound to the given name.  As each
name reference is encountered, match it to the corresponding symbol.

For each name resolved, you should print a message like:
```
x resolves to local 3
y resolves to global y
z resolves to param 5
```

For each name that is used without a corresponding declaration, emit a message like this:

```
resolve error: foo is not defined
resolve error: x is not defined
```

## Hints

For name resolution, you will need to build a `scope`
module which keeps track of the binding between names and symbols
in each level of nesting, with an interface like this:

```
void            scope_enter();
void            scope_exit();
void            scope_bind( const char *name, struct symbol *s );
struct symbol * scope_lookup( const char *name );
```

This module will keep track of a linked list of hash
tables, each one representing nested scopes in the program.
`scope_enter` will push a new (empty) hash table on to the
stack, while `scope_delete` will pop one from the stack.
`scope_bind` will insert into the current scope
an entry binding a name to a symbol object.
`scope_lookup` will search the stack of hash tables,
looking for the closest instance of a matching definition.

## Testing

As with the previous step, create ten good test cases named `test/resolve/good[0-10].bminor`
that consist of valid B-minor programs and ten bad test cases `test/resolve/bad[0-10].bminor`
that contain at least one typechecking error.
We will evaluate your code using these and some other hidden test cases.

As always, exercise good style in programming by choosing sensible
variable names, breaking complex tasks down into smaller functions,
and using constructive comments where appropriate.

Ensure that `make clean`, `make`, and `make test`, and continue to work properly.

## Grading

**Tag your submission with `resolve` in github to turn in.**

For this assignment, your grade will be based upon the following:

-  Continued correctness of the --scan, --parse, and --print options. (30 percent)
-  General correctness of the --resolve option. (20 percent)
-  Correctness of your test cases. (20 percent)
-  Correctness on our test cases.  (20 percent)
-  Good programming style. (10 percent)

This assignment is due **Thursday, November 9th at 11:59PM**.  Late assignments are not accepted.

## Frequently Asked Questions

See the bottom of the [B-Minor Language Guide](bminor.md) for some FAQs about typechecking.
