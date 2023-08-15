# Midterm Exam

The midterm exam will be held on Friday, October 14th during the usual class time.
It will be closed book, and no calculators or phones are needed.
The exam will cover chapters 1-6 in the book, and anything from the course
project and homeworks is fair game.  Be sure to study:

- Overall structure and purpose of a compiler.
- Scanning:
    - Formal definition of regular expressions.
    - Writing regular expressions to match various tokens.
    - Converting REs into NFAs using Thompson's construction.
    - Converting NFAs into DFAs using subset construction.
    - Minimizing DFAs using Hopcroft's algorithm.
    - Conversion of regular expressions into NFAs and DFAs.
    - Use of Flex to generate a scanner.
- Context Free Grammars:
    - Identifying and removing ambiguity from CFGs.
    - Top-Down Parsing
        - Recursive Descent Parsing
        - Converting grammars into LL(1) form.
        - Generating and using the LL(1) parse table.
    - Bottom-Up Parsing
        - Converting grammars in to LR(1) form.
        - Generating the LR(0) automaton and parse table.
        - Performing SLR parsing.
        - Generating the LR(1) automaton and parse table.
        - Generating the LALR automaton.
        - Performing LR(1) parsing.
    - Use of Bison to generate a parser.
