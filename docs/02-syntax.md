# Syntax

I have constructed a new "language" for this project.
It is designed to be permissive and flexible to make the project easier to learn and use.
Moreover, it has similar syntax to the [C programming language](<https://en.wikipedia.org/wiki/C_(programming_language)>).
I hope this will benefit experienced users, while helping new users.

As of January 1st, 2024, the project supports process blocks, test-first loop blocks, test-last loop blocks, and if-else blocks.
I do not plan to add support for switch blocks since if-else blocks convey the same idea.
Functions and procedures are relatively easy to implement, but the project does not supoort them yet.

On this section, I have embedded multiple interactive examples using `iframe` elements.
However, on smaller screens, live preview is shown by default.

## Process block

Process block are rendered as is without modification.
They are pieces of text followed by a semicolon `;`.
I want users to imagine a process block as a text box which you can write anything on.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?content=process%3B"></iframe>

Process blocks are permissive.
I have included three ways to convey variable assignment, but the project does not enforce any particular style.

If you are an ELTE student, you might want to use the `:=` operator.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?content=x+%3A%3D+0%3B"></iframe>

I have seen some Wikipedia articles, for example [Insertion sort](https://en.wikipedia.org/wiki/Insertion_sort#Algorithm), uses the `<-` operator.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?content=x+%3C-+0%3B"></iframe>

Even better, you can describe what you want in the process.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?content=Initialize+a+variable+%22x%22+and+%0Aassign+integer+%220%22+to+it."></iframe>

## Test-first loop block

Test-first loop blocks, also known as for loops or while loops, have two components.
First, texts between parentheses are belong to the "condition" component.
Second, texts between curly braces are belong to the "body" component.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?content=for+%28condition%29+%7B%0A++process%3B%0A%7D"></iframe>

Nesting loops is possible, but you can only nest so deep before the diagram becomes unreadable.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?content=for+%28condition%29+%7B%0A++for+%28another+condition%29+%7B%0A++++for+%28another+another+condition%29+%7B%0A++++++uhhhhh...%3B%0A++++%7D%0A++%7D%0A%7D"></iframe>

I want to mention that the project does not distinguish between for loops and while loops.
Internally, they are the exact same.
Here is the example above but written with while loops.
They produce the same diagram.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?content=while+%28condition%29+%7B%0A++while+%28another+condition%29+%7B%0A++++while+%28another+another+condition%29+%7B%0A++++++uhhhhh...%3B%0A++++%7D%0A++%7D%0A%7D"></iframe>

The condition component is flexible much like process blocks.
I have included a few ways you might write a test-first loop block.

If you are an ELTE student, you might want to use the following syntax.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?content=for+%28i+%3D+1..10%29+%7B%0A++...%3B%0A%7D"></iframe>

Some pseudocode uses `<-` to signifies each iteration.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?content=for+%28i+%3C-+1..10%29+%7B%0A++...%3B%0A%7D"></iframe>

The property of the double dots can be confusing, so we can also write a description.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?content=for+%28i+%3C-+from+1+to+10+increment+by+1%29+%7B%0A++...%3B%0A%7D"></iframe>

## Test-last loop block

Test-last loop blocks, also known as do-while loops, has two components.
First, texts between curly braces are belong to the "body" component.
Second, texts between parentheses are belong to the "condition" component.

Generally, test-last loop blocks supports everything that [test-first loop blocks](#test-first-loop-block) supports.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?content=do+%7B%0A++process%3B%0A%7D+while+%28condition%29%3B"></iframe>

## If-else block

If blocks have two components.
First, texts between parentheses are belong to the "condition" component.
Second, texts between curly braces are belong to the "body" component.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?content=if+%28condition%29+%7B%0A++process%3B%0A%7D"></iframe>

Optionally, you can convert an if block into an if-else block using the `else` keyword.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?content=if+%28condition%29+%7B%0A++process%3B%0A%7D+else+%7B%0A++another+process%3B%0A%7D"></iframe>

## Context-free grammar

For those of you who are interested, here is the context-free grammar of the constructed language.

Note that:

- a star `*` means zero or more repetitions of the preceding element.
- a plus `+` means one or more repetitions of the preceding element.
- a verticle bar `|` means "or" only one of the elements can be present.
- element enclosed by square brackets `[]` is optional.
- characters enclosed by single quotes `'` is a literal.

```bnf
<diagram> ::= <statement>

<statement> ::= <token>* ';'
            |   <for-statement>
            |   <while-statement>
            |   <do-while-statement>
            |   <if-statement>

<for-statement> ::= 'for' '(' <token>* ')' '{' <statement>* '}'

<while-statement> ::= 'while' '(' <token>* ')' '{' <statement>* '}'

<do-while-statement> ::= 'do' '{' <statement>* '}' 'while' '(' <token>* ')' ';'

<if-statement> ::= 'if' '(' <token>* ')' '{' <statement>* '}' ['else' '{'<statement>* '}']

<token> ::= <any-character>+

<any-character> ::= <letter>
                |   <digits>
                |   <non-whitespace-character>
```
