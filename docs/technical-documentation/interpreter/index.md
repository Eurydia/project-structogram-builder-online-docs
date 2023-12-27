# Overview

This section of the documentation will discuss about the interpter which is responsible generating an AST from user input.

The interpreter consists of two components: the lexer and the parser both of whic hare written in pure TypeScript.
I did not used any external libraries for the lexer and the parser, and I wrote them from scratch and inituition, so the implementation may not be the most efficient.

Each of these are placed in their own module at `src/interpreter/lexer.ts` and `src/interpreter/parser.ts` respectively.

## Lexer

The lexer is responsible for tokenizing the user input.
Its implementation can be found at `src/interpreter/lexer.ts`.

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

Let's discuss each of these in detail.

### `TokenKind` enum

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
I have decided to keep the token types as simple as possible, so the lexer only recognizes the following token types:

#### `TokenKind.END`

`TokenKind.END` represents the end of the input.
I used this to indicate the end of the input to the parser to avoid having to check for `undefined` or `null` values.

#### `TokenKind.SYMBOL`

`TokenKind.SYMBOL` represents symbols, but I should clarify that a symbol is a sequence of non-whitespace, non-literal characters, non-keyword characters.

So for example, the following input:

```txt
result: int := 0
```

would be tokenized as:

```ts
[
	{ kind: TokenKind.Symbol, value: "result" },
	{ kind: TokenKind.Symbol, value: "int" },
	{ kind: TokenKind.Symbol, value: ":=" },
	{ kind: TokenKind.Symbol, value: "0" },
];
```

#### `TokenKind.KEYWORD`

`TokenKind.KEYWORD` represents reserved keywords which are `for`, `if`, `else`, `while`, and `do`.

The list `KEYWORD` contains all the keywords that the lexer recognizes and helped the lexer to determine whether a symbol is a keyword or not.

### `Token` type

```ts
export type Token = {
	kind: TokenKind;
	text: string;
};
```

The `Token` type represents a token.
Since there will be a lot of tokens, I decided to keep it as simple as possible, so it only has two properties: `kind` and `text`.

#### `Token.kind` property

`Token.kind` stores the type of the token, represented as a `TokenKind` enum.

#### `Token.text` property

`Token.text` stores the text of the token since the lexer removes all whitespace characters, the `text` property cannot be empty and will always contain some text.

The only exception to this is the `TokenKind.END` token which has an empty `text` property.

### `Lexer` type

```ts
export type Lexer = {
	content: string;
	contentLength: number;
	cursor: number;
};
```

The `Lexer` type represents the lexer.
It is a simple object with three properties: `content`, `contentLength`, and `cursor`.

Lexers should be initialized using the `lexerInit` function to ensure that the input is properly sanitized.

To tokenize the input, the lexer uses the `lexerGetAllTokens` function which returns a list of `Token`s.

#### `Lexer.content` property

`Lexer.content` stores the input as a string.
This string is not explicitly immutable, but the lexer does not change the string in any way.

#### `Lexer.contentLength` property

`Lexer.contentLength` stores the length of the input string.
It ensures that the lexer does not go out of bounds when advancing the cursor causing an index out of bounds error.

#### `Lexer.cursor` property

`Lexer.cursor` stores the current position of the lexer.
It keeps track of the current position of the lexer in the input string, and instead of modifying the input string, the lexer advances the cursor.

### `lexerInit` function

```ts
export const lexerInit: (
	content: string,
) => Lexer;
```

The `lexerInit` function initializes a lexer from the input string.
It calls `.normalize` on the input string, set the `content` and `contentLength`, set `cursor` properties to zero.
Then, it returns the lexer object.

### `lexerGetAllTokens` function

```ts
export const lexerGetAllTokens: (
	lexer: Lexer,
) => Token[];
```

The `lexerGetAllTokens` function calls other functions in the module.
I added this function to simplify the interface of the module, so I only need to call this function to tokenize the input.

Internally, this function calls `lexerSafeGetNextTokenThenAdvance` until it reaches a `TokenKind.END` token, in which case it terminates, and returns the list of collected tokens.

Note that this function does not return the `TokenKind.END` token.

### `lexerSafeGetNextTokenThenAdvance` function

```ts
const lexerSafeGetNextTokenThenAdvance: (
	lexer: Lexer,
) => Token;
```

This function does a majority of the lexing work.
So I will try to explain it in detail.

Firstly, it calls `lexerTrimLeft` to skip all leading whitespace characters.

Then, it checks if the lexer has reached the end of the input, in which case it returns a `TokenKind.END` token.

If there are characters left, it calls `lexerSafeGetNextCharThenAdvance` to get the next character, this collects the current character and moves the cursor forward.

Then, it checks if the current character is a literal token or not.
If it is, it returns a token with appropriate `TokenKind`.

If not, it collects the rest of the characters until it reaches a whitespace character or a literal token, then it checks whether the collected characters are a keyword or not.

If it is a keyword, it returns a `TokenKind.KEYWORD` token.
If not, it returns a `TokenKind.SYMBOL` token.

### `lexerSafeGetNextCharThenAdvance` function

```ts
const lexerSafeGetNextCharThenAdvance: (
	lexer: Lexer,
) => string;
```

This function collects the current character and moves the cursor forward.

If the cursor is at the end of the input, it returns an empty string.

### `lexerTrimLeft` function

```ts
const lexerTrimLeft: (lexer: Lexer) => void;
```

This function skips all leading whitespace characters by moving the cursor forward until it reaches a non-whitespace character.
