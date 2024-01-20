# Examples

This section demonstrates the capabilities to draw diagrams.
It is not a tutorial on how to use the project, but rather a showcase of what the project can do.

## Variable assignment

Textual description:

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?preview=true&content=Set+%22var%22+to+%221%22%3B"></iframe>

The [Pseudocode](https://en.wikipedia.org/wiki/Pseudocode#Common_mathematical_symbols) style variable assignment:

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?preview=true&content=var+%3A%3D+1%3B"></iframe>

## Type annotation

Textual description:

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?preview=true&content=Set+%22var%22+of+type+%22Integer%22+to+%221%22%3B"></iframe>

The [C programming language](https://en.wikipedia.org/wiki/The_C_Programming_Language) style type declaration:

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?preview=true&content=Integer+var+%3A%3D+0%3B"></iframe>

[Python](https://docs.python.org/3/library/typing.html) and [Typescript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html) type annotation:

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?preview=true&content=var%3A+Integer+%3A%3D+0%3B"></iframe>

## Loop

The [Pascal](<https://en.wikipedia.org/wiki/Pascal_(programming_language)>) style loop:

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?preview=true&content=for+%28i+%3A%3D+1+to+100%29+%7B%0A++processes%3B%0A%7D"></iframe>

## Sequence calculation

Sequence calculation is a pattern of algorithm which reduces a sequence of elements to one element.
In the most generic form, this pattern requires an initial value as a starting point and a reducer function.

The "result" variable is the accummulator as the sequence is calculated and the "op" function is the reducer function.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?preview=true&content=result+%3A%3D+init%3B%0Afor+%28i+%3D+1..length%28seq%29%29+%7B%0A++result+%3A%3D+op%28result%2C+seq%5Bi%5D%29%3B%0A%7D%0A"></iframe>

## Counting

Counting is a pattern of algorithm which reduces a sequence of elements to a natural number.
The behavior is archieved through a predicate function.

The "counter" variable keeps track of valid and invalid elements and the "hasAttr" function serves as the predicate.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?preview=true&content=counter%3A+natural+%3A%3D+0%3B%0Afor+%28i+%3D+1..length%28seq%29%29+%7B%0A++if+%28hasAttr%28seq%5Bi%5D%29%29+%7B%0A++++counter+%3A%3D+counter+%2B+1%3B%0A++%7D%0A%7D%0A"></iframe>
