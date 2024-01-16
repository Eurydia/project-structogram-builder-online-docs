# Syntax

Much like [Mermaid](https://mermaid.js.org/), the project uses a special scripting language.

I designed the langauge to be permissive and mimicked its syntax after the [C programming language](<https://en.wikipedia.org/wiki/C_(programming_language)>).
I expect users who are experienced with coding should have no issue with the project.
As for users with less experience, I hope to provide a risk-free playground to experiment.

At the time of writing, the project supports [process blocks](#process-block), [testing loops](#testing-loop), [branching blocks](#branching-block), and [functions](#function-blocks).

There are multiple interactive examples on this section.
On smaller devices, live preview is shown by default.
Press "Show code" to hide the preview.

## Process block

From [Wikipedia](https://en.wikipedia.org/wiki/Nassi%E2%80%93Shneiderman_diagram#Diagrams):

> "The process block represents the simplest of steps and requires no analysis.
> When a process block is encountered, the action inside the block is performed and we move onto the next block. "

Process blocks are flexible by design.
A piece of text is "essentially" copied from the code and pasted onto the diagram with no modification.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?preview=true&content=process%3B"></iframe>

I have included three ways to convey variable assignment.
The project does not enforce a particular style, but if you are an ELTE student, you might want to use the following:

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?preview=true&content=x+%3A%3D+0%3B"></iframe>

I have seen some Wikipedia articles, for example, an article on [Insertion sort](https://en.wikipedia.org/wiki/Insertion_sort#Algorithm), uses the `<-` operator.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?preview=true&content=x+%3C-+0%3B"></iframe>

Even better, you can describe what you want in the process.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?preview=true&content=Initialize+a+variable+%22x%22+and+%0Aassign+integer+%220%22+to+it."></iframe>

## Testing loop

From [Wikipedia](https://en.wikipedia.org/wiki/Nassi%E2%80%93Shneiderman_diagram#Diagrams):

> "The testing loop allows the program to loop one or a set of processes until a particular condition is fulfilled.
> The process blocks covered by each loop are subset with a side-bar extending out from the condition."

There are two types of testing loops, test first and test last blocks. The difference is the order in which the steps involved are completed.

In test-first loops, the condition is tested before the processes, while in test-last loops, the condition is tested after the processes.

Both testing loops have two components.

Elements enclosed by a pair of parentheses `(...)` belong to the "condition" component.
Such elements are copied from the code and pasted onto the diagram.

Elements enclosed by a pair of curly braces `{...}` belong to the "body" component.

### Test-first loop

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?preview=true&content=for+%28condition%29+%7B%0A++process%3B%0A%7D"></iframe>

Nesting loops is possible, but you can only nest so deep before the diagram becomes unreadable.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?preview=true&content=for+%28condition%29+%7B%0A++for+%28another+condition%29+%7B%0A++++for+%28another+another+condition%29+%7B%0A++++++uhhhhh...%3B%0A++++%7D%0A++%7D%0A%7D"></iframe>

Alternatively, a test-first loop may be invoked with "while" keyword, instead of "for."
The project produces the same diagram and does not distinguish between "for" and "while" keyword.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?preview=true&content=while+%28condition%29+%7B%0A++while+%28another+condition%29+%7B%0A++++while+%28another+another+condition%29+%7B%0A++++++uhhhhh...%3B%0A++++%7D%0A++%7D%0A%7D"></iframe>

I have included a few ways to write a test-first loop.
If you are an ELTE student, you might want to use the following syntax.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?preview=true&content=for+%28i+%3D+1..10%29+%7B%0A++...%3B%0A%7D"></iframe>

Some pseudocode uses `<-` to signifies each iteration.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?preview=true&content=for+%28i+%3C-+1..10%29+%7B%0A++...%3B%0A%7D"></iframe>

The property of the double dots can be confusing, so we can also write a description.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?preview=true&content=for+%28i+%3C-+from+1+to+10+increment+by+1%29+%7B%0A++...%3B%0A%7D"></iframe>

### Test-last loops

Generally, test-last loop blocks supports everything that [test-first loop blocks](#test-first-loop-block) support.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?preview=true&content=do+%7B%0A++process%3B%0A%7D+while+%28condition%29%3B"></iframe>

Here is an example with nested test-last loops.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?preview=true&content=do+%7B%0A++do+%7B%0A++++do+%7B%0A++++++uhhhhh...%3B+%0A++++%7D+while+%28another+another+condition%29%3B%0A++%7D+while+%28another+condition%29%3B%0A%7D+while+%28condition%29%3B%0A"></iframe>

## Branching block

If blocks have two components.
Texts enclosed by a pair of parentheses `(...)` belong to the "condition" component.
Texts enclosed by a pair of curly braces `{...}` belong to the "body" component.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?preview=true&content=if+%28condition%29+%7B%0A++process%3B%0A%7D"></iframe>

Optionally, you can convert an if block into an if-else block by including an else block.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?preview=true&content=if+%28condition%29+%7B%0A++process%3B%0A%7D+else+%7B%0A++another+process%3B%0A%7D"></iframe>
