## Evidence Lower Bound ELBO

**Objective function to be optimized**

Represents a lower bound on the marginal log-likelihood (or evidence) of the observed data.  
As earlier mentioned, the goal of variational inference is to put forward a family of distributions and then find the one that is closest to the target.  
For the measure of closeness, we can use the Kullback-Leibler divergence (KL divergence) defined as average difference between two log probabilities:
$$D_{KL}[Q(x)||P(x)] \triangleq E_{Q(x)} [\ln Q(x) - \ln P(x)]$$ {#eq:kl-divergence}  
where $E$ indicates average or expectation.

To successfully setup the optimization for Variational Inference and to find the approximation of the posterior we need to define ELBO, since we cannot compute KL divergence directly. 
<!-- That's because the KL divergence we are truying to minimize to find the approximation is itself dependent on the same evidence that led us to look for an approximation in the first place. -->
