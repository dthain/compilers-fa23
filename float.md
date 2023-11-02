# Floating Point Code Generation Handbook 

## Floating point overview

The Bminor language specifies [double precision floating point](https://en.wikipedia.org/wiki/IEEE_754). This means that floating point variables are stored as 64 bit values (equivalent to C's `double` type).

There are four supported arithmetic operators for floating point types for simplicity: +, -, *, / (an aspiring student could add support for more operators). The six comparison operators (< <= > >= == !=) are also supported.

## Floating point representation

In a normal assembler, one could write the following to represent the global x with a floating point number value of 5.5:

```
x:
  	.quad 5.5
```

We would hope that the assembler could do the work for us of convering the floating point 5.5 to its binary value. In GCC's assembly synatx, things are not quite so simple! If you compile a C program using double values to assembly using GCC, you'll find something interesting:

```
x:
    .long   858993459
    .long   1072902963
```

GCC does some bit hacking and stores floating point values as integers (since doubles are 64 bits wide, a single double takes two long values of 32 bits each). In order to simplify things, we can instead store the floating point value as a single 64 bit value. We can perform the conversion using something like the C program below:

```
#include <stdio.h>

int main()
{
        double x = 5.5;
        long *p = &x;
        printf("%ld\n", *p);
}
```

The magic happens in the following line: `long *p = &x;`. We take the binary representation of the double value 5.5 and bit hack it into the value of a long (64) bit integer. When we print out the value of *p, we get `4617878467915022336`. This means we can instead write the following assembly:

```
x:
  	.quad 4617878467915022336
```

And now x has the correct floating point representation for 5.5

## Registers
All 64 bit floating point computations on modern x86-64 systems are performed in the xmm registers. These are 128 bit wide registers that can also be used for vector operations, but for our purposes they will be general purpose floating point registers. There are 8 xmm registers, xmm0-xmm8. We can load a floating point value into one of these registers like any other register (assuming we have the global x shown above):

```
    MOVSD   x, %xmm0
```

MOVSD is a special mov instruction used for double precision floating point values. After running this operation, the xmm0 register has the floating point representation of whatever value is in x (5.5 in this case). The upper 64 bits of the register are zeroed out.

## Arithmetic operations
Lets say we want to add two global floating point values x and y (with values 5.5 and 3.5 respectively). We load x into xmm0 and y into xmm1. If we want to add x and y and store it into xmm0, we can use the ADDSD instruction:

```
x:
  	.quad 4617878467915022336 # 5.5
y:
  	.quad 4614838538166547251 # 3.4

...

    MOVSD   x, %xmm0     # xmm0 has the value of x
    MOVSD   y, %xmm1     # xmm1 has the value of y
    ADDSD   %xmm1, %xmm0 # xmm0 has the value of x + y
```

To perform subtraction instead, one could use the `SUBSD` instruction similarly.

Multiplication and divison are easier for floating point values than integer values because the xmm registers are already 128 bits. Here are some examples

```
x:
  	.quad 4617878467915022336 # 5.5
y:
  	.quad 4614838538166547251 # 3.4

...

    MOVSD   x, %xmm0     # xmm0 has the value of x
    MOVSD   y, %xmm1     # xmm1 has the value of y
    MULSD   %xmm1, %xmm0 # xmm0 has the value of x * y (18.7)
    DIVSD   %xmm1, %xmm0 # xmm0 has the value of (x * y) / y = x (5.5)
```

## Function calls
Floating point values have special rules when used as parameters of a function. Here is a rough overview:
* The first 8 floating point arguments are placed in xmm0-xmm7 
* The number of floating point argument is placed in rax

Lets say we want to call the following C function:

```
void print_float(double y) {
    printf("%lf", y);
}
```

It is expecting a single double precision floating point value as an argument.

```
x:
  	.quad 4617878467915022336 # 5.5

...
        MOVSD   x, %xmm0     # xmm0 has the value of x
        MOVQ    $1, %rax     # number of floating point arguments
        call print_float
```