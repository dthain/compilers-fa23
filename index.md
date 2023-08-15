# CSE 40243 - Compilers and Language Design - Fall 2023

## Instructors

|----|----|
|![](images/dthain-small.jpg)| Prof. Douglas Thain (`dthain@nd.edu`)<br> Office Hours: 1-3PM Mon/Wed <br> Office: 384 Fitpatrick Hall|
|![]()| TA: Colin Thomas (`cthoma26@nd.edu`)<br> Office Hours: TBA <br> Office: 150B Fitpatrick Hall (Student Commons)|
|![]()| TA: David Simonetti (`dsimonet@nd.edu`)<br> Office Hours: TBA <br> Office: 150B Fitpatrick Hall (Student Commons)|

## Online Textbook

|----|----|
|![](images/compilerbook-small.jpg)| Douglas Thain,<br>Introduction to Compilers and Language Design,<br>2nd edition, 2020.<br>[http://compilerbook.org](http://compilerbook.org)

## Important Documents

- [Course Syllabus](syllabus.md)
- [Slack Channel](https://nd-cse.slack.com/channels/compilers-fa23)
- [Online Textbook](http://compilerbook.org)
- [Canvas Course Page]()
- [General Assignment Instructions](general.md)
- [Starter Code](https://github.com/dthain/compilerbook-starter-code)
- [Flex Scanner Generator](https://westes.github.io/flex/manual/)
- [Bison Parser Generator](https://www.gnu.org/software/bison/manual/html_node/index.html)
- [B-Minor 2023 Language Guide](bminor.md)

## Course Schedule

(Subject to change as needed.)

|Week | Reading | Monday | Wednesday | Friday | Assignment | Extra Links |
|-----|---------|-------|------------|--------|------------|-------------|
|Aug 21 | Ch 1-2     |                     | Introduction  | Overview    | [Syllabus](syllabus.md)  |
|Aug 28 | Ch 3       | Regular Expressions | Finite Automata       | RE->NFA    | [HW1 Due Wed](homework.md) | / [Hand Parser](https://github.com/cooperative-computing-lab/cctools/blob/master/dttools/src/jx_parse.c#L254) / [Regex 101](https://regex101.com/) / [Regex Golf](http://alf.nu/RegexGolf?world=regex&level=r02) / [Unicode](https://www.joelonsoftware.com/2003/10/08/the-absolute-minimum-every-software-developer-absolutely-positively-must-know-about-unicode-and-character-sets-no-excuses/) |
|Sep 4  | Ch 3       | NFA->DFA            | Flex | Context Free Grammars | [HW2 Due Wed](homework.md) | [Flex Scanner Generator](https://westes.github.io/flex/manual/)
|Sep 11 | Ch 4.1-4.3 | Context Free Grammars  | LL(1) Grammars | LL(1) Parsing    | Scanner Due |
|Sep 18 | Ch 4.4-4.6 |  Shift-Reduce Parsing  | LR(0) Automaton | SLR Parsing     | [HW3 Due Wed](homework.md) |
|Sep 25 | Ch 5       | LR(1) and Recap | Bison                 | Bison            | [HW4 Due Wed](homework.md) |

|Oct 2  | Ch 5       | Parsing B-Minor | Parsing B-Minor       | Abstract Syntax Tree |  | AST Handout](ast.html) |
|Oct 9  | Ch 6       | Abstract Syntax Tree | Review           | **Midterm Exam** | Parser Due     |
|Oct 16 |            | *Fall Break*    | *Fall Break*          | *Fall Break*     |                   |
|Oct 23 | Ch 7       | Type Systems    | Name Resolution       | Typechecking     |                   |
|Oct 30 | Ch 9       | Memory Org      | Memory Org            | Guest Lecture    | Printer Due Tue   |
|Nov 6  | Ch 10      | Assembly        | Assembly              | Assembly         |                   |
|Nov 13 | Ch 11      | Codegen         | Codegen               | Codegen          | [Typecheck Due Mon](typecheck.md)|
|Nov 20 | Ch 11      | Codegen         | *Thanksgiving*        | *Thanksgiving*   |                   |
|Nov 27 | Ch 12      | Optimization    | Garbage Coll.         | Garbage Coll.    |                   |
|Dec 4  |            | Catch Up        | Review                |                  | [Code Generator Due Wed](codegen.md)|
|Dec 11 |            | **Final Exam 8-10AM** |                     |                  |                    |

[CFG Tool](https://web.stanford.edu/class/archive/cs/cs103/cs103.1156/tools/cfg/)
[Joke](https://xkcd.com/1090/)
[Intel Manuals](https://www.intel.com/content/www/us/en/developer/articles/technical/intel-sdm.html)
[Calling Convention](https://refspecs.linuxbase.org/elf/x86_64-abi-0.99.pdf)
[Bison Manual](https://www.gnu.org/software/bison/manual/html_node/index.html)
[Bison Examples](https://github.com/dthain/compilerbook-examples/tree/master/chapter5)

