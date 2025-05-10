## Active Inference

Under Active Inference, all cognitive operations are conceptualized as inference over **generative model**- a construct that generates predictions about observations.  
Generative model can be formulated as the joint probability $P(y,x)$ of observations $y$ and hidden states $x$ that generate those observations. 
The latter are referred to as **hidden states** or **latent variables** as they are not directly observed.  
This joint probability can be decomposed as follows:

- Prior $P(x)$: **prior beliefs** about the hidden states- agent's knowledge about hidden states prior to observing sensory data.
- Latter $P(y|x)$: **likelihood of the observations** given the hidden states- agent's knowledge of how observations are generated from states.

---

Single quantity that Active Inference agent minimize through perception and action is **Variational Free Energy** (VFE). This means performing variational inference, which in turn implies substituting two intractable parameters:

- posterior $P(x|y)$
- log model evidence $P(y)$

with two quantities that approximate them respectively:

- approximate posterior $Q(x)$
- variational free energy $F[Q,y]$

Thanks to this substitution the problem of Bayesian inference is transformed into an optimization problem, where the agent minimizes the variational free energy with respect to the approximate posterior.
<!-- 
---

From the general free energy equation ([@eq:free-energy]), we are still left with untractable model evidence $P(y)$ distribution. To this end, we can use the ELBO to approximate the model evidence, with the help of amortization parameters $\phi$ found in recognition model $q_\phi(z|y)$:
$$
\begin{aligned}
\log P_\theta(y) &= \log \int_z p_\theta(y, z) dz \\
&= \log \int_z p_\theta(y, z) \frac{q_\phi(z \vert y)}{q_\phi(z \vert y)} dz \\
&= \log \mathbb{E}_{z \sim q_\phi(z \vert y)} \left[ \frac{p_\theta(y, z)}{q_\phi(z \vert y)}\right] \\
&\geq \mathbb{E}_z \left[ \log \frac{p_\theta(y,z)}{q_\phi(z \vert y)}\right] \text{ (by Jensen's inequality)} \\
&= \mathbb{E}_z \left[ \log p_\theta(y,z) \right] + \int_z q_\phi(z \vert y) \log \frac{1}{q_\phi(z \vert y)} dz \\
&= \mathbb{E}_z \left[ \log p_\theta(y,z) \right] + \mathcal{H} \left(q_\phi \left(z \vert y\right) \right)
\end{aligned}$$

---

$$
\log P_\theta(y) \geq \mathbb{E}_z \left[ \log p_\theta(y,z) \right] + \mathcal{H} \left(q_\phi \left(z \vert y\right) \right) 
$$ {#eq:shannon-entropy}

where $\mathcal{H}(\cdot)$ is called *Shannon entropy*; and $z\sim q_\phi(z \vert y)$. 

By definition, the term *"Evidence"* in ELBO is the value of a likelihood function evaluated with fixed parameters. With the definition of:
$$\mathcal{L}= \mathbb{E}_z \left[ \log p_\theta(y,z) \right] + \mathcal{H} \left(q_\phi \left(z \vert y\right) \right)$$ {#eq:elbo}
it turns out that $\mathcal{L}$ sets a lower bound for the evidence of observations and maximizing $\mathcal{L}$ will push the log likelihood of $x$. Hence we call $\mathcal{L}$ the *Evidence Lower Bound* (ELBO). -->
