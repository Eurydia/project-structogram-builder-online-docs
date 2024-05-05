# Examples

This section demonstrates the capabilities to draw diagrams.
It is not a tutorial on how to use the project, but rather a showcase of what the project can do.

## Variable assignment

> Variable assignment is a fundamental concept that involves giving a name to a piece of data.
> It allows for storage and manipulation of information within a computer program.

When a value is assigned to a variable, it is akin to instructing the system, "Remember this information by this name."
It's like storing a number, a word, or any other data type under a chosen label.
The label can then be utilized in the code to perform operations, make decisions, or simply reference that piece of data.

Textual description:

<iframe width="100%" style="aspect-ratio: 16/10; border:none;" loading="lazy" src="https://eurydia.github.io/project-structogram-builder-online/?preview=true&content=Set+%22var%22+to+%221%22%3B"></iframe>

[Pseudocode](https://en.wikipedia.org/wiki/Pseudocode#Common_mathematical_symbols) style using ":=" symbol:

<iframe width="100%" style="aspect-ratio: 16/10; border:none;" loading="lazy" src="https://eurydia.github.io/project-structogram-builder-online/?preview=true&content=var+%3A%3D+1%3B"></iframe>

[Pseudocode](https://en.wikipedia.org/wiki/Pseudocode#Common_mathematical_symbols) style using "<-" symbol:

<iframe width="100%" style="aspect-ratio: 16/10; border:none;" loading="lazy" src="https://eurydia.github.io/project-structogram-builder-online/?preview=true&content=var+%3C-+1%3B"></iframe>

## Type annotation

> Type annotation is the practice of explicitly specifying the data type of a variable.
> This helps in defining the kind of information that a variable can hold, promoting code clarity and preventing potential errors.

When annotating the type of a variable, additional information is provided to both programmers and the compiler or interpreter.
It is similar to informing the system that a variable is meant to store numbers, text, or some other specific data type.

Textual description:

<iframe width="100%" style="aspect-ratio: 16/10; border:none;" loading="lazy" src="https://eurydia.github.io/project-structogram-builder-online/?preview=true&content=Set+%22var%22+of+type+%22Integer%22+to+%221%22%3B"></iframe>

[C programming language](https://en.wikipedia.org/wiki/The_C_Programming_Language) style:

<iframe width="100%" style="aspect-ratio: 16/10; border:none;" loading="lazy" src="https://eurydia.github.io/project-structogram-builder-online/?preview=true&content=Integer+var+%3A%3D+1%3B"></iframe>

[Python](https://docs.python.org/3/library/typing.html) style:

<iframe width="100%" style="aspect-ratio: 16/10; border:none;" loading="lazy" src="https://eurydia.github.io/project-structogram-builder-online/?preview=true&content=var%3A+Integer+%3A%3D+1%3B"></iframe>

## Loop

Textual Description (Test-first loop):

<iframe width="100%" style="aspect-ratio: 16/10; border:none;" loading="lazy" src="https://eurydia.github.io/project-structogram-builder-online/?preview=true&content=for+%28Repeat+until+%22condition%22%29+%7B%0A++processes%3B%0A%7D"></iframe>

Pseudocode style (Test-first loop):

<iframe width="100%" style="aspect-ratio: 16/10; border:none;" loading="lazy" src="https://eurydia.github.io/project-structogram-builder-online/?preview=true&content=for+%28i+%3D+%22something%22+TO+%22something+else%22%29+%7B%0A++processes%3B%0A%7D"></iframe>

Python style:

<iframe width="100%" style="aspect-ratio: 16/10; border:none;" loading="lazy" src="https://eurydia.github.io/project-structogram-builder-online/?preview=true&content=for+%28EACH+item+IN+container%29+%7B%7D"></iframe>

C style:

<iframe width="100%" style="aspect-ratio: 16/10; border:none;" loading="lazy" src="https://eurydia.github.io/project-structogram-builder-online/?preview=true&content=for+%28i+%3A%3D+FROM+a+TO+b+STEP+c%29+%7B%7D"></iframe>

## Functions

Python style:

<iframe width="100%" style="aspect-ratio: 16/10; border:none;" loading="lazy" src="https://eurydia.github.io/project-structogram-builder-online/?preview=true&content=def+sum%28a%3A+Integer%2C+b%3A+Integer%29%3A+Integer+%7B%7D"></iframe>

C style:

<iframe width="100%" style="aspect-ratio: 16/10; border:none;" loading="lazy" src="https://eurydia.github.io/project-structogram-builder-online/?preview=true&content=Integer+sum%28Integer+a%2C+Integer+b%29+%7B%7D"></iframe>

[Bash](https://www.gnu.org/software/bash/) style:

<iframe width="100%" style="aspect-ratio: 16/10; border:none;" loading="lazy" src="https://eurydia.github.io/project-structogram-builder-online/?preview=true&content=sum+%7B%7D"></iframe>

## Sequence calculation

Sequence calculation is a pattern of algorithm which reduces a sequence of elements to one element, which is archieved by repeated applying functions or operations to two elements and combining them into one.

Sequence calculation on integers using addition:

<iframe width="100%" style="aspect-ratio: 16/10; border:none;" loading="lazy" src="https://eurydia.github.io/project-structogram-builder-online/?preview=true&content=Summation%28Integer%5B1..%5D+sequence%29+%7B%0A++Integer+result+%3A%3D+sequence%5B1%5D%3B%0A++for+%28i+%3D+2..length%28sequence%29%29+%7B%0A++++result+%3A%3D+result+%2B+sequence%5Bi%5D%3B%0A++%7D%0A%7D "></iframe>

## Counting

Counting is a pattern of algorithm which reduces a sequence of elements to a natural number.
It looks at every element in a sequence and see how many of those elements have a certain property.

Counting the number of primes numbers in an interval:

<iframe width="100%" style="aspect-ratio: 16/10; border:none;" loading="lazy" src="https://eurydia.github.io/project-structogram-builder-online/?preview=true&content=Counting%28Integer+start%2C+Integer+end%29+%7B%0A++Integer+count+%3A%3D+0%3B%0A++for+%28i+%3D+start..end%29+%7B%0A++++if+%28isPrime%28i%29%29+%7B%0A++++++count+%3A%3D+count+%2B+1%3B%0A++++%7D%0A++%7D%0A%7D"></iframe>

## Maximum selection and minimum selection

Maximum selection and minmium selection are a similar pattern algorithm.
Both of them reduce a sequence of elements to one element.
This element is either the "maximum" or the "minimum" element of the sequence.

Maximum selection on integers:

<iframe width="100%" style="aspect-ratio: 16/10; border:none;" loading="lazy" src="https://eurydia.github.io/project-structogram-builder-online/?preview=true&content=MaximumSelection%28Integer%5B1..%5D+sequence%29+%7B%0A++Integer+result+%3A%3D+sequence%5B1%5D%3B%0A++for+%28i+%3D+2..length%28sequence%29%29+%7B%0A++++if+%28sequence%5Bi%5D+%3E+result%29+%7B%0A++++++result+%3A%3D+sequence%5Bi%5D%3B%0A++++%7D%0A++%7D%0A%7D"></iframe>

Minimum selection on integers:

<iframe width="100%" style="aspect-ratio: 16/10; border:none;" loading="lazy" src="https://eurydia.github.io/project-structogram-builder-online/?preview=true&content=MinimumSelection%28Integer%5B1..%5D+sequence%29+%7B%0A++Integer+result+%3A%3D+sequence%5B1%5D%3B%0A++for+%28i+%3D+2..length%28sequence%29%29+%7B%0A++++if+%28sequence%5Bi%5D+%3C+result%29+%7B%0A++++++result+%3A%3D+sequence%5Bi%5D%3B%0A++++%7D%0A++%7D%0A%7D"></iframe>

## Search

Search is a pattern of algorithm which reduces a sequence of elements to one element.
The element is chosen based on whether it has a certain property or not.
However, such an element might not exist in the sequence.

Searching for a prime number in a sequence of integers, defaults to "-1" when the sequence does not contain a prime number:

<iframe width="100%" style="aspect-ratio: 16/10; border:none;" loading="lazy" src="https://eurydia.github.io/project-structogram-builder-online/?preview=true&content=Search%28Integer%5B1..%5D+sequence%29+%7B%0A++Integer+result+%3A%3D+-1%3B%0A++for+%28i+%3D+1..length%28sequence%29%29+%7B%0A++++if+%28isPrime%28sequence%5Bi%5D%29%29+%7B%0A++++++result+%3A%3D+sequence%5Bi%5D%3B%0A++++%7D%0A++%7D%0A%7D"></iframe>

## Selection

Selection is a pattern of an algorithm which reduces a sequence of elements to one element.
Unlike Search, at least one such element exists.

Selecting the last prime number in a sequence of integers:

<iframe width="100%" style="aspect-ratio: 16/10; border:none;" loading="lazy" src="https://eurydia.github.io/project-structogram-builder-online/?preview=true&content=Select%28Integer%5B1..%5D+sequence%29+%7B%0A++Integer+result+%3A%3D+sequence%5B1%5D%3B%0A++for+%28i+%3D+2..length%28sequence%29%29+%7B%0A++++if+%28isPrime%28sequence%5Bi%5D%29%29+%7B%0A++++++result+%3A%3D+sequence%5Bi%5D%3B%0A++++%7D%0A++%7D%0A%7D"></iframe>

## Decision

Decision is a pattern of an algorithm which reduces a sequence of elements to a boolean value.
If an element in a sequence satisfies a certain property, it resolves to true, and false otherwise.

Decide whether a sequence of integers contains a prime number or not:

<iframe width="100%" style="aspect-ratio: 16/10; border:none;" loading="lazy" src="https://eurydia.github.io/project-structogram-builder-online/?preview=true&content=Decision%28Integer%5B1..%5D+sequence%29+%7B%0A++Boolean+result+%3A%3D+NO%3B%0A++for+%28i+%3D+2..length%28sequence%29%29+%7B%0A++++if+%28isPrime%28sequence%5Bi%5D%29%29+%7B%0A++++++result+%3A%3D+YES%3B%0A++++%7D%0A++%7D%0A%7D"></iframe>

## Algorithmic patterns over intervals

An object-oriented programming summary of interval-based patterns of algorithms.

### Summation

Consider an arbitrary set $H$, a binary operation $\text{+}:H\times H\to H$ called **addition**, a neutral element $0\in H$ called **zero**, such that, $0+h\mapsto h$ for all $h\in H$, and a unary function $f:[m, n]\to H$ which maps integers in interval $[m,n]\subseteq\mathbb{Z}$ to $H$.

The summation pattern takes an integer interval, perform operations on it, and reduce it down a single element.

$$
\begin{aligned}
A&:=(m:\mathbb{Z}, n:\mathbb{Z}, r:\mathbb{H})\\
\text{pre}&:=m=m'\land n=n'\\
\text{post}&:=\text{pre}\land\left(r=\sum_{i=m}^{n} f(i)\right)
\end{aligned}
$$

<iframe loading="lazy" height="auto" width="100%" src="https://eurydia.github.io/project-structogram-builder-online/?preview=true&content=%24r%3A%3D0%24%3B%0Afor+%28%24i+%3D+m..n%24%29+%7B%0A++%24r%3A%3D%5Ctext%7Badd%7D%28r%2C+f%28i%29%29%24%3B%0A%7D%0A" style="aspect-ratio: 16/10; border: none;"></iframe>

### Counting

Consider a predicate function $\text{pred}:[m,n]\to\mathbb{L}$ which maps each integer in the interval $[m,n]\subseteq\mathbb{Z}$ to $\mathbb{L}:=\{\top,\bot\}$.

In general, the counting pattern takes an interval and **count** the number of elements which satisfy a condition.

$$
\begin{aligned}
A&:=(m:\mathbb{Z}, n:\mathbb{Z}, r:\mathbb{Z})\\
\text{pre}&:=m=m'\land n=n'\\
\text{post}&:=\text{pre}\land\left(r=\sum_{\substack{i=m\\ \text{pred}(i)}}^{n} 1\right)
\end{aligned}
$$

<iframe loading="lazy" height="auto" width="100%" src="https://eurydia.github.io/project-structogram-builder-online/?preview=true&content=%24r%3A%3D0%24%3B%0Afor+%28%24i+%3D+m..n%24%29+%7B%0A++if+%28%24%5Ctext%7Bpred%7D%28i%29%24%29+%7B%0A++++r+%3A%3D+r+%2B+1%3B%0A++%7D%0A%7D%0A" style="aspect-ratio: 16/10; border: none;"></iframe>

### Maximum selection

Consider a totally-ordered set $H$, a total-ordering binary relation $\gt\subseteq H\times H$ called **greater than**, and a unary function $f:[m, n]\to H$ which maps integers in interval $[m,n]\subseteq\mathbb{Z}$ to $H$.

The maxmima selection pattern takes a integer interval, and returns the **maximal element**. The semantic meaning of **maximal element** is different based on context and implementation.

$$
\begin{aligned}
A&:=(m:\mathbb{Z}, n:\mathbb{Z}, r:\mathbb{H}, k_{r}:\mathbb{Z})\\
\text{pre}&:=m=m'\land n=n'\\
\text{post}&:=\text{pre}\land\left((r,k_{r})=\max_{i=m}^{n} f(i)\right)
\end{aligned}
$$

<iframe loading="lazy" height="auto" width="100%" src="https://eurydia.github.io/project-structogram-builder-online/?preview=true&content=%24r%3A%3Df%28m%29%24%3B%0A%24k_%7Br%7D%3A%3Dm%24%3B%0Afor+%28%24i+%3D+%28m%2B1%29..n%24%29+%7B%0A++if+%28%24f%28i%29+%5Cgt+r%24%29+%7B%0A++++%24r+%3A%3D+f%28i%29%24%3B%0A++++%24k_%7Br%7D%3A%3Di%24%3B%0A++%7D%0A%7D%0A" style="aspect-ratio: 16/10; border: none;"></iframe>

### Conditional maximum selection

Consider a totally-ordered set $H$, a total-ordering binary relation $\gt\subseteq H\times H$ called **greater than**, a predicate function $\text{pred}:[m,n]\to\mathbb{L}$ which maps each integer in the interval $[m,n]\subseteq\mathbb{Z}$ to $\mathbb{L}:=\{\top,\bot\}$, and a unary function $f:[m, n]\to H$ which maps integers in interval $[m,n]\subseteq\mathbb{Z}$ to $H$.

The conditional maximum selection pattern takes an integer interval, and returns the **maximal element** which satisfy the given condition.

$$
\begin{aligned}
A&:=(m:\mathbb{Z}, n:\mathbb{Z}, u:\mathbb{L}, r:\mathbb{H}, k_{r}:\mathbb{Z})\\
\text{pre}&:=m=m'\land n=n'\\
\text{post}&:=\text{pre}\land\left((u, r,k_{r})=\max_{\substack{i=m\\\text{pred}(i)}}^{n} f(i)\right)
\end{aligned}
$$

<iframe loading="lazy" height="auto" width="100%" src="https://eurydia.github.io/project-structogram-builder-online/?preview=true&content=%24u%3A%3D%5Cbot%24%3B%0Afor+%28%24i+%3D+m..n%24%29+%7B%0A++if+%28%24%5Ctext%7Bpred%7D%28i%29%24%29%7B%0A++++if+%28%24u%24%29+%7B%0A++++++if+%28%24f%28i%29%5Cgt+r%24%29+%7B%0A++++++++%24r%3A%3Df%28i%29%24%3B%0A++++++++%24k_%7Br%7D%3A%3Di%24%3B++%0A++++++%7D%0A++++%7D+else%7B%0A++++++%24u%3A%3D%5Ctop%24%3B%0A++++++%24r%3A%3Df%28i%29%24%3B%0A++++++%24k_%7Br%7D%3A%3Di%24%3B%0A++++%7D%0A++%7D%0A%7D%0A" style="aspect-ratio: 16/10; border: none;"></iframe>

### Selection

Consider a arbitrary set $H$ and a predicate function $p:[m,n]\to\mathbb{L}$ which maps each integer in the interval $[m,n]\subseteq\mathbb{Z}$ to $\mathbb{L}:=\{\top,\bot\}$.

The selection pattern takes an integer interval and returns an element which satisfy the given condition with the assumption that such a element exists.

$$
\begin{aligned}
A&:=(m:\mathbb{Z}, k:\mathbb{Z})\\
\text{pre}&:=m=m'\land (\exists k\in\mathbb{Z}: k\ge m\land p(k))\\
\text{post}&:=\text{pre}\land\left(k=\underset{i\ge m}{\text{SELECT }} p(i)\right)
\end{aligned}
$$

<iframe loading="lazy" height="auto" width="100%" src="https://eurydia.github.io/project-structogram-builder-online/?preview=true&content=%24k%3A%3Dm%24%3B%0Afor+%28%24%5Cneg+p%28k%29%24%29+%7B%0A++%24k+%3A%3D+k+%2B+1%24%3B%0A%7D" style="aspect-ratio: 16/10; border: none;"></iframe>

### Linear search

Consider a arbitrary set $H$ and a predicate function $p:[m,n]\to\mathbb{L}$ which maps each integer in the interval $[m,n]\subseteq\mathbb{Z}$ to $\mathbb{L}:=\{\top,\bot\}$.

The linear search pattern takes an integer interval and returns the first element which satisfy the given condition, though such an element might not exist.

$$
\begin{aligned}
A&:=(m:\mathbb{Z},n:\mathbb{Z},u:\mathbb{L}, k:\mathbb{Z})\\
\text{pre}&:=m=m'\land n=n'\\
\text{post}&:=\text{pre}\land\left((u, k) = \underset{i=m}{\overset{n}{\text{SEARCH }}} p(i)\right)
\end{aligned}
$$

<iframe loading="lazy" height="auto" width="100%" src="https://eurydia.github.io/project-structogram-builder-online/?preview=true&content=%24u%3A%3D%5Cbot%24%3B%0A%24k%3A%3Dm%24%3B%0Awhile+%28%24%5Cneg+u%5Cland+k%5Cle+n%24%29+%7B%0A++%24u%3A%3Dp%28k%29%24%3B%0A++%24k%3A%3D+k+%2B+1%24%3B%0A%7D" style="aspect-ratio: 16/10; border: none;"></iframe>

### Binary search

Consider a totally-ordered set $H$, an element $h\in H$, a total-ordering binary relation $\gt\subseteq H\times H$ called **greater than**, and a monotomically-increasing unary function $f:[m,n]\to H$ which maps integers in the interval $[m,n]$ to $H$.

The binary search pattern takes an integer interval and decide whether it contains specific element or not.

$$
\begin{aligned}
A&:=(m:\mathbb{Z},n:\mathbb{Z},h: H, u:\mathbb{L}, k:\mathbb{Z})\\
\text{pre}&:=m=m'\land n=n'\\
\text{post}&:=\text{pre}\land\left(u=\left(\exists i\in\mathbb{Z}:i\in[m,n]\land f(i)=h\right)\right)\land\left(u\implies (k\in[m,n]\land f(k)=h\right)
\end{aligned}
$$

<iframe loading="lazy" height="auto" width="100%" src="https://eurydia.github.io/project-structogram-builder-online/?preview=true&content=%24%5Ctext%7Blower%7D+%3A%3D+m%24%3B%0A%24%5Ctext%7Bupper%7D+%3A%3D+n%24%3B%0A%24u%3A%3D%5Cbot%24%3B%0Awhile+%28%24%5Cneg+u%5Cland%5Ctext%7Blower%7D%5Cle%5Ctext%7Bupper%7D%24%29+%7B%0A++%24k%3A%3D+%5Cfrac%7B%5Ctext%7Blower%7D%2B%5Ctext%7Bupper%7D%7D%7B2%7D%24%3B%0A++if+%28%24f%28k%29%3Dh%24%29+%7B%0A++++%24u%3A%3D%5Ctop%24%3B%0A++%7D+else+%7B%0A++++if+%28%24f%28k%29%5Cgt+h%24%29+%7B%0A++++++%24%5Ctext%7Bupper%7D%3A%3D%5Ctext%7Bupper%7D-1%24%3B%0A++++%7D%0A++++else+%7B%0A++++++%24%5Ctext%7Blower%7D%3A%3D%5Ctext%7Blower%7D-1%24%3B%0A++++%7D%0A++%7D%0A%7D" style="aspect-ratio: 16/10; border: none;"></iframe>
