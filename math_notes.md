# Math Notes



* **[Measure and Probability](#Measure and Probability)**



* **[Linear Algebra](#Linear Algebra)**

<div style="page-break-after: always; break-after: page;"></div>

## Measure and Probability

**Notations**: Let $P$ and $Q$ be two probability distributions on a measure space $(\mathcal{X}, \mathcal{F})$.



* **$f$-divergence**

  Let $f: (0, \infty) \rightarrow \R$ be a **convex** function with $f(1) = 0$. If $P \ll Q$ ($P$ is [absolutely continuous](#absolute-continuity-of-measures) w.r.t $Q$), then $f$-divergence is defined as:
  $$
  D_f(P||Q) \triangleq \mathbb{E}_Q [f(\frac{dP}{dQ})]
  $$
  where $\frac{dP}{dQ}$ is a Radon-Nikodym derivative.

  * **KL-divergence**
    $$
    f(x) = x\log x
    $$

  * **Total variation**
    $$
    f(x) = \frac{1}{2}|x-1|
    $$

  * **$\chi^2$-divergence**
    $$
    f(x) = (x-1)^2
    $$

  * **Squared Hellinger distance(Metric)**
    $$
    f(x) = (1-\sqrt x)^2
    $$

  * **Jensen-Shannon divergence(Metric)**
    $$
    f(x) = x \log {\frac{2x}{x+1}} + \log{\frac{2}{x+1}}
    $$
    



* **absolute continuity of measures**

  A measure $\mu$ on Borel subsets of the real line is absolutey continuous w.r.t. the Lebesgue measure $\lambda$ if for every $\lambda$-measurable set $A$, 
  $$
  \lambda(A) = 0 \implies \mu(A) = 0
  $$
  This is written as $\mu \ll \lambda$. We say $\mu$ is dominated by $\lambda$.



* **Radon-Nikodym Thm**



* **Caratheodory's Extension Thm**



- ##### **Vapnik-Chervonenkis dimension(VC-dim)**

  - **Shattered sets**

    Suppose $A$ is a set and $C$ is a class of sests. The class $C$ shatters $A$ if for each $B \subset A$ , there is some $c \in C$ s.t. $B = c \cap A$

    Equivalently, $C$ shatters $A$ when $P(A) = \{ c \cap A: c \in C\}$. Now we define:
    $$
    A \cap C = \{A \cap c: c \in C\}
    $$
    then $|A \cap C| = 2^{|A|}$

    Note: $A$ is usually assumed to be **finite**

  - The VC dimension of $C$ is the largest cardinality of sets  shattered by $C$. If arbitrarily large subsets can be shattered, then VC dimension is $\infty$

  - **VC dimension of a classification model**

    The VC dimension of a model is the maximum number of points that can be arranged so that $f$ shatters them.

    1. $f$ is a constant classifier. VC-dim($f$) $= 0$

    2. $f$ is a single-parametric threshold classifier. VC-dim($f$)$=1$

    3. $f$ is a straight line. VC-dim($f$)$=3$

    4. $f$ is a single-parametric sine classifier, i.e, $f_\theta = 1$ if $\sin (\theta x) >0$ otherwise 0. VC-dimension($f$)$=\infty$. Consider
       $$
       \{2^{-m}: m\in \mathbb{N}\}
       $$

    5. NOTE: We need fix an arrangement of these $n$ points at first, then consider all the possiblities of the labels of these $n$ points. If this classifier $f$ works for all possiblities but failed to $n+1$ points, then we call VC-dimension $n$.

- 



<div style="page-break-after: always; break-after: page;"></div>



## Linear Algebra

* **Unitary Transformation**

  * A transformation that preserves the **inner product**

  * An **isomorphism** between two Hilbert spaces: $U: H_1 \rightarrow H_2$ s.t.
    $$
    \langle Ux, Uy \rangle_{H_2} = \langle x, y \rangle_{H_1}
    $$
    for all $x$ and $y$ in $H_1$

  * **Unitary Matrix**: its conjugate transpose is also its inverse
    $$
    U^*U = UU^*=UU^{-1}=I
    $$

    * $|det(U)| =1 $
    * $U$ is diagonalizable
    * In **real number** matrces, the condition is simplified as $U^T = U^{-1}$



* **Vector $p$-norm ($l^p$ norm)**
  $$
  ||x||_p = (\sum_i^n |x_i|)^{\frac{1}{p}} \quad p \geq 1, x\in \R^n
  $$

  * **1-norm(Taxicab metric)**

  * **2-norm(Euclidean norm)**
    $$
    ||x||_2 = \sqrt {x^Tx}
    $$
    
  * **$\infty$-norm**
    $$
    ||x||_{\infty} = \max_{1 \leq i \leq n} |x_i|
    $$
  
* **Matrix norm**

  * Induced by Vector norm
    $$
    ||A||_p := \sup_{||x||_p=1}||Ax||_p
    $$
    

    * $$
      ||A||_1 := \max_{1 \leq j \leq n } \sum_{i=1}^m|a_{ij}|
      $$

      the maximum absolute **column** sum of the matrix

    * $$
      ||A||_\infty := \max_{1 \leq i \leq n } \sum_{j=1}^m|a_{ij}|
      $$

      the maximum absolute **row** sum of the matrix

    * Denote $|A| = (A^*A)^{\frac{1}{2}}$ and by $s(A)$ the vector whose coordinates are the singular values of $A$(i.e. the eigenvalues of $|A|$), arranged as $s_1(A) \geq s_2(A) \geq \cdot \cdot \cdot \geq s_n(A)$. Then
      $$
      ||A||_2 = s_1(A) \\
      ||A||_2 = \sqrt{\lambda_{max}(A^*A)} = \sigma_{max}(A)
      $$
      the **largest** singular value of $A$

      * $$
        ||A^*A||_2=||AA^*||=||A||_2^2
        $$

        since $||A^*A||_2=\sigma(A^*A)=\sigma(A)^2=||A||_2^2$

      * $$
        \sigma_{max}(A) = ||A||_2^2 \leq ||A||_F 
        = \left[ \sum_{i=1}^{m}\sum_{j=1}^n|a_{ij}^2| \right] ^\frac{1}{2}
        = \left[trace(A^*A) \right]^\frac{1}{2}
        =\left[\sum_{k=1}^{min(m,n)}\sigma_k^2\right]^\frac{1}{2}
        $$

        where $||A||_F$ is the **Frobenius** norm

  

  * Two norms that are **unitary invariant**

    * **Unitary invariant**
      $$
      ||A||=||UAV||
      $$
      for any unitary operators $U$, $V$ on $\C^n$

    1. **Schatten p-normd**
       $$
       ||A||_p = ||s(A)||_p 
       = \left[ \sum_{i=1}^n(s_i(A))^p\right]^\frac{1}{p}
       $$
       if $p=\infty$, then $||A||_\infty(Schatten)=\sigma_{max}(A) = ||A||_2(Vector \ norm)$. 

    2. **Ky Fan k-norm**
       $$
       ||A||_{(k)} := \sum_{i=1}^kS_i(A), \quad 1 \leq k \leq n
       $$
       In other words, $||A||_{(k)}$ is the sum of the k largest singular values of $A$



* **Spectral Decomposition Theorem**



* 