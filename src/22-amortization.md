## Amortized Variational Inference

To avoid integrating over the whole latent space we can infer any information about $z$ after observing a sample $x_i \in \mathcal{X}$. We can use $q_i(z)$ to approximate the distribution of $z$ given $i$-th observation.  
Sadly, there is a major drawback, namely, the number of parameters of $q_i(z)$ will scale up with the size of the set of observations *because we build individual distribution after observing each data*.  
To alleviate this problem, we introduce another neural network with parameters $\phi$ to parameterize an approximation of $q_i(z)$, i.e. $q_\phi(z|x)\approx q_i(z)\forall x_i\in\mathcal X$ such that the increase of the number of parameters is **amortized**.  
In other words, we replace all of those $q_i(z)$ distributions with a single parameterized network $q_\phi(z|x)$. This network learns to map from any input observation $x$ to an appropriate distribution over the latent variables $z$.

---

## Amortization

- Refers to transforming what would traditionally be a separate optimization for each data point (or each time step) into a shared optimization across all data points (or time steps).  
- Instead of optimizing variational parameters from scratch at every inference, one learns a recognition model -- a neural network -- whose weights (amortization parameters) $\phi$ produce approximate posterior distributions in a single forward pass.  
- Recognition model $q_\phi(z|x)$ acts as a proxy for the expensive per-instance optimization with $\phi$ representing weights of that proxy model.
- Amortized parameters $\phi$ encapsulate all inferences in a fixed-size model, enabling real-time inference.

<!-- ---

## Amortization in Active Inference

-  -->