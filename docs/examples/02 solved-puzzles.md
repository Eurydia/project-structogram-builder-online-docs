# Solved puzzles

Here is a collection of solved problems and its diagrams.
Since the goal of this section is to show the diagrams, the solutions are not explained in detail, and only one approach is shown.

The puzzles are collected from LeetCode and a few other sources the specific source is mentioned in the description of each puzzle.

## Is palindrome

Check [Palindrome Number](https://leetcode.com/problems/palindrome-number/) on LeetCode for the full description.

**Question**

Given an integer `x`, return true if `x` is a
palindrome, and false otherwise.

**Solution**

In this solution, all negative numbers are considered as non-palindrome by example, so we will only draw the diagram in cases where `x` is positive.

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?content=digits%3A+int%5B1..%5D+%3A%3D+toDigits%28x%29%3B%0Asize%3A+int+%3A%3D+length%28digits%29%3B%0A%0Aresult%3A+bool+%3A%3D+True%3B%0A%0Afor+%28i+%3D+1..size%29+%7B%0A++result+%3A%3D+result+AND+%0A++++%28digits%5Bsize+-+i+%2B+1%5D+%3D+digits%5Bi%5D%29%3B%0A%7D%0A"></iframe>

## Is prime

**Question**

Given a non-negative integer `x`, return true if `x` is prime, and false otherwise.

**Solution**

<iframe width="100%" style="aspect-ratio: 16/9; border:none;" loading="lazy" src="https://eurydia.github.io/project-nassi-shneiderman-diagram-builder-online/?content=result%3A+bool+%3A%3D+True%3B%0Afor+%28div+%3D+2..%28x+-+1%29%29+%7B%0A++result+%3A%3D+result+AND+%28x%7Cdiv+%21%3D+0%29%3B%0A%7D"></iframe>
