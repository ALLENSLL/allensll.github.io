---
layout: post
title: A brief introduction to Dimensionality Reduction
---

Dimensionality reduction can be divided  into *feature selection* and *feature extraction*, this text concerns about feature extraction, for feature extraction, there are *linear dimensionality reduction* and *nonlinear dimensionality reduction* techniques.

* *linear dimensionality reduction*: PCA

* *nonlinear dimensionality reduction*: MDS Isomap LLE

### Principal component analysis

Principal Component Analysis a classical technique for dimensionality reducion, Goal of PCA is to find an orthogonal linear transformation that transforms the data to a new coordinates system such that the greatest variance by some projection of the data comes to lie on the first coordinate(called the first principal component), the second greatest variance on the second coordinate, and so on.
we can generalize PCA to four steps:

* Step 1. Centering the data
* Step 2. Find the covariance matrix
* Step 3. Calculate the eigenvectors and eigenvalues of the covariance matrix
* Step 4. Select principal component and form a transformational matrix
* Step 5. Calculate the new data

#### *Bibliography & External links*

* ["Dimensionality reduction"](https://en.wikipedia.org/wiki/Dimensionality_reduction). wikipedia.org.
* ["Principal Component Analysis"](https://en.wikipedia.org/wiki/Principal_component_analysis). wikipedia.org.
* [UIUC CS498 Lecture 9 - PCA.pdf](http://luthuli.cs.uiuc.edu/~daf/courses/CS-498-DAF-PS/Lecture%209%20-%20PCA.pdf). cs.illinois.edu
* ["A tutorial on Principal Components Analysis"](http://www.cs.otago.ac.nz/cosc453/student_tutorials/principal_components.pdf). cs.otago.ac.nz.
* ["We Recommend a Singular Value Decomposition"](http://www.ams.org/samplings/feature-column/fcarc-svd). ams.org.

### Multidimensional Scaling

Multidimensional Scaling is a form of non-linear dimensionality reduction. Goal of Multidimensional scaling: given raw data‘s pairwise dissmilarities, reconstruct a map that preserves distances. MDS is a family of different algorithms, including Classsical MDS, Metric MDS, Non-metric MDS. When using Classical MDS, you need to do a eigenvalue decomposion for the coordinate matrix. So essentially Classical MDS do the same thing like PCA. Classical MDS assumes Euclidean distances. So this is not applicable for direct dissimilarity ratings.

Classical MDS try to find an optional configuration $$ x_{i} $$ that gives $$ d_{ij} \approx \hat{d}_{ij} = \left \lVert x_{i} - x_{j} \right \rVert _{2} $$ as close as possible. Let's relaxing Classical MDS by allowing $$ d_{ij} \approx \hat{d}_{ij} \approx f(d_{ij}) $$, $$ f $$ is a monotone function([Isotonic regression](https://en.wikipedia.org/wiki/Isotonic_regression)). we named it as metric MDS if dissimilarities $$ d_{ij} $$ are quantitative and non-metric MDS if $$ d_{ij} $$ are qualitative. Unlike Classical MDS, metric or non-metric MDS is an optimization process([Stress majorization](https://en.wikipedia.org/wiki/Stress_majorization)) minimzing stress function, and is solved by iterative algorithms.

#### *Bibliography & Extermal links*

* ["Nonlinear dimensionality reduction"](https://en.wikipedia.org/wiki/Nonlinear_dimensionality_reduction). wikipedia.org.
* ["Multidimensional Scaling"](https://en.wikipedia.org/wiki/Multidimensional_scaling). wikipedia.org.
* [PITT STAT 2221 Lecture 8: Multidimensional scaling](http://www.stat.pitt.edu/sungkyu/course/2221Fall13/lec8_mds_combined.pd). stat.pitt.edu.

### Isomap

Isomap and LLE bring research boom of manifold learning---is usually considered to be a branch of the nonlinear dimensionality reduction. Goal of Isomap is to find an isometric mapping configuration and keep the [geodesic distances](https://en.wikipedia.org/wiki/Geographical_distance) on the manifold. we can generalize Isomap to two steps:

* Step 1. Calculate the geodesic distances
  * Determine the neighbors of each point
  * Construct a neighborhood graph
  * Compute shortest path between two nodes
* Step 2. Compute lower-dimensional embedding
  * use MDS

#### *Bibliography & External links*

* ["Isomap"](https://en.wikipedia.org/wiki/Isomap). wikipedia.org.
* ["A Global Geometric Framework for Nonlinear Dimensionality Reduction"](http://web.mit.edu/cocosci/isomap/isomap.html). mit.edu.
* ["流形学习" ZJU 何晓飞](http://www.cad.zju.edu.cn/reports/%C1%F7%D0%CE%D1%A7%CF%B0.pdf). cad.zju.edu.cn.

### Locally Linear Embedding

Locally Linear Embedding is a milestone in nonlinear dimensionality reduction. LLE tends to handle non-uniform sample densities poorly because there is no fixed unit to prevent the weights from drifting as various regions differ in sample densities.

#### *Bibliography & External links*

* ["Locally Linear Embedding"](https://www.cs.nyu.edu/~roweis/lle/). cs.nyu.edu.
* [Saul, Lawrence K., and Sam T. Roweis. "An introduction to locally linear embedding."](https://www.cs.nyu.edu/~roweis/lle/papers/lleintro.pdf) unpublished. Available at: http://www. cs. toronto. edu/~ roweis/lle/publications. html (2000).
* [Think globally, fit locally: unsupervised learning of low dimensional manifolds](http://www.jmlr.org/papers/volume4/saul03a/saul03a.pdf). jmlr.org.
* ["Lagrange multipliers"](https://www.khanacademy.org/math/multivariable-calculus/applications-of-multivariable-derivatives/constrained-optimization/a/lagrange-multipliers-single-constraint). khanacademy.org.