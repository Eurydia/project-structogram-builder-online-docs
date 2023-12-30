# Syntax

The NSD builder uses a custom syntax to generate the diagram, which is similar to the C programming language.

Note if you are using a small screen like a phone, the live preview is hidden by default, you can show it by toggling the code button.

## Process

A process is any sequence of characters that is not a statement followed by a semicolon `;`.

Processes will be rendered as is without any modification.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?content=process%3B"></iframe>

Two processes can be placed on the same line, just like in the C programming language.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?content=process%3Banother+process%3B"></iframe>

The builder will not complain if you forgot the semicolon, instead, it will render the processes as as one.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?content=process+another+process"></iframe>

## For and while statement

Under the hood, while statements are converted to for statements, so, in way, they are aliases of each other.

A for state has two components which are the "condition" and the "body".

- Tokens between the parentheses `(` and `)` are considered to be part of the "condition". They loses their meaning and are rendered as is similar to processes.
- Tokens between the curly braces `{` and `}` are considered to be part of the "body". They are rendered as processes and keep their meaning.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?content=for+%28condition%29+%7B%0A++process%3B%0A%7D"></iframe>

Nesting for statements is possible, but you can only nest so deep before the diagram becomes unreadable.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?content=for+%28condition%29+%7B%0A++for+%28another+condition%29+%7B%0A++++for+%28another+another+condition%29+%7B%0A++++++uhhhhh...%3B%0A++++%7D%0A++%7D%0A%7D"></iframe>

Here is an example but with while statements, instead of for statements to show that they are rendered to the same diagram.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?content=while+%28condition%29+%7B%0A++while+%28another+condition%29+%7B%0A++++while+%28another+another+condition%29+%7B%0A++++++uhhhhh...%3B%0A++++%7D%0A++%7D%0A%7D"></iframe>

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
