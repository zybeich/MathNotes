# Distributional Robustness with IPMs and links to Regularization and GANs



## Distributional Robustness

* For a function $h: \Omega \rightarrow \R$ and distribution $P$ we are interested in
  $$
  \int_{\Omega}hdP
  $$
  

* For an uncertainty set $U$, we are interested in 
  $$
  \sup_{Q\in U}\int_{\Omega}hdQ
  $$



## Uncertainty Set

* Use a divergence $d: \P(\Omega) \times \P(\Omega) \rightarrow \R$ to choose uncertainty sets:
  $$
  U_{d} = {Q: d(Q, P) < \epsilon}
  $$
  where $\epsilon > 0$ is the budget of uncertainty 

* 

