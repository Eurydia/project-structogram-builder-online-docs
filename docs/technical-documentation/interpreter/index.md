# Overview

This section of the documentation will discuss about the interpter which is responsible generating an AST from user input.

The interpreter consists of two components: the lexer and the parser both of which are written in pure TypeScript.
I did not used any external libraries for the lexer and the parser, and I wrote them from scratch and inituition, so the implementation may not be the most efficient.

Each of these are placed in their own module at `src/interpreter/lexer.ts` and `src/interpreter/parser.ts` respectively.
