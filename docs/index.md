# Documentation for online NSD builder

## Introduction

This is a documentation for the "Online Nassi-Shneiderman diagram builder" that can be found at [https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/](https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/).

I have decided to place the dcumentation in a separate repository because I want to separate the documentation from the code.
The documentation is written in Markdown and is converted to HTML using [MkDocs](https://www.mkdocs.org/), more specifically the [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) theme.

## Motivation

The motivation of the project is to create a tool that can be used to programatically create Nassi-Shneiderman diagrams.

There are a few criteria that the tool has to meet:

- must feature a C-like syntax
- must be flexible and easy to use
- must be online
- must have live preview
- must be able to export the diagram as an image
- must be able to share the diagram as a URL

These criteria are met by the tool, and I am really happy with the result.
During the development, these criteria served as a guide and set the scope of the project.

## Constructed language

The tool uses a constructed language tailored to mimic that of C programming language.
The constructed language could pass a more strict psuedocode, but that is by design.

There is a few keywords and symbols that are used in the language.

Keywords:

- `for`
- `while`
- `do`
- `if`
- `else`

Symbols:

- `;` semicolon
- `(` left parenthesis
- `)` right parenthesis
- `{` left curly brace
- `}` right curly brace

### Process

A process renders to the diagram as is without any modifications.

<iframe src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?content=A+simple+process"></iframe>

Two processes can be placed on the same line by separating them with a semicolon `;`.

<iframe src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?content=A+simple+process%3B%0AAnother+process%3B"></iframe>

Without the semicolon, they are treated as the same process.

<iframe src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?content=A+simple+process%0AAnother+process"></iframe>

### For and while statement

Note that the while statement is simply an alias for the for statement.
Under the hood, the while statement is converted to a for statement, so they are equivalent in every way.

There are two components to the for statement, the "condition" and the "body".

Tokens between the parentheses `(` and `)` are considered to be part of the condition.
They loses their meaning and are rendered as is.

Tokens between the curly braces `{` and `}` are considered to be part of the body.
They are rendered as processes and keep their meaning.

<iframe src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?content=for+%28condition%29+%7B%0A++process%3B%0A++another+process%3B%0A%7D"></iframe>

### Do-while statement

The do-while statement is similar to the for statement, but the "condition" component is placed after the "body" component.

Tokens between the curly braces `{` and `}` are considered to be part of the body.
They are rendered as processes and keep their meaning.

Tokens between the parentheses `(` and `)` are considered to be part of the condition.
They loses their meaning and are rendered as is.

<iframe src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?content=do+%7B%0A++process%3B%0A++another+process%3B%0A%7D+while+%28condition%29%3B"></iframe>

### If statement

There are two components to the if statement, the "condition" and the "body".

Tokens between the parentheses `(` and `)` are considered to be part of the condition.
They loses their meaning and are rendered as is.

Tokens between the curly braces `{` and `}` are considered to be part of the body.
They are rendered as processes and keep their meaning.

<iframe src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?content=if+%28condition%29+%7B%0A++process%3B%0A++another+process%3B%0A%7D"></iframe>

Optionally, the if statement can have an else statement.

<iframe src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?content=if+%28condition%29+%7B%0A++process%3B%0A++another+process%3B%0A%7D+else+%7B%0A++process%3B%0A++another+process%3B%0A%7D"></iframe>

### Context-free grammar

- star `*` means zero or more repetitions of the preceding element.
- pipe `|` means "or" only one of the elements can be present.
- square brackets `[]` mean that the enclosed element is optional.
- any character enclosed by single quotes `'` is a literal.

```bnf
<diagram> ::= <statement>

<statement> ::=   <token>* ';'          |
                  <for-statement>       |
                  <while-statement>     |
                  <do-while-statement>  |
                  <if-statement>

<for-statement> ::= 'for' '(' <token>* ')' '{' <statement>* '}'

<while-statement> ::= 'while' '(' <token>* ')' '{' <statement>* '}'

<do-while-statement> ::= 'do' '{' <statement>* '}' 'while' '(' <token>* ')' ';'

<if-statement> ::= 'if' '(' <token>* ')' '{' <statement>* '}' ['else' '{'<statement>* '}']

<token> ::= <any-character>+
<any-character> ::= <letter> |
                    <digits> |
                    <non-whitespace-character>
```
