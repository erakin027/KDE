# KDE
**Fast Kernel Density Estimation using HODLR, Chebyshev, and SVD**

This project explores scalable algorithms for **Kernel Density Estimation (KDE)**.

We focus on accelerating KDE and its gradient-based bandwidth optimization using:
- Hierarchical matrices (HODLR)
- Chebyshev interpolation
- Low-rank approximations (SVD)

---

## Motivation

Kernel Density Estimation is widely used to estimate probability density functions from data. However, computing KDE and its gradients involves dense kernel matrices with **O(N²)** complexity.

This becomes a bottleneck in:
- Large-scale datasets
- Iterative optimization (e.g., learning adaptive bandwidths)

To address this, we use **hierarchical low-rank structure** to reduce computational cost while maintaining accuracy.

As described in the problem formulation, the key idea is:
- Separate **geometry-dependent structure** from **kernel parameter dependence**
- Reuse hierarchical decomposition across iterations
- Update only small coupling matrices efficiently

---

## Core Concepts

### Kernel Density Estimation (KDE)

We estimate the density as:

$$
\hat{f}(x;h) = \frac{1}{N} \sum_{j=1}^{N} \frac{1}{h_j} \kappa\left(\frac{x - x_j}{h_j}\right)
$$

CDF form:

$$
\hat{F}(z;h) = \frac{1}{N} \sum_{j=1}^{N} K\left(\frac{z - x_j}{h_j}\right)
$$

Matching KDE to empirical distribution is done via:

$$
J(h) = \| \hat{F}(h) - T \|^2
$$

Gradient-based optimization is used to learn bandwidths efficiently.
---

## Key Techniques

### 1. HODLR Matrices
- Hierarchical Off-Diagonal Low-Rank structure
- Reduces mat-vec from **O(N²)** → ~**O(N log N)**

### 2. Chebyshev Interpolation
- Used to approximate admissible blocks
- Basis depends only on geometry (not kernel parameters)
- Enables fast updates during optimization

### 3. SVD-Based Low-Rank Approximation
- Baseline low-rank compression method
- Used for comparison with Chebyshev

---

## Repository Structure

### Hierarchical Matrices
- `HMatrices_combined.ipynb`
  - Full HODLR implementation
  - SVD + Chebyshev methods
  - Time, memory, and accuracy comparisons

- `HMatrices_Cheby_Indiv.ipynb`
  - Standalone Chebyshev implementation
  - Focused experiments and plots

---

### KDE (1D)

- `KDE_cheby.ipynb`
  - Chebyshev-based KDE
  - Compared against Dense implementation

- `KDE_combined.ipynb`
  - Full pipeline:
    - Dense vs Chebyshev vs SVD
    - Performance + accuracy comparison

---

### KDE (2D)

- `KDE_2d_combined.ipynb`
  - Extension of KDE to 2D
  - Includes:
    - 2D kernel formulation
    - Gradient computation
    - Performance evaluation

The 2D KDE formulation follows the same structure as 1D, but with Gaussian kernels in ℝ².

---

## What This Project Shows

- Significant speedups using HODLR vs dense computation
- Chebyshev interpolation is:
  - Faster than SVD in many cases
  - More scalable for repeated computations
- Efficient gradient computation enables bandwidth optimization

---

## Contributions

- Unified framework for:
  - KDE evaluation
  - Gradient computation
- Reusable hierarchical structure across optimization iterations
- Comparison of:
  - Dense vs SVD vs Chebyshev approaches
- Extension from 1D → 2D KDE

---

## Contributors

- Abhijit Dibbidi (IMT2023054)
- Marudi Praneeth Reddy (IMT2023555)

---

