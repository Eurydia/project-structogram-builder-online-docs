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

The purpose of each member is discussed later in parts of this section.

## `Token` type

```ts
export type Token = {
	kind: TokenKind;
	text: string;
};
```

The `Token` type represents a token.

The `kind` property represents which kind of token it is.

The `text` property represents the piece of text that made up the token.
Since the lexer removes whitespace characters, this property will be non-empty.
The only exception is `TokenKind.END` tokens which has an empty `text` property.

## `KEYWORDS` array

```ts
const KEYWORDS: string[] = [
	"for",
	"if",
	"else",
	"while",
	"do",
];
```

The `KEYWORD` array stores reserved keywords.

I added it reduce code duplication in [lexerSafeGetNextTokenThenAdvance](#lexersafegetnexttokenthenadvance-function) function.
In the future, if I want to introduce additional keywords, I can add them to this array.

## `LITERAL_TOKENS` record

```ts
const LITERAL_TOKENS: Record<string, TokenKind> =
	{
		"{": TokenKind.LEFT_CURLY,
		"}": TokenKind.RIGHT_CURLY,
		"(": TokenKind.LEFT_PAREN,
		")": TokenKind.RIGHT_PAREN,
		";": TokenKind.SEMICOLON,
	};
```

The `LITERAL_TOKENS` record maps each literal token to their appropriate [kind](#tokenkind-enum).

Similar to the [KEYWORDS](#keywords-array) array, I added it to reduce code duplication in [lexerSafeGetNextTokenThenAdvance](#lexersafegetnexttokenthenadvance-function) function.

## `Lexer` type

```ts
export type Lexer = {
	content: string;
	contentLength: number;
	cursorPos: number;
};
```

The `Lexer` type represents a lexer.

Lexers are initialized with [lexerInit](#lexerinit-function) function.
After a lexer is initialized, use [lexerGetAllTokens](#lexergetalltokens-function) to obtain a list of [token](#token-type).

The `content` property stores content of a particular lexer.
Though the property is not explicitly immutable, a lexer does not change manipulate it directly.

The `contentLength` property stores the length of `content` during initialization of a lexer.
I added this property so I do not have to keep using [length](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/length) property.

The `cursorPos` property stores the current position of the cursor.

## `lexerInit` function

```ts
export const lexerInit = (
	content: string,
): Lexer => {
	return {
		content: content.normalize(),
		contentLength: content.normalize().length,
		cursorPos: 0,
	};
};
```

The `lexerInit` function initializes a [lexer](#lexer-type) object from user input.

Calling [normalize](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/normalize) on user input is quite important due to the way accented characters behave.

## `lexerGetAllTokens` function

```ts
export const lexerGetAllTokens = (
	l: Lexer,
): Token[] => {
	const tokens: Token[] = [];
	let token: Token;
	while (
		(token = lexerSafeGetNextTokenThenAdvance(l))
			.kind !== TokenKind.END
	) {
		tokens.push(token);
	}
	return tokens;
};
```

The `lexerGetAllTokens` function takes a [lexer](#lexer-type) and return a list of [tokens](#token-type) left in it.

I added this function to simplify the interface.
The real work is done by [lexerSafeGetNextTokenThenAdvance](#lexersafegetnexttokenthenadvance-function) function.

The `tokens` array collects the tokens.
The function returns this array back to the caller.

The "magic" part about this function lies in following snippet, so let me clarify what happens.

```ts
let token: Token;
while (
	(token = lexerSafeGetNextTokenThenAdvance(l))
		.kind !== TokenKind.END
) {}
```

Outside of the while loop, it declares a variable of type [token](#token-type).

```ts
let token: Token;
```

Then, in a condition, it invokes [lexerSafeGetNextTokenThenAdvance](#lexersafegetnexttokenthenadvance-function) which returns a token.
It assign the returned token to the declared variable.

```ts
token = lexerSafeGetNextTokenThenAdvance(l);
```

In JavaScript, the [assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Assignment) operation has a return value which is the right-hand side of the equal sign.

It can access the `kind` property of the returned token.

```ts
(token = lexerSafeGetNextTokenThenAdvance(l))
	.kind;
```

The loop terminates once the returned token is a `TokenKind.END` token.

```ts
(token = lexerSafeGetNextTokenThenAdvance(l))
	.kind !== TokenKind.END;
```

## `lexerSafeGetNextTokenThenAdvance` function

```ts
export const lexerSafeGetNextTokenThenAdvance = (
	l: Lexer,
): Token => {
	lexerTrimLeft(l);

	const token = {
		kind: TokenKind.END,
		text: "",
	};

	if (l.cursorPos >= l.contentLength) {
		return token;
	}

	token["text"] = l.content[l.cursorPos];

	if (token["text"] in LITERAL_TOKENS) {
		token["kind"] = LITERAL_TOKENS[token["text"]];
		return token;
	}

	while (
		l.cursorPos < l.contentLength &&
		!(l.content[l.cursorPos] in LITERAL_TOKENS) &&
		!/\s/.test(l.content[l.cursorPos])
	) {
		token["text"] += l.content[l.cursorPos];
		l.cursorPos++;
	}

	if (KEYWORDS.includes(token["text"])) {
		token["kind"] = TokenKind.KEYWORD;
		return token;
	}

	token["kind"] = TokenKind.SYMBOL;
	return token;
};
```

The `lexerSafeGetNextTokenThenAdvance` function returns a [token](#token-type).

This function does a majority of the work, but the idea is that it tokenize the user input and return a token.
If it has completely tokenize a lexer, it returns a `TokenKind.END` token.

First, it calls [lexerTrimLeft](#lexertrimleft-function) to skip all leading whitespace characters.
This will move the cursor to a non-whitespace character or the end of user input.

```ts
lexerTrimLeft(l);
```

Then, it prepares a placeholder token with `TokenKind.END` and empty string.

```ts
const token = {
	kind: TokenKind.END,
	text: "",
};
```

If the cursor would be out of bound, it returns the placeholder token.

```ts
if (l.cursorPos >= l.contentLength) {
	return token;
}
```

Otherwise, there is at least one character left to be tokenize.
It consumes the current character and advances the cursor.

```ts
token["text"] = l.content[l.cursorPos];
l.cursorPos++;
```

It checks whether the character is one of the [LITERAL_TOKENS](#literal_tokens-record) or not.
If the token should be interpreted as a literal token, it sets the `kind` property to the appropriate value, and returns the token.

```ts
if (token["text"] in LITERAL_TOKENS) {
	token["kind"] = LITERAL_TOKENS[token["text"]];
	return token;
}
```

If it is not a literal token, it collects the rest of the characters until it reaches a whitespace character or a literal token.

```ts
while (
	l.cursorPos < l.contentLength &&
	!(l.content[l.cursorPos] in LITERAL_TOKENS) &&
	!/\s/.test(l.content[l.cursorPos])
) {
	token["text"] += l.content[l.cursorPos];
	l.cursorPos++;
}
```

The first condition prevents over-indexing.

```ts
l.cursorPos < l.contentLength;
```

The second condition terminates the loop if it encounters a literal token.

```ts
!(l.content[l.cursorPos] in LITERAL_TOKENS);
```

The third condition terminates the loop if it encounters a whitespace character.

```ts
!/\s/.test(l.content[l.cursorPos]);
```

After the loop has terminated, it checks whether the collected characters form a keyword or not.
If they form a keyword, it sets the `kind` property on the token to `TokenKind.KEYWORD` and returns the token.

```ts
if (KEYWORDS.includes(token["text"])) {
	token["kind"] = TokenKind.KEYWORD;
	return token;
}
```

If they do not form a keyword, it sets the `kind` property on the token to `TokenKind.SYMBOL` and returns the token.

```ts
token["kind"] = TokenKind.SYMBOL;
return token;
```

## `lexerTrimLeft` function

```ts
const lexerTrimLeft = (l: Lexer): void => {
	while (
		l.cursorPos < l.contentLength &&
		/\s/.test(l.content[l.cursorPos])
	) {
		l.cursorPos++;
	}
};
```

The `lexerTrimLeft` function is a helper to [lexerSafeGetNextTokenThenAdvance](#lexersafegetnexttokenthenadvance-function) function.

It consumes whitespace characters by moving the cursor forward until it reaches the first a non-whitespace character.
