# Parser

The primary purpose of this module is to convert a list of tokens into an abstract syntax tree.

Here is an interface of the module:

```ts
export enum NodeKind {}

export type NodeEnd;
export type NodeProcess;
export type NodeLoopFirst;
export type NodeLoopLast;
export type NodeIfElse;
export type Node;

export type Parser;

export const parserInit: (tokens: Token[]) => Parser;
const parserCollectTokens: (
	p: Parser,
	startToken: TokenKind,
	stopToken: TokenKind
) => Token[];
const parserSkipWhiteSpace: (p: Parser) => void;

const parserBuildLoopFirstNode: (p: Parser) => NodeLoopFirst;
const parserBuildLoopLastNode: (p: Parser) => NodeLoopLast;
const parserBuildIfElseNode: (p: Parser) => NodeIfElse;

const parserGetNextNodeThenAdvance = (p: Parser) => Node;
export const parserGetAllNodes: (p: Parser) => Node[];
```

## `NodeKind` enum

```ts
export enum NodeKind {
	END,
	PROCESS,
	LOOP_FIRST,
	LOOP_LAST,
	IF_ELSE,
}
```

The `NodeKind` enumeration represents different kinds of nodes.

It has five members: `END`, `PROCESS`, `LOOP_FIRST`, `LOOP_LAST`, and `IF_ELSE`.
Each member represents a different kind of node that can appear in the AST.

## `NodeEnd` type

```ts
type NodeEnd = {
	kind: NodeKind.END;
};
```

The `NodeEnd` type represents an end node.

It is an object with a single property `kind`, which is always `NodeKind.END`.

## `NodeProcess` type

```ts
type NodeProcess = {
	kind: NodeKind.PROCESS;
	body: Token[];
};
```

The `NodeProcess` type represents a process node.

It is an object with two properties:

- `kind` is always `NodeKind.PROCESS`.
- `body` is an array of `Token` objects, which represent the tokens that make up the body of the process.

## `NodeLoopFirst` type

```ts
type NodeLoopFirst = {
	kind: NodeKind.LOOP_FIRST;
	condition: Token[];
	body: Node[];
};
```

The `NodeLoopFirst` type represents a loop-first node, such as a `for` or `while` loop.

It is an object with three properties:

- `kind` is always `NodeKind.LOOP_FIRST`.
- `condition` is an array of `Token` objects, which represent the tokens that make up the condition of the loop.
- `body` is an array of `Node` objects, which represent the nodes that make up the body of the loop.

For example, when I encounter a node of type `NodeLoopFirst` during the interpretation process, I can evaluate the `condition` array to determine whether to execute the `body` array, simulating the execution of the loop in the original code.

## `NodeLoopLast` type

```ts
type NodeLoopLast = {
	kind: NodeKind.LOOP_LAST;
	condition: Token[];
	body: Node[];
};
```

The `NodeLoopLast` type represents a loop-last node, such as a `do-while` loop.

It is an object with three properties:

- `kind` is always `NodeKind.LOOP_LAST`.
- `condition` is an array of `Token` objects, which represent the tokens that make up the condition of the loop.
- `body` is an array of `Node` objects, which represent the nodes that make up the body of the loop.

## `NodeIfElse` type

```ts
type NodeIfElse = {
	kind: NodeKind.IF_ELSE;
	condition: Token[];
	bodyIf: Node[];
	bodyElse: Node[];
};
```

The `NodeIfElse` type represents an if-else node.

It is an object with four properties:

- `kind` is always `NodeKind.IF_ELSE`.
- `condition` is an array of `Token` objects, which represent the tokens that make up the condition of the `if` statement.
- `bodyIf` and `bodyElse` properties are arrays of `Node` objects, which represent the nodes that make up the `if` and `else` parts of the if-else statement, respectively.

## `Node` type

```ts
export type Node =
	| NodeEnd
	| NodeProcess
	| NodeLoopFirst
	| NodeLoopLast
	| NodeIfElse;
```

The `Node` type represents a node.

It is a union type that can be one of five types: `NodeEnd`, `NodeProcess`, `NodeLoopFirst`, `NodeLoopLast`, or `NodeIfElse`.
Each of these types represents a different kind of node that can appear.

## `Parser` type

```ts
export type Parser = {
	tokens: Token[];
	tokenLength: number;
	cursorPos: number;
};
```

The `Parser` type represents a parser.

A parser is an object with three properties:

- `tokens` is an array of `Token` objects, which represent the tokens that have been parsed.
- `tokenLength` represents the total number of tokens.
- `cursorPos` represents the current position of the parser in the array of tokens.

## `parserInit` function

```ts
export const parserInit = (
	tokens: Token[],
): Parser => {
	return {
		tokens: tokens,
		tokenLength: tokens.length,
		cursorPos: 0,
	};
};
```

The `parserInit` function initializes a new `Parser` object with a given array of `Token` objects.

The function takes an array of `Token` objects as its argument.
It returns a new `Parser` object with the `tokens` property set to the given array, the `tokenLength` property set to the length of the array, and the `cursorPos` property set to 0.

## `parserCollectTokens` function

```ts
const parserCollectTokens = (
	p: Parser,
	startToken: TokenKind,
	stopToken: TokenKind,
): Token[] => {
	if (p.cursorPos >= p.tokenLength) {
		return [];
	}
	if (p.tokens[p.cursorPos].kind !== startToken) {
		return [];
	}
	p.cursorPos++;
	const tokens: Token[] = [];
	let depth = -1;
	let token: Token;
	while (p.cursorPos < p.tokenLength) {
		token = p.tokens[p.cursorPos];
		p.cursorPos++;
		if (token.kind === startToken) {
			depth--;
		}
		if (token.kind === stopToken) {
			depth++;
		}
		if (depth === 0) {
			break;
		}
		tokens.push(token);
	}
	return tokens;
};
```

The `parserCollectTokens` function collects a sequence of tokens from a `Parser` object between a specified start token and stop token.
It is particularly useful for parsing constructs that are enclosed by specific tokens and keeps the code DRY.

The function takes three arguments: a `Parser` object, a start token, and a stop token.
It returns an array of `Token` objects that were found between the start token and the stop token.

The breakdown of the function is as follows:

First, it checks if the parser's cursor position is beyond the length of the tokens array or if the current token is not the start token.
If either of these conditions is true, it returns an empty array.

```ts
// ...
if (p.cursorPos >= p.tokenLength) {
	return [];
}
if (p.tokens[p.cursorPos].kind !== startToken) {
	return [];
}
//...
```

Next, it increments the cursor position and initializes an empty array `tokens` to collect the tokens and a variable `depth` to keep track of nested tokens of the same kind as the start and stop tokens.

```ts
// ...
p.cursorPos++;
const tokens: Token[] = [];
let depth = -1;
let token: Token;
// ...
```

Then, it enters a loop where it continues to collect tokens until it encounters the stop token at the same nesting level as the start token or until it has processed all the tokens.

```ts
// ...
while (p.cursorPos < p.tokenLength) {
	token = p.tokens[p.cursorPos];
	p.cursorPos++;
	if (token.kind === startToken) {
		depth--;
	}
	if (token.kind === stopToken) {
		depth++;
	}
	if (depth === 0) {
		break;
	}
	tokens.push(token);
}
return tokens;
// ...
```

## `parserSkipWhiteSpace` function

```ts
const parserSkipWhiteSpace = (
	p: Parser,
): void => {
	while (
		p.cursorPos < p.tokenLength &&
		p.tokens[p.cursorPos].kind ===
			TokenKind.WHITE_SPACE
	) {
		p.cursorPos++;
	}
};
```

The `parserSkipWhiteSpace` function advances the cursor position of a `Parser` object past any white space tokens.

The function takes a `Parser` object as its argument.
It does not return anything, but it modifies the `cursorPos` property of the `Parser` object.

The function enters a loop where it checks if the cursor position is less than the length of the tokens array and if the current token is a white space token. If both conditions are true, it increments the cursor position.
The loop continues until it encounters a non-white space token or has processed all the tokens.

## `parserBuildLoopFirstNode` function

```ts
const parserBuildLoopFirstNode = (
	p: Parser,
): NodeLoopFirst => {
	const node: NodeLoopFirst = {
		kind: NodeKind.LOOP_FIRST,
		body: [],
		condition: [],
	};
	parserSkipWhiteSpace(p);
	if (p.cursorPos >= p.tokenLength) {
		return node;
	}
	if (
		p.tokens[p.cursorPos].kind !==
		TokenKind.LEFT_PAREN
	) {
		return node;
	}
	node.condition = parserCollectTokens(
		p,
		TokenKind.LEFT_PAREN,
		TokenKind.RIGHT_PAREN,
	);
	parserSkipWhiteSpace(p);
	if (p.cursorPos >= p.tokenLength) {
		return node;
	}
	if (
		p.tokens[p.cursorPos].kind !==
		TokenKind.LEFT_CURLY
	) {
		return node;
	}
	node.body = parserGetAllNodes(
		parserInit(
			parserCollectTokens(
				p,
				TokenKind.LEFT_CURLY,
				TokenKind.RIGHT_CURLY,
			),
		),
	);
	return node;
};
```

The `parserBuildLoopFirstNode` function builds a `NodeLoopFirst` object from a `Parser` object.

The function takes a `Parser` object as its argument.
It returns a `NodeLoopFirst` object.

Here is the breakdown of the function:

First, it creates a new `NodeLoopFirst` object `node` with the `kind` property set to `NodeKind.LOOP_FIRST` and the `condition` and `body` properties set to empty arrays.

```ts
// ...
const node: NodeLoopFirst = {
	kind: NodeKind.LOOP_FIRST,
	body: [],
	condition: [],
};
// ...
```

Then, it uses the `parserSkipWhiteSpace` function to skip any white space tokens in the `Parser` object.
If the cursor position is beyond the length of the tokens array or if the current token is not a left parenthesis token, it returns the `node` object as is.

```ts
// ...
parserSkipWhiteSpace(p);
if (p.cursorPos >= p.tokenLength) {
	return node;
}
if (
	p.tokens[p.cursorPos].kind !==
	TokenKind.LEFT_PAREN
) {
	return node;
}
// ...
```

Otherwise, it uses the `parserCollectTokens` function to collect the tokens between the left parenthesis token and the corresponding right parenthesis token, and assigns the result to the `condition` property of the `node` object.

```ts
// ...
node.condition = parserCollectTokens(
	p,
	TokenKind.LEFT_PAREN,
	TokenKind.RIGHT_PAREN,
);
// ...
```

Next, it again uses the `parserSkipWhiteSpace` function to skip any white space tokens.
If the cursor position is beyond the length of the tokens array or if the current token is not a left curly brace token, it returns the `node` object as is.

```ts
// ...
parserSkipWhiteSpace(p);
if (p.cursorPos >= p.tokenLength) {
	return node;
}
if (
	p.tokens[p.cursorPos].kind !==
	TokenKind.LEFT_CURLY
) {
	return node;
}
// ...
```

Otherwise, it uses the `parserCollectTokens` function to collect the tokens between the left curly brace token and the corresponding right curly brace token, initializes a new `Parser` object with these tokens using the `parserInit` function, obtains all nodes from this new `Parser` object using the `parserGetAllNodes` function, assigns the result to the `body` property of the `node` object, and returns the `node` object.

```ts
// ...
node.body = parserGetAllNodes(
	parserInit(
		parserCollectTokens(
			p,
			TokenKind.LEFT_CURLY,
			TokenKind.RIGHT_CURLY,
		),
	),
);
return node;
// ...
```

## `parserBuildLoopLastNode` function

```ts
const parserBuildLoopLastNode = (
	p: Parser,
): NodeLoopLast => {
	const node: NodeLoopLast = {
		kind: NodeKind.LOOP_LAST,
		body: [],
		condition: [],
	};
	parserSkipWhiteSpace(p);
	if (p.cursorPos >= p.tokenLength) {
		return node;
	}
	if (
		p.tokens[p.cursorPos].kind !==
		TokenKind.LEFT_CURLY
	) {
		return node;
	}
	node.body = parserGetAllNodes(
		parserInit(
			parserCollectTokens(
				p,
				TokenKind.LEFT_CURLY,
				TokenKind.RIGHT_CURLY,
			),
		),
	);
	parserSkipWhiteSpace(p);
	if (p.cursorPos >= p.tokenLength) {
		return node;
	}
	if (
		p.tokens[p.cursorPos].kind !==
			TokenKind.KEYWORD ||
		p.tokens[p.cursorPos].text !== "while"
	) {
		return node;
	}
	p.cursorPos++;
	parserSkipWhiteSpace(p);
	if (p.cursorPos >= p.tokenLength) {
		return node;
	}
	if (
		p.tokens[p.cursorPos].kind !==
		TokenKind.LEFT_PAREN
	) {
		return node;
	}
	node.condition = parserCollectTokens(
		p,
		TokenKind.LEFT_PAREN,
		TokenKind.RIGHT_PAREN,
	);
	parserSkipWhiteSpace(p);
	if (p.cursorPos >= p.tokenLength) {
		return node;
	}
	if (
		p.tokens[p.cursorPos].kind ===
		TokenKind.SEMICOLON
	) {
		p.cursorPos++;
	}
	return node;
};
```

The `parserBuildLoopLastNode` function builds a `NodeLoopLast` object from a `Parser` object.

The function takes a `Parser` object as its argument.
It returns a `NodeLoopLast` object.

Here is the breakdown of the function:

First, it creates a new `NodeLoopLast` object `node` with the `kind` property set to `NodeKind.LOOP_LAST` and the `condition` and `body` properties set to empty arrays.

```ts
// ...
const node: NodeLoopLast = {
	kind: NodeKind.LOOP_LAST,
	body: [],
	condition: [],
};
// ...
```

Then, it uses the `parserSkipWhiteSpace` function to skip any white space tokens in the `Parser` object.
If the cursor position is beyond the length of the tokens array or if the current token is not a left curly brace token, it returns the `node` object as is.

```ts
// ...
parserSkipWhiteSpace(p);
if (p.cursorPos >= p.tokenLength) {
	return node;
}
if (
	p.tokens[p.cursorPos].kind !==
	TokenKind.LEFT_CURLY
) {
	return node;
}
// ...
```

Otherwise, it uses the `parserCollectTokens` function to collect the tokens between the left curly brace token and the corresponding right curly brace token, initializes a new `Parser` object with these tokens using the `parserInit` function, obtains all nodes from this new `Parser` object using the `parserGetAllNodes` function, and assigns the result to the `body` property of the `node` object.

```ts
// ...
node.body = parserGetAllNodes(
	parserInit(
		parserCollectTokens(
			p,
			TokenKind.LEFT_CURLY,
			TokenKind.RIGHT_CURLY,
		),
	),
);
// ...
```

Next, it again uses the `parserSkipWhiteSpace` function to skip any white space tokens. If the cursor position is beyond the length of the tokens array or if the current token is not a ` while` keyword token, it returns the `node` object as is.

```ts
// ...
parserSkipWhiteSpace(p);
if (p.cursorPos >= p.tokenLength) {
	return node;
}
if (
	p.tokens[p.cursorPos].kind !==
		TokenKind.KEYWORD ||
	p.tokens[p.cursorPos].text !== "while"
) {
	return node;
}
// ...
```

Otherwise, it increments the cursor position to consume the `while` keyword, uses the `parserCollectTokens` function to collect the tokens between the left parenthesis token and the corresponding right parenthesis token, and assigns the result to the `condition` property of the `node` object.

```ts
// ...
p.cursorPos++;
parserSkipWhiteSpace(p);
if (p.cursorPos >= p.tokenLength) {
	return node;
}
if (
	p.tokens[p.cursorPos].kind !==
	TokenKind.LEFT_PAREN
) {
	return node;
}
node.condition = parserCollectTokens(
	p,
	TokenKind.LEFT_PAREN,
	TokenKind.RIGHT_PAREN,
);
// ...
```

Finally, it again uses the `parserSkipWhiteSpace` function to skip any white space tokens.
If the cursor position is beyond the length of the tokens array or if the current token is a semicolon token, it increments the cursor position to consume the semicolon.

```ts
// ...
parserSkipWhiteSpace(p);
if (p.cursorPos >= p.tokenLength) {
	return node;
}
if (
	p.tokens[p.cursorPos].kind ===
	TokenKind.SEMICOLON
) {
	p.cursorPos++;
}
return node;
// ...
```

## `parserBuildIfElseNode` function

```ts
const parserBuildIfElseNode = (
	p: Parser,
): NodeIfElse => {
	const node: NodeIfElse = {
		kind: NodeKind.IF_ELSE,
		condition: [],
		bodyIf: [],
		bodyElse: [],
	};
	parserSkipWhiteSpace(p);
	if (p.cursorPos >= p.tokenLength) {
		return node;
	}
	if (
		p.tokens[p.cursorPos].kind !==
		TokenKind.LEFT_PAREN
	) {
		return node;
	}
	node.condition = parserCollectTokens(
		p,
		TokenKind.LEFT_PAREN,
		TokenKind.RIGHT_PAREN,
	);
	parserSkipWhiteSpace(p);
	if (p.cursorPos >= p.tokenLength) {
		return node;
	}
	if (
		p.tokens[p.cursorPos].kind !==
		TokenKind.LEFT_CURLY
	) {
		return node;
	}
	node.bodyIf = parserGetAllNodes(
		parserInit(
			parserCollectTokens(
				p,
				TokenKind.LEFT_CURLY,
				TokenKind.RIGHT_CURLY,
			),
		),
	);
	parserSkipWhiteSpace(p);
	if (p.cursorPos >= p.tokenLength) {
		return node;
	}
	if (
		p.tokens[p.cursorPos].kind !==
			TokenKind.KEYWORD ||
		p.tokens[p.cursorPos].text !== "else"
	) {
		return node;
	}
	p.cursorPos++;
	parserSkipWhiteSpace(p);
	if (p.cursorPos >= p.tokenLength) {
		return node;
	}
	if (
		p.tokens[p.cursorPos].kind !==
		TokenKind.LEFT_CURLY
	) {
		return node;
	}
	node.bodyElse = parserGetAllNodes(
		parserInit(
			parserCollectTokens(
				p,
				TokenKind.LEFT_CURLY,
				TokenKind.RIGHT_CURLY,
			),
		),
	);
	return node;
};
```

The `parserBuildIfElseNode` function builds a `NodeIfElse` object from a `Parser` object.
It takes a `Parser` object as its argument, and returns a `NodeIfElse` object.

Here is the breakdown of the function:

First,it creates a new `NodeIfElse` object `node` with the `kind` property set to `NodeKind.IF_ELSE` and the `condition`, `bodyIf`, and `bodyElse` properties set to empty arrays.

```ts
// ...
const node: NodeIfElse = {
	kind: NodeKind.IF_ELSE,
	condition: [],
	bodyIf: [],
	bodyElse: [],
};
// ...
```

Then, it uses the `parserSkipWhiteSpace` function to skip any white space tokens in the `Parser` object.
If the cursor position is beyond the length of the tokens array or if the current token is not a left parenthesis token, it returns the `node` object as is.

```ts
// ...
parserSkipWhiteSpace(p);
if (p.cursorPos >= p.tokenLength) {
	return node;
}
if (
	p.tokens[p.cursorPos].kind !==
	TokenKind.LEFT_PAREN
) {
	return node;
}
// ...
```

Otherwise, it uses the `parserCollectTokens` function to collect the tokens between the left parenthesis token and the corresponding right parenthesis token, and assigns the result to the `condition` property of the `node` object.

```ts
// ...
node.condition = parserCollectTokens(
	p,
	TokenKind.LEFT_PAREN,
	TokenKind.RIGHT_PAREN,
);
// ...
```

Next, it again uses the `parserSkipWhiteSpace` function to skip any white space tokens.
If the cursor position is beyond the length of the tokens array or if the current token is not a left curly brace token, it returns the `node` object as is.

```ts
// ...
parserSkipWhiteSpace(p);
if (p.cursorPos >= p.tokenLength) {
	return node;
}
if (
	p.tokens[p.cursorPos].kind !==
	TokenKind.LEFT_CURLY
) {
	return node;
}
// ...
```

Otherwise, it uses the `parserCollectTokens` function to collect the tokens between the left curly brace token and the corresponding right curly brace token, initializes a new `Parser` object with these tokens using the `parserInit` function, obtains all nodes from this new `Parser` object using the `parserGetAllNodes` function, and assigns the result to the `bodyIf` property of the `node` object.

```ts
// ...
node.bodyIf = parserGetAllNodes(
	parserInit(
		parserCollectTokens(
			p,
			TokenKind.LEFT_CURLY,
			TokenKind.RIGHT_CURLY,
		),
	),
);
// ...
```

Then, it again uses the `parserSkipWhiteSpace` function to skip any white space tokens.
If the cursor position is beyond the length of the tokens array or if the current token is not an `else` keyword token, it returns the `node` object as is.

```ts
// ...
parserSkipWhiteSpace(p);
if (p.cursorPos >= p.tokenLength) {
	return node;
}
if (
	p.tokens[p.cursorPos].kind !==
		TokenKind.KEYWORD ||
	p.tokens[p.cursorPos].text !== "else"
) {
	return node;
}
// ...
```

Otherwise, it increments the cursor position to consume the `else` keyword, uses the `parserCollectTokens` function to collect the tokens between the left curly brace token and the corresponding right curly brace token, initializes a new `Parser` object with these tokens using the `parserInit` function, obtains all nodes from this new `Parser` object using the `parserGetAllNodes` function, and assigns the result to the `bodyElse` property of the `node` object.

```ts
// ...
p.cursorPos++;
parserSkipWhiteSpace(p);
if (p.cursorPos >= p.tokenLength) {
	return node;
}
if (
	p.tokens[p.cursorPos].kind !==
	TokenKind.LEFT_CURLY
) {
	return node;
}
node.bodyElse = parserGetAllNodes(
	parserInit(
		parserCollectTokens(
			p,
			TokenKind.LEFT_CURLY,
			TokenKind.RIGHT_CURLY,
		),
	),
);
// ...
```

Finally, it returns the `node` object.

```ts
// ...
return node;
// ...
```

By using the `parserBuildIfElseNode` function, I can build a `NodeIfElse` object from a `Parser` object, which represents an if-else node in an AST. This is particularly useful for parsing if-else constructs in the code.

## `parserGetNextNodeThenAdvance` function

```ts
const parserGetNextNodeThenAdvance = (
	p: Parser,
): Node => {
	parserSkipWhiteSpace(p);
	if (p.cursorPos >= p.tokenLength) {
		return {
			kind: NodeKind.END,
		};
	}
	let token = p.tokens[p.cursorPos];
	p.cursorPos++;
	if (token.kind === TokenKind.KEYWORD) {
		switch (token.text) {
			case "for":
			case "while":
				return parserBuildLoopFirstNode(p);
			case "do":
				return parserBuildLoopLastNode(p);
			case "if":
				return parserBuildIfElseNode(p);
			default:
				break;
		}
	}
	const node: NodeProcess = {
		kind: NodeKind.PROCESS,
		body: [],
	};
	if (token.kind === TokenKind.SEMICOLON) {
		return node;
	}
	node.body.push(token);
	while (p.cursorPos < p.tokenLength) {
		token = p.tokens[p.cursorPos];
		p.cursorPos++;
		if (
			token.kind === TokenKind.END ||
			token.kind === TokenKind.SEMICOLON
		) {
			break;
		}
		node.body.push(token);
	}
	return node;
};
```

The `parserGetNextNodeThenAdvance` function parses the next node from a `Parser` object and advances the cursor position.
It function takes a `Parser` object as its argument, and returns a `Node` object.

Here is the breakdown of the function:

First, it uses the `parserSkipWhiteSpace` function to skip any white space tokens in the `Parser` object.
If the cursor position is beyond the length of the tokens array, it returns a `NodeEnd` object.

```ts
// ...
parserSkipWhiteSpace(p);
if (p.cursorPos >= p.tokenLength) {
	return {
		kind: NodeKind.END,
	};
}
// ...
```

Then, it obtains the current token and increments the cursor position.
If the current token is a keyword token, it checks the text of the token and calls the corresponding function to build a loop or if-else node, and returns the result.

```ts
// ...
let token = p.tokens[p.cursorPos];
p.cursorPos++;
if (token.kind === TokenKind.KEYWORD) {
	switch (token.text) {
		case "for":
		case "while":
			return parserBuildLoopFirstNode(p);
		case "do":
			return parserBuildLoopLastNode(p);
		case "if":
			return parserBuildIfElseNode(p);
		default:
			break;
	}
}
// ...
```

Otherwise, it creates a new `NodeProcess` object `node` with the `kind` property set to `NodeKind.PROCESS` and the `body` property set to an empty array.
If the current token is a semicolon token, it returns the `node` object as is.

```ts
// ...
const node: NodeProcess = {
	kind: NodeKind.PROCESS,
	body: [],
};
if (token.kind === TokenKind.SEMICOLON) {
	return node;
}
// ...
```

Otherwise, it adds the current token to the `body` property of the `node` object.

```ts
// ...
node.body.push(token);
// ...
```

Then, it enters a loop where it obtains the current token, increments the cursor position, and checks if the current token is an end or semicolon token.
If it is, it breaks the loop. Otherwise, it adds the current token to the `body` property of the `node` object.

```ts
// ...
while (p.cursorPos < p.tokenLength) {
	token = p.tokens[p.cursorPos];
	p.cursorPos++;
	if (
		token.kind === TokenKind.END ||
		token.kind === TokenKind.SEMICOLON
	) {
		break;
	}
	node.body.push(token);
}
// ...
```

Finally, it returns the `node` object.

```ts
// ...
return node;
// ...
```

## `parserGetAllNodes` function

```ts
export const parserGetAllNodes = (
	p: Parser,
): Node[] => {
	const nodes: Node[] = [];
	let node: Node;
	while (
		(node = parserGetNextNodeThenAdvance(p))
			.kind !== NodeKind.END
	) {
		nodes.push(node);
	}
	return nodes;
};
```

The `parserGetAllNodes` parses all nodes from a `Parser` object.
It takes a `Parser` object as its argument and returns an array of `Node` objects.

Here is the breakdown of the function:

First, it creates an empty array `nodes` to store the nodes.

```ts
// ...
const nodes: Node[] = [];
// ...
```

Then, it enters a loop where it uses the `parserGetNextNodeThenAdvance` function to get the next node from the `Parser` object and advance the cursor position, and checks if the `kind` property of the node is `NodeKind.END`.
If it is, it breaks the loop. Otherwise, it adds the node to the `nodes` array.

```ts
// ...
let node: Node;
while (
	(node = parserGetNextNodeThenAdvance(p))
		.kind !== NodeKind.END
) {
	nodes.push(node);
}
// ...
```

Finally, it returns the `nodes` array.

```ts
// ...
return nodes;
// ...
```

## Context-free grammar

Note that:

- a star `*` means zero or more repetitions of the preceding element.
- a plus `+` means one or more repetitions of the preceding element.
- a verticle bar `|` means only one of the elements can be present.
- element enclosed by square brackets `[]` is optional.
- characters enclosed by single quotes `'` is a literal.

```bnf
<diagram> ::= <statement>*

<statement> ::= <token>+ ';'
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
