## Variational Inference VI

Variational inference is a technique in Bayesian statistics that approximates complex posterior distributions with simpler, tractable distributions.   

VI *transforms the problem of computing the posterior distribution into an optimization problem*. Instead of directly calculating the posterior distribution $p(\theta | D)$, we define a family of simpler distributions $q(\theta)$ and find the one that is closest to the true posterior.


![The variational inference for analyzing the optimal posterior distribution $p(\theta |D)$ by estimating a relatively simpler distribution
$q(\theta)$. Source [@variational-inf]](img/The-variational-inference-for-analyzing-the-optimal-posterior-distribution-pthD-by.jpg){ width=50%}

---

Given observations $x$, we can build a latent variable model with the variable $z$ (we call it **latent** as it is not directly observed) such that the distribution of interest $p(x)$ can be written as:
$$
p(x) = \int_z p(x|z)p(z)dz
$$ {#eq:latent-variable-model}

We condition our observations on some variables we don't know. Therefore, the probability of observations will be the multiplication of the conditional probability and the prior probability of those unknown variables. Subsequently, we integrate out all cases of $z$ to get the distribution of interest $p(x)$.

Unfortunately, this integral is often intractable because it is performed over the whole latent space, which is impractical when latent variables are continuous.  

Another challenge is determining a function that maps $p(z)$ to $p(x)$.  
To address this, we can use a **neural network** with parameters $\theta$ to approximate the distribution $p(x|z)$, resulting in $p_\theta(x|z)$.
