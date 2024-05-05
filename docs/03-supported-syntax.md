# Supported syntax

The syntax draws inspiration from the C-style language with more flexibility to suit our use cases.

The project delivers a comprehensive syntax for various programming constructs, including process blocks, for and while loops, do-while loops, if-else blocks, functions, and comments.

It is worth noting that two structures from the [orignal diagram design](https://www.cs.umd.edu/hcil/members/bshneiderman/nsd/Yoder-Schrag-nassi_schart.pdf) are currently not supported: parallel blocks and switch blocks, the latter being if-else blocks with more than two branches.

> The examples are fully interactive, as such, do feel free to play around and experiment with them.

## Process

From [Wikipedia's article on Nassi–Shneiderman diagram](https://en.wikipedia.org/wiki/Nassi%E2%80%93Shneiderman_diagram):

> "A process represents the simplest of steps and requires no analysis.
> When a process block is encountered, the action described is performed before moving onto the next."

A process is a sequence of words and symbols separated by spaces and terminates by a semicolon.

<iframe width="100%" style="aspect-ratio: 16/10; border:none;" loading="lazy" src="https://eurydia.github.io/project-structogram-builder-online/?preview=true&content=Hello+World%21%3B"></iframe>

A process can contain any number of words and symbols, but it must contain at least one word or symbol.

<iframe width="100%" style="aspect-ratio: 16/10; border:none;" loading="lazy" src="https://eurydia.github.io/project-structogram-builder-online/?preview=true&content=Hello+World%21+but+also+something+else+really+really+really+really+long%3B%0A"></iframe>

## Loop

From Wikipedia's article on Nassi–Shneiderman diagram:

> "The loop allows the program to loop one or a set of processes until a particular condition is fulfilled."

The project supports two types of loops: test-first loops and test-last loops, each differing in the sequence of executed steps.

- **Test-First Loops**: In these loops, the condition is assessed before the execution of processes, aligning with the behavior of for loops and while loops.
- **Test-Last Loops**: Conversely, test-last loops evaluate the condition after the processes have been executed, mirroring the behavior of do-while loops.

Both types of loops consist of two components:

- **Condition Component**: Enclosed within parentheses, this component comprises elements directly derived from the code, and pasted onto the diagram.
- **Body Component**: Enclosed within curly braces, this component defines the processes to be iteratively performed.

### For loop

<iframe width="100%" style="aspect-ratio: 16/10; border:none;" loading="lazy" src="https://eurydia.github.io/project-structogram-builder-online/?preview=true&content=for+%28Condition%29+%7B%0A++Hello+World%21%3B%0A%7D"></iframe>

Additionally, it's worth noting that a test-first loop can be invoked with either "for" or "while."
The project generates the same diagram for both variations, making no distinction between the keywords.

<iframe width="100%" style="aspect-ratio: 16/10; border:none;" loading="lazy" src="https://eurydia.github.io/project-structogram-builder-online/?preview=true&content=while+%28Condition%29+%7B%0A+++Hello+World%21%3B%0A%7D"></iframe>

### Do-while loop

<iframe width="100%" style="aspect-ratio: 16/10; border:none;" loading="lazy" src="https://eurydia.github.io/project-structogram-builder-online/?preview=true&content=do+%7B%0A+++Hello+World%21%3B%0A%7D+while+%28Condition%29%3B"></iframe>

## If-else block

From Wikipedia's article on Nassi–Shneiderman diagram:

> "The simple True/False branching block offers the program two paths to take depending on whether or not a condition has been fulfilled."

If-else blocks consist of two components:

- **Condition Component**: Enclosed within parentheses, this component comprises elements directly derived from the code, and pasted onto the diagram.
- **Body Component**: Enclosed within curly braces, this component defines the processes to be performed when the condition is fulfilled.

<iframe width="100%" style="aspect-ratio: 16/10; border:none;" loading="lazy" src="https://eurydia.github.io/project-structogram-builder-online/?preview=true&content=if+%28Condition%29+%7B%0A++Hello+World%21%3B%0A%7D"></iframe>

The "else" keyword is used to access the other branch.

<iframe width="100%" style="aspect-ratio: 16/10; border:none;" loading="lazy" src="https://eurydia.github.io/project-structogram-builder-online/?preview=true&content=if+%28Condition%29+%7B%0A++Hello+World%21%3B%0A%7D+else+%7B%0A++Hello+Space%21%3B%0A%7D"></iframe>

## Function

> "Functions encapsulate specific sets of processes.
> They promote clarity and reusability."

Functions and procedures within the project are characterized by two components:

- **Declaration Components**: From the beginning of the statement up to the opening curly braces, this component comprises elements directly derived from the code, and pasted onto the diagram.
- **Body Component**: Enclosed within curly braces, this component encapsulates the procedural elements of the function or procedure, defining the processes to be executed.

<iframe width="100%" style="aspect-ratio: 16/10; border:none;" loading="lazy" src="https://eurydia.github.io/project-structogram-builder-online/?preview=true&content=Return_type+Name%28Parameters%29+%7B%0A+Hello+World%21%3B%0A%7D"></iframe>

## Comment

Comments within the project are invoked with two forward slashes. When a line is commented, the remainder of the line is excluded from the diagram.

Importantly, comments are preserved when a diagram is shared through a link.
This ensures that the explanatory remarks remain intact, contributing to the collaborative and communicative nature of the shared diagrams.

<iframe width="100%" style="aspect-ratio: 16/10; border:none;" loading="lazy" src="https://eurydia.github.io/project-structogram-builder-online/?preview=true&content=%2F%2F+The+three+hardest+things+for+people+to+say%3A%0A%2F%2F+I+was+wrong%0A%2F%2F+I+need+help%0A%2F%2F+W-worches%2C+w-wirhest%2C+wooster-shire+sauce%0A%0AI+have+a+hidden+message%3B%0A%0A"></iframe>

## Context-free grammar

Note that:

- a star `*` means zero or more repetitions of the preceding element.
- a plus `+` means one or more repetitions of the preceding element.
- a verticle bar `|` means only one of the elements can be present.
- element enclosed by square brackets `[]` is optional.
- characters enclosed by single quotes `'` is a literal.

```bnf
<diagram> ::= <statement>+

<statement> ::= <token>* ';'
            |   <for-statement>
            |   <while-statement>
            |   <do-while-statement>
            |   <if-statement>
            |   <function>

<for-statement> ::= 'for' '(' <token>* ')' '{' <statement>* '}'

<while-statement> ::= 'while' '(' <token>* ')' '{' <statement>* '}'

<do-while-statement> ::= 'do' '{' <statement>* '}' 'while' '(' <token>* ')' ';'

<if-statement> ::= 'if' '(' <token>* ')' '{' <statement>* '}' ['else' '{'<statement>* '}']

<function> ::= <non-keyword-token>+ <token>* '{' <statement>* '}'

<keyword-token> ::= 'for'
                |   'while'
                |   'do'
                |   'if'

<token> ::= <any-character>+

<any-character> ::= <letter>
                |   <digits>
                |   <non-whitespace-character>
```
