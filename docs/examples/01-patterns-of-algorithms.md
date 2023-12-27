# Pattterns of algorithms

I have included common patterns of algorithms to demonstrate how each pattern is represented in the builder.

## Sequence calculation

Let `seq` be a sequence of integers of length `n` start indexing from one, `init` be an integer, and `op` be a binary operator that takes two integers and returns an integer, then we can draw the diagram like this:

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?content=result%3A+int+%3A%3D+init%3B%0Afor+%28i+%3D+1..n%29+%7B%0A++result+%3A%3D+op%28result%2C+seq%5Bi%5D%29%3B%0A%7D"></iframe>

## Counting

Let `seq` be a sequence of integers of length `n` start indexing from one, and `Attr` be a predicate that takes an integer and returns a boolean, then we can draw the diagram like this:

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?content=cnt%3A+int+%3A%3D+0%3B%0Afor+%28i+%3D+1..n%29+%7B%0A++if+%28Attr%28seq%5Bi%5D%29%29+%7B%0A++++cnt+%3A%3D+cnt+%2B+1%3B%0A++%7D+else+%7B%0A++++-%3B%0A++%7D%0A%7D%0A"></iframe>

## Search

Let `seq` be a sequence of integers of length `n` start indexing from one, `fallback` be an integer, and `Attr` be a predicate that takes an integer and returns a boolean, then we can draw the diagram like this:

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?content=result%3A+int+%3A%3D+fallback%3B%0Afor+%28i+%3D+1..n%29+%7B%0A++if+%28Attr%28seq%5Bi%5D%29%29+%7B%0A++++result+%3A%3D+seq%5Bi%5D%3B%0A++%7D+else+%7B%0A++++-%3B%0A++%7D%0A%7D"></iframe>

## Decision

Let `seq` be a sequence of integers of length `n` start indexing from one, and `Attr` be a predicate that takes an integer and returns a boolean, then we can draw the diagram like this:

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?content=result%3A+bool+%3A%3D+False%3B%0Afor+%28i+%3D+1..n%29+%7B%0A++if+%28Attr%28seq%5Bi%5D%29%29+%7B%0A++++result+%3A%3D+True%0A++%7D+else+%7B%0A++++-%3B%0A++%7D%0A%7D"></iframe>
