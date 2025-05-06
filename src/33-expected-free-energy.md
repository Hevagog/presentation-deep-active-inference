## Expected Free Energy (EFE)

At time step $t$ and for a time horizon up to $T$, the expected free energy is:
$$
G(\pi) = \sum_{\tau=t}^T G(\pi, \tau) = \sum_{\tau=t}^T \mathbb{E}_{\tilde{Q}} \left[ \log Q(s_\tau, \theta|\pi) - \log \tilde{P}(o_\tau, s_\tau, \theta|\pi) \right]
$$ {#eq:t-expected-free-energy}

where:

- $\tilde{Q} = Q(o_\tau, s_\tau, \theta|\pi) = Q(\theta|\pi) Q(s_\tau|\theta, \pi) Q(o_\tau|s_\tau, \theta, \pi)$ is the variational posterior,
- $\tilde{P} = P(o_\tau, s_\tau, \theta|\pi) = P(o_\tau|s_\tau, \theta) P(s_\tau|\theta, \pi) P(\theta|\pi)$ is the generative model.

---

### Decomposition of EFE

At each time step $\tau$:
$$
\begin{aligned}
G(\pi, \tau) = &-\mathbb{E}_{\tilde{Q}}[\log P(o_{\tau}|\pi)]  \\
 &+ \mathbb{E}_{\tilde{Q}}[\log Q(s_{\tau}|\pi) - \log P(s_{\tau}|o_{\tau}, \pi)] \\
 &+ \mathbb{E}_{\tilde{Q}}[\log Q(\theta|s_{\tau}, \pi) - \log P(\theta|s_{\tau}, o_{\tau}, \pi)] \\
\end{aligned}
$$ {#eq:efe-time-step}

where:

- $P(o_\tau|s_\tau,\theta)$ is the likelihood mapping also called a *Generative Model*,
- $G(\pi,\tau)$ is the expected free energy at time $\tau$.

---

## Unpacking the EFE

1. **Reward-seeking term**:

$$
 -\mathbb{E}_{\tilde{Q}}[\log P(o_{\tau}|\pi)]  
$$ {#eq:likelihood}

- This term is responsible for picking actions that make the agent's observations more likely. 
- Measure of how well the agent's generative model predicts the observations it receives. The more likely the observations are given the policy, the lower the expected free energy.

We could compare this to the *reward* term in *Reinforcement Learning*, where the agent is rewarded for taking actions that lead to desirable outcomes.  
In this case if we encode the reward as  certain desirable observations having high prior $P(o_\tau|\pi)$, then minimizing this term is equivalent to maximizing expected log-probability of those observations -- just as the RL agent would maximize expected reward.

---

2. **State-uncertainty term**:

$$
 \mathbb{E}_{\tilde{Q}}[\log Q(s_{\tau}|\pi) - \log P(s_{\tau}|o_{\tau}, \pi)]
$$ {#eq:mutual-information}

- Mutual information between the agent's beliefs about its latent representation of the world, before and after making an observation.
- Reflects a motivation to explore areas of the environment that resolve state uncertainty.

---

3. **Policy-uncertainty term**:

$$
 \mathbb{E}_{\tilde{Q}}[\log Q(\theta|s_{\tau}, \pi) - \log P(\theta|s_{\tau}, o_{\tau}, \pi)] 
$$ {#eq:tendency}

- Tendency of Active Inference agents to reduce their uncertainty about model parameters via new observations.
- Referred to as *active learning*, *novelty* or *curiosity* in the literature.

## MC Sampling to the rescue

Sadly, the second and the third term in the EFE ([@eq:efe-time-step]) are intractable. Therefore, we will use *Monte Carlo* (MC) sampling to approximate the intractable terms.

$$
G(\pi, \tau) = - \mathbb{E}_{Q(\theta|\pi)Q(s_{\tau}|\theta, \pi)Q(o_{\tau}|s_{\tau}, \theta, \pi)} [\log P(o_{\tau}|\pi)]
$$ {#eq:mc-sampling-likelihood}
$$
+ \mathbb{E}_{Q(\theta|\pi)} [\mathbb{E}_{Q(o_{\tau}|\theta, \pi)} H(s_{\tau}|o_{\tau}, \pi) - H(s_{\tau}|\pi)] 
$$ {#eq:mc-b}
$$
+ \mathbb{E}_{Q(\theta|\pi)Q(s_{\tau}|\theta, \pi)Q(o_{\tau}|s_{\tau}, \theta, \pi)} H(o_{\tau}|s_{\tau}, \theta, \pi) - \mathbb{E}_{Q(s_{\tau}|\pi)} H(o_{\tau}|s_{\tau}, \pi) 
$$ {#eq:mc-c}



---

![Relevant quantities for the calculation of EFE $G$, computed by simulating the future using the generative model and ancestral sampling. Where appropriate, expectations are taken with a single MC sample.](img/EFE-calc.svg){width=50%}
