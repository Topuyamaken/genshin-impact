<img src="https://latex.codecogs.com/gif.latex?">

## Introduction
A leaked artifact set "Echoes of an Offering" has an interesting effect which increases damage dynamically. Its set bonus is as follows:

>When *Normal Attacks* hit opponents, there is a 36% chance that it will trigger Valley Rite, which will increase *Normal Attack DMG* by 60% of *ATK*. This effect will be dispelled 0.05s after a *Normal Attack* deals *DMG*. If a *Normal Attack* fails to trigger Valley Rite, the odds of it triggering the next time will increase by 20%. This trigger can occur once every 0.3s.

In this analysis, there's two problems we need to figure out:

1. What is the average chance to trigger Valley Rite <img src="https://latex.codecogs.com/gif.latex?\left(x\right)">? 
3. How many of your hits on average is affected by the *Normal Attack DMG* increase <img src="https://latex.codecogs.com/gif.latex?\left(y\right)">?

## Markov chain analysis

To find <img src="https://latex.codecogs.com/gif.latex?x">, we have to construct a transition matrix <img src="https://latex.codecogs.com/gif.latex?P_1"> of the trigger chance system, then find the first element of some vector, <img src="https://latex.codecogs.com/gif.latex?\pi">, such that <img src="https://latex.codecogs.com/gif.latex?\pi%20P_1=\pi">:

<img src="assets/equation1.svg">

Find some vector, <img src="https://latex.codecogs.com/gif.latex?\pi">, such that <img src="https://latex.codecogs.com/gif.latex?\pi%20P_1=\pi">.

<img src="assets/equation2.svg">

And we get the following system of equations:

<img src="assets/equation3.svg">

After solving the system of equations, we finally get our stationary distribution:

<img src="assets/equation4.svg">

Since $x$ is equivalent to $π_1$, we have solved the first problem:

<img src="assets/equation5.svg">

To find $y$, repeat the method above and arrive at the second element of some vector, $ψ$.

<img src="assets/equation6.svg">

We have solved the second problem:

<img src="assets/equation7.svg">

## Findings

1. The average chance to trigger Valley Rite is roughly 50.20%.
2. The average number of hits that have the *Normal Attack DMG* increase is roughly 33.42%.

## References

1. [Markov Chains: Stationary Distributions](https://www.stat.berkeley.edu/~mgoldman/Section0220.pdf)
2. [Chapter 8: Markov Chains](https://www.stat.auckland.ac.nz/~fewster/325/notes/ch8.pdf)
3. [Echoes of an Offering](https://genshin.honeyhunterworld.com/db/art/a_15024/?lang=EN)
