## Variational Free Energy

In Active Inference agent minimize *Variational Free Energy* (VFE), which is formally the negative of the *Evidence Lower Bound* (ELBO) of the (log) model evidence.
We can interpret Free Energy minimization as finding the best explanation for sensory data, which must be simplest (minimally complex) explanation that is able to accurately account for the data.  
Denoted as $F[Q,y]$, where $Q$ is the approximate posterior and $y$ is the observed data:
$$ F[Q,y] = D_{KL}[Q(x)||P(x|y)]-\ln P(y)$$ {#eq:free-energy}
where $P(y)$ is the model evidence (or marginal likelihood) of the observed data, $P(x|y)$ likelihood of the observations given the hidden states. 

Variational free energy has a retrospective aspect, as it is a measure of how well the generative model explains the observed data. We can use it to evaluate the quality of the generative model and its parameters. We can think of it as a *training loss function that we want to minimize*.
