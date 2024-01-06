# Structogram node

This compnent is a collection of smaller components that are used to render a `Node` object as a `StructogramNodeLoopFirst`, `StructogramNodeLoopLast`, `StructogramNodeIfElse`, or `StructogramNodeProcess` component based on its `kind` property.

Here is an interface of the component:

```tsx
type StructogramNodeWrapperProps;
const StructogramNodeWrapper: FC<
	StructogramNodeWrapperProps
>;

type StructogramComponentTextProps;
const StructogramComponentText: FC<
	StructogramComponentTextProps
>;

type StructogramNodeProcessProps;
const StructogramNodeProcess: FC<
	StructogramNodeProcessProps
>;

type StructogramNodeLoopFirstProps;
const StructogramNodeLoopFirst: FC<
	StructogramNodeLoopFirstProps
>;

type StructogramNodeLoopLastProps;
const StructogramNodeLoopLast: FC<
	StructogramNodeLoopLastProps
>;

type StructogramNodeIfElseProps;
const StructogramNodeIfElse: FC<
	StructogramNodeIfElseProps
>;

const fitlerEmptyProcessNodes = (node: Node) => boolean;

type StructogramNodeProps;
export const StructogramNode: FC<
	StructogramNodeProps
>;
```

## `StructogramNodeWrapper` component

```tsx
type StructogramNodeWrapperProps = {
	children: ReactNode | ReactNode[];
	borderTop?: boolean;
	borderBottom?: boolean;
	borderRight?: boolean;
	borderLeft?: boolean;
};
const StructogramNodeWrapper: FC<
	StructogramNodeWrapperProps
> = (props) => {
	const {
		children,
		borderTop,
		borderBottom,
		borderLeft,
		borderRight,
	} = props;
	return (
		<Box
			height="100%"
			sx={{
				borderColor: "inherit",
				backgroundColor: "inherit",
				borderStyle: "solid",
				borderLeftWidth: borderLeft
					? "inherit"
					: 0,
				borderTopWidth: borderTop ? "inherit" : 0,
				borderBottomWidth: borderBottom
					? "inherit"
					: 0,
				borderRightWidth: borderRight
					? "inherit"
					: 0,
			}}
		>
			{children}
		</Box>
	);
};
```

The `StructogramNodeWrapper` component is a wrapper around other node components, providing them with a border and a background color.

This component includes `children` which can be a single React node or an array of React nodes, and optional `borderTop`, `borderBottom`, `borderLeft`, and `borderRight` properties which are boolean values indicating whether the wrapper should have a border on the top, bottom, left, and right respectively.

## `StructogramComponentText` component

```tsx
type StructogramComponentTextProps =
	TypographyProps & {
		children?: string;
	};
const StructogramComponentText: FC<
	StructogramComponentTextProps
> = (props) => {
	const { children, ...rest } = props;

	return (
		<Typography
			fontFamily="inherit"
			fontWeight="inherit"
			padding={1}
			paddingLeft={2}
			{...rest}
		>
			{children ?? "..."}
		</Typography>
	);
};
```

The `StructogramComponentText` component displays text with inherited font family and weight, and with some padding.

Since the text is optional, the component will display `...` if no text is provided.

## `StructogramNodeProcess` component

```tsx
type StructogramNodeProcessProps = {
	text?: string;
	borderTop?: boolean;
	borderBottom?: boolean;
	borderRight?: boolean;
	borderLeft?: boolean;
};
const StructogramNodeProcess: FC<
	StructogramNodeProcessProps
> = (props) => {
	const { text, ...rest } = props;

	return (
		<StructogramNodeWrapper {...rest}>
			<StructogramComponentText>
				{text}
			</StructogramComponentText>
		</StructogramNodeWrapper>
	);
};
```

The `StructogramNodeProcess` component represents a process node in a structogram.

It takes a `StructogramNodeProcessProps` object as its props.
This object includes an optional `text` property which is a string, and optional `borderTop`, `borderBottom`, `borderRight`, and `borderLeft` properties which are boolean values indicating whether the node should have a border on the top, bottom, right, and left respectively.

## `StructogramNodeLoopFirst` component

```tsx
type StructogramNodeLoopFirstProps = {
	condition?: string;
	body: Node[];
	borderTop?: boolean;
	borderBottom?: boolean;
	borderRight?: boolean;
	borderLeft?: boolean;
};
export const StructogramNodeLoopFirst: FC<
	StructogramNodeLoopFirstProps
> = (props) => {
	const { condition, body, ...rest } = props;

	let bodyNode: ReactNode | ReactNode[] = (
		<StructogramNodeProcess
			borderTop
			borderLeft
		/>
	);

	if (body.length > 0) {
		bodyNode = body.map((subnode, index) => (
			<StructogramNode
				key={`subnode-${index}`}
				borderTop
				borderLeft
				node={subnode}
			/>
		));
	}

	return (
		<StructogramNodeWrapper {...rest}>
			<StructogramComponentText>
				{condition}
			</StructogramComponentText>
			<Box paddingLeft={2}>{bodyNode}</Box>
		</StructogramNodeWrapper>
	);
};
```

The `StructogramNodeLoopFirst` component represent a test-first loop node in a structogram.

It takes a `StructogramNodeLoopFirstProps` object as its props.
This object includes an optional `condition` property which is a string, a `body` property which is an array of `Node` objects, and optional `borderTop`, `borderBottom`, `borderRight`, and `borderLeft` properties which are boolean values indicating whether the node should have a border on the top, bottom, right, and left respectively.

The indented effect of the loop is achieved by wrapping the `body` in a `Box` component with a `paddingLeft` of 2.

## `StructogramNodeLoopLast` component

```tsx
type StructogramNodeLoopLastProps = {
	condition?: string;
	body: Node[];
	borderTop?: boolean;
	borderBottom?: boolean;
	borderRight?: boolean;
	borderLeft?: boolean;
};
export const StructogramNodeLoopLast: FC<
	StructogramNodeLoopLastProps
> = (props) => {
	const { condition, body, ...rest } = props;

	let bodyNode: ReactNode | ReactNode[] = (
		<StructogramNodeProcess
			borderBottom
			borderLeft
		/>
	);
	if (body.length > 0) {
		bodyNode = body.map((subnode, index) => (
			<StructogramNode
				key={`subnode-${index}`}
				node={subnode}
				borderBottom
				borderLeft
			/>
		));
	}
	return (
		<StructogramNodeWrapper {...rest}>
			<Box paddingLeft={2}>{bodyNode}</Box>
			<StructogramComponentText>
				{condition}
			</StructogramComponentText>
		</StructogramNodeWrapper>
	);
};
```

The `StructogramNodeLoopLast` component represents a test-last loop node in a structogram.

It takes a `StructogramNodeLoopLastProps` object as its props.
This object includes an optional `condition` property which is a string, a `body` property which is an array of `Node` objects, and optional `borderTop`, `borderBottom`, `borderRight`, and `borderLeft` properties which are boolean values indicating whether the node should have a border on the top, bottom, right, and left respectively.

The indented effect of the loop is achieved by wrapping the `body` in a `Box` component with a `paddingLeft` of 2.

## `StructogramNodeIfElse` component

```tsx
type StructogramNodeIfElseProps = {
	condition?: string;
	bodyIf: Node[];
	bodyElse: Node[];
	borderTop?: boolean;
	borderBottom?: boolean;
	borderRight?: boolean;
	borderLeft?: boolean;
};
export const StructogramNodeIfElse: FC<
	StructogramNodeIfElseProps
> = (props) => {
	const { condition, bodyIf, bodyElse, ...rest } =
		props;

	let bodyNodeIf: ReactNode | ReactNode[] = (
		<StructogramNodeProcess
			borderTop
			borderRight
		/>
	);
	if (bodyIf.length > 0) {
		bodyNodeIf = bodyIf.map((subnode, index) => (
			<StructogramNode
				key={`index-${index}`}
				borderTop
				borderRight
				node={subnode}
			/>
		));
	}

	let bodyNodeElse: ReactNode | ReactNode[] = (
		<StructogramNodeProcess borderTop />
	);
	if (bodyElse.length > 0) {
		bodyNodeElse = bodyElse.map(
			(subnode, index) => (
				<StructogramNode
					key={`index-${index}`}
					borderTop
					node={subnode}
				/>
			),
		);
	}

	return (
		<StructogramNodeWrapper {...rest}>
			<Grid
				container
				height="100%"
			>
				<Grid
					item
					xs={12}
				>
					<StructogramComponentText>
						{condition}
					</StructogramComponentText>
				</Grid>
				<Grid
					item
					xs={6}
				>
					<Box
						height="100%"
						display="flex"
						alignItems="center"
						justifyContent="center"
						position="relative"
					>
						<ArrowTopLeftBottomRight color="inherit" />
						<StructogramComponentText
							sx={{
								zIndex: 2,
								backgroundColor: grey[300],
							}}
						>
							True
						</StructogramComponentText>
					</Box>
				</Grid>
				<Grid
					item
					xs={6}
				>
					<Box
						height="100%"
						display="flex"
						alignItems="center"
						justifyContent="center"
						position="relative"
					>
						<ArrowBottomLeftTopRight color="inherit" />
						<StructogramComponentText
							sx={{
								zIndex: 2,
								backgroundColor: grey[300],
							}}
						>
							False
						</StructogramComponentText>
					</Box>
				</Grid>
				<Grid
					item
					xs={6}
				>
					{bodyNodeIf}
				</Grid>
				<Grid
					item
					xs={6}
				>
					{bodyNodeElse}
				</Grid>
			</Grid>
		</StructogramNodeWrapper>
	);
};
```

The `StructogramNodeIfElse` component represents an if-else node in a structogram.

It takes a `StructogramNodeIfElseProps` object as its props.
This object includes an optional `condition` property which is a string, `bodyIf` and `bodyElse` properties which are arrays of `Node` objects, and optional `borderTop`, `borderBottom`, `borderRight`, and `borderLeft` properties which are boolean values indicating whether the node should have a border on the top, bottom, right, and left respectively.

## `filterEmptyProcessNodes` function

```tsx
const fitlerEmptyProcessNodes = (
	node: Node,
): boolean => {
	return (
		node.kind !== NodeKind.PROCESS ||
		node.body
			.map((token) => token.text)
			.join("")
			.trim().length > 0
	);
};
```

The `fitlerEmptyProcessNodes` function filters out process nodes that do not have text in their body.

It takes a `Node` object as its argument and returns a boolean value.
This function is typically used as a callback function for the `Array.prototype.filter` method, which creates a new array with all elements that pass the test implemented by the provided function.

## `StructogramNode` component

```tsx
type StructogramNodeProps = {
	node: Node;
	borderTop?: boolean;
	borderBottom?: boolean;
	borderRight?: boolean;
	borderLeft?: boolean;
};
export const StructogramNode: FC<
	StructogramNodeProps
> = (props) => {
	const { node, ...rest } = props;
	switch (node.kind) {
		case NodeKind.LOOP_FIRST: {
			let text: string | undefined;
			if (node.condition.length > 0) {
				text = node.condition
					.map((token) => token.text)
					.join("")
					.trim();
			}
			return (
				<StructogramNodeLoopFirst
					{...rest}
					condition={text}
					body={node.body.filter(
						fitlerEmptyProcessNodes,
					)}
				/>
			);
		}
		case NodeKind.LOOP_LAST: {
			let text: string | undefined;
			if (node.condition.length > 0) {
				text = node.condition
					.map((token) => token.text)
					.join("")
					.trim();
			}
			return (
				<StructogramNodeLoopLast
					{...rest}
					condition={text}
					body={node.body.filter(
						fitlerEmptyProcessNodes,
					)}
				/>
			);
		}
		case NodeKind.IF_ELSE: {
			let text: string | undefined;
			if (node.condition.length > 0) {
				text = node.condition
					.map((token) => token.text)
					.join("")
					.trim();
			}
			return (
				<StructogramNodeIfElse
					{...rest}
					condition={text}
					bodyIf={node.bodyIf.filter(
						fitlerEmptyProcessNodes,
					)}
					bodyElse={node.bodyElse.filter(
						fitlerEmptyProcessNodes,
					)}
				/>
			);
		}
		case NodeKind.PROCESS: {
			let text: string | undefined = node.body
				.map((token) => token.text)
				.join("")
				.trim();

			if (text.length === 0) {
				text = undefined;
			}
			return (
				<StructogramNodeProcess
					{...rest}
					text={text}
				/>
			);
		}
	}
	return <Fragment />;
};
```

The `StructogramNode` component a node in a structogram.

It takes a `StructogramNodeProps` object as its props.
This object includes a `node` property which is a `Node` object, and optional `borderTop`, `borderBottom`, `borderRight`, and `borderLeft` properties which are boolean values indicating whether the node should have a border on the top, bottom, right, and left respectively.

If the `kind` property is `NodeKind.LOOP_FIRST` or `NodeKind.LOOP_LAST`, it returns a `StructogramNodeLoopFirst` or `StructogramNodeLoopLast` component respectively, passing it the `rest` object as props, a `condition` prop which is a string created by joining and trimming the `text` properties of the tokens in the `condition` array of the `Node` object, and a `body` prop which is an array of `Node` objects filtered by the `fitlerEmptyProcessNodes` function.

If the `kind` property is `NodeKind.IF_ELSE`, it return a `StructogramNodeIfElse` component, passing it the `rest` object as props, a `condition` prop similar to the one described above, and `bodyIf` and `bodyElse` props which are arrays of `Node` objects filtered by the `fitlerEmptyProcessNodes` function.

If the `kind` property is `NodeKind.PROCESS`, it returns a `StructogramNodeProcess` component, passing it the `rest` object as props and a `text` prop which is a string created by joining and trimming the `text` properties of the tokens in the `body` array of the `Node` object.
