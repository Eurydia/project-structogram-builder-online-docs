# Lexer

The lexer tokenizes the user input.
Its implementation can be found at the [lexer](https://github.com/Eurydia/project-nassi-shneiderman-diagram-builder-online/blob/1bf484c9082dc5ea0fcfc6cf37121d273f7831b5/src/interpreter/lexer.ts) module.

The interface of the module is as follows:

```ts
// src/interpreter/lexer.ts
export enum TokenKind {}
export type Token;

const KEYWORDS: string[];
const LITERAL_TOKENS: Record<string, TokenKind>;

export type Lexer;

export const lexerInit: (content: string) => Lexer;
export const lexerGetAllTokens: (lexer: Lexer) => Token[];
const lexerSafeGetNextCharThenAdvance: (lexer: Lexer) => string;
const lexerSafeGetNextTokenThenAdvance: (lexer: Lexer) => Token;
const lexerTrimLeft: (lexer: Lexer) => void;
```

## `TokenKind` enum

```ts
export enum TokenKind {
	END = 0,
	SYMBOL,
	KEYWORD,

	LEFT_PAREN,
	RIGHT_PAREN,
	LEFT_CURLY,
	RIGHT_CURLY,
	SEMICOLON,
}
```

The `TokenKind` enum represents the type of a token.
I have decided to keep the token types as simple as possible.

I should mention that `TokenKind.LEFT_PAREN`, `TokenKind.RIGHT_PAREN`, `TokenKind.LEFT_CURLY`, `TokenKind.RIGHT_CURLY`, and `TokenKind.SEMICOLON` serve the same role.
They are literal tokens.

### `TokenKind.END`

`TokenKind.END` represents the end of the input.

This token type tells the lexer to terminate.

### `TokenKind.SYMBOL`

`TokenKind.SYMBOL` represents symbols.

A symbol is a sequence of non-whitespace non-literal characters non-keyword characters.

So for example, the following input:

```txt
result: int := 0
```

would be tokenized as:

```json
["result", ":", "int", ":=", "0"]
```

### `TokenKind.KEYWORD`

`TokenKind.KEYWORD` represents reserved keywords

There are five reserved keywords which are `for`, `if`, `else`, `while`, and `do`.

The list `KEYWORD` contains all the keywords that the lexer recognizes and helped the lexer to determine whether a symbol is a keyword or not.

## `Token` type

```ts
export type Token = {
	kind: TokenKind;
	text: string;
};
```

The `Token` type represents a token.

It has two properties: `kind` and `text`.

### `Token.kind` property

`Token.kind` stores the type of the token, represented as a `TokenKind` enum.

### `Token.text` property

`Token.text` stores the text of the token.

The lexer removes all whitespace characters, so the `text` property will always contain some text.

The only exception is `TokenKind.END` tokens which has an empty `text` property.

## `Lexer` type

```ts
export type Lexer = {
	content: string;
	contentLength: number;
	cursorPos: number;
};
```

The `Lexer` type represents the lexer.

It has three properties: `content`, `contentLength`, and `cursorPos`.

Lexers should be initialized using the `lexerInit` function to ensure that the input is properly sanitized.

To tokenize the input, the lexer uses the `lexerGetAllTokens` function which returns a list of `Token`.

### `Lexer.content` property

`Lexer.content` stores the user input.

This string is not explicitly immutable, but the lexer does not change the string in any way.

### `Lexer.contentLength` property

`Lexer.contentLength` stores the length of the input string.

It ensures that the lexer does not go out of bounds when advancing the cursor causing an index out of bounds error.

### `Lexer.cursorPos` property

`Lexer.cursorPos` stores the current position of the lexer.

It keeps track of the current position of the lexer in the input string, and instead of modifying the input string, the lexer advances the cursor.

## `lexerInit` function

```ts
export const lexerInit: (
	content: string,
) => Lexer;
```

The `lexerInit` function initializes a lexer from user input.

It calls `normalize()` on `content`, set the `content` and `contentLength`, set `cursor` properties to zero.
Then, it returns the lexer object.

## `lexerGetAllTokens` function

```ts
export const lexerGetAllTokens: (
	lexer: Lexer,
) => Token[];
```

The `lexerGetAllTokens` returns a list of all token in the lexer.

I added this function to simplify the interface of the module.

Internally, this function calls `lexerSafeGetNextTokenThenAdvance` until it reaches a `TokenKind.END` token, in which case it terminates, and returns the list of collected tokens.

Note that this function does not return the `TokenKind.END` token.

## `lexerSafeGetNextTokenThenAdvance` function

```ts
const lexerSafeGetNextTokenThenAdvance: (
	lexer: Lexer,
) => Token;
```

The `lexerSafeGetNextTokenThenAdvance` function returns a `Token` with proper `kind` and `text` property.
It returns a `TokenKind.END` token when it is unable to tokenize.

This function does a majority of the lexing work.
So I will try to explain it in detail.

Firstly, it calls `lexerTrimLeft` to skip all leading whitespace characters.

Then, it checks if the lexer has reached the end of the input.
If it has reached the end, it returns a `TokenKind.END` token.

If there are characters left, it calls `lexerSafeGetNextCharThenAdvance` to get the next character, this collects the current character and moves the cursor forward.

Then, it checks if the current character is a literal token or not.
If it is, it returns a token with appropriate `TokenKind` kind.

If it is not a literal token, it collects the rest of the characters until it reaches a whitespace character or a literal token.

Then it checks whether the collected characters forms a keyword or not.

If they form a keyword, it returns a `TokenKind.KEYWORD` token.

If they do not form a keyword, it returns a `TokenKind.SYMBOL` token.

## `lexerSafeGetNextCharThenAdvance` function

```ts
const lexerSafeGetNextCharThenAdvance: (
	lexer: Lexer,
) => string;
```

The `lexerSafeGetNextCharThenAdvance` function collects the current character and moves the cursor forward.

If the cursor has reached the end, it returns an empty string.

## `lexerTrimLeft` function

```ts
const lexerTrimLeft: (lexer: Lexer) => void;
```

This function skips all leading whitespace characters by moving the cursor forward until it reaches the first a non-whitespace character.
