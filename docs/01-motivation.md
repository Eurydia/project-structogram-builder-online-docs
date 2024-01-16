# Background and motivation

During the first year of Computer Science degree at ELTE, I was completing a basic programming course, which extensively used [Nassi–Shneiderman diagrams](https://en.wikipedia.org/wiki/Nassi%E2%80%93Shneiderman_diagram) from course materials to assignments.
It was a reasonable method to introduce students to general concepts of programming much like [pseudocode](https://en.wikipedia.org/wiki/Pseudocode) or even [flowcharts](https://en.wikipedia.org/wiki/Flowchart).

Unfortunately, I found out quite early on that there was not an easy way to draw a Nassi–Shneiderman diagram on the internet, or elsewhere.
The course instructor and demonstrators did briefly introduced students to a diagrammingtool called "Structorizer", but it was rather cumbersome to learn and difficult to use.

Some of my coursemates perservered and used the tool provided anyway,
some resorted to graphic design tools like [Figma](https://www.figma.com/), and some went as far as drawing a diagram on a piece of paper and taking a picture of it.

As for myself, I built a [React](https://react.dev/) component library.
Each structure is represented by a component, and I would put these components together to build a diagram.
The library was far from perfect since I had no intention publishing it.
The source code is available on [Github](https://github.com/Eurydia/project-nassi-shneiderman-diagram-builder).

At the end of the course, it was clear that students needed an alternative method of building a diagram, so I took inititive and create this project.

## Mission statement

> "Mermaid for Nassi–Shneiderman diagrams."

[MermaidJS](https://mermaid.js.org/), or Mermaid is a [JavaScript](https://developer.mozilla.org/en-US/docs/Web/javascript) library.
It is well-known in the frontend web development community as a robust tool for building diagrams and charts from a piece of code.

In a sense, I planned for this project to take a similar approach.
It would take a piece of code and generate a diagram.

## Scopes and goals

Apart from building diagrams, I wanted to implement additional quality-of-life features.
These features are not meant to be ground-breaking, but something that users have come to expect.

Namely,

- it should work on any device,
- it should provide a way to share and export the diagram,
- it should automatically save the progress,
- it is online and responsive,
- it is easy to learn and easy to use.
