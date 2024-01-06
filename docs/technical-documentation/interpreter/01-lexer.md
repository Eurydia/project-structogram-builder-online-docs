# Lexer

The primary purpose of this module is to convert a string into a sequence of tokens.

Here is an interface of the module:

```ts
export enum TokenKind {}
export type Token;

const KEYWORDS: string[];
const LITERAL_TOKENS: Record<string, TokenKind>;

export type Lexer;

export const lexerInit: (content: string) => Lexer;
export const lexerGetAllTokens: (lexer: Lexer) => Token[];
const lexerGetNextTokenThenAdvance: (lexer: Lexer) => Token;
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

	WHITE_SPACE,
}
```

The `TokenKind` enumeration categorize the different types of tokens that a lexer recognizes.
Each token is assigned a `TokenKind` to denote its type.

- `END`: represents the end of the input. When a lexer encounters this token, it knows there are no more tokens to process.
- `SYMBOL`: represents any piece of text.
- `KEYWORD`: represents keywords, like `if`, `for`, `while`, etc.
- `LEFT_PAREN` and `RIGHT_PAREN`: represent left and right parentheses (`(...)`), respectively.
- `LEFT_CURLY` and `RIGHT_CURLY`: represent left and right curly braces (`{...}`), respectively.
- `SEMICOLON`: represents the semicolon (`;`) used at the end of statements.
- `WHITE_SPACE`: represents any whitespace characters, like spaces, tabs, or newlines.

## `Token` type

```ts
export type Token = {
	kind: TokenKind;
	text: string;
};
```

The `Token` type represents a token in a string.
A token is a meaningful sequence of characters, such as a keyword or a delimiter.

A token is an object with two properties:

- `kind`: represents a `TokenKind`, which is an enumeration of the different types of tokens that can be recognized.
- `text`: represents the actual text of the token.

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

The `KEYWORDS` array defines a list of keywords for the lexer.

During tokenization, a lexer checks if each word in the string is in the `KEYWORDS` array.
If it is, the lexer creates a `Token` with a `kind` of `TokenKind.KEYWORD`.

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

The `LITERAL_TOKENS` object defines a mapping of literal characters to their corresponding token kinds.

During tokenization, a lexer checks if each character in the string is a key in the `LITERAL_TOKENS` object.
If it is, the lexer creates a `Token` with a `kind` that corresponds to the value of that key in the `LITERAL_TOKENS` object.

## `Lexer` type

```ts
export type Lexer = {
	content: string;
	contentLength: number;
	cursorPos: number;
};
```

The `Lexer` type defines the structure of a lexer object.

A lexer is an object with three properties:

- `content` represents a string which is being tokenize.
- `contentLength` that represents the length of the `content` string. This is useful for when a lexer needs to check if it has reached the end of the `content` string.
- `cursorPos` represents the current position of the cursor in the `content` string. This is used to keep track of where a lexer is in the `content` string during tokenization.

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

The `lexerInit` function initializes a new `Lexer` object with a given string.
It is used to prepare a `Lexer` object for the tokenization process.

The function takes a string argument `content`.
It returns a `Lexer` object with the `content` property set to the normalized version of the `content` string, the `contentLength` property set to the length of the normalized `content` string, and the `cursorPos` property set to 0.

Calling [normalize](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/normalize) on user input is quite important due to the way [accented characters](https://stackoverflow.com/questions/63013552/whats-the-point-of-string-normalize) behave.

## `lexerGetNextTokenThenAdvance` function

```ts
export const lexerGetNextTokenThenAdvance = (
	l: Lexer,
): Token => {
	const token = {
		kind: TokenKind.END,
		text: "",
	};

	if (l.cursorPos >= l.contentLength) {
		return token;
	}

	if (/\s/.test(l.content[l.cursorPos])) {
		token["kind"] = TokenKind.WHITE_SPACE;
		token["text"] = l.content[l.cursorPos];
		l.cursorPos++;
		return token;
	}

	token["text"] = l.content[l.cursorPos];
	l.cursorPos++;

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

The `lexerGetNextTokenThenAdvance` function tokenize the next token from a `Lexer` object and advance the cursor position.
It is a key part of the tokenization process.

The function takes a `Lexer` object as an argument and returns a `Token` object.

The breakdown of the function is as follows:

First, it starts by creating a `Token` object with a `kind` of `TokenKind.END` and an empty `text` string.
If the cursor position in the `Lexer` object is at or beyond the end of the content string, it returns this `Token` object as is.

```ts
// ...
const token = {
	kind: TokenKind.END,
	text: "",
};

if (l.cursorPos >= l.contentLength) {
	return token;
}
// ...
```

If the character at the cursor position is a whitespace character, it sets the `kind` of the `Token` object to `TokenKind.WHITE_SPACE`, sets the `text` of the `Token` object to the whitespace character, increments the cursor position, and returns the `Token` object.

```ts
// ...
if (/\s/.test(l.content[l.cursorPos])) {
	token["kind"] = TokenKind.WHITE_SPACE;
	token["text"] = l.content[l.cursorPos];
	l.cursorPos++;
	return token;
}
// ...
```

Otherwise, it sets the `text` of the `Token` object to the character at the cursor position and increments the cursor position.
If the character is a key in the `LITERAL_TOKENS` object, it sets the `kind` of the `Token` object to the corresponding value in the `LITERAL_TOKENS` object and returns the `Token` object.

```ts
// ...
token["text"] = l.content[l.cursorPos];
l.cursorPos++;

if (token["text"] in LITERAL_TOKENS) {
	token["kind"] = LITERAL_TOKENS[token["text"]];
	return token;
}
// ...
```

If the character is not a key in the `LITERAL_TOKENS` object, it continues to add the following characters to the `text` of the `Token` object and increment the cursor position until it reaches a character that is a key in the `LITERAL_TOKENS` object or a whitespace character, or until it reaches the end of the content string.

```ts
// ...
while (
	l.cursorPos < l.contentLength &&
	!(l.content[l.cursorPos] in LITERAL_TOKENS) &&
	!/\s/.test(l.content[l.cursorPos])
) {
	token["text"] += l.content[l.cursorPos];
	l.cursorPos++;
}
// ...
```

If the `text` of the `Token` object is a keyword, it sets the `kind` of the `Token` object to `TokenKind.KEYWORD` and returns the `Token` object.
Otherwise, it sets the `kind` of the `Token` object to `TokenKind.SYMBOL` and returns the `Token` object.

```ts
// ...
if (KEYWORDS.includes(token["text"])) {
	token["kind"] = TokenKind.KEYWORD;
	return token;
}

token["kind"] = TokenKind.SYMBOL;
return token;
// ...
```

## `lexerGetAllTokens` function

```ts
export const lexerGetAllTokens = (
	l: Lexer,
): Token[] => {
	const tokens: Token[] = [];
	let token: Token;
	while (
		(token = lexerGetNextTokenThenAdvance(l))
			.kind !== TokenKind.END
	) {
		tokens.push(token);
	}
	return tokens;
};
```

The `lexerGetAllTokens` function generates a list of all tokens from a `Lexer` object.
It is used to tokenize an entire string at once.

The function takes a `Lexer` object as an argument and returns an array of `Token` objects.

The breakdown of the function is as follows:

First, it starts by creating an empty array `tokens` to store the `Token` objects.

```ts
// ...
const tokens: Token[] = [];
// ...
```

Then, it enters a while loop where it calls the `lexerGetNextTokenThenAdvance` function with the `Lexer` object as the argument to get the next `Token` object and advance the cursor position.
If the `kind` of the `Token` object is `TokenKind.END`, it breaks out of the while loop.
Otherwise, it pushes the `Token` object to the `tokens` array and continues the loop.

After the while loop, it returns the `tokens` array, which contains all the `Token` objects that represent the tokens in the `Lexer` object's content string.

```ts
// ...
let token: Token;
while (
	(token = lexerGetNextTokenThenAdvance(l))
		.kind !== TokenKind.END
) {
	tokens.push(token);
}
return tokens;
// ...
```
