## Amortization parameters

Instead of optimizing variational parameters from scratch at every inference, one learns a recognition model -- a neural network -- whose weights (amortization parameters) produce approximate posterior distributions in a single forward pass.

Active Inference frames perception and action as joint variational inference over a generative model parameterized by $\theta$ and a recognition model parameterized by $\phi$.

---

- Generative model $\theta = \{\theta_o, \theta_s\}$: 
  - $\theta_o$: parametrizes the generative model $P_{\theta_o}(o_t|s_t)$
    - $\theta_o$ are the amortization parameters of the state-decoder network $P_{\theta_o}(o_t|s_t)$ that maps the current latent state $s_t$ to the distribution over observations $o_t$.
  - $\theta_s$: parametrizes the transition function $P_{\theta_s}(s_\tau|s_{t},a_{t})$
    - $\theta_s$ are the amortization parameters of the plain feed-forward network that predicts the next state $s_\tau$ given the current state $s_t$ and action $a_t$.
- Recognition model $\phi = \{\phi_s, \phi_a\}$:
  - $\phi_s$: parametrizes the recognition model $Q_{\phi_s}(s_t)$
    - $\phi_s$ are the amortization parameters of the state-encoder network $Q_{\phi_s}(s_t)$
  - $\phi_a$: parametrizes the recognition model $Q_{\phi_a}(a_t)$
    - $\phi_a$ are the amortization parameters of the habitual policy network $Q_{\phi_a}(a_t)$, which maps inferred states to an action distribution, embodying habitual behavior learned through experience.

Note that since tasks used in this presentation have discrete action spaces $\mathcal{A}$, the recognition model $Q_{\phi_a}(a_t)$ is a neural network with parameters $\phi_a$ and $|\mathcal{A}|$ softmax output units.