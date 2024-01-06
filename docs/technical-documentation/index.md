# Overview

This section discusses the implementation of the project.
It is written entirely in [TypeScript](https://www.typescriptlang.org/) with [React](https://react.dev/) and bundled together using [vite](https://vitejs.dev/).

In my persective, the project consists of three major parts: the interpreter,the renderer, and the frontend.

The interpreter and the renderer belong to the business logic, abd the frontend belongs to the application logic.

## Interpreter

The interpreter builds an [abstract syntax trees](https://en.wikipedia.org/wiki/Abstract_syntax_tree) from user input.

It is worth noting that I did not used any external libraries for the lexer and the parser.
Instead, I wrote them from inituition, so the implementation may not be the most efficient.

## Renderer

The renderer takes an abstract syntax tree and generate a diagram.
I should preface that the renderer is nothing more than a React component.

## Frontend

The frontend handles features discussed in [motivation](../01-motivation.md), such as exporting diagram and auto-saving.
It also bridges the interpreter and the renderer.
