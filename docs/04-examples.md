# Examples

This section demonstrates the capabilities to draw diagrams.
It is not a tutorial on how to use the project, but rather a showcase of what the project can do.

## Variable assignment

The [origial paper](https://www.cs.umd.edu/hcil/members/bshneiderman/nsd/Yoder-Schrag-nassi_schart.pdf) uses textual description to explain that a variable is initialized or assigned to.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?preview=true&content=Set+%22var%22+to+%221%22%3B"></iframe>

If you are an ELTE student, the Facualty of Informatics uses the ":=" symbol, which traced back to a [Wikipedia article](https://en.wikipedia.org/wiki/Pseudocode#Common_mathematical_symbols).

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?preview=true&content=var+%3A%3D+1%3B"></iframe>

## Type annotation

Textual description seems to be the most straight-forward way method of type annotation.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?preview=true&content=Initialize+%22var%22+of+type+%22Integer%22+to+%220%22%3B%0ASet+%22var%22+of+type+%22Integer%22+to+%221%22%3B"></iframe>

I cannot find a universally-accepted syntax for type annotation, so I think it is fair to say the sky is the limit.

If you are looking for an inspiration, I find the C-style type declaration rather suitable since it does not modify the overall variable assignment syntax by much.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?preview=true&content=Integer+i+%3A%3D+0%3B%0ABoolean+b+%3A%3D+False%3B%0AReal++++r+%3A%3D+0.0%3B%0AString++s+%3A%3D+%220%22%3B"></iframe>

In accordance with the Facaulty of Informatics at ELTE, the syntax for type annotation is similar to that of [Python](https://docs.python.org/3/library/typing.html) or [Typescript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html).

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?preview=true&content=i%3A+Integer+%3A%3D+0%3B%0Ab%3A+Boolean+%3A%3D+False%3B%0Ar%3A+Real++++%3A%3D+0.0%3B%0As%3A+String++%3A%3D+%220%22%3B"></iframe>

The type annotation for sequences compose of three components; the element type, the starting index, and the terminating index, which is optional.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?preview=true&content=%2F%2F+A+finite+sequence%0Aseq%3A+Integer%5B1..3%5D+%3A%3D+%5B1%2C+2%2C+3%5D%3B%0A%0A%2F%2F+An+%22infinite%22+sequence%0AinfSeq%3A+Integer%5B1..%5D+%3A%3D+%5B1%2C+2%2C+3%2C+...%5D%3B"></iframe>

## Loop

The processes inside a loop is not particularly interesting, and the condition component does not have a systematic standard either.

The Facualty often uses the [Pascal](<https://en.wikipedia.org/wiki/Pascal_(programming_language)>) style albeit with some modification.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?preview=true&content=for+%28i+%3A%3D+1+to+100%29+%7B%0A++processes%3B%0A%7D"></iframe>

The ".." symbol helps reduce visual clutter every so slightly, but it works when enough context is provided.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?preview=true&content=for+%28i+%3D+1..100%29+%7B%0A++processes%3B%0A%7D"></iframe>

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
