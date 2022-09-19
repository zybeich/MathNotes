# [Towards Optimal Transport with Global Invariances](https://arxiv.org/pdf/1806.09277.pdf)







## Intro: Calculate the correspondence

* Word Embedding

  ![image-20220905160032613](/Users/ich/Library/Application Support/typora-user-images/image-20220905160032613.png)

(https://www.youtube.com/watch?v=bKD2ywAFNqk&t=1895s)

* But this requires the two spaces are registered(i.e. axes are in correspondence)

* What if

  ![image-20220905160234469](/Users/ich/Library/Application Support/typora-user-images/image-20220905160234469.png)

  (https://www.youtube.com/watch?v=bKD2ywAFNqk&t=1895s)

<div style="page-break-after: always; break-after: page;"></div>

## Problem Setting: 

* **Data:**
  $$
  X = \{\mathbf{x}^{i}\}_{i=1}^n, \quad \mathbf{x} \in \mathcal{X} \subset \mathbb{R}^{d_x}
  $$

  $$
  Y = \{\mathbf{y}^{i}\}_{i=1}^n, \quad \mathbf{y} \in \mathcal{Y} \subset \mathbb{R}^{d_y}
  $$

* **Assumptions:**

  * No prior correspondence between $X$ and $Y$ are known
  * Spaces $\mathcal{X}$ ajnd $\mathcal{Y}$ are unregistered

* **Goal:**

  Learn correspondences between $X$ and $Y$

* **Approach:**

  Divide it into two subproblems:

  * find a global alignment of spaces $\mathcal{X}$ and $\mathcal{Y}$ (e.g.  $T: \mathcal{Y} \rightarrow \mathcal{X}$ )s.t. $||\mathbf{x} - T(\mathbf{y})||$ is small for every correspondence pair $(\mathbf{x}, \mathbf{y})$
  * find correspondence between $X$ and $Y$ (e.g. $\mathcal{A}: [n] \rightarrow [m])$ s.t. $\mathbf{x}^i \rightarrow \mathbf{y}^j$ if these points are in correspondence



<div style="page-break-after: always; break-after: page;"></div>



## Optimal Transport: 

* **Monge's Problem**

  * Move $n$ mine to $m$ factories.

  * Define $\sigma: [n] \rightarrow [m] $ by $\sigma(i) = j$ if mine $i$ assigned to facotry $j$. Then we want to find the minimum cost i.e.

  $$
  \min_\sigma \sum_{i} d(x_i, y_{\sigma(i)})
  $$

  ![image-20220905165313852](/Users/ich/Library/Application Support/typora-user-images/image-20220905165313852.png)

  (https://www.youtube.com/watch?v=bKD2ywAFNqk&t=1895s)

* **Kantorovich's Relaxation**

  * Allow "**mass splitting**"

  * Define $\Gamma_{ij} =$ "mass" moved from $x_i$ to $y_j$, then the problem can be relaxed to 
    $$
    \min_\Gamma \sum_{i, j} \Gamma_{ij}d(x_i, y_j) \\
    subject\  to \sum_j \Gamma_{ij} = a_i \  (\forall i), \quad
    \sum_i \Gamma_{ij} = b_j \  (\forall j)
    $$
    ![image-20220905170752056](/Users/ich/Library/Application Support/typora-user-images/image-20220905170752056.png)

    (https://www.youtube.com/watch?v=bKD2ywAFNqk&t=1895s)

* **Between Distributions**

  ![image-20220905164254435](/Users/ich/Library/Application Support/typora-user-images/image-20220905164254435.png)(https://www.youtube.com/watch?v=bKD2ywAFNqk&t=1895s)

* **Wasserstein Distance**

  When $c(x, y)$ is a distance, the optimal value is called the **Wasserstein Distance**



<div style="page-break-after: always; break-after: page;"></div>

## First Subproblem: Space alignment from paired samples

* Assume that $m=n$ and $d_x = d_y$ for now. 

* Consider $\mathbf{X} \in \R ^{d \times n}$ and $\mathbf{Y} \in \R ^ {d \times n}$, whose columns correspond to these paired elements

* Let $\mathcal{F}$ be some class of functions, then the problem is
  $$
  \min_{T \in \mathcal{F}} ||\mathbf{X} - T(\mathbf{Y})||
  $$
  where $||\cdot||$ is the Frobenius norm



* For example, the problem is known as Orthogonal Procrustes Problem if  $\mathcal{F} = \mathcal{O}_n$ (orthonogal matrices):
  $$
  \min_{\mathbf{P} \in \mathcal{O}_n} ||\mathbf{X} - \mathbf{PY}||_F^2
  $$
  which can be solved by SVD



<div style="page-break-after: always; break-after: page;"></div>



## Second Subproblem: Correspondences between aligned spaces

* Consider two measures $\mu$ and $\nu$ over space $\mathcal{X}$ and $\mathcal{Y}$ and a transport cost $c: \mathcal{X} \times \mathcal{Y} \rightarrow \R^+$. Then minimize the cost of transporting measure $\mu$ onto $\nu$

* $\mu$ and  $\nu$ are regarded as empirical distributions:
  $$
  \mu=\sum_{i=1}^n p_i \delta_{x^{(i)}} \quad
  \nu=\sum_{i=1}^m q_i \delta_{y^{(i)}}
  $$
   All pointwise costs can be represented as a matrix $\mathbf{C} \in \R^{n \times m}$.

* So the problem(**DOT**) can be formulated as 
  $$
  \min_{\Gamma \in \Pi(\mathbf{p}, \mathbf{q})} \langle \Gamma, \mathbf{C} \rangle
  $$
  

<div style="page-break-after: always; break-after: page;"></div>



## OT with Global Invariances

* Simultaneously find **the best global transfromation** of the space within $\mathcal{F}$ and **the best local correspondences** between the two collections i.e. jointly optimize $f \in \mathcal{F}$ and $\Gamma \in \Pi(\mathbf{x}, \mathbf{y})$:
  $$
  \min_{\Gamma \in \Pi(\mathbf{x}, \mathbf{y})} \min_{f \in \mathcal{F}} \langle \Gamma, C(\mathbf{X}, f(\mathbf{Y})) \rangle
  $$
  where $[C(\mathbf{X}, f(\mathbf{Y}))]_{ij} = c(x^{i}, f(y^j))$

* Focus on invariances defined by linear operators with bounded norm:
  $$
  \mathcal{F} \triangleq \{\mathbf{P} \in \R^{d\times d} |\  ||\mathbf{P}||_p \leq k_p\}
  $$
  where $||\cdot ||_p$ is the Schatten $l_p$-norm i.e. $||\mathbf{P}||_p = ||\sigma(\mathbf{P})||_p$, where $||\sigma(\mathbf{P})||$ is a vector containing the singular values of $\mathbf{P}$.

* Choose $c$ to be the squared Euclidean distance. Let $\mathbf{u}, \mathbf{v}$ be vectors with entries $u_i = ||\mathbf{x}^{(i)}||_2^2$, and  $v_j = ||\mathbf{Py}^{(j)}||_2^2$. Then the formula above is equivalent to 
  $$
  \max_{\Gamma \in \Pi(\mathbf{p}, \mathbf{q})} \max_{\mathbf{P} \in \mathcal{F}} 2 \langle \Gamma, \mathbf{X}^T \mathbf{PY} \rangle - \langle \mathbf{u}, \mathbf{p} \rangle -\langle \mathbf{v}, \mathbf{q} \rangle
  $$

* This problem is not jointly cancave on $\mathbf{P}$ and $\Gamma$, but it concaves in either variable if the other one is fixed(**alternating optimizition approach**):

  * Fix $\mathbf{P}$: a usual OT problem
  * Fix $\Gamma$: a concave maximization over a compact and convex set

* Simplify the optimization:

  * **Lemma 4.1**: under some conditions, the problem above is equivalent to 

  $$
  \max_{\Gamma \in \Pi(\mathbf{p}, \mathbf{q})} \max_{\mathbf{P} \in \mathcal{F}}  \langle \mathbf{X}\Gamma \mathbf{Y}^T ,  \mathbf{P} \rangle
  $$

  * **Lemma 4.2**: for a fixed $\Gamma$, we can obtain a closed-form solution $\mathbf{P}^*%+$

* Optimization:

  * Regularized problem:
    $$
    \max_{\Gamma \in \Pi(\mathbf{p}, \mathbf{q})} \max_{\mathbf{P} \in \mathcal{F}}  \langle \mathbf{X}\Gamma \mathbf{Y}^T ,  \mathbf{P} \rangle + \lambda H(\Gamma)
    $$

  * Alternating optimization methods for non-convex objectives is sensitive to initialization(addtional step to generate)

  * the strength of the entropic regularization controls the extent of non-concavity

  * Decay $\lambda$ by $\lambda _t = \alpha \times \lambda_{t-1}$ with $\alpha \in (0, 1)$ until a minimum value $\lambda$ is found

# Experiments

* Synthetic Datasets

  ![image-20220907085355617](/Users/ich/Library/Application Support/typora-user-images/image-20220907085355617.png)