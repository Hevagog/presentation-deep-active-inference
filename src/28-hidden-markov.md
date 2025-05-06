<!-- ## Hidden Markov Model (HMM)


- A statistical model representing a system assumed to be a Markov process with **unobserved (hidden)** states. Core assumptions:
    - *Markov Assumption*
    - *Output Independence Assumption*
- We only observe outputs that are probabilistically dependent on the current hidden state.
- Formally defined by the tuple $\lambda = (S, O, A, B, \pi)$:
    - $S = \{s_1, \dots, s_N\}$: The set of $N$ hidden states.
    - $O = \{o_1, \dots, o_M\}$: The set of $M$ possible observations; directly measurable outputs.
    - $A = \{A_{ij}\}$: The state transition probability matrix, where $A_{ij} = P(q_{t}=s_j | q_{t-1}=s_i)$ denotes probability of transitioning from state $i$ at time $t-1$ to state $j$ at time $t$.
    - $B = \{B_{kj}\}$: Probability of observing a particular output given that the system is in a specific state, where $B_{kj}$ represents the probability of observing output $k$ when the hidden state is $j$.
    - $\pi = \{\pi_i\}$: State probabilities, where each element $\pi_i$ indicates probability of starting in state $s_i$.
::: -->
