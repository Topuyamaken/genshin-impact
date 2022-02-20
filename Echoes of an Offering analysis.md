## Introduction
A leaked artifact set "Echoes of an Offering" has an interesting effect which increases damage dynamically. Its set bonus is as follows:

>When *Normal Attacks* hit opponents, there is a $36\%$ chance that it will trigger Valley Rite, which will increase *Normal Attack DMG* by $60\%$ of *ATK*. This effect will be dispelled $0.05s$ after a *Normal Attack* deals *DMG*. If a *Normal Attack* fails to trigger Valley Rite, the odds of it triggering the next time will increase by $20\%$. This trigger can occur once every $0.3s$.

In this analysis, there's two problems we need to figure out:

1. What is the average chance to trigger Valley Rite $\left(x\right)$? 
2. How many of your hits on average is affected by the *Normal Attack DMG* increase $\left(y\right)$?

## Markov chain analysis

To find $x$, we have to construct a transition matrix $P_1$ of the trigger chance system, then find the first element of some vector, $π$, such that $πP_1=π$:

- <img src="https://latex.codecogs.com/gif.latex?P_1=\begin{bmatrix}0.36&0.64&0&0&0\\0.56&0&0.44&0&0\\0.76&0&0&0.24&0\\0.96&0&0&0&0.04\\1&0&0&0&0\end{bmatrix}">

Find some vector, $π$, such that $πP_1=π$.

$\left[π_1,π_2,π_3,π_4,π_5\right]\begin{bmatrix}0.36&0.64&0&0&0\\0.56&0&0.44&0&0\\0.76&0&0&0.24&0\\0.96&0&0&0&0.04\\1&0&0&0&0\end{bmatrix}=π$

And we get the following system of equations:

$\begin{align}0.36π_1+0.56π_2+0.76π_3+0.96π_4+π_5&=π_1\newline0.64π_1&=π_2\newline0.44π_2&=π_3\newline0.24π_3&=π_4\newline0.04π_4&=π_5\newlineπ_1+π_2+π_3+π_4+π_5&=1\end{align}$

After solving the system of equations, we finally get our stationary distribution:

$π=\left[\frac{390625}{778081},\frac{250000}{778081},\frac{110000}{778081},\frac{26400}{778081},\frac{1056}{778081}\right]$

Since $x$ is equivalent to $π_1$, we have solved the first problem:

$x=π_1=\frac{390625}{778081}\approx50.20\%$

To find $y$, repeat the method above and arrive at the second element of some vector, $ψ$.

$\begin{align}P_2&=\begin{bmatrix}1-x&x\\1&0\end{bmatrix}\newline\newlineψP_2&=ψ\newline\left[ψ_1,ψ_2\right]\begin{bmatrix}1-x&x\\1&0\end{bmatrix}&=ψ\newline\newline\left(1-x\right)ψ_1+ψ_2&=ψ_1\newline xψ_1&=ψ_2\newline\newlineψ&=\left[\frac{778081}{1168706},\frac{390625}{1168706}\right]\end{align}$

We have solved the second problem:

$y=ψ_2=\frac{390625}{1168706}\approx33.42\%$

## Findings

1. The average chance to trigger Valley Rite is roughly $50.20\%$.
2. The average number of hits that have the *Normal Attack DMG* increase is roughly $33.42\%$.

## References

1. [Markov Chains: Stationary Distributions](https://www.stat.berkeley.edu/~mgoldman/Section0220.pdf)
2. [Chapter 8: Markov Chains](https://www.stat.auckland.ac.nz/~fewster/325/notes/ch8.pdf)
3. [Echoes of an Offering](https://genshin.honeyhunterworld.com/db/art/a_15024/?lang=EN)
