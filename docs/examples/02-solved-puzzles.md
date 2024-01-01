# Solved puzzles

This section is a collection of solved problems and its diagrams.
The goal is to provide some practical uses, so the solutions are not explained in detail, and only one approach is shown.

## Is palindrome

Check [Palindrome Number](https://leetcode.com/problems/palindrome-number/) on LeetCode for the full description.

**Context**

lLet $x$ be an integer, check whether it is a palindrome number or not.

**Diagram**

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?content=digits%3A+int%5B1..%5D+%3A%3D+toDigits%28x%29%3B%0Asize%3A+int+%3A%3D+length%28digits%29%3B%0A%0Aresult%3A+bool+%3A%3D+True%3B%0A%0Afor+%28i+%3D+1..size%29+%7B%0A++result+%3A%3D+result+AND+%0A++++%28digits%5Bsize+-+i+%2B+1%5D+%3D+digits%5Bi%5D%29%3B%0A%7D%0A"></iframe>

## Is prime

**Context**

Let $x$ be a non-negative integer, check whether it is a prime number or not.

**Diagram**

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?content=result%3A+bool+%3A%3D+True%3B%0Afor+%28div+%3D+2..%28x+-+1%29%29+%7B%0A++result+%3A%3D+result+AND+%28x%7Cdiv+%21%3D+0%29%3B%0A%7D"></iframe>

## Air pollution deterioration

**Context**

Let $X$ be a list of ordered pairs, count the number of ordered pairs whose first and second component are greater than the previous.

**Diagram**

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?content=result+%3A%3D+0%3B%0Afor+%28i+%3D+2..n%29+%7B%0A++if+%28X%5Bi-1%2C+1%5D+%3C+X%5Bi%2C+1%5D+AND+X%5Bi-1%2C+2%5D+%3C+X%5Bi%2C+2%5D%29+%7B%0A++++result+%3A%3D+result+%2B+1%3B%0A++%7D%0A%7D"></iframe>

## Biggest volume

**Context**

Let $L$ be a list of integers, which represent side length of a cude, count the total volume.

**Diagram**

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?content=total+%3A%3D+0%3B%0Afor+%28i+%3D+1..n%29+%7B%0A++volumn+%3A%3D+L%5Bi%5D+*+L%5Bi%5D+*+L%5Bi%5D%3B%0A++total+%3A%3D+total+%2B+volume%3B%0A%7D"></iframe>
