# B-Minor 2023 Language Overview

**Note: The B-Minor language used in this class changes
each year in order to provide new challenges 
and opportunities.  This document differs from the one
in the textbook in the following ways:**

- Strings and characters have a number of additional escape codes.
- Arrays can be declared with length determined at runtime.
- Floating point values and types have been added.

## Overview

This is an informal specification of B-Minor 2023,
a C-like language for use in an undergraduate compilers class.
B-minor includes expressions, basic control flow,
recursive functions, and strict type checking.
It is object-code compatible with ordinary C and thus
can take advantage of the standard C library, within
its defined types.  It is similar enough to C to feel familiar,
but different enough to give you some sense of alternatives.

This document is deliberately informal: the most precise
specification of a language is the compiler itself, and
it is your job to write the compiler!  It is your job
to read the document carefully and extract a formal specification.
You will certainly find elements that are unclear or incompletely
specified, and you are encouraged to raise questions in class.

## Whitespace and Comments 

In B-minor, whitespace is any combination of the following characters:
tabs, spaces, linefeed (\n), and carriage return (\r).
The placement of whitespace is not significant in B-minor.
Both C-style and C++-style comments are valid in B-minor:
```
/* A C-style comment */
a=5; // A C++ style comment
```

## Identifiers

Identifiers (i.e. variable and function names) may contain
letters, numbers, and underscores.  Identifiers must begin with a letter
or an underscore.  These are examples of valid identifiers:

```
i x mystr fog123 BigLongName55
```

The following strings are B-minor keywords (or reserved for future expansion) and may not be used as identifiers:
```
array auto boolean char else false float for function if integer print return string true void while
```

## Types

B-minor has five atomic types: integers, floats, booleans, characters, and strings.
A variable is declared as a name followed by a colon, then a type and
an optional initializer.  For example:

```
x: integer;
y: integer = 123;
f: float = 45.67;
b: boolean = false;
c: char    = 'q';
s: string  = "hello bminor\n";
```

An `integer` is always a signed 64 bit value.   `float` is a floating point number that follows the [IEEE 754 double-precision standard](https://en.wikipedia.org/wiki/Double-precision_floating-point_format).   `boolean` can take the literal values `true` or `false`.  `char` is a single 8-bit ASCII character.  `string` is a double-quoted constant string that is null-terminated and cannot be modified.

`float` values can be represented in various ways. One method is to place the integer component, a period, and the fractional component all in a row, such as in `12.34`. Another valid method is to use the scientific representation of the value, which involves having a floating point value as described above followed by an exponent (represented as either `e` or `E`). Some examples of this would be `5.67E1` which has the value of 56.7, or `89e-2` which has the value of .89. `float` values can be preceeded by an optional plus or minus sign. The value of the exponent can also be preceeded by an optional plus or minus sign. Additionally, only the integer portion of the float can be omitted for valid values of `float`. This makes `.123` a valid floating point number but not `11.`.

Both `char` and `string` may contain any printable character
between ASCII decimal values 32 and 126 inclusive.
In addition, the following backslash codes are used to represent
special characters:

Code | Value | Meaning
-----|-------|--------
`\a` |  7 | Bell
`\b` |  8 | Backspace
`\e` | 27 | Escape
`\f` | 12 | Form Feed (clear)
`\n` | 10 | Newline
`\r` | 13 | Carriage Return
`\t` |  9 | Tab
`\v` | 11 | Vertical Tab
`\\` | 92 | Backslash
`\'` | 39 | Single Quote
`\"` | 34 | Double Quote
`\0xHH` | HH | The byte given by two characters HH in hexadecimal

(Any other character following a backslash is not valid.)

Both strings and identifiers may be up to **255** characters long, not including the null terminator.

B-minor also supports global arrays of a fixed size, and local arrays of variable size. They may be declared with no value, which causes them to contain all zeros:

```
a: array [5] integer;
```

Or, the entire array may be given specific values:

```
a: array [5] integer = {1,2,3,4,5};
```

## Expressions

B-minor has many of the arithmetic operators found in C, with the same
meaning and level of precedence:

| Symbol | Meaning |
|--------|---------| 
| `()` `[]` `f()` | grouping, array subscript, function call |
| `++` `--`       | postfix increment, decrement |
| `-` `!`         | unary negation, logical not |
| `^`             | exponentiation |
| `*` `/` `%`     | multiplication, division, remainder |
| `+` `-`         | addition, subtraction |
| `<` `<=` `>` `>=` `==` `!=` | comparison |
| `&&`            | logical and |
| `||`            | logical or |
| `=`             | assignment |

B-minor is **strictly typed**.  This means that you may only assign a value
to a variable (or function parameter) if the types match **exactly**.
You cannot perform many of the fast-and-loose conversions found in C.

Following are examples of some (but not all) type errors:
```
x: integer = 65;
y: char = 'A';
if(x>y) ... // error: x and y are of different types!

f: integer = 0;
if(f) ...      // error: f is not a boolean!

writechar: function void ( c: char );
a: integer = 65;
writechar(a);  // error: a is not a char!

b: array [2] boolean = {true,false};
x: integer = 0;
x = b[0];      // error: x is not a boolean!

x: integer = 0;
y: float = x;  // error: integer types can not be implicitly converted to float
```

Following are some (but not all) examples of correct type assignments:
```
b: boolean;
x: integer = 3;
y: integer = 5;
b = x<y;     // ok: the expression x<y is boolean

f: integer = 0;
if(f==0) ...    // ok: f==0 is a boolean expression

c: char = 'a';
if(c=='a') ...  // ok: c and 'a' are both chars
```

## Declarations and Statements

In B-minor, you may declare global variables
with optional constant initializers, function
prototypes, and function definitions.
Within functions, you may declare local variables
(including arrays) with optional initialization expressions.
Scoping rules are identical to C.
Function definitions may not be nested.

Within functions, basic statements may be 
arithmetic expressions, return statements,
print statements, if and if-else statements, 
for loops, or code within inner { } groups:

```
// An arithmetic expression statement.
y = m*x + b;

// A return statement.
return (f-32)*5/9;

// An if-else statement.
if( temp>100 ) {
    print "It's really hot!\n";
} else if( temp>70 ) {
    print "It's pretty warm.\n";
} else {
    print "It's not too bad.\n";
}

// A for loop statement.
for( i=0; i<100; i++ ) {
    print i;
}
```

B-minor does not have switch statements, while-loops, or do-while loops.
(But you could consider adding them as a little extra project.)

The `print` statement is a little unusual
because it is a **statement** and not a function call like `printf` is in C.
`print` takes a list of expressions separated by commas,
and prints each out to the console, like this:

```
print "The temperature is: ", temp, " degrees\n";
```

## Functions

Functions are declared in the same way as variables,
except giving a type of `function` followed by
the return type, arguments, and code:

```
square: function integer ( x: integer ) = {
	return x^2;
}
```

The return type must be one of the four atomic types,
or `void` to indicate no type.  Function arguments
may be of any type.  `integer`, `boolean`,
and `char` arguments are passed by value, while
`string` and `array` arguments are passed
by reference. The implementation of arrays will include a 
`array_length()` function which can be used to obtain the length of
an array at runtime. 

```
printarray: function void ( a: array [] integer ) = {
	i: integer;
	for( i=0;i<array_length(a);i++) {
		print a[i], "\n";
	}
}

```

A function prototype may be given, which states the existence
and type of the function, but includes no code.   This must
be done if the user wishes to call an external function linked
by another library.  For example, to invoke the C function `puts`:

```
puts: function void ( s: string );

main: function integer () = {
	puts("hello world");
}
```

A complete program must have a `main` function
that returns an integer.  the arguments to `main`
may either be empty, or use `argc` and `argv`
with the same meaning as in C:

```
main: function integer ( argc: integer, argv: array [] string ) = {
        puts("hello world");
}
```

## Questions and Clarifications for 2023

Many fine-grained questions about exceptions and corner cases come up
during the semester.  Clarifications will be posted here as they are decided.

### Scanning

- **Q: Is `""` a valid string literal?**

A: Yes, two double quotes represents an empty string consisting only of the null terminator.

- **Q: Is this a valid string literal?**
```
"hello
world"
```

A: No, a newline in a string needs to be escaped, like this: `"hello\nworld"`

- **Q: Do we need to handle #include, #define, and so forth?**

A: No, they are not part of B-minor.

- **Q: Can an integer have a leading negative/positive sign?**

A: Yes, and it's important later that this counts as a single
token, and not as two separate tokens. `-10` and `+123` should scan as NUMBER.

### Parsing

- **Q: Is `print;` a valid statement?**

A: Yes, it means to print out nothing.

- **Q: Is `return;` a valid statement?**

A: Yes, it indicates a return with no value in a `void` function.

- **Q: Does B-minor permit this syntax?**

```
for(i=0;i<10,j<10;i++) { ... }
```

A: No, commas may only be used in `print` statements,
function calls, function prototypes, and array expressions.

- **Q: Can a single statement (without braces) be used after a for-loop or an if-statement?**

A: Yes, the following are valid statements, just as in C and C++:

```
for(i=0;i<10;i++) print i;
if(a) x=y; else z=w;
```

- **Q: Is a single semicolon a valid statement?**

A: No.

- **Q: Can an array be zero length?**

A: No - An array must be declared with a positive length.

- **Q: Can an array initializer by empty?**

A: No - An initializer must either match the length of the array, or be omitted.  It cannot be empty.
(It also avoids the case of an empty initializer `{}` begin confused with an
empty statement block `{}`.

### Pretty Printing

TBA

### Typechecking

- *Q: Can you clarify how each operator can be used?*
A: See section 7.3 in the textbook.

- *Q: Does B-minor allow arrays of functions, functions that return functions, variables of type function, and things of that sort?*
A: No, those should be flagged as type errors, since we won't be implementing them in the code generation.

- *Q: What sort of expression can be used to initialize the length of an array?*
A: When an array is declared as a global variable, the length must be given as a constant integer. When an array is declared as a local variable, its length may be specified as an expression which the typechecker will evaluate as an integer. Any other expression should result in a type error.  When an array is declared as a function parameter, it should have no length given.

-  *Q: What type should be assumed for a variable or function that cannot be resolved?*
A:  There is no good assumption that you can make.  To avoid this problem, you should stop after the name resolution phase, if any name resolution errors are discovered.

### Code Generation

TBA
