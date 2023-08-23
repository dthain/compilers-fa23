# Syllabus - CSE 40243/60243 - Compilers and Language Design - Fall 2022

## Instructors

Prof. Douglas Thain
- Email: `dthain@nd.edu`
- Office: 384C Fitzpatrick Hall
- Office Hours: 1-3PM Mon/Thu

TA: Colin Thomas
- Email: `cthoma26@nd.edu`
- Office: 150B Fitzpatrick (CSE Student Commons)
- Office Hours: 3-5PM Mon/Wed

TA: David Simonetti
- Email: `dsimone2@nd.edu`
- Office: 150B Fitzpatrick (CSE Student Commons)
- Office Hours: 3-5PM Tue/Thu

## Overview

This class will introduce students to the theory and practice of compilers.
Students will construct a working compiler
that transforms C into x86 assembly.  This project will proceed in five
steps, requiring the construction of a scanner, parser, type checker,
source translator, and code generator.   More theoretical topics will
be explored in lectures and written assignments and evaluated in exams.

This will be a fun and challenging course for advanced undergraduates
as well as graduate students.  Compilers cover a broad array of topics in computer
science, ranging from the abstract theory of automata to the very practical details
of assembly languages.   In addition, students will gain experience with tools
and techniques for software engineering.
Students completing this course will gain a broad range of skills valuable
in both the job market and in graduate studies.

Graduate students taking 60243 will attend the same class but will have
some additional work to earn graduate credit, including an expository
paper on a modern compiler technique, and a substantial extension to
the project compiler.

The textbook is online and your are welcome to download 
PDFs for online reading, or purchase a hard copy online.
Make a habit of reading the appropriate chapter over the weekend before
Monday's lecture begins.  (Read Chapters 1 and 2 today.)

Note there are still a few typos lurking here and there in the book,
and I will grant a little credit (1/10th of a point) for each typo
correctly reported and fixed, up to a maximum of 10 points.  Read carefully!

## Course Web Page

[http://dthain.github.io/compilers-fa23](http://dthain.github.io/compilers-fa23)

## Textbook

- Print: [Douglas Thain, Introduction to Compilers and Language Design, 2nd edition, 2021.](http://compilerbook.org)
- Online: `compilerbook.org`

## Suggested References
- Aho, Lam, Sethi, Ullman, "Compilers: Principles, Techniques, and Tools", Pearson, 2007.
- [Intel Corp, "Intel-64 and IA-32 Architectures Software Developer's Manuals", 2015](https://www.intel.com/content/www/us/en/developer/articles/technical/intel-sdm.html)

## Course Goals and Evaluation

- Discuss the role and limitations of the compiler in a computer system. (Midterm, Final)
- Create and analyze finite state automata for lexical analysis. (Project 1, Midterm, Homework 1)
- Create and analyze parsing algorithms for common catetgories of grammars. (Project 2, Midterm, Homework 2)
- Apply type theory to find bugs in compiled programs. (Project 3, Midterm and/or Final)
- Create and analyze direct and pattern-matching code generators. (Project 4, Final)
- Understand and apply basic optimization techniques. (Final)
- Employ standard tools to create scanners, parsers, and code generators. (Projects 1, 2, and 4)
- Construct a complete working compiler for a small language. (Overall Project)

## How to Get the Most Out of Class

To succeed in the class, you should attend all class meetings,
take notes, and participate in class discussions.
During most class sessions, I'll give a prepared lecture for about 30 minutes,
and then we will shift into Q&amp;A or working on an example. 

The textbook is dense in places; sometimes a key algorithm may only occupy
two pages in the book, but requires 30 minutes of class discussion
to work out all the details.  So, it works best if you read the textbook
for a broad understanding before class, and then go back and review details
and work some examples afterward.

Because much of the class material involves working with data structures
and examples of algorithms, I will mostly work on the blackboard instead
of presenting slide decks.  I recommend that you take notes by sketching
along with pen and paper: the simple act of note-taking exercises your
mental muscles in a way that passive observation does not.  If you prefer to
take notes on your laptop or tablet, then that's fine too.

However, I do ask that you refrain from using your laptops or phones
for non-class related tasks during class time.  I know it is tempting
during a brief lull to respond to messages, check the news, etc,
but even one laptop open can be an unavoidable distraction for other
people in the class.  Let's reserve this time for working together.

Also note that this class is designed to be primarily an in-person
learning experience.  Class recordings are a backup available if you
are sick or otherwise excused.  But don't use recordings as a substitute
for attending.

## Communications

Assignments and the course schedule are available on the course website,
and assignment grades will be posted in Canvas.
We will be using Slack (\#compilers-fa23) to handle general Q&amp;A for the class.
If you have a technical question that could be of interest to others,
please post it here, so that others can benefit from the answers.

You are welcome to post (or answer) questions anytime, and we will
generally monitor and answer questions on weekday afternoons.
(Keep in mind that we do go home at night, and so late-night questions
will get answered the next day.)

For questions about grades or anything else that just applies specifically
to you, just email the instructor or TA directly.

Office hours are a good to get focused help on a tricky bit
of code or homework problem.  We are happy to help you during that
time -- just knock, come in, and introduce yourself.
If you can't make any of the office hours, then send email to
see if we can work out another time.

## Grading Policies

Written homeworks will be submitted as PDFs or images on Canvas,
and programming assignments must be pushed to your private github
repository by the deadline.  Both are due **before 11:59PM** on the date due.

**Late assignments will receive no credit.**
You are free to turn in programming assignments
multiple times before the deadline expires, so it
would be a good habit to turn in your partial work
on a daily basis, so as to ensure something is submitted.

Exceptions will only be made for serious circumstances
such as an extended illness, death in the family,
mandatory participation in a university sponsored event,
or the other items outlined in section 3.1 of the Undergraduate Academic Code.
In those cases, please confer with the instructor at the earliest possibility,
and we will make alternate arrangements.

For each assignment, a numeric grade will be awarded.
Throughout the semester, grades and class averages will be posted through Sakai.
At the end of the semester, I'll convert number grades to letter grades on
a scale of A/B/C/D = 90/80/70/65, and exercise some prudential judgement
for pluses and minuses and borderline grades.

If you believe that an error has been made in grading an item,
please bring it to the attention of the person who graded it
(usually the TA) within seven days. Mistakes do occasionally
happen in grading, so factual and clerical errors will be
cheerfully corrected.  Matters of judgement are reserved to the grader.
If, after talking to the grader, you are unconvinced,
you can bring it up with Prof. Thain.

For undergraduate students in CSE 40243, grades are weighted as follows:
Homeworks 15%, Code Assignments 55%, Midterm 15%, Final 15%.

For graduate students in CSE 60243, grades are weighted as follows:
Homeworks 10%, Code Assignments 50%, Paper 10%, Midterm 15%, Final 15%.

## Academic Code of Honor

As a student at Notre Dame, you are bound by the [Academic Code of Honor] (http://honorcode.nd.edu),
which states:

*As a member of the Notre Dame community, I acknowledge that it is my responsibility to learn and abide by principles of intellectual honesty and academic integrity, and therefore I will not participate in or tolerate academic dishonesty.*

The purpose of the homeworks and assignments in this course is for each student
to gain the discipline and skills in analysis, design, and programming so that
they will be able to work independently in a professional setting.
To that end, all exams, homeworks, and programming assignments are to be completed individually.
Each student must write their own code from scratch with their own hands
based on their own understanding of the course material.

- You **may** consult with other students and outside resources in order to
better understand concepts and techniques, or to debug localized problems.
- You **may not** copy code from another student or resource (or AI assistant!),
excepting the "starter code" provided by the instructor.

## Some Campus Resources

- If you require an accommodation for a disability, please first contact the
Sara Bea Center [http://sarabeadisabilityservices.nd.edu](sarabeadisabilityservices.nd.edu) for a consultation, and we will be happy to work together on a solution.
-  If you encounter a difficult life situation and don't know what to do,
the University Counseling Center [http://ucc.nd.edu](http://ucc.nd.edu) or the Care and Wellness Consultants [http://care.nd.edu](care.nd.edu) can help and also connect you with other campus resources.
