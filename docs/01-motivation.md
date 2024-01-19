# Background and motivation

During the first year of Computer Science degree at ELTE, I was completing a basic programming course, which featured [Nassi–Shneiderman diagrams](https://en.wikipedia.org/wiki/Nassi%E2%80%93Shneiderman_diagram) in the course materials and assignments.
Since Nassi–Shneiderman diagrams are not dependent of programming languages, it was a reasonable introduction to programming much like [pseudocode](https://en.wikipedia.org/wiki/Pseudocode) or [flowcharts](https://en.wikipedia.org/wiki/Flowchart).

Unfortunately, I found out early on that there was not an easy way to draw a Nassi–Shneiderman diagram online, or elsewhere.
The course instructor and demonstrators did briefly introduced students to a diagramming tool called "Structorizer", but it was rather cumbersome to learn and difficult to use.

Some of my coursemates perservered and used Structorizer regardless,
some resorted to graphic design tools like [Figma](https://www.figma.com/), and some went as far as drawing a diagram on a piece of paper and taking a picture of it.

As for myself, I built a [React](https://react.dev/) component library, whose source code is available on [GitHub](https://github.com/Eurydia/project-nassi-shneiderman-diagram-builder), and used it to build diagrams

At the end of the course, it was clear that students needed an alternative method of building a diagram, so I took inititive and create this project.

## Mission statement

> "Mermaid for Nassi–Shneiderman diagrams."

[MermaidJS](https://mermaid.js.org/) is a [JavaScript](https://developer.mozilla.org/en-US/docs/Web/javascript) library.
It is well-known in the frontend web development community as a robust tool for building diagrams and charts dynamically.
This project take the same approach by building a diagram from a piece of code.

## Scopes and goals

Apart from building diagrams, the project needs additional quality-of-life features.
Namely,

- it should work on any device,
- it should provide a way to share and export the diagram,
- it should automatically save the progress,
- it is online and responsive,
- it is easy to learn and easy to use.
