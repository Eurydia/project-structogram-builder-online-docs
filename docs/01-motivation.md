# Background and motivation

During my first year in the Computer Science program at ELTE, I completed a fundamental programming course that incorporated [Nassi–Shneiderman diagrams](https://en.wikipedia.org/wiki/Nassi%E2%80%93Shneiderman_diagram) in the coursework.
As these diagrams are programming language-agnostic, they served as a practical introduction to programming, comparable to the utility of [pseudocode](https://en.wikipedia.org/wiki/Pseudocode) or [flowcharts](https://en.wikipedia.org/wiki/Flowchart).

Unfortunately, I discovered early on that there was no straightforward method available for creating Nassi–Shneiderman diagrams online or elsewhere.
While the course briefly introduced a tool named "Structorizer," it proved to be cumbersome and challenging for students to learn and use effectively.

Various approaches were adopted by my peers to address this challenge.
Some persevered with Structorizer, while others turned to graphic design tools such as [Figma](https://www.figma.com/).
Some even resorted to hand-drawing diagrams on paper and capturing them with a camera.

In my case, I proactively addressed the challenge by developing a [React](https://react.dev/) [UI component library](https://github.com/Eurydia/project-nassi-shneiderman-diagram-builder) to construct diagrams, initially meant for my personal use. As my proficiency in diagram creation became evident, several of my peers approached me for assistance, highlighting a clear need for a more accessible and user-friendly alternative.

Recognizing the inefficiency of personally creating diagrams for others on an individual basis, I keenly observed the widespread need for a more accessible and user-friendly alternative.
This realization became the driving force behind taking the initiative to create this project.

## Mission statement

> "MermaidJS for Nassi–Shneiderman diagrams."

[MermaidJS](https://mermaid.js.org/) is a well-established [JavaScript](https://developer.mozilla.org/en-US/docs/Web/javascript) library in the frontend web development community which excels at dynamically constructing diagrams and charts.
This project adopts a similar methodology to create Nassi–Shneiderman diagrams from code snippets.

## Scopes and goals

In addition to the core functionality of diagram creation, the project encompasses several much-needed features:

- **Device Compatibility**: Ensuring seamless functionality across various devices.
- **Diagram Sharing and Export**: Facilitating the easy sharing and exportation of created diagrams.
- **Auto-Save Functionality**: Implementing an automatic progress-saving mechanism.
- **Online Accessibility and Responsiveness**: Enabling online access with a responsive design for user-friendly interaction.
- **User-Friendly Design**: Prioritizing an intuitive and easily comprehensible interface to enhance the learning curve and overall usability of the platform.
