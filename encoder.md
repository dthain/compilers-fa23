# Encoder Assignment

For the first step of the compiler, you are going to write
a small amount of code to handle the encoding and decoding
of strings.  This won't be a large amount of code, but will
get you started on the process of writing testable functions,
generating complete test cases, and turning in via github.

## Getting Started with Git

First, follow the [general instructions](general) to clone
the starter code repository, set up the permissions, and make
a local copy.  (You won't need anything from the starter code
just yet, but it's easier to add everything at the beginning.)

## Encode/Decode Functions

Read the [B-Minor Specification](bminor.md) and carefully
look at the definition of strings, which may contain ordinary
characters, or a number of backslash codes.  When it encounters
such a string, your compiler must convert it into an ordinary C string.

Write two functions like this:

```
int string_decode( const char *es, char *s );
int string_encode( const char *s, char *es );
```

`string_decode` should take in an encoded input string `es` containing
quotes and (possibly) backslash codes, then convert it into a normal string `s`
without quotes or codes.  If the input string is valid and the conversion
is successful, it should return true.  Otherwise, it should return false.
`string_encode` should do the opposite and convert a normal string into
an encoded string that can be printed back out.

For example, if the input encoded string looks like this:

![](encode1.png)

Then `string_decode` should convert it into this:

![](encode2.png)

In a similar way, `string_encode` should reverse the process.

## Main Program

Then, write a main program called `bminor` to exercise your functions.
(This program will eventually become the main program of your whole compiler.)

```
./bminor --encode input.bminor
```

This main program should open the filename given on the command line,
read in the first line of the file and feed it to `string_decode`
.
If it contains a valid string, then use `string_encode` to convert
it back <s>(check that it is the same string)</s>, print it back out,
and exit indicating success.

On the other hand, if the input is not a valid string, then
print a detailed error message and exit indicating failure.

## Testing

A compiler has many odd corner cases that you must carefully handle.
The way to ensure that your program meets its requirements is to
generate a large number of test cases, and run them after making any change.

To that end, we will require you to turn in twenty test cases
at each step of the compiler.  (You are very welcome to write more than that!)
Create ten files called `test/encode/good[0-9].bminor` each containing
a valid B-minor string, and `test/encode/bad[0-9].bminor` each containing invalid
strings.  Take some time to think carefully about the wide variety of possible
good and bad cases.

The exit status of `bminor` is **very important** because it indicates to the caller whether the program succeeded or not.  The Unix convention is that the result of `main` (or the call to `exit`) should be zero to indicate success and non-zero to indicate failure.  We will use the program exit status to determine the correctness of your submissions and your test.

You can do the same by creating a script called `runtest.sh` that does something like this:

```
#!/bin/sh

for testfile in test/encode/good*.bminor
do
	if bminor --encode $testfile > $testfile.out
	then
		echo "$testfile success (as expected)"
	else
		echo "$testfile failure (INCORRECT)"
	fi
done

for testfile in test/encode/bad*.bminor
do
	if bminor --encode test/encode/$testfile > $testfile.out
	then
		echo "$testfile success (INCORRECT)"
	else
		echo "$testfile failure (as expected)"
	fi
done
```

## Make a Makefile

Now is the time to have a proper Makefile, and use it to build your compiler at all stages.  Make sure that the following commands work:
- `make` should build the program `bminor` from sources.
- `make clean` should remove all executables and object files.
- `make test` should run all your test cases.

## Turning In

Be sure to `git add` and `git commit` all of your source files to your repository.  (Don't add object files, executables files, or anything else that is built from source files.)  Then review the [General Instructions for Turning In](general.md).  Make sure that your code is tagged as a release named `encoder`.

**This assignment is due on Thursday, August 31st at 11:59PM  Late assignments are not accepted.**

