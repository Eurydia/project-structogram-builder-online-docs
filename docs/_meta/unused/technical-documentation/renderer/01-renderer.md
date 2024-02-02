# Renderer

The primary purpose of the renderer is to take a list of nodes and render them as a React component.

The render consists of two parts: the `StructogramNode` component and the `renderer` function.
The `StructogramNode` component renders a single node as a React component, and the `renderer` function renders a list of nodes as a React component.

## `renderer` function

```tsx
export const renderer = (
	nodes: Node[],
	id: string,
	boxProps: SxProps,
): ReactNode => {
	let component: ReactNode | ReactNode[] = (
		<Typography
			fontFamily="inherit"
			fontStyle="italic"
		>
			Nothing to display.
		</Typography>
	);
	const filteredNodes = nodes.filter(
		(node) =>
			node.kind !== NodeKind.PROCESS ||
			node.body
				.map((token) => token.text)
				.join("")
				.trim().length > 0,
	);
	if (filteredNodes.length > 0) {
		component = filteredNodes.map(
			(node, index) => (
				<StructogramNode
					key={index}
					node={node}
					borderLeft
					borderTop
					borderRight
					borderBottom={
						index === filteredNodes.length - 1
					}
				/>
			),
		);
	}
	return (
		<Box sx={boxProps}>
			<Box
				id={id}
				maxWidth="640px"
				fontFamily="Fira Code"
				sx={{
					wordBreak: "break-all",
					fontVariantLigatures: "contextual",
					userSelect: "none",
				}}
			>
				{component}
			</Box>
		</Box>
	);
};
```

The `renderer` function renders a list of nodes as a series of `StructogramNode` components or a `Typography` component if there are no nodes to display.
It takes an array of `Node` objects, a string, and an `SxProps` object as arguments, and returns a `ReactNode`.

- The `nodes` argument is an array of `Node` objects that represent the nodes to render.
- The `id` argument is a string that represents the `id` prop of the outermost `Box` component. This `id` is used to capture the rendered nodes as an image.
- The `boxProps` argument is an `SxProps` object that represents the `sx` prop of the outermost `Box` component. Primirily, it is used to set the height of the outermost `Box` component.

Here is the implementation of the `renderer` function:

First, it initializes a `ReactNode` object `component` with a `Typography` component.
This is for the case where there are no nodes to display.

```tsx
let component: ReactNode | ReactNode[] = (
	<Typography
		fontFamily="inherit"
		fontStyle="italic"
	>
		Nothing to display.
	</Typography>
);
```

Then, it creates a new array `filteredNodes` that contains the `Node` objects in the `nodes` array that either have a `kind` property not equal to `NodeKind.PROCESS` or have a `body` property that contains at least one non-white space character.
This prevents empty `PROCESS` nodes from being rendered.

```tsx
const filteredNodes = nodes.filter(
	(node) =>
		node.kind !== NodeKind.PROCESS ||
		node.body
			.map((token) => token.text)
			.join("")
			.trim().length > 0,
);
```

If the `filteredNodes` array is not empty, it reassigns the `component` object with an array of `StructogramNode` components that each represent a node in the `filteredNodes` array.

```tsx
if (filteredNodes.length > 0) {
	component = filteredNodes.map((node, index) => (
		<StructogramNode
			key={index}
			node={node}
			borderLeft
			borderTop
			borderRight
			borderBottom={
				index === filteredNodes.length - 1
			}
		/>
	));
}
```

Each `StructogramNode` component is given a `key` prop equal to its index in the array, a `node` prop equal to the corresponding `Node` object, and `borderLeft`, `borderTop`, `borderRight`, and `borderBottom` props.
The `borderBottom` prop is only true for the last `StructogramNode` component in the array.

```tsx
<StructogramNode
	key={index}
	node={node}
	borderLeft
	borderTop
	borderRight
	borderBottom={
		index === filteredNodes.length - 1
	}
/>
```

Finally, it returns a `Box` component that contains another `Box` component.
This inner `Box` component contains the `component` object.

```tsx
// ...
return (
	<Box sx={boxProps}>
		<Box
			id={id}
			maxWidth="640px"
			fontFamily="Fira Code"
			sx={{
				wordBreak: "break-all",
				fontVariantLigatures: "contextual",
				userSelect: "none",
			}}
		>
			{component}
		</Box>
	</Box>
);
// ...
```
