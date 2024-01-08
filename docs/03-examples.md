# Examples

This section demonstrates the capabilities of the project to draw diagrams.
It is not a tutorial on how to use the project, but rather a showcase of what the project can do and how it can be used to draw diagrams.

## Example 1

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?preview=true&content=result%3A+int+%3A%3D+init%3B%0Afor+%28i+%3D+1..n%29+%7B%0A++result+%3A%3D+op%28result%2C+seq%5Bi%5D%29%3B%0A%7D"></iframe>

## Example 2

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?preview=true&content=cnt%3A+int+%3A%3D+0%3B%0Afor+%28i+%3D+1..n%29+%7B%0A++if+%28Attr%28seq%5Bi%5D%29%29+%7B%0A++++cnt+%3A%3D+cnt+%2B+1%3B%0A++%7D+else+%7B%0A++++-%3B%0A++%7D%0A%7D%0A"></iframe>

## Example 3

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?preview=true&content=result%3A+int+%3A%3D+fallback%3B%0Afor+%28i+%3D+1..n%29+%7B%0A++if+%28Attr%28seq%5Bi%5D%29%29+%7B%0A++++result+%3A%3D+seq%5Bi%5D%3B%0A++%7D+else+%7B%0A++++-%3B%0A++%7D%0A%7D"></iframe>

## Example 4

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?preview=true&content=result%3A+bool+%3A%3D+False%3B%0Afor+%28i+%3D+1..n%29+%7B%0A++if+%28Attr%28seq%5Bi%5D%29%29+%7B%0A++++result+%3A%3D+True%0A++%7D+else+%7B%0A++++-%3B%0A++%7D%0A%7D"></iframe>

## Example 5

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?preview=true&content=digits%3A+int%5B1..%5D+%3A%3D+toDigits%28x%29%3B%0Asize%3A+int+%3A%3D+length%28digits%29%3B%0A%0Aresult%3A+bool+%3A%3D+True%3B%0A%0Afor+%28i+%3D+1..size%29+%7B%0A++result+%3A%3D+result+AND+%0A++++%28digits%5Bsize+-+i+%2B+1%5D+%3D+digits%5Bi%5D%29%3B%0A%7D%0A"></iframe>

## Example 6

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?preview=true&content=result%3A+bool+%3A%3D+True%3B%0Afor+%28div+%3D+2..%28x+-+1%29%29+%7B%0A++result+%3A%3D+result+AND+%28x%7Cdiv+%21%3D+0%29%3B%0A%7D"></iframe>

## Example 7

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?preview=true&content=result+%3A%3D+0%3B%0Afor+%28i+%3D+2..n%29+%7B%0A++if+%28X%5Bi-1%2C+1%5D+%3C+X%5Bi%2C+1%5D+AND+X%5Bi-1%2C+2%5D+%3C+X%5Bi%2C+2%5D%29+%7B%0A++++result+%3A%3D+result+%2B+1%3B%0A++%7D%0A%7D"></iframe>

## Example 8

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?preview=true&content=total+%3A%3D+0%3B%0Afor+%28i+%3D+1..n%29+%7B%0A++volumn+%3A%3D+L%5Bi%5D+*+L%5Bi%5D+*+L%5Bi%5D%3B%0A++total+%3A%3D+total+%2B+volume%3B%0A%7D"></iframe>
