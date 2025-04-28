## Action Selection

In active inference, agents choose an action given by their EFE. In particular, any given action is selected with a probability proportional to the accumulated negative EFE of the corresponding policies $G(\pi)$, defined in [@eq:expected-free-energy].  

We can write the process of action selection in active inference as sampling from the distribution:

$$
P(\pi) = \sigma (-G(\pi)) = \sigma (-\sum_{\tau>t} G(\pi,\tau))
$$
Where $\sigma(\cdot)$ is the softmax function.

Again we are faced with computational issues, since computing $G(\pi)$ for all possible policies is computationally expensive, since it involves making an exponentially-increasing number of predictions for $T$ -steps into the future, and computing all the terms in [@eq:mc-sampling-likelihood]. We are going to employ two methods operating in tandem:

---

First, we employ Monte Carlo Tree Search (MCTS) to calculate the distribution over actions $P(a_t)$, defined in [@eq:probability-of-action], and control the agent's final action selection.

During the MCTS process, the agent generates a weighted search tree iteratively that is later sampled during action selection.  
In each MCTS loop, one plausible state-action trajectory -- starting from the current time-step $t$ -- is calculated.  
For states that are explored for the first time, the distribution $P_\theta(s_{t+1}|s_t,a_t)$ is used.

States that have been explored are stored in the buffer search tree and accessed during later loops of the same planning process. The weights of the search tree $\tilde{G}(s_t,a_t)$ represent the agent’s best estimation for EFE after taking action $a_t$ in state $s_t$.

---

An upper confidence bound (UCB) for $G(s_t,a_t)$ is calculated as:
$$
U(s_t,a_t)= \tilde{G}(s_t,a_t) +c_{\text{explore}}\cdot Q_{\phi_a}(a_t|s_t) \frac{1}{1+N(a_t,s_t)} 
$$ {#eq:ucb}
where $N(a_t,s_t)$ is the number of times action $a_t$ was explored from state $s_t$, and $c_{\text{explore}}$ is a hyperparameter that controls exploration.

In each round, the EFE of the newly-explored parts of the trajectory is calculated and back-propagated to all visited nodes of the search tree. Additionally, actions are sampled in two ways. Actions from states that have been explored are sampled from $\sigma(U(s_t,a_t))$, while actions from new states are sampled from $Q_{\phi_a}(a_t)$.