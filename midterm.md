# Midterm Exam

The midterm exam will be held on Friday, October 13th during the usual class time.
It will be closed book, and no calculators or phones are needed.
The exam will cover chapters 1-5 in the book, and anything from the course
project and homeworks is fair game.  Expect about four pages, each one covering a different problem.
Be sure to study:

- Overall structure and purpose of a compiler.
- Scanning:
    - Formal definition of regular expressions.
    - Writing regular expressions to match various tokens.
    - Converting REs into NFAs using Thompson's construction.
    - Converting NFAs into DFAs using subset construction.
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

An excellent way to study for the exam would be to work in small groups,
and propose problems that are variations on those found in the homeworks.
Work your solutions independently first, and then get together to see if you 
agree on the results. 

Need some additional grammars to practice on?  Try some of these taken from previous midterms.
Practice converting to LL form, writing out First/Follow, making parse tables, and then
parsing.  Then, do the same for SLR and LR(1).

- Grammar 101:
```
E -> E + E
E -> T
T -> id
T -> id ( L )
L -> E, L
L -> E
```

- Grammar 102:
```
S -> ID = E
E -> E + P
E -> P
P -> id
P -> id = E
```

- Grammar 103:
```
E -> E + E
E -> E * E
E -> id
E -> id ( E ) ;
E -> id [ E ] ;
```

- Grammar 104:
```
P -> E
E -> E * T
E -> T
T -> id ( E )
T -> id = E
T -> ( E )
```

- Grammar 105:
```
P -> { L }
L -> S L
L -> S
S -> id = E ;
E -> E * E
E -> id
E -> id ( E ) ;
```

