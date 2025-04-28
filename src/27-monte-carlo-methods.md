## Monte Carlo Methods

Class of computational algorithms that use random sampling to approximate high dimensional integrals & expectations that are otherwise analytically intractable.

At their core, Monte Carlo methods rely on the law of large numbers, which states that as the number of samples increases, the sample mean converges to the expected value.

For a function $h(x)$ and a random variable $X$ with probability density function $f_X(x)$, the expectation can be written as:
$$
E[h(X)] = \int h(x) f_X(x) dx
$$ {#eq:expectation}

---

### Monte Carlo Sampling

In MC sampling we generate $N$ independent samples $\{x^{(i)}\}_{i=1}^N$ from the distribution $f_X(x)$ and approximate the expectation as:
$$
E[h(X)] \approx \frac{1}{N} \sum_{i=1}^N h(x^{(i)})
$$ {#eq:monte-carlo-approximation}

- The accuracy of the approximation improves with the number of samples $N$.

## Monte Carlo Tree Search

MCTS extends MC sampling to sequential decision-making problems, in which different potential future trajectories of states are explored in the form of a search tree, giving emphasis to the most likely future trajectories.  
MCTS builds a search tree incrementally by repeatedly running simulations. In each iteration, the process is generally divided into 4 phases:

1. **Selection**: Starting from the root node, a tree policy is used to traverse the tree, selecting child nodes that balance exploration and exploitation until a leaf node is reached.
2. **Expansion**: If the leaf node is not a terminal state, one or more child nodes are added to the tree, representing possible future states.
3. **Simulation**: A simulation (or rollout) is performed from the newly added node to a terminal state or until the horizon is reached. The result is an estimated cumulative cost for that action sequence
4. **Backpropagation**: The result of the simulation is propagated back up the tree, updating the values of the nodes along the path taken during selection.
