## Deriving Variational Free Energy for MCTS

First, we are going to transform aforementioned *Variational Free Energy* $F$ from [@eq:free-energy] into a more tractable form:

$$ 
F[Q,y] = D_{KL}[Q(x)||P(x|y)]-\ln P(y)
$$ 
Let's focus on the *KL Divergence* term:
$$
\begin{aligned}
D_{KL}[Q(x)||P(x|y)] &\triangleq E_{Q(x)}[\ln Q(x) -\ln P(x|y)] \\
&= E_{Q(x)}[\ln Q(x)-(\ln P(x,y) - \ln P(y))] \\
&= E_{Q(x)}[\ln Q(x)-\ln P(x,y)] + \ln P(y) \\
&= E_{Q(x)}[\ln Q(x)] - E_{Q(x)}[\ln P(x,y)] + \ln P(y)
\end{aligned}
$$
After substituting this into the original equation [@eq:free-energy], we get:
$$
F[Q,y] = E_{Q}[\ln Q(x)] - E_{Q(x)}[\ln P(x,y)]
$$

---

Since Negative Variational Free Energy is also known as an *Evidence Lower Bound* (ELBO) $\mathcal L$, we can write:

$$
\mathcal L = -F[Q,y] = -E_{Q}[\ln Q(x)] + E_{Q(x)}[\ln P(x,y)]
$$ {#eq:elbo}

Knowing that we can plug it into the equation [@eq:free-energy]:

$$
\mathcal L = D_{KL}[Q(x)||P(x|y)] - \ln P(y)
$$
$$
\ln P(y) = D_{KL}[Q(x)||P(x|y)] + \mathcal L
$$
Since the true posterior $P(x|y)$ is intractable and hence  we canot calculate KL divergence analytically, we get an important property of non-negativity of KL divergence.

$$
\ln P(y) \geq \mathcal L
$$ {#eq:inequality-elbo}

---

## Calculating Variational Free Energy

Finally, we can exploit the above equation [@eq:inequality-elbo] and [@eq:free-energy] to calculate the *Variational Free Energy* for each time-step $t$ as:

$$
\begin{aligned}
F_t = &-E_{Q_\phi(s)(s_t)}[\ln P_{\theta_o}(o_t|s_t)] + D_{KL}[Q_{\phi_s}(s_t)||P_{\theta_s}(s_t|s_{t-1},a_{t-1})] \\
&+ E_{Q_{\phi_s}(s_t)}[D_{KL}[Q_{\phi_a}(a_t)||P(a_t)]]
\end{aligned}
$$ {#eq:timed-free-energy}
where:
$$
P(a) = \sum_{\pi:a_1=a} P(\pi)
$$ {#eq:probability-of-action}
is the summed probability of all policies $\pi$ that start with action $a$.  
We assume that $s_t$ is normally distributed and $o_t$ is *Bernoulli distributed* (which means that the observation $o_t$​ at time $t$ is a binary outcome (e.g., 0 or 1)), with all parameters given by a neural network, parameterized by $\theta_0$,$\theta_s$ and $\phi_s$ for the observation, transition, and encoder models, respectively. The expectations over $Q_{\phi_s}(s_t)$ are taken via MC sampling, using a single sample from the encoder.  

<!-- $$
D_{KL}[Q_\phi(s_t)||P(s_t|o_t)] = \int_{s_t} Q_\phi(s_t) \ln \frac{Q_\phi(s_t)}{P(s_t|o_t)} ds_t
$$ -->

