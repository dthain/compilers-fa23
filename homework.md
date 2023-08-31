# CSE 40243 Homeworks - Fall 2023

Written homework assignments should be submitted via Canvas.

Homework 1 should be a typed document and submitted as a PDF.

Homeworks 2-4 will require drawing out some complex graphs and examples via hand.
Please write these out on paper, then snap pictures and submit to Canvas
as either JPGs or PDF.  Some of these graphs can get rather complicated,
please take the time to draw (or re-draw) them clearly on a clean sheet of paper.
It's fine to start each problem on a new page.

## Homework 1

Select a C or C++ program of your own
creation from a prior class.  It doesn't have to be very large,
but should consist of more than a few functions or methods.
Determine how to invoke the
different parts of the compiler (`gcc` or `g++`) in order
to create the various stages of the compiler pipeline.

Then, answer the following questions:
- Briefly summarize the original purpose and structure of your program.
- Count the number of files, lines, and bytes present in the source code.
- Run the preprocessor on each source file, count the number of lines and bytes, and compare to the source files.  Examine the preprocessed code: is there anything surprising present?
- Run the compiler on each source file to generate object code, and again count and compare the number of bytes.  Use `nm` to observe all of the symbols in the file.  How many symbols are defined, and how many undefined?  Identify at least three undefined symbols, and look up their purpose using `man` or other reference materials, and briefly explain why they are there.
- Generate the final executable, and again count and compare the number of bytes.  Use `nm` to observe all of the symbols in the file.  Again, count the defined and undefined symbols.  Use `ldd` to observe what dynamic libraries the program requires.  Look up the purpose of each library and briefly explain it.
- Generate the final executable again, using the `-static` option to produce a fully statically linked executable.  Again, count the defined and undefined symbols.

Then select one non-trivial function or method from that program,
and show the complete body of that function in each stage of
the compiler:

- Original source of the function.
- Source code after preprocessing.
- Object code after compiling. (Use `objdump` to show readable assembly language.)
- Executable code after linking. (Again, use `objdump`)

Comment on the evolution of the function through each of these stages.
Without knowing X86 assembly language in detail, can you identify parts
of the source code present in the assembly language output?
Is anything surprising?

Compile (ha) your answers together into one large document, taking care
to organize and format answers and code, so that it is easy to follow.
Submit one PDF document via Canvas.

<!--

## Homework 2

1. Match the names of months which end in "ember"

2. Match the pattern of a game of "duck duck goose" 
    
    Ex. "Duck Duck Duck Duck Goose", "Duck Duck Duck Goose"

3. Match any 48-bit MAC address in hexadecimal separated by hyphens. 
    
    Ex. 4C-8F-CE-DA-9E-F3

4. Match any ICAO airport code from airports following the pattern of the United States, Canada, or Mexico    
https://en.wikipedia.org/wiki/ICAO_airport_code    

    Ex. KSBN, MMLP, CYBE 
    
5. Match any valid IPv4 Address in dot-decimal format https://en.wikipedia.org/wiki/Internet_Protocol_version_4
    
    Ex. 192.168.1.1, 10.200.1.1

Do problems 1, 2, 4, 5, 6 at the end of Chapter 3.

## Homework 3
  
Do problems 1, 2, 3, at the end of Chapter 4.

## Homework 4

Do problems 4, 5, 6 at the end of Chapter 4.
-->
