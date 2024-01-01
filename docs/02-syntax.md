# Syntax

I have constructed a new "language" for this project.
It is designed to be permissive and flexible to make the project easier to learn and use.
Moreover, it has similar syntax to the [C programming language](<https://en.wikipedia.org/wiki/C_(programming_language)>).
I hope this will benefit experienced users, while helping new users.

As of January 1st, 2024, the project supports process blocks, if-else blocks, test-first loop blocks, test-last loop blocks.
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
I refer to the first component as the "condition", and the second component as the "body".

Texts between parentheses are belong to the "condition" component.

Texts between curly braces are belong to the "body" component.

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

## Do-while statement

A do-while statement has two components which are the "condition" and the "body".
Similar to for and while statements, they can be nested but the condition is placed after the body.

- Tokens between the curly braces `{` and `}` are considered to be part of the "body". They are rendered as processes and keep their meaning.
- Tokens between the parentheses `(` and `)` are considered to be part of the "condition". They loses their meaning and are rendered as is similar to processes.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?content=do+%7B%0A++process%3B%0A%7D+while+%28condition%29%3B"></iframe>

Here is an example on nested do-while statements.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?content=do+%7B%0A++do+%7B%0A++++do+%7B%0A++++++uhhhhh...%3B%0A++++%7D+while+%28another+another+condition%29%3B%0A++%7D+while+%28another+condition%29%3B%0A%7D+while+%28condition%29%3B"></iframe>

## If statement

An if statement has two components which are the "condition" and the "body".

- Tokens between the parentheses `(` and `)` are considered to be part of the "condition". They loses their meaning and are rendered as is similar to processes.
- Tokens between the curly braces `{` and `}` are considered to be part of the "body". They are rendered as processes and keep their meaning.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?content=if+%28condition%29+%7B%0A++process%3B%0A%7D"></iframe>

Optionally, the if statement can have an else statement.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?content=if+%28condition%29+%7B%0A++process%3B%0A%7D+else+%7B%0A++another+process%3B%0A%7D"></iframe>

## Context-free grammar

For those of you who are interested, here is the context-free grammar of the language.

- star `*` means zero or more repetitions of the preceding element.
- pipe `|` means "or" only one of the elements can be present.
- square brackets `[]` mean that the enclosed element is optional.
- any character enclosed by single quotes `'` is a literal.

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
